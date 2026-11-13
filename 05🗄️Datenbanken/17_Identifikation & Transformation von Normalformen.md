tags: [fisi, ihk, lernsheet]
## 🧭 Navigation & Zusammenhänge
- **Vorausgesetztes Thema:** [[16_Datenwerte mit INSERT INTO]]
- **Nächstes Thema:** [[18_Tabellenstrukturen mit Datentypen & Constraints physisch anlegen]]
- **Verwandte Bausteine:** [[05🗄️Datenbanken/07_Schritt-für-Schritt-Normalisierung]], [[09_Bestimmung von Normalformen]]
---

🎯 IHK-Prüfungsrelevanz

> [!WARNING] AP02: Konzeption, Administration & Netzwerke
> 
> - **Relevanz:** Extrem Hoch (Pflichtaufgabe)
> - **Fokus:** Diese 10 Beispiele decken die gesamte Bandbreite typischer IHK-Datenbankaufgaben ab. Du musst in der Prüfung in der Lage sein, Hinderungsgründe (Teilabhängigkeiten oder transitive Abhängigkeiten) zu benennen und das bereinigte relationale Zielschema in Textform anzugeben.

---

📖 Analyse & Transformationsschritte

📊 Schnellübersicht der 10 Beispiele

|Bsp.|Thema|Ist-Zustand|Primärschlüssel (PK)|IHK-Hinderungsgrund für die 3NF|
|---|---|---|---|---|
|**1**|IT-Infrastruktur|**2NF**|`(Switch_ID, Port_Nummer)`|Transitive Abhängigkeiten (`VLAN_ID` \(\rightarrow \) `VLAN_Name` und `Zielgerät_ID` \(\rightarrow \) `Zielgerät_Typ`).|
|**2**|Rezeptdatenbank|**UNF**|`Rezept_ID`|Mehrwertige Attribute (`Zutaten` und `Kategorien` als Listen).|
|**3**|Hotel-Belegung|**2NF**|`Buchungs_ID`|Transitive Abhängigkeiten (`Zimmer_Nr` \(\rightarrow \) `Zimmer_Typ` \(\rightarrow \) `Preis` und `Gast_ID` \(\rightarrow \) `Gast_Name`).|
|**4**|Kfz-Werkstatt|**1NF**|`(Auftrags_Nr, Ersatzteil_ID)`|Teilabhängigkeiten (`Teil_Bezeichnung`/`Lager_Regal` von `Ersatzteil_ID` sowie `KFZ_Kennzeichen` von `Auftrags_Nr`).|
|**5**|Event-Ticketing|**2NF**|`Ticket_Code`|Transitive Abhängigkeiten (`Event_ID` \(\rightarrow \) `Event_Titel` \(\rightarrow \) `Halle_ID` \(\rightarrow \) `Halle_Name`/`Kapazität`).|
|**6**|Personal-Zertifikate|**1NF**|`(Mitarbeiter_ID, Zertifikats_Code)`|Teilabhängigkeit (`Zertifikats_Name`/`Herausgeber` von `Zertifikats_Code`) + transitive Abhängigkeit (`Herausgeber` \(\rightarrow \) `URL`).|
|**7**|Bestandsführung|**1NF**|`(Artikel_ID, Lagerhaus_ID)`|Teilabhängigkeit (`Artikel_Name` von `Artikel_ID`) + transitive Abhängigkeit (`Lagerhaus_ID` \(\rightarrow \) `Kategorie` \(\rightarrow \) `Temperatur`).|
|**8**|Uni-Prüfungen|**1NF**|`(Matrikel_Nr, Modul_ID, Semester)`|Teilabhängigkeit (`Modul_Leiter` von `Modul_ID`) + transitive Abhängigkeit (`Modul_Leiter` \(\rightarrow \) `Leiter_Lehrstuhl`).|
|**9**|Flugplan-Daten|**2NF**|`Flug_Nummer`|Transitive Abhängigkeiten (`Airline_Code` \(\rightarrow \) `Airline_Name` und `Ziel_Flughafen` \(\rightarrow \) `Land_ID` \(\rightarrow \) `Land_Name`).|
|**10**|Lieferanten-Kond.|**2NF**|`(Lieferant_ID, Material_Gruppe)`|Transitive Abhängigkeit (`Lieferant_ID` \(\rightarrow \) `Ansprechpartner` \(\rightarrow \) `Zentrale_Telefon`).|

---

🔎 Detail-Analyse & Zielschemata (Textform)

Beispiel 1: IT-Infrastruktur

- **Analyse:** Die 1NF und 2NF sind erfüllt, da alle Felder atomar sind und die Nicht-Schlüssel voll funktional vom zusammengesetzten PK abhängen. Es liegen aber zwei transitive Abhängigkeiten vor: `VLAN_ID` bestimmt `VLAN_Name`, und `Zielgerät_ID` bestimmt `Zielgerät_Typ`.
- **Zielschema (3NF):**
    - `Ports(<u>Switch_ID</u>, <u>Port_Nummer</u>, ↑VLAN_ID, ↑Zielgerät_ID)`
    - `VLAN(<u>VLAN_ID</u>, VLAN_Name)`
    - `Zielgerät(<u>Zielgerät_ID</u>, Zielgerät_Typ)`

Beispiel 2: Rezeptdatenbank

- **Analyse:** UNF aufgrund der Kommalisten in `Zutaten` und `Kategorien`. Da eine Zutat in vielen Rezepten vorkommt und ein Rezept viele Zutaten hat (analog für Kategorien), handelt es sich um `m:n-Beziehungen`.
- **Zielschema (3NF):**
    - `Rezepte(<u>Rezept_ID</u>, Gericht_Name)`
    - `Zutaten(<u>Zutat_ID</u>, Zutat_Name)`
    - `Rezept_Zutaten(<u>↑Rezept_ID</u>, <u>↑Zutat_ID</u>, Menge)`
    - `Kategorien(<u>Kategorie_ID</u>, Kategorie_Name)`
    - `Rezept_Kategorien(<u>↑Rezept_ID</u>, <u>↑Kategorie_ID</u>)`

Beispiel 3: Hotel-Belegung

- **Analyse:** Da der PK einfach ist (`Buchungs_ID`), ist die 2NF erfüllt. Es liegen transitive Abhängigkeiten vor: `Zimmer_Nr` bestimmt den Typ und den Preis. `Gast_ID` bestimmt den `Gast_Name`.
- **Zielschema (3NF):**
    - `Buchungen(<u>Buchungs_ID</u>, ↑Zimmer_Nr, ↑Gast_ID)`
    - `Zimmer(<u>Zimmer_Nr</u>, ↑Zimmer_Typ_ID)`
    - `Zimmer_Typ(<u>Zimmer_Typ_ID</u>, Bezeichnung, Typ_Preis_pro_Nacht)`
    - `Gast(<u>Gast_ID</u>, Gast_Name)`

Beispiel 4: Kfz-Werkstatt (Reparaturen)

- **Analyse:** 1NF. Bei zusammengesetztem PK liegen Teilabhängigkeiten vor: `Teil_Bezeichnung` und `Lager_Regal` hängen nur von der `Ersatzteil_ID` ab. Das `KFZ_Kennzeichen` hängt nur von der `Auftrags_Nr` ab.
- **Zielschema (3NF):**
    - `Reparatur_Positionen(<u>↑Auftrags_Nr</u>, <u>↑Ersatzteil_ID</u>, Menge)`
    - `Ersatzteile(<u>Ersatzteil_ID</u>, Teil_Bezeichnung, Lager_Regal)`
    - `Aufträge(<u>Auftrags_Nr</u>, KFZ_Kennzeichen)`

Beispiel 5: Event-Ticketing

- **Analyse:** 2NF (einfacher PK). Transitive Abhängigkeit: `Ticket_Code` bestimmt `Event_ID` \(\rightarrow \) bestimmt `Event_Titel` \(\rightarrow \) bestimmt `Halle_ID` \(\rightarrow \) bestimmt Name und Kapazität.
- **Zielschema (3NF):**
    - `Tickets(<u>Ticket_Code</u>, ↑Event_ID)`
    - `Events(<u>Event_ID</u>, Event_Titel, ↑Halle_ID)`
    - `Hallen(<u>Halle_ID</u>, Halle_Name, Halle_Kapazität)`

Beispiel 6: Personal-Zertifizierungen

- **Analyse:** 1NF. Teilabhängigkeit vom PK: `Zertifikats_Name` und `Herausgeber` hängen nur von `Zertifikats_Code` ab. Zusätzlich transitive Abhängigkeit: `Herausgeber` bestimmt `Herausgeber_URL`.
- **Zielschema (3NF):**
    - `Mitarbeiter_Zertifikate(<u>Mitarbeiter_ID</u>, <u>↑Zertifikats_Code</u>, Erlangungsdatum)`
    - `Zertifikate(<u>Zertifikats_Code</u>, Zertifikats_Name, ↑Herausgeber_ID)`
    - `Herausgeber(<u>Herausgeber_ID</u>, Herausgeber_Name, Herausgeber_URL)`

Beispiel 7: Lager-Bestandsführung

- **Analyse:** 1NF. Teilabhängigkeit: `Artikel_Name` hängt nur von `Artikel_ID` ab. Transitive Abhängigkeit: `Lagerhaus_ID` bestimmt `Lager_Kategorie` bestimmt `Lager_Temperatur`.
- **Zielschema (3NF):**
    - `Lagerbestände(<u>↑Artikel_ID</u>, <u>↑Lagerhaus_ID</u>, Bestand)`
    - `Artikel(<u>Artikel_ID</u>, Artikel_Name)`
    - `Lagerhäuser(<u>Lagerhaus_ID</u>, ↑Kategorie_ID)`
    - `Lager_Kategorien(<u>Kategorie_ID</u>, Bezeichnung, Lager_Temperatur)`

Beispiel 8: Universitäts-Prüfungen

- **Analyse:** 1NF. Teilabhängigkeit: `Modul_Leiter` hängt funktional nur von `Modul_ID` ab. Transitive Abhängigkeit: `Modul_Leiter` bestimmt den `Leiter_Lehrstuhl`.
- **Zielschema (3NF):**
    - `Prüfungen(<u>Matrikel_Nr</u>, <u>↑Modul_ID</u>, <u>Semester</u>, Note)`
    - `Module(<u>Modul_ID</u>, ↑Leiter_ID)`
    - `Lehrkräfte(<u>Leiter_ID</u>, Name, Leiter_Lehrstuhl)`

Beispiel 9: Flugplan-Daten

- **Analyse:** 2NF. Transitive Abhängigkeiten: `Airline_Code` bestimmt `Airline_Name`. `Ziel_Flughafen` bestimmt `Land_ID`, diese bestimmt wiederum `Land_Name`.
- **Zielschema (3NF):**
    - `Flugplan(<u>Flug_Nummer</u>, ↑Airline_Code, ↑Ziel_Flughafen)`
    - `Airlines(<u>Airline_Code</u>, Airline_Name)`
    - `Flughäfen(<u>Ziel_Flughafen</u>, ↑Land_ID)`
    - `Länder(<u>Land_ID</u>, Land_Name)`

Beispiel 10: Lieferanten-Konditionen

- **Analyse:** 2NF (Die Kombination aus Lieferant und Materialgruppe bestimmt den spezifischen Rabattsatz). Allerdings hängen `Ansprechpartner` und `Zentrale_Telefon` transitiv rein von der `Lieferant_ID` ab.
- **Zielschema (3NF):**
    - `Konditionen(<u>↑Lieferant_ID</u>, <u>Material_Gruppe</u>, Rabatt_Satz)`
    - `Lieferanten(<u>Lieferant_ID</u>, Ansprechpartner, Zentrale_Telefon)`