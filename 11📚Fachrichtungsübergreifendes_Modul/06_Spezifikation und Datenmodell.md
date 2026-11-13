

**Tags:** #Programmierung #Datenbanken #Lastenheft #Pflichtenheft #ERM #FisiPrüfung #Lernfeld5

---

### 🗺️ Navigation & Zusammenfassung
* **Vorheriges Thema:** [[01_IT_Basics]] <!-- ⚠️ Nicht vorhanden – Bitte erstellen -->
* **Nächstes Thema:** [[02_Grundlagen relationaler Datenbanken & ER-Modellierung]]
* **Verwandte Bausteine:** [[01_Einführung in Programmierlogik & Logikgrundlagen]], [[03_SQL_Datentypen & Dokumente im Detail]]

> [!INFO] **Manko in der Wissensdatenbank**
> ⚠️ Das Thema **01_IT_Basics** ist noch nicht vorhanden oder konnte nicht verifiziert werden. Dieses Lernblatt sollte als nächstes angelegt werden.

---

### 🎓 IHK-Prüfungsrelevanz: AP01 & AP02

> [!IMPORTANT] **🟢 IHK Prüfungsrelevanz: AP01 (Teil 1 der gestreckten Abschlussprüfung)**
> * **Relevanz:** Sehr hoch / Basiswissen
> * **Fokus:** In der AP01 musst du funktionale von nichtfunktionalen Anforderungen trennen und einfache Datenstrukturen (wie Listen und Dictionaries) im Programmierkontext verstehen. Grundlagen von Programmablaufplänen (PAP) und Struktogrammen sind feste IHK-Prüfungsbestandteile.

> [!INFO] **🔵 IHK Prüfungsrelevanz: AP02 (Teil 2 der gestreckten Abschlussprüfung)**
> * **Relevanz:** Kernkompetenz / Ergänzend
> * **Fokus:** Für die AP02 musst du Geschäftsprozesse lückenlos in relationale Datenmodelle (ER-Diagramme nach Chen) übersetzen können. Die Transformation vom Konzept zum physischen Tabellenschema inklusive der korrekten Fremdschlüsselplatzierung auf der n-Seite ist eine absolute Kernkompetenz.

---

### 📖 Einfache Erklärung & Praxisbeispiele

#### 💡 Das Konzept einfach erklärt
Wenn ein Kunde (z. B. Gastronom Luigi) eine Software bestellt, drückt er seine Wünsche zunächst in eigenen Worten aus. Das ist die **Anforderung** (ein kleines *Lastenheft*, das das *Was* und *Wofür* klärt). Die IT-Entwicklung übersetzt dies in eine präzise **Spezifikation** (Teil des *Pflichtenhefts*, das das *Wie* und *Womit* regelt).

Dabei unterscheidet man zwei fundamentale Säulen:
1. **Die funktionale Spezifikation (Ablauf):** Was tut das Programm genau? Unklare Formulierungen wie *"etwa zwei Stunden"* werden zu harten Regeln (*"exakt 120 Minuten"*) geformt. Der logische Ablauf wird in Pseudocode, Struktogrammen (Nassi-Shneiderman) oder Programmablaufplänen (PAP) visualisiert.
2. **Das Datenmodell (Struktur):** Welche Daten müssen gespeichert werden? Substantive im Kundentext werden zu **Entitätstypen** (Dinge, Tabellen) oder **Attributen** (Eigenschaften, Spalten). Verben beschreiben die **Beziehungen** dazwischen.

#### 💻 Praxisbeispiel & Technische Umsetzung: Luigis Tischreservierung
Aus Luigis Text extrahieren wir die logischen Regeln und überführen sie in Python-Datenstrukturen zur algorithmischen Prüfung:

```python
from dataclasses import dataclass

ZWEI_STUNDEN = 120 # Minuten-Konstante aus Luigis Vorgabe

@dataclass
class Tisch:
    nummer: int
    plaetze: int
    bereich: str

# Repräsentation der Datenbank-Tabelle als Liste von Datensätzen (Objekten)
tische = [
    Tisch(4, 4, "Gastraum"),
    Tisch(5, 4, "Gastraum"),
    Tisch(8, 6, "Gastraum")
]

# Aktuelle Reservierungen als Liste von Dictionaries
reservierungen = [
    {"tisch": 4, "tag": "2026-11-07", "beginn": 1020} # 17:00 Uhr = 1020 Minuten
]

def tisch_frei(tisch_nr, tag, beginn_neu):
    """Prüft, ob der Tisch im Intervall von 2 Stunden kollisionsfrei ist."""
    for r in reservierungen:
        if r["tisch"] == tisch_nr and r["tag"] == tag:
            # Wenn der Abstand zum neuen Beginn kleiner als 120 Minuten ist -> Belegt
            if abs(r["beginn"] - beginn_neu) < ZWEI_STUNDEN:
                return False
    return True

# Validierung für Anfrage A1: 4 Personen, Gastraum, 07.11., 19:00 Uhr (1140 Min)
print(f"Tisch 4 frei für 19:00 Uhr? {tisch_frei(4, '2026-11-07', 1140)}") # Ausgabe: True
```

---

### 📊 Visualisierung & Logik (Mermaid)

Das nachfolgende Entity-Relationship-Diagramm (ERD) in Chen-Notation zeigt die logischen Beziehungen und Kardinalitäten der Tabellen auf Basis von Luigis Anforderungen:

```mermaid
graph TD
    Gast["Gast"] -- "1" --- macht(("macht"))
    macht --- "n" --- Reservierung["Reservierung"]
    
    Personal["Personal"] -- "1" --- traegt(("trägt ein"))
    traegt --- "n" --- Reservierung
    
    Reservierung -- "n" --- belegt(("belegt"))
    belegt --- "1" --- Tisch["Tisch"]
    
    Tisch -- "n" --- steht(("steht in"))
    steht --- "1" --- Bereich["Bereich"]
```

#### Das daraus abgeleitete relationale Datenbankschema:
* **`gast`** (\(\underline{gast\_nr},\) name, telefon)
* **`bereich`** (\(\underline{name},\) offen\_ab, offen\_bis)
* **`personal`** (\(\underline{personal\_nr},\) name)
* **`tisch`** (\(\underline{tisch\_nr},\) plaetze, *bereich*)
* **`reservierung`** (\(\underline{reservierung\_nr},\) tag, uhrzeit, personen, *gast\_nr*, *tisch\_nr*, *personal\_nr*)
*(Hinweis: Primärschlüssel sind unterstrichen, Fremdschlüssel kursiv gesetzt. `personal_nr` darf NULL/leer sein, wenn die Buchung "online" über den Webshop reinkam).*

---

### ⚠️ IHK-Prüfungsstolperfallen
* **Stolperfalle 1:** Vermischung von Lastenheft und Pflichtenheft -> *Lösung:* Merk dir die klare IHK-Zuweisung: Das **Lastenheft** schreibt immer der Auftraggeber (Luigi), das **Pflichtenheft** schreibt immer der Auftragnehmer (Entwickler).
* **Stolperfalle 2:** Falsche Platzierung des Fremdschlüssels bei 1:n-Beziehungen -> *Lösung:* Der Primärschlüssel der 1-Seite wandert **immer als Fremdschlüssel auf die n-Seite**. Im Beispiel wandert `gast_nr` in die Tabelle `reservierung`, da ein Gast viele Reservierungen haben kann.
* **Stolperfalle 3:** Ignorieren von (0..1) Multiplizitäten / optionalen Beziehungen -> *Lösung:* Wenn eine Buchung online erfolgt, hat kein Personal sie eingetragen. Die Spalte `personal_nr` in der Tabelle `reservierung` muss daher zwingend **NULL-Werte (leere Werte) erlauben**, sonst schlägt der Datenbank-Insert fehl.

---
# 08_Schritt-für-Schritt-Normalisierung

**Tags:** #Datenbanken #Normalisierung #1NF #2NF #3NF #FisiPrüfung #Lernfeld5

---

### 🗺️ Navigation & Zusammenfassung
* **Vorheriges Thema:** [[04_Normalisierung von Datenbanken & ER-Modellierung]]
* **Nächstes Thema:** [[10_Bestimmung von Normalformen]]
* **Verwandte Bausteine:** [[02_Grundlagen relationaler Datenbanken & ER-Modellierung]], [[03_SQL_Datentypen & Dokumente im Detail]]

---

### 🎓 IHK-Prüfungsrelevanz: AP01 & AP02

> [!IMPORTANT] **🟢 IHK Prüfungsrelevanz: AP01 (Teil 1 der gestreckten Abschlussprüfung)**
> * **Relevanz:** Sehr hoch / Kernkompetenz
> * **Fokus:** In der AP01 musst du eine unnormalisierte Tabelle (Unerlaubte Listenstrukturen) fehlerfrei in die 1. Normalform überführen können. Atomisierung von Datenfeldern ist eine Standardaufgabe.

> [!INFO] **🔵 IHK Prüfungsrelevanz: AP02 (Teil 2 der gestreckten Abschlussprüfung)**
> * **Relevanz:** Exzellenzniveau / Pflichtaufgabe
> * **Fokus:** In der AP02 wird das vollständige Beherrschen der 2. und 3. Normalform verlangt. Du musst funktionale Abhängigkeiten präzise erkennen, zusammengesetzte Primärschlüssel auflösen und transitive Abhängigkeiten eliminieren, um relationale Datenmodelle komplett anomaliefrei zu machen.

---

### 📖 Erklärung & Praxisbeispiel: Luigis Reservierungsliste

Die Normalisierung dient der **Vermeidung von Redundanzen und Anomalien** (Einfüge-, Änderungs- und Lösch-Anomalien). Wir führen Luigis unstrukturierte Excel-Zettelsammlung schrittweise in eine saubere relationale Struktur über.

#### 📋 Die Ausgangslage: Unnormalisierte Form (UNF)
In der UNF liegen Daten oft nicht-atomar (als Listen) vor. Ein Feld enthält mehrere Informationen.

| *<u>Res\_Nr</u>* | Gast\_Name | Gast\_Telefon | Reservierungsdaten (Tag, Uhrzeit, Personen) | Tisch\_Nr | Tisch\_Plaetze | Bereich\_Info | Personal |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **101** | Christian Schmidt | 0172-123456 | 2026-11-07, 19:00, 4 Pers. | 4 | 4 | Gastraum (offen: 17-23) | Giulia |
| **102** | Michael Weber | 0151-987654 | 2026-11-07, 17:30, 4 Pers.; 2026-11-14, 18:00, 2 Pers. | 8, 2 | 6, 2 | Gastraum; Terrasse (Sommer) | Giulia, Servicekraft Stefan |

---

### 1️⃣ Die 1. Normalform (1NF)
> [!NOTE] **Definition 1NF**
> Eine Relation befindet sich in der 1. Normalform, wenn alle ihre Attribute **atomar** (nicht weiter zerlegbar) sind und die Tabelle **frei von Wiederholungsgruppen** (Listen innerhalb eines Feldes) ist.

* **Schritt 1:** Trennung des Feldes "Reservierungsdaten" in `Tag`, `Uhrzeit` und `Personen`.
* **Schritt 2:** Auflösung der Wiederholungsgruppen (Jede Reservierung erhält eine eigene Zeile).
* **Schritt 3:** Schlüsselbestimmung. Um Einträge eindeutig zu identifizieren, reicht `Res_Nr` nicht mehr aus. Wir benötigen einen zusammengesetzten Primärschlüssel aus **`Res_Nr`** + **`Tisch_Nr`**.

#### Tabelle in 1NF:

| **<u>Res\_Nr</u>** | **<u>Tisch\_Nr</u>** | Gast\_Name | Gast\_Telefon | Tag | Uhrzeit | Personen | Tisch\_Plaetze | Bereich\_Name | Bereich\_Öffnung | Personal |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **101** | **4** | Christian Schmidt | 0172-123456 | 2026-11-07 | 19:00 | 4 | 4 | Gastraum | 17-23 Uhr | Giulia |
| **102** | **8** | Michael Weber | 0151-987654 | 2026-11-07 | 17:30 | 4 | 6 | Gastraum | 17-23 Uhr | Giulia |
| **102** | **2** | Michael Weber | 0151-987654 | 2026-11-14 | 18:00 | 2 | 2 | Terrasse | Nur Sommer | Stefan |

---

### 2️⃣ Die 2. Normalform (2NF)
> [!NOTE] **Definition 2NF**
> Eine Relation befindet sich in der 2. Normalform, wenn sie in der **1NF** ist und **jedes Nicht-Schlüsselattribut vom gesamten Primärschlüssel voll funktional abhängig ist** (und nicht nur von einem Teil des Schlüssels).
> *Hinweis: Gilt nur bei zusammengesetzten Schlüsseln!*

* **Problem-Analyse:** Unser Schlüssel ist (`Res_Nr`, `Tisch_Nr`). 
  * Die Kundendaten (`Gast_Name`, `Tag`, `Uhrzeit` etc.) hängen *nur* von der `Res_Nr` ab, nicht vom Tisch.
  * Die Tischkapazität (`Tisch_Plaetze`, `Bereich_Name`) hängt *nur* von der `Tisch_Nr` ab.
* **Lösung:** Aufspaltung in drei separate Tabellen. Die Verknüpfungstabelle erhält den zusammengesetzten Schlüssel.

#### Tabelle 2.1: Reservierungs-Stamm (`tbl_reservierung`)
Schlüssel: **`Res_Nr`**

| **<u>Res\_Nr</u>** | Gast\_Name | Gast\_Telefon | Tag | Uhrzeit | Personen | Personal |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **101** | Christian Schmidt | 0172-123456 | 2026-11-07 | 19:00 | 4 | Giulia |
| **102** | Michael Weber | 0151-987654 | 2026-11-07 | 17:30 | 4 | Giulia |

#### Tabelle 2.2: Tisch-Stamm (`tbl_tisch`)
Schlüssel: **`Tisch_Nr`**

| **<u>Tisch\_Nr</u>** | Tisch\_Plaetze | Bereich\_Name | Bereich\_Öffnung |
| :--- | :--- | :--- | :--- |
| **4** | 4 | Gastraum | 17-23 Uhr |
| **8** | 6 | Gastraum | 17-23 Uhr |
| **2** | 2 | Terrasse | Nur Sommer |

#### Tabelle 2.3: Belegung (`tbl_belegung`) – *Verknüpfung*
Schlüssel: (**`Res_Nr`**, **`Tisch_Nr`**)

| **<u>Res\_Nr</u>** | **<u>Tisch\_Nr</u>** |
| :--- | :--- |
| **101** | **4** |
| **102** | **8** |
| **102** | **2** |

---

### 3️⃣ Die 3. Normalform (3NF)
> [!NOTE] **Definition 3NF**
> Eine Relation befindet sich in der 3. Normalform, wenn sie in der **2NF** ist und **kein Nicht-Schlüsselattribut transitiv (über Umwege) vom Primärschlüssel abhängig ist**. Nicht-Schlüsselattribute dürfen sich nicht untereinander bedingen.

* **Problem-Analyse in `tbl_tisch`:** `Tisch_Nr` bestimmt den `Bereich_Name`. Aber der `Bereich_Name` bestimmt wiederum die `Bereich_Öffnung`. Das ist eine transitive Abhängikheit!
* **Problem-Analyse in `tbl_reservierung`:** Wenn wir `Gast_Telefon` ändern müssten, weil der Gast wiederkommt, gäbe es Redundanzen. Daher lagern wir den Gast aus.
* **Lösung:** Erneute Auslagerung der abhängigen Attribute in eigene Tabellen.

#### Endzustand der relationalen Tabellen (3NF):

**`tbl_gast`**

| **<u>Gast\_ID</u>** | Gast\_Name | Gast\_Telefon |
| :--- | :--- | :--- |
| **G01** | Christian Schmidt | 0172-123456 |
| **G02** | Michael Weber | 0151-987654 |

**`tbl_bereich`**

| **<u>Bereich\_Name</u>** | Bereich\_Öffnung |
| :--- | :--- |
| **Gastraum** | 17-23 Uhr |
| **Terrasse** | Nur Sommer |

**`tbl_tisch`**

| **<u>Tisch\_Nr</u>** | Tisch\_Plaetze | *Bereich\_Name (FS)* |
| :--- | :--- | :--- |
| **4** | 4 | Gastraum |
| **8** | 6 | Gastraum |
| **2** | 2 | Terrasse |

**`tbl_reservierung`**

| **<u>Res\_Nr</u>** | *Gast\_ID (FS)* | Tag | Uhrzeit | Personen | Personal |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **101** | G01 | 2026-11-07 | 19:00 | 4 | Giulia |
| **102** | G02 | 2026-11-07 | 17:30 | 4 | Giulia |

**`tbl_belegung`**

| **<u>Res\_Nr (FS)</u>** | **<u>Tisch\_Nr (FS)</u>** |
| :--- | :--- |
| **101** | **4** |
| **102** | **8** |
| **102** | **2** |

---

### ⚠️ IHK-Prüfungsstolperfallen
* **Stolperfalle 1:** Die 2NF bei einfachen Primärschlüsseln prüfen -> *Lösung:* Wenn eine Tabelle nur einen **einfachen Primärschlüssel** hat (bestehend aus nur einer Spalte), ist sie automatisch **immer in der 2. Normalform**! Verletzungen der 2NF können konstruktionsbedingt nur bei zusammengesetzten Schlüsseln auftreten.
* **Stolperfalle 2:** Transitive Abhängigkeiten in der 2NF jagen -> *Lösung:* Unterscheide die Formen sauber. Wenn ein Attribut von einem *Teil des Schlüssels* abhängt, ist es ein Verstoß gegen die **2NF**. Wenn ein Attribut von einem *anderen Nicht-Schlüsselattribut* abhängt, ist es ein Verstoß gegen die **3NF**.

---
