## tags: [fisi, ihk, lernsheet]
## 🧭 Navigation & Zusammenhänge
- **Vorausgesetztes Thema:** [[07_Qualitätsmanagementsysteme & Normen (ISO 9000er-Reihe)]]
- **Nächstes Thema:** [[09_IT-Qualitätsmessung, -überwachung & -verbesserung]]
- **Verwandte Bausteine:** [[01_Grundlagen der IT-Sicherheit & Schutzziele]], [[16_Security by Design, IT-Grundschutz & Kontrollebenen]]
## 🎯 IHK-Prüfungsrelevanz

> [!IMPORTANT] AP01: Einrichten eines IT-gestützten Arbeitsplatzes
> 
> - **Relevanz:** Hoch
>     
> - **Fokus:** Sichere Konfiguration von IT-Systemen (Firewall, Virenscanner, Verschlüsselung), Umsetzung des Prinzip des kleinsten Privilegs (Least Privilege) beim User-Onboarding sowie Einhaltung der Identitätsprüfung und Multi-Faktor-Authentifizierung (MFA).
>     

> [!WARNING] AP02: Konzeption, Administration & Netzwerke
> 
> - **Relevanz:** Sehr hoch
>     
> - **Fokus:** Abgrenzung von Informationssicherheit, IT-Sicherheit und Datenschutz, Definition und Anwendung aller Schutzziele (CIA-Triade & CIANA+PS), risikobasiertes Denken, Notfallplanung/USV/Redundanz zur Gewährleistung der Verfügbarkeit und gerichtsfeste Protokollierung (Logging) zur Nichtabstreitbarkeit.
>     

## 📖 Einfache Erklärung & Praxisbeispiele

Qualitätsmanagement (QM) und Informationssicherheit sind zwei Seiten derselben Medaille. Während das QM dafür sorgt, dass Prozesse wie vorgesehen, effektiv und effizient ablaufen, stellt die Informationssicherheit sicher, dass ein Prozess nicht unbeabsichtigt oder böswillig manipuliert wird. Beide nutzen das gleiche Fundament: Prozessorientierung, Dokumentation, klare Verantwortlichkeiten, den PDCA-Zyklus und risikobasiertes Denken.

### Begriffsabgrenzung:

- **Informationssicherheit:** Der Gesamtrahmen zum Schutz aller geschäftlich relevanten Informationen (digital, gedruckt, gesprochen oder visuell), um Betrieb und Unternehmenswerte zu sichern.
    
- **IT-Sicherheit:** Ein Teilbereich der Informationssicherheit, der sich auf den technischen Schutz von IT-Systemen und elektronischen Daten konzentriert (z. B. Firewalls, Virenscanner, Verschlüsselung).
    
- **Datenschutz (Data Privacy):** Schutz des Grundrechts natürlicher Personen auf informationelle Selbstbestimmung bei der Verarbeitung personenbezogener Daten (z. B. Name, IP-Adresse, Standortdaten).
    

### Unterthemen & Schutzziele im Überblick (CIANA+PS):

- **Verknüpfung QM & Informationssicherheit:** Prozesse werden aus zwei Blickwinkeln betrachtet.
    
    - 💡 **Praxisbeispiel (Patch-Management):** QM fragt: _"Gibt es einen dokumentierten Standardprozess zum Einspielen von Updates?"_ Informationssicherheit fragt: _"Schließt der Patch eine kritische Sicherheitslücke und wie schnell wird er eingespielt, um das Angriffsfenster zu minimieren?"_
        
    - 💡 **Praxisbeispiel (User-Onboarding):** QM achtet darauf, dass der neue Mitarbeiter am 1. Arbeitstag alle Zugänge vorfindet. Die Sicherheits-Perspektive prüft, ob seine Identität zweifelsfrei verifiziert wurde und ob ihm strikt nach dem _Least-Privilege-Prinzip_ nur die absolut notwendigen Rechte zugewiesen werden.
        
- **Die Klassische CIA-Triade (Basis-Schutzziele):**
    
    - **Confidentiality (Vertraulichkeit):** Schutz vor unbefugter Kenntnisnahme und Mitlesen.
        
        - 💡 **Praxisbeispiel:** Der Zugriff auf Verzeichnisse der Personalabteilung wird per ACL und Verschlüsselung so beschränkt, dass nur HR-Mitarbeiter Zugriff haben.
            
    - **Integrity (Integrität):** Schutz vor unbemerkter und unautorisierter Manipulation/Verfälschung.
        
        - 💡 **Praxisbeispiel:** Beim Herunterladen einer ISO-Datei oder beim Online-Banking wird die Korrektheit mittels kryptografischer Prüfsummen (Hashes) sichergestellt.
            
    - **Availability (Verfügbarkeit):** Schutz vor Ausfall und Gewährleistung des Zugriffs bei Bedarf.
        
        - 💡 **Praxisbeispiel:** Um den Ausfall von Servern bei Stromausfällen abzufangen, werden redundante Netzteile an eine USV (Unterbrechungsfreie Stromversorgung) angeschlossen.
            
- **Erweiterte Schutzziele (CIANA+PS):**
    
    - **Authenticity (Authentizität):** Echtheit und Glaubwürdigkeit eines Benutzers oder der Quelle einer Information.
        
        - 💡 **Praxisbeispiel:** Ein Systemadministrator authentifiziert sich am VPN per Passwort und MFA-Token (Benutzer), während eingehende E-Mails per DKM/S/MIME digital signiert werden (Information).
            
    - **Non-Repudiation (Nichtabstreitbarkeit / Verbindlichkeit):** Beweisbarkeit von durchgeführten Aktionen.
        
        - 💡 **Praxisbeispiel:** Ein zentrales Logfile der Firewall dokumentiert rechtssicher und unmanipulierbar mit Zeitstempel, welcher Administrator um 14:32 Uhr eine Regel angepasst hat.
            
    - **Privacy (Datenschutz):** Wahrung der Rechte natürlicher Personen bei der Verwertung persönlicher Daten durch Maßnahmen wie Datensparsamkeit und Anonymisierung.
        
        - 💡 **Praxisbeispiel:** Testdatenbanken für Anwendungsentwickler enthalten keine Klarnamen oder echte Kreditkartennummern, sondern vollständig pseudonymisierte Datensätze.
            
    - **Safety (Betriebssicherheit):** Schutz von Menschen, Umwelt und Sachwerten vor physischen Schäden durch IT-Systeme (Fail-Safe-Konzept).
        
        - 💡 **Praxisbeispiel:** Fällt der Steuerungsserver einer industriellen Roboterzelle im Werk aus, geht das System sofort in den gesicherten Not-Halt-Zustand über, anstatt unkontrollierte Bewegungen auszuführen.
    ```mermaid
    graph TD
    subgraph Das Gesamtbild der Sicherheit
        IS[Informationssicherheit: Schutz aller Unternehmenswerte & Informationen] --> IT[IT-Sicherheit: Technischer Schutz von Systemen & Daten]
        IS --> DS[Datenschutz: Schutz natürlicher Personen & personenbezogener Daten]
    end

    subgraph Schutzziele CIANA+PS
        CIA[CIA-Triade] --> C[Vertraulichkeit / Confidentiality]
        CIA --> I[Integrität / Integrity]
        CIA --> A[Verfügbarkeit / Availability]
        
        EXT[Erweiterungen] --> AUT[Authentizität / Authenticity]
        EXT --> NR[Nichtabstreitbarkeit / Non-Repudiation]
        EXT --> PR[Datenschutz / Privacy]
        EXT --> SAF[Betriebssicherheit / Safety]
    end

    IT --> CIA
    IT --> EXT
    ```
    