tags: [fisi, ihk, lernsheet]
## 🧭 Navigation & Zusammenhänge
- **Vorausgesetztes Thema:** [[19_Netzwerkprotokolle, Kern-Dienste & IHK-Portmatrix]]
- **Nächstes Thema:** [[02_DSGVO_und BDSG]]
- **Verwandte Bausteine:** [[08_Von der Qualität zur Sicherheit & Schutzziele (CIANA+PS)]], [[16_Security by Design, IT-Grundschutz & Kontrollebenen]]
---

🎯 IHK-Prüfungsrelevanz

> [!IMPORTANT] AP01: Einrichten eines IT-gestützten Arbeitsplatzes
> 
> - **Relevanz:** Mittel
> - **Fokus:** Implementierung grundlegender Schutzmaßnahmen am Client, wie lokale Verschlüsselungsverfahren (BitLocker), sichere Passwörter und das Verständnis von Zugriffskontrollen zur Gewährleistung der Vertraulichkeit.

> [!WARNING] AP02: Konzeption, Administration & Netzwerke
> 
> - **Relevanz:** Hoch
> - **Fokus:** Kernkompetenz für Systemintegratoren. Die IHK fordert regelmäßig die Definition und Abgrenzung der CIA-Schutzziele, die Klassifizierung von Risiken sowie die systematische Bedrohungsanalyse (z. B. mittels STRIDE-Modell oder Angriffsvektoren).

---

📖 Einfache Erklärung & Praxisbeispiele

Die **Informationssicherheit** umfasst den Schutz von Informationen und Informationssystemen vor unbefugtem Zugriff, Ausfällen, Manipulationen und Katastrophen. Während sich die _Informationssicherheit_ auf alle Datenmedien (auch Papier) bezieht, konzentriert sich die _IT-Sicherheit_ spezifisch auf den Schutz digitaler IT-Prozesse und technischer Systeme. Das Fundament bildet hierbei die sogenannte **CIA-Triade** (Vertraulichkeit, Integrität und Verfügbarkeit).

Unterthemen & Anschauliche Beispiele:

- **Vertraulichkeit (Confidentiality):** Daten dürfen nur von Personen eingesehen werden, die die entsprechende Berechtigung besitzen. Sie wird durch Verschlüsselung, Schulungen und Zugangskontrollen sichergestellt.
    - 💡 **Praxisbeispiel:** Ein Systemadministrator richtet für die Personalabteilung eine Ende-zu-Ende-Verschlüsselung sowie eine strikte ACL (Access Control List) ein, damit sensible Gehaltsdaten nicht von Mitarbeitern anderer Abteilungen eingesehen werden können.
- **Integrität (Integrity):** Die Unversehrtheit und absolute Korrektheit von Daten muss sowohl bei der Übertragung als auch bei der Speicherung garantiert sein. Manipulationen müssen ausgeschlossen oder sofort erkennbar sein.
    - 💡 **Praxisbeispiel:** Beim Download eines neuen Server-Betriebssystems prüft der FISI den SHA-256-Hash-Wert der ISO-Datei, um sicherzustellen, dass das Image auf dem Transportweg nicht durch einen Angreifer verändert wurde.
- **Verfügbarkeit (Availability):** Autorisierte Benutzer müssen jederzeit bei Bedarf auf Daten, Dienste und IT-Systeme zugreifen können. Ausfälle werden durch Redundanzen abgefangen.
    - 💡 **Praxisbeispiel:** Zur Absicherung des zentralen Datenbankservers installiert das IT-Team eine unterbrechungsfreie Stromversorgung (USV) im Serverraum und konfiguriert ein redundantes Storage-System (RAID) sowie tägliche automatisierte Backups.
- **Systematische Bedrohungsanalyse:** Um Schwachstellen frühzeitig aufzudecken, werden strukturierte Frameworks eingesetzt. Das **STRIDE-Modell** (Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege) hilft dabei, gezielt Angriffsvektoren zu identifizieren.
    - 💡 **Praxisbeispiel:** Vor dem Release einer neuen internen Web-API führt der FISI ein Threat Modeling durch, um zu prüfen, ob Angreifer über SQL-Injections (Information Disclosure) oder Rechteausweitung (Elevation of Privilege) unbefugten Zugriff erhalten könnten.
```mermaid
graph TD
    A[IT-Sicherheit & Informationsschutz] --> B[Die Kern-Schutzziele: CIA-Triade]
    A --> C[Erweiterte Schutzziele]
    A --> D[Methoden der Bedrohungsanalyse]

    subgraph CIA-Triade [CIA-Triade]
        B --> B1[Vertraulichkeit / Confidentiality]
        B --> B2[Integrität / Integrity]
        B --> B3[Verfügbarkeit / Availability]
        
        B1 --- B1_Ex[Maßnahme: Verschlüsselung & ACLs]
        B2 --- B2_Ex[Maßnahme: Hash-Werte & Prüfsummen]
        B3 --- B3_Ex[Maßnahme: Backups & USV / Redundanz]
    end

    subgraph Erweiterte Ziele [Erweiterte Schutzziele]
        C --> C1[Authentizität]
        C --> C2[Verbindlichkeit]
        C --> C3[Datenschutz / Privacy]
    end

    subgraph Analyse [Frameworks & Modellierung]
        D --> D1[STRIDE-Modell]
        D --> D2[BSI-Grundschutz]
        D --> D3[CVSS Schwachstellen-Score]
        D --> D4[Attack Trees / Angriffsäume]
    end

    style CIA-Triade fill:#f9f,stroke:#333,stroke-width:2px
    style Analyse fill:#bbf,stroke:#333,stroke-width:1px

```
