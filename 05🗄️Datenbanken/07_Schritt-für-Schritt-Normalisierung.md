---
tags: [fisi, ihk, lernsheet]
---
## 🧭 Navigation & Zusammenhänge
- **Vorausgesetztes Thema:** [[06_Datenbank-Anomalien]]
- **Nächstes Thema:** [[08_Grundlagen der persistenten Datenhaltung & Datenmodellierung]]
- **Verwandte Bausteine:** [[09_Bestimmung von Normalformen]], [[17_Identifikation & Transformation von Normalformen]]
---

## 🎯 IHK-Prüfungsrelevanz
> [!IMPORTANT] AP01: Einrichten eines IT-gestützten Arbeitsplatzes
> - **Relevanz:** Niedrig
> - **Fokus:** Strukturierung von Austauschdateien nach dem Prinzip der Eindeutigkeit.

> [!WARNING] AP02: Konzeption, Administration & Netzwerke
> - **Relevanz:** Extrem Hoch
> - **Fokus:** Das ist die absolute IHK-Kernkompetenz! Du musst in der Prüfung eine unnormalisierte Tabelle (UNF) fehlerfrei in die 3. Normalform (3NF) überführen. Die Prüfer achten penibel darauf, ob du Primärschlüssel (PK) und Fremdschlüssel (FK) korrekt setzt und die Tabellen logisch trennst, um die in der vorherigen Aufgabe analysierten Anomalien vollständig zu eliminieren.

---

## 📖 Schritt-für-Schritt-Transformation

### 1. Ausgangslage: Die Unnormalisierte Form (UNF)
Unsere Tabelle leidet unter massiven Redundanzen, da Kurs-, Dozenten- und Teilnehmerdaten unstrukturiert zusammengeworfen wurden.

**Tabelle: `Akademie_Liste`**

| TeilnehmerId (PK) | Kurs | Dozent | Dozent_Telefon |
| :--- | :--- | :--- | :--- |
| 1 | SQL-Basis | Herr Schmidt | 0123-4455 |
| 2 | SQL-Basis | Herr Schmidt | 0123-4455 |
| 3 | Java-Intro | Frau Meyer | 0987-1122 |

---

### 2. Schritt: Überführung in die 1. Normalform (1NF)
- **Bedingung der 1NF:** Alle Attribute müssen **atomar** (unteilbar) sein und es dürfen keine Wiederholungsgruppen existieren.
- **Analyse:** Die Anrede und der Nachname im Feld `Dozent` (*"Herr Schmidt"*) sind zusammengesetzte Informationen. Zudem trennen wir zur sauberen Strukturierung direkt die `Kurs_ID` vom Kursnamen.
- **Maßnahme:** Aufspaltung von `Dozent` in `Dozent_Anrede` und `Dozent_Nachname`.

**Tabelle: `Akademie_1NF`**

| <u>TeilnehmerId</u> | Kurs_ID | Kurs_Name | Dozent_Anrede | Dozent_Nachname | Dozent_Telefon |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | K01 | SQL-Basis | Herr | Schmidt | 0123-4455 |
| 2 | K01 | SQL-Basis | Herr | Schmidt | 0123-4455 |
| 3 | K02 | Java-Intro | Frau | Meyer | 0987-1122 |

---

### 3. Schritt: Überführung in die 2. Normalform (2NF)
- **Bedingung der 2NF:** Die 1NF muss erfüllt sein. Zusätzlich muss jedes Nicht-Schlüsselattribut vom **vollständigen Primärschlüssel** funktional abhängig sein (keine Teilabhängigkeiten).
- **Analyse:** Da ein Teilnehmer mehrere Kurse besuchen kann, besteht der logische Primärschlüssel dieser Tabelle eigentlich aus einer Kombination von `TeilnehmerId` und `Kurs_ID`. Der `Kurs_Name` sowie die Dozentendaten hängen jedoch **nur** von der `Kurs_ID` ab (Teil des Schlüssels). Sie verstoßen gegen die 2NF.
- **Maßnahme:** Auslagerung der kursabhängigen Attribute in eine eigene Tabelle `Kurs`.

**Tabelle: `Teilnehmer_Belegung` (Verknüpfungstabelle)**

| <u>TeilnehmerId</u> | <u>Kurs_ID</u> |
| :--- | :--- |
| 1 | K01 |
| 2 | K01 |
| 3 | K02 |

**Tabelle: `Kurs_2NF`**

| <u>Kurs_ID</u> | Kurs_Name | Dozent_Anrede | Dozent_Nachname | Dozent_Telefon |
| :--- | :--- | :--- | :--- | :--- |
| K01 | SQL-Basis | Herr | Schmidt | 0123-4455 |
| K02 | Java-Intro | Frau | Meyer | 0987-1122 |

---

### 4. Schritt: Überführung in die 3. Normalform (3NF)
- **Bedingung der 3NF:** Die 2NF muss erfüllt sein. Zudem dürfen **keine transitiven Abhängigkeiten** existieren (Abhängigkeiten "über Bande" von Nicht-Schlüssel zu Nicht-Schlüssel).
- **Analyse:** In der Tabelle `Kurs_2NF` bestimmt die `Kurs_ID` den Dozenten. Allerdings bestimmen die Attribute `Dozent_Anrede` und `Dozent_Nachname` wiederum das Attribut `Dozent_Telefon`. Die Telefonnummer hängt also transitiv über den Dozenten von der `Kurs_ID` ab.
- **Maßnahme:** Auslagerung der Dozenten-Stammdaten in eine eigene Tabelle `Dozent`. In der Tabelle `Kurs` verbleibt lediglich eine `Dozent_ID` als Fremdschlüssel (`FK`).

#### Das finale, bereinigte Datenmodell in 3NF (Textform)
- **`Teilnehmer_Belegung`** (<u>TeilnehmerId</u>, <u>Kurs_ID</u>)
- **`Kurs`** (<u>Kurs_ID</u>, Kurs_Name, ↑Dozent_ID)
- **`Dozent`** (<u>Dozent_ID</u>, Anrede, Nachname, Telefon)

---

### 5. Ergebnis: Der Praxis-Check (Beseitigung der Anomalien)
- **Keine Einfüge-Anomalie mehr:** Ein neuer Dozent oder ein neuer Kurs (`Kurs_ID` K03) kann nun problemlos in die Tabellen `Dozent` bzw. `Kurs` eingepflegt werden, selbst wenn noch kein einziger Teilnehmer angemeldet ist.
- **Keine Änderungs-Anomalie mehr:** Ändert Herr Schmidt seine Telefonnummer, muss dieser Wert **exakt an einer einzigen Stelle** in der Tabelle `Dozent` aktualisiert werden. Widersprüche sind ausgeschlossen.
- **Keine Lösch-Anomalie mehr:** Tritt der Teilnehmer 3 aus und wird aus `Teilnehmer_Belegung` gelöscht, bleiben der Kurs *"Java-Intro"* und die Kontaktdaten von *"Frau Meyer"* in den Stammdatentabellen vollständig erhalten.

---

## 📊 Visuelle Darstellung (Mermaid.js)
```mermaid
erDiagram
    TEILNEHMER_BELEGUNG {
        int TeilnehmerId PK
        string Kurs_ID PK_FK
    }
    KURS {
        string Kurs_ID PK
        string Kurs_Name
        int Dozent_ID FK
    }
    DOZENT {
        int Dozent_ID PK
        string Anrede
        string Nachname
        string Telefon
    }

    KURS ||--o{ TEILNEHMER_BELEGUNG : "wird belegt in"
    DOZENT ||--o{ KURS : "leitet"
```
