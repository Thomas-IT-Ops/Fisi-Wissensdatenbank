tags: [fisi, ihk, lernsheet]
## 🧭 Navigation & Zusammenhänge
- **Vorausgesetztes Thema:** [[04_Rechtliche Rahmenbedingungen & IT-Sicherheitsberatung]]
- **Nächstes Thema:** [[06_Audits & Zertifizierungen]]
- **Verwandte Bausteine:** [[07_Qualitätsmanagementsysteme & Normen (ISO 9000er-Reihe)]], [[09_IT-Qualitätsmessung, -überwachung & -verbesserung]]
---

🎯 IHK-Prüfungsrelevanz

> [!IMPORTANT] AP01: Einrichten eines IT-gestützten Arbeitsplatzes
> 
> - **Relevanz:** Mittel
> - **Fokus:** Einhaltung standardisierter Arbeitsabläufe bei Bereitstellungen (z. B. Nutzung von QM-Checklisten bei der Client-Einarbeitung oder Hardware-Konfiguration, um Fehlerkosten und Nacharbeit zu reduzieren).

> [!WARNING] AP02: Konzeption, Administration & Netzwerke
> 
> - **Relevanz:** Hoch
> - **Fokus:** Regelmäßiger Bestandteil von Wirtschafts- und Geschäftsprozess-Aufgaben. Die IHK prüft hier die strategischen Unterschiede zwischen **Qualitätsmanagement (QM)** und **Qualitätssicherung (QS)**, die sieben Grundprinzipien nach **ISO 9000 / 9001** sowie die praktische Anwendung des **PDCA-Zyklus (KVP)** auf IT-Services (z. B. im IT-Support/Helpdesk).

---

📖 Einfache Erklärung & Praxisbeispiele

Fehler, Systemausfälle und Datenverluste kosten Unternehmen massives Geld und zerstören Kundenvertrauen. Deshalb bildet das Qualitätsmanagement zusammen mit der IT-Sicherheit und dem Datenschutz einen untrennbaren **Dreiklang** im IT-Betrieb: **Qualität** sorgt für verlässliche, reproduzierbare Prozesse, **Sicherheit** schützt die Systeme und **Datenschutz** schützt den Menschen. Das moderne Qualitätsverständnis besagt: _Qualität entsteht im laufenden Prozess, nicht durch eine nachträgliche Endprüfung_.

Unterthemen & Anschauliche Beispiele:

- **Qualitätsmanagement (QM) vs. Qualitätssicherung (QS):**
    - **QM (strategisch):** Das übergeordnete System zur Planung, Steuerung und kontinuierlichen Verbesserung aller Qualitätsaspekte im Unternehmen.
    - **QS (operativ):** Konkrete Maßnahmen, um Fehler während der Umsetzung direkt zu prüfen und gezielt zu vermeiden (z. B. Testverfahren).
    - 💡 **Praxisbeispiel:** Die IT-Abteilung legt fest, dass alle Ticket-Lösungen nach festen Kriterien ausgewertet werden (**QM**). Der Techniker nutzt beim Schließen des Tickets zwingend ein vorgegebenes Prüfskript (**QS**).
- **Das Qualitätsmanagementsystem (QMS) nach ISO 9001:** Ein strukturiertes Rahmenwerk, das Rollen, Dokumente und messbare Kennzahlen (KPIs) definiert, um Arbeitsergebnisse vergleichbar und zertifizierbar zu machen. Es basiert auf den ISO-9000-Grundprinzipien wie **Kundenorientierung**, **Prozessorientierung** und **faktengestützten Entscheidungen**.
    - 💡 **Praxisbeispiel:** Das QMS definiert die Qualitätspolitik: _"90% aller Helpdesk-Anfragen müssen innerhalb von 24h gelöst sein"_. Statt Entscheidungen nach "Bauchgefühl" zu treffen, wertet der Abteilungsleiter monatlich die Ticket-KPIs aus, um Engpässe zu identifizieren.
- **Der PDCA-Zyklus (Kontinuierlicher Verbesserungsprozess - KVP):** Auch bekannt als _Deming-Kreis_ oder _Kaizen-Ansatz_. Er beschreibt die dauerhafte Routine zur Optimierung von IT-Abläufen in vier Schritten:
    
    1. **Plan:** Ziel und Methode festlegen (z. B. Reaktionszeit im Support optimieren).
    2. **Do:** Umsetzung im kleinen, kontrollierten Rahmen (z. B. neue Support-Checkliste im Team A testen).
    3. **Check:** Ergebnisse anhand von Daten prüfen und mit dem Ziel abgleichen.
    4. **Act:** Erfolg absichern, den Prozess als neuen Standard etablieren und global ausrollen.
    
    - 💡 **Praxisbeispiel:** Nach häufigen Fehlern bei Server-Updates (_Plan_) führt der FISI ein standardisiertes Bereitstellungs-Protokoll ein (_Do_). Nach drei Wochen wird geprüft, ob die Fehler zurückgingen (_Check_). Das Protokoll wird zur offiziellen Arbeitsanweisung für alle Admins erklärt (_Act_).
    ```mermaid
    flowchart TD
    subgraph Dreiklang [Der IT-Dreiklang]
        A[Qualität<br>Verlässliche Prozesse] <--> B[Sicherheit<br>Schutz von Systemen]
        B <--> C[Datenschutz<br>Schutz von Menschen]
        C <--> A
    end

    subgraph QMS [ISO 9001 Rahmenwerk]
        D[Qualitätspolitik & SMART-Ziele] --> E[Verantwortlichkeiten & Prozesse]
        E --> F[Dokumentation & Überwachung]
        F --> G[Kontinuierliche Verbesserung / KVP]
        G --> D
    end

    subgraph PDCA [PDCA-Zyklus / Deming-Kreis]
        direction LR
        P[Plan<br>Ziel definieren] --> D_[Do<br>Im Kleinen testen]
        D_ --> C_[Check<br>Ergebnis prüfen]
        C_ --> Act[Act<br>Standardisieren]
        Act --> P
    end

    QMS --> |Methodik zur Umsetzung| PDCA
    Dreiklang -.-> |Fundament| QMS

    style Dreiklang fill:#f2f2f9,stroke:#333,stroke-width:1px
    style QMS fill:#f2f9f2,stroke:#00aa00,stroke-width:2px
    style PDCA fill:#fff9e6,stroke:#ffaa00,stroke-width:1px

    ```
    