---
aliases: []
tags:
  - ihk/ap1
  - modul/01-bwl
  - status/gelernt
  - typ/konzept
---
---
📌 Allgemeine Betriebswirtschaftslehre & IT-Arbeitsplatzgestaltung

## 🧭 Navigation & Zusammenhänge
- **Vorausgesetztes Thema:** *Keines (Start des Moduls)*
- **Nächstes Thema:** [[02_Management, Projektplanung & Arbeitsplatz-Ergonomie]]
- **Verwandte Bausteine:** [[05_Aufbau- und Ablauforganisation]], [[07_Controlling]]

🎯 IHK-Prüfungsrelevanz

> [!IMPORTANT] AP01: Einrichten eines IT-gestützten Arbeitsplatzes
> 
> - **Relevanz:** Hoch
> - **Fokus:** Einhaltung der gesetzlichen Ergonomie-Vorgaben am IT-Arbeitsplatz (ArbStättV) sowie Grundsätze der Benutzerfreundlichkeit und Software-Ergonomie nach ISO 9241.

> [!WARNING] AP02: Konzeption, Administration & Netzwerke
> 
> - **Relevanz:** Mittel
> - **Fokus:** Anwendung des ökonomischen Prinzips (Minimal- vs. Maximalprinzip) bei der Ressourcenplanung sowie das Verständnis digitaler Güter (First-Copy-Costs vs. Grenzkosten).

---

📖 Einfache Erklärung & Praxisbeispiele

Die **Allgemeine Betriebswirtschaftslehre (ABWL)** verknüpft das IT-Fachwissen mit wirtschaftlichem Denken. Da Ressourcen (Zeit, Geld, Hardware) im IT-Alltag knapp sind, zwingt uns das ökonomische Prinzip zum rationalen Auswählen zwischen Alternativen.

Unterthemen & Anschauliche Beispiele:

- **Das Ökonomische Prinzip (Minimal vs. Maximal):**
    - **Minimalprinzip:** Ein festes Ziel mit minimalen Mitteln (Kosten) erreichen.
        - 💡 **Praxisbeispiel:** Ein Kunde fordert den _„Aufbau eines WLANs für exakt 100 User“_. Du planst die Infrastruktur so, dass die Anforderungen exakt erfüllt werden, wählst aber die kostengünstigsten, zuverlässigen Komponenten.
    - **Maximalprinzip:** Mit vorgegebenen Mitteln den maximalen Erfolg erzielen.
        - 💡 **Praxisbeispiel:** Dein Chef gibt dir ein festes _„Hardware-Budget von 5.000 EUR“_ für einen neuen Virtualisierungsserver. Du versuchst, für dieses feste Geld das Maximum an CPU-Kernen und RAM herauszuholen.
- **Ökonomie digitaler Güter:** Digitale Produkte haben einzigartige Eigenschaften: Extrem hohe Entwicklungskosten (**First-Copy-Costs**), aber Reproduktions- und Vertriebskosten von nahezu Null (**Grenzkosten**) sowie keine physische Abnutzung.
    - 💡 **Praxisbeispiel:** Die Entwicklung einer neuen Monitoring-Software kostet ein Systemhaus 50.000 EUR. Das Bereitstellen einer weiteren Lizenz per Download kostet das Unternehmen dagegen fast gar nichts.
- **Arbeitsorganisation (Analyse & Synthese):** Komplexe Gesamtaufgaben werden in Teilaufgaben zerlegt (**Aufgabenanalyse** nach Verrichtung oder Objekt) und anschließend zu sinnvollen Stellen gebündelt (**Aufgabensynthese**). Die Stelle ist die kleinste organisatorische Einheit.
    - 💡 **Praxisbeispiel:** Beim Aufbau einer IT-Abteilung trennst du die Aufgabenanalyse nach Objekten (z. B. Frontend vs. Datenbank). Daraus bildest du die Stellenbeschreibung für einen „Datenbankadministrator“ mit klarem Aufgaben-, Kompetenz- und Anforderungsprofil.
- **Ergonomie am IT-Arbeitsplatz:** Einhaltung gesetzlicher Richtlinien der Arbeitsstättenverordnung (ArbStättV). Dazu gehören ein Sehabstand von 50–70 cm, strahlungsarme Monitore, ergonomische Mäuse/Tastaturen sowie Umgebungsfaktoren wie 20–22 °C Raumtemperatur und eine Beleuchtung von mindestens 500 Lux.
    - 💡 **Praxisbeispiel:** Bei der Neueinrichtung eines Entwickler-Arbeitsplatzes installierst du höhenverstellbare Tische und stellst sicher, dass die Monitore blendfrei und im richtigen Abstand positioniert sind.
- **Selbstmanagement (ALPEN & Eisenhower):** Methoden zur effizienten Strukturierung des Arbeitsalltags zur Vermeidung von Projektverzug und Stress.
    - 💡 **Praxisbeispiel:** Du sortierst morgens deine Support-Tickets nach der **Eisenhower-Matrix**: Ein akuter Serverausfall ist _Wichtig und Dringend_ (Quadrant A – sofort erledigen). Die Dokumentation eines abgeschlossenen Projekts ist _Wichtig, aber nicht dringend_ (Quadrant B – terminieren).
- **Informationsfluss & Dokumentation:** Vermeidung von "Information Silos" durch die Balance aus Bringschuld (aktives Melden von Status-Updates) und Holschuld (eigenständiges Einlesen im Wiki). Dokumentation sichert die rechtliche Nachweisbarkeit und den Know-how-Erhalt bei Personalwechseln.
    - 💡 **Praxisbeispiel:** Nach dem Patchen einer Firewall dokumentierst du die Änderungen sofort im Firmen-Wiki, um deiner Dokumentationspflicht nachzukommen und Kollegen den Haftungsschutz bei Folgeproblemen zu sichern.
    
	```mermaid
    graph TD
    A[Knappheit von Ressourcen] --> B(Zwang zum rationalen Wählen)
    B --> C{Ökonomisches Prinzip}
    C -->|Fixe Anforderung / Minimale Mittel| D[Minimalprinzip]
    C -->|Fixes Budget / Maximaler Erfolg| E[Maximalprinzip]
    
    F[Bedürfnis nach IT-Infrastruktur] --> G(Bedarf + Kaufkraft)
    G --> H[Nachfrage am Markt]
    
    I[Gesamtaufgabe] -->|Aufgabenanalyse| J[Teilaufgaben]
    J -->|Aufgabensynthese| K[Stelle / Planstelle]
    K --> L[Abteilung]
    ```
