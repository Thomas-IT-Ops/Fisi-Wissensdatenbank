## tags: [fisi, ihk, lernsheet]
## 🧭 Navigation & Zusammenhänge
- **Vorausgesetztes Thema:** [[09_IT-Qualitätsmessung, -überwachung & -verbesserung]]
- **Nächstes Thema:** [[11_Prüf- und Testverfahren in der IT]]
- **Verwandte Bausteine:** [[11_Prüf- und Testverfahren in der IT]], [[09_Software-Qualität, Testing & Künstliche Intelligenz]]
## 🎯 IHK-Prüfungsrelevanz

> [!IMPORTANT] AP01: Einrichten eines IT-gestützten Arbeitsplatzes
> 
> - **Relevanz:** Hoch
>     
> - **Fokus:** Einhaltung technischer und organisatorischer Qualitätskontrollen bei der Arbeitsplatz- und Systembereitstellung (z. B. Konfigurationsstandards, Vier-Augen-Prinzip und Dokumentation).
>     

> [!WARNING] AP02: Konzeption, Administration & Netzwerke
> 
> - **Relevanz:** Sehr hoch
>     
> - **Fokus:** Abgrenzung von Qualitätsplanung ("was ist gut genug") und Qualitätslenkung ("im Betrieb dafür sorgen"), Bestimmung der 4 Qualitätsdimensionen, Ausarbeitung prüfbarer SMARTer SLAs und deren Unterbau (OLA, UC), Anwendung präventiver/detektiver/korrektiver Lenkungsmaßnahmen sowie Wirtschaftlichkeits- und ROI-Berechnungen von Vorbeugemaßnahmen.
>     

## 📖 Einfache Erklärung & Praxisbeispiele

**Qualitätsplanung** legt fest, was "gut genug" ist, bevor ein System oder Service live geht (Ziele, Ressourcen, Standards, SLAs). **Qualitätslenkung** überwacht und steuert den laufenden Betrieb, erkennt Abweichungen frühzeitig und steuert gegen, damit die festgelegten Zielwerte dauerhaft eingehalten werden.

### Unterthemen & Anschauliche Beispiele:

- **Die 4 Dimensionen der IT-Qualität:**
    
    - **Funktionelle Qualität:** Das System tut genau das, was es soll (fehlerfreie Funktion).
        
    - **Technische Qualität:** Antwortzeiten, Stabilität, Performanz und Sicherheit unter Last.
        
    - **Prozessqualität:** Die Abläufe im Hintergrund sind klar geregelt, dokumentiert und nachvollziehbar.
        
    - **Servicequalität:** Betreuung, Erreichbarkeit und Verlässlichkeit gegenüber den Endnutzern.
        
    - 💡 **Praxisbeispiel (Gastronomie-IT "Bella Napoli"):** Samstags zwischen 18 und 21 Uhr fallen 40 % des Wochenumsatzes an.
        
        - _Funktionell:_ Bestellungen aus der Smartphone-App kommen vollständig auf dem Küchen-Tablet an.
            
        - _Technisch:_ Webshop und Kassen-PC halten Spitzenlasten stand und verarbeiten Zahlungen ohne Absturz.
            
        - _Prozessual:_ Es ist klar definiert, was zu tun ist, wenn die Internetverbindung ausfällt.
            
        - _Service:_ Kunden erhalten ihre Pizza pünktlich zur zugesagten Zeit.
            
- **Verknüpfung von SLA, OLA und UC:**
    
    - **SLA (Service Level Agreement):** Zusage des IT-Dienstleisters an den Kunden (z. B. 99,5 % Verfügbarkeit am Samstagabend).
        
    - **OLA (Operational Level Agreement):** Interne Vereinbarung zwischen IT-Teams (z. B. Netzwerk-Team garantiert dem Web-Team max. 15 Minuten Reaktionszeit).
        
    - **UC (Underpinning Contract):** Vertrag mit externen Zulieferern (z. B. SLA mit dem Zahlungsdienstleister).
        
    - ⚠️ **Wichtiger Grundsatz:** Ein SLA ist nur so belastbar wie die OLAs und UCs darunter! Deckt der externe Zahlungsdienstleister die kritische Servicezeit nicht ab, kann das SLA gegenüber dem Kunden nicht eingehalten werden.
        
- **Klassifikation der Lenkungsmaßnahmen (Präventiv, Detektiv, Korrektiv):**
    
    - **Präventiv (Fehler vermeiden):** Testen von Updates unter Last in einer Staging-Umgebung, Vier-Augen-Prinzip, Infrastructure as Code.
        
    - **Detektiv (Fehler erkennen):** Automatisierte Monitoring-Systeme und Alerting schlagen Alarm, noch bevor Kunden Ausfälle bemerken.
        
    - **Korrektiv (Fehler beheben):** Automatisiertes Rollback oder Einspielen von Patches nach einer Störung.
        
- **Qualitätskosten & Return on Investment (ROI):**
    
    - **Fehlerverhütungs- & Prüfkosten:** Geplante Ausgaben für Tests, Qualitätstools und Reviews (Shift-Left).
        
    - **Fehlerkosten:** Ungeplante Kosten durch Ausfälle, Nacharbeit, Imageschäden und entgangenen Umsatz.
        
    - **Optimaler Investitionspunkt:** Dahinter kostet zusätzliche Vorbeugung mehr, als sie an Fehlerkosten einspart.
        
    - 💡 **Praxisbeispiel (ROI-Berechnung):**
        
        - $$ROI = \frac{\text{Nutzen} - \text{Kosten}}{\text{Kosten}} \times 100\%$$
            
        - Vermeidung von 2 Ausfällen samstags = **4.000 € eingesparter Umsatzverlust (Nutzen)**.
            
        - Kosten für vorbeugendes Monitoring & Staging-Tests = **1.600 € (Kosten)**.
            
        - $$ROI = \frac{4.000 € - 1.600 €}{1.600 €} \times 100\% = 150\%$$
    ```mermaid
    graph TD
    subgraph 1. Qualitätsplanung: Was ist gut genug?
        SMART[SMART-Qualitätsziele festlegen] --> DIM[4 Dimensionen: Funktionell, Technisch, Prozess, Service]
        DIM --> SLA[SLA-Definition: Messbare Zielwerte]
        SLA --> BASE[Unterbau absichern: OLAs & UCs]
    end

    subgraph 2. Qualitätslenkung: Betrieb auf Kurs halten
        PREV[Präventiv: Tests, CI/CD, Code-Reviews] --> DET[Detektiv: Monitoring & Alerting]
        DET --> KORR[Korrektiv: Incident & Root-Cause-Analyse]
    end

    BASE --> PREV
    KORR --> SMART
    ```
    