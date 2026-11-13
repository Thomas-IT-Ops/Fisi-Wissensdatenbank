Nachdem das Fundament der **globalen Infrastruktur** (Regionen, AZs, Edge Locations) felsenfest sitzt, schauen wir uns das wichtigste Rechen-Workhorse von AWS an: **Amazon EC2 (Elastic Compute Cloud)**.

EC2 stellt dir virtuelle Server (Instanzen) in der Cloud bereit. Ein absolut zentrales Thema für die **CLF-C02-Prüfung** sind die **EC2-Preismodelle**.

#### Die 4 wichtigsten EC2-Preismodelle:

1. **On-Demand (Nach Bedarf):**
    
    - _Prinzip:_ Du zahlst sekunden- oder minutengenau nur für die Zeit, in der die Instanz läuft. Keine Mindestlaufzeit, keine Vorauszahlung.
        
    - _Einsatz:_ Unvorhersehbare Workloads, Tests, Entwicklung, neue Anwendungen ohne historische Daten.
        
2. **Reserved Instances (Reservierte Instanzen):**
    
    - _Prinzip:_ Du verpflichtest dich fest für **1 oder 3 Jahre**. Dafür erhältst du erhebliche Rabatte (bis zu 72 %) im Vergleich zu On-Demand.
        
    - _Einsatz:_ Vorhersehbare, kontinuierliche Workloads ("Steady-State"), z. B. die Hauptdatenbank einer Firma.
        
3. **Spot Instances:**
    
    - _Prinzip:_ Du nutzt ungenutzte AWS-Rechenkapazität zu extrem niedrigen Preisen (bis zu 90 % Rabatt). **Haken:** AWS kann dir die Instanz mit einer Vorwarnzeit von nur **2 Minuten** entziehen, wenn die Kapazität anderweitig benötigt wird!
        
    - _Einsatz:_ Unterbrechbare, unterbrechungstolerante, hochflexible Batch-Jobs, Big-Data-Analysen oder Bild-/Videorendering.
        
4. **Dedicated Hosts (Dedizierte Hosts):**
    
    - _Prinzip:_ Ein physischer Server, der komplett und exklusiv für dich reserviert ist.
        
    - _Einsatz:_ Strenge Compliance-Vorgaben oder spezielle Software-Lizenzen, die an physische Sockets/Cores gebunden sind (z. B. ältere Microsoft- oder Oracle-Lizenzen).