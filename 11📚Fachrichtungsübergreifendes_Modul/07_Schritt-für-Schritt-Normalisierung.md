
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
