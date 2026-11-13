tags: [fisi, ihk, lernsheet]
## 🧭 Navigation & Zusammenhänge
- **Vorausgesetztes Thema:** [[01_Grundlagen der IT-Sicherheit & Schutzziele]]
- **Nächstes Thema:** [[03_Gefahrenquellen, Malware-Typen & Gegenmaßnahmen]]
- **Verwandte Bausteine:** [[04_Rechtliche Rahmenbedingungen & IT-Sicherheitsberatung]], [[04_Technical English Cyber Security & Data Privacy]]
---

🎯 IHK-Prüfungsrelevanz

> [!IMPORTANT] AP01: Einrichten eines IT-gestützten Arbeitsplatzes
> 
> - **Relevanz:** Mittel bis Hoch
> - **Fokus:** Praktische Umsetzung von **Technischen und organisatorischen Maßnahmen (TOMs)** direkt am Arbeitsplatz. Dazu gehören Festplattenverschlüsselung, Passwortrichtlinien, Bildschirmsperren und die physische Zugangskontrolle zur Einhaltung der DSGVO-Grundprinzipien (wie Datenminimierung).

> [!WARNING] AP02: Konzeption, Administration & Netzwerke
> 
> - **Relevanz:** Hoch
> - **Fokus:** In Kundenprojekten oder Netzwerkkonzepten fordert die IHK die exakte Einhaltung rechtlicher Vorgaben. Essentiell sind das Beherrschen der **Meldepflicht bei Datenschutzverletzungen (72-Stunden-Regel)**, die Ausgestaltung von Verträgen zur **Auftragsverarbeitung (AVV)** sowie die gesetzlichen Pflichten zur Benennung eines **Datenschutzbeauftragten (DSB)**.

---

📖 Einfache Erklärung & Praxisbeispiele

Der Datenschutz beruht in Europa maßgeblich auf der **Datenschutz-Grundverordnung (DSGVO)** und schützt personenbezogene Daten vor Missbrauch. Im IT-Umfeld gilt das fundamentale Prinzip des **Verbots mit Erlaubnisvorbehalt**: Jede Verarbeitung personenbezogener Daten ist grundsätzlich verboten, es sei denn, es liegt eine gesetzliche Rechtsgrundlage (z. B. Einwilligung, Vertragserfüllung) vor. Als Systemintegrator bist du dafür verantwortlich, Systeme so zu konzipieren, dass sie die gesetzlichen Prinzipien technisch erzwingen und absichern.

Unterthemen & Anschauliche Beispiele:

- **Grundprinzipien der DSGVO:** Daten müssen rechtmäßig, transparent und zweckgebunden verarbeitet werden. Die **Datenminimierung** fordert, dass nur für den Zweck absolut notwendige Daten erhoben werden. Zudem gilt eine **Speicherbegrenzung** (Daten müssen gelöscht werden, wenn der Zweck entfällt).
    - 💡 **Praxisbeispiel:** Ein FISI konfiguriert das CRM-System eines Kunden so, dass Altdaten von Leads nach Ablauf der gesetzlichen Aufbewahrungsfristen automatisch vollständig gelöscht oder anonymisiert werden (**Speicherbegrenzung**).
- **Technische und organisatorische Maßnahmen (TOMs):** Nach Art. 32 DSGVO müssen dem Risiko angemessene Schutzmaßnahmen dokumentiert und regelmäßig aktualisiert werden. _Technische Maßnahmen_ betreffen die Hard- und Software (z. B. Verschlüsselung), _organisatorische Maßnahmen_ betreffen Abläufe und Personen (z. B. Mitarbeiterschulungen).
    - 💡 **Praxisbeispiel:** Um den unbefugten Zugriff auf Kundendaten zu verhindern, implementiert das IT-Team eine **Zugangs- und Zugriffskontrolle** mittels Active Directory und rollenbasierter Rechtevergabe (RBAC) sowie eine Multi-Faktor-Authentisierung (MFA) für den VPN-Zugang.
- **Verantwortliche und Auftragsverarbeiter:** Der _Verantwortliche_ entscheidet über Zwecke und Mittel der Datenverarbeitung (z. B. das Kundenunternehmen). Der _Auftragsverarbeiter_ verarbeitet Daten streng weisungsgebunden im Auftrag (z. B. ein Cloud-Hoster oder externer IT-Dienstleister). Hierfür ist ein **Auftragsverarbeitungs-Vertrag (AVV)** rechtlich zwingend erforderlich.
    - 💡 **Praxisbeispiel:** Dein IT-Systemhaus hostet die Mailserver für eine Arztpraxis. Da ihr Zugriff auf sensible Patientendaten haben könntet, muss zwischen eurem Systemhaus (**Auftragsverarbeiter**) und der Praxis (**Verantwortlicher**) ein AV-Vertrag geschlossen werden, der eure Weisungsgebundenheit regelt.
- **Datenschutzverletzungen (Data Breaches):** Kommt es zu einer Sicherheitsverletzung (z. B. durch ein Datenleck oder Ransomware), greift eine strikte **72-Stunden-Meldepflicht** an die zuständige Aufsichtsbehörde. Bei hohem Risiko für die Betroffenen müssen auch diese unverzüglich benachrichtigt werden. Jeder Vorfall muss intern lückenlos dokumentiert werden.
    - 💡 **Praxisbeispiel:** Nach einer Ransomware-Attacke stellt das IT-Team fest, dass Kundendaten abgeflossen sind. Der FISI unterstützt das Management dabei, den Vorfall innerhalb der gesetzlichen **72-Stunden-Frist** an den Landesdatenschutzbeauftragten zu melden.
- **Der Datenschutzbeauftragte (DSB):** Unternehmen müssen unter bestimmten gesetzlichen Voraussetzungen (z. B. ab 20 Personen, die ständig automatisiert Daten verarbeiten, oder bei der Verarbeitung besonderer Datenkategorien wie Gesundheitsdaten) einen DSB benennen. Seine Aufgaben sind die Beratung, Überwachung der DSGVO-Einhaltung und die Zusammenarbeit mit den Behörden.
    - 💡 **Praxisbeispiel:** Bei der Planung eines neuen Zeiterfassungssystems mittels Biometrie (Fingerabdruck) zieht das Projektteam den internen DSB hinzu, um eine **Datenschutz-Folgenabschätzung (DSFA)** durchzuführen.
    ```mermaid
    flowchart TD
    subgraph Prinzipien [DSGVO-Kernpunkte]
        A[Rechtmäßigkeit & Transparenz] --> A1[Verbot mit Erlaubnisvorbehalt]
        B[Zweckbindung & Datenminimierung] --> B1[Nur erforderliche Daten erheben]
        C[Speicherbegrenzung] --> C1[Automatische Löschkonzepte]
    end

    subgraph Rollen [Akteure & Verträge]
        V[Verantwortlicher<br>entscheidet über Zweck/Mittel] -- weist an / AV-Vertrag --> AV[Auftragsverarbeiter<br>verarbeitet weisungsgebunden]
        V -- Daten & Verträge --> BP[Betroffene Person]
        BP -- Rechteausübung: Auskunft/Löschung --> V
    end

    subgraph Notfall [Prozess bei Datenpanne]
        E[Datenschutzverletzung] --> E1[Interne Meldung & Erstbewertung]
        E1 --> E2[Risikobewertung]
        E2 -- Risiko vorhanden --> E3[Meldung an Aufsichtsbehörde<br>max. 72 Stunden]
        E2 -- Hohes Risiko für Individuum --> E4[Benachrichtigung der Betroffenen]
        E2 --> E5[Lückenlose Dokumentation & Aufarbeitung]
    end

    subgraph TOMs [Technische & Organisatorische Maßnahmen - Art. 32]
        T1[Technische Maßnahmen] --> T1a[Verschlüsselung & Pseudonymisierung]
        T1 --> T1b[Zugangs-/Zugriffskontrollen MFA/ACL]
        T1 --> T1c[Wiederherstellbarkeit Backups/USV]
        
        O1[Organisatorische Maßnahmen] --> O1a[Mitarbeiterschulungen]
        O1 --> O1b[Richtlinien & Dokumentationspflichten]
    end

    style Prinzipien fill:#f9f2f2,stroke:#333,stroke-width:1px
    style Rollen fill:#f2f2f9,stroke:#333,stroke-width:1px
    style Notfall fill:#fff9e6,stroke:#ffcc00,stroke-width:2px
    style TOMs fill:#f2f9f2,stroke:#333,stroke-width:1px

    ```
    
    