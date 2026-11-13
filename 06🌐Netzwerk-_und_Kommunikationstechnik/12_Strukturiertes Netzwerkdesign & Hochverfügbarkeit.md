tags: [fisi, ihk, lernsheet]
## 🧭 Navigation & Zusammenhänge
- **Vorausgesetztes Thema:** [[11_Netzwerksegmentierung Virtual Local Area Networks (VLANs)]]
- **Nächstes Thema:** [[13_Core-Dienste auf Anwendungsebene DHCP, DNS & E-Mail-Infrastruktur]]
- **Verwandte Bausteine:** [[17_Gerätekonfiguration & Netzwerksicherheit Switches, Router, ACLs & WLAN]], [[06_Stromversorgung, USV & Netzformen]]
---

🎯 IHK-Prüfungsrelevanz

> [!IMPORTANT] AP01: Einrichten eines IT-gestützten Arbeitsplatzes
> 
> - **Relevanz:** Hoch
> - **Fokus:** Anschluss von Endgeräten an der Zugangsschicht. Verständnis von Basiskonzepten wie **Power over Ethernet (PoE)** für VoIP-Telefone/Access Points, **Port Security** gegen unbefugte Geräte und **QoS-Klassifizierung** für unterbrechungsfreie Telefonie directly am Arbeitsplatz.

> [!WARNING] AP02: Konzeption, Administration & Netzwerke
> 
> - **Relevanz:** Extrem Hoch (IHK-Standard für Systemarchitektur)
> - **Fokus:** Du musst Netzwerktopologien nach dem klassischen **3-Schichten-Modell** oder der **Leaf-Spine-Architektur** konzipieren und begründen können. Ein absoluter Schwerpunkt sind IHK-Fragen zur Vermeidung von _Single Points of Failure (SPOF)_ mittels Redundanzverfahren. Die genaue Funktionsweise von **STP/RSTP**, **Link Aggregation (LACP)** und **FHRP (VRRP/HSRP)** wird in fast jeder Linux-/Netzwerk-Prüfung detailliert abgefragt.

---

📖 Einfache Erklärung & Praxisbeispiele

Ein professionelles Netzwerkdesign sorgt für Skalierbarkeit, Performance, Wartbarkeit und Hochverfügbarkeit. Um Ausfälle (Single Points of Failure) zu minimieren, wird gezielte **Redundanz** eingebaut. Diese redundanten Pfade müssen über spezielle Protokolle verwaltet werden, um fatale Nebenwirkungen (wie Layer-2-Schleifen) zu verhindern.

1. Das hierarchische 3-Schichten-Modell (Campus-Design)

Dieses klassische Modell teilt die Infrastruktur in drei logische Funktionsebenen auf:

- **Core Layer (Kernschicht):** Das Hochgeschwindigkeits-Backbone des Netzwerks. Seine einzige Aufgabe ist der ultraschnelle und zuverlässige Transport von Datenpaketen ohne komplexe Filterregeln.
- **Distribution Layer (Verteilschicht):** Die Schnittstelle dazwischen. Sie aggregiert die Kabel des Access Layers, setzt Netzwerkrichtlinien um (Access Control Lists - ACLs) und übernimmt das **Inter-VLAN-Routing** über Layer-3-Switches.
- **Access Layer (Zugangsschicht):** Der physikalische Anschluss für Endgeräte (PCs, Drucker, APs) über Layer-2-Switches. Hier greifen Port Security und PoE.
- _Hinweis:_ Kleinere Unternehmen verschmelzen Core und Distribution oft zu einem einzigen Baustein (**Collapsed Core**).

2. Moderne Alternative: Leaf-Spine-Architektur

Im modernen Rechenzentrum wird das 3-Schichten-Modell durch das **Zwei-Schichten-Modell (Leaf-Spine)** ersetzt. Es ist speziell für den **Ost-West-Traffic** (Server-zu-Server-Kommunikation) optimiert:

- Jeder Leaf-Switch (Top-of-Rack) ist mit **jedem** Spine-Switch verbunden (Full-Mesh).
- Es gibt keine direkten Querverbindungen innerhalb einer Schicht (nicht Leaf-zu-Leaf).
    
- **Vorteil:** Jeder Datenpfad hat eine exakt vorhersagbare, niedrige Latenz von genau 2 Hops (Leaf → Spine → Leaf). Schleifen blockierende Protokolle werden durch Layer-3-Routing (ECMP) bis zum Leaf komplett vermieden.

3. Protokolle für Hochverfügbarkeit & Redundanz

- **Spanning Tree Protocol (STP / RSTP - IEEE 802.1w):**  
    Schließt man Switches redundant mit mehreren Kabeln an, entstehen Layer-2-Schleifen. Broadcasts (wie ARP-Requests) laufen unendlich im Kreis (**Broadcast Storm**) und bringen das Netz zum Absturz. **RSTP** löst dies, indem es die Switches eine _Root Bridge_ wählen lässt, die Pfade berechnet und Schleifen-Pfade **logisch blockiert**. Es reagiert bei Topologieänderungen innerhalb weniger Sekunden.
- **Link Aggregation (LAG / LACP - IEEE 802.3ad):**  
    Bündelt mehrere physische Netzwerkports zu einer einzigen logischen Verbindung (z. B. EtherChannel). Das erhöht zeitgleich die Bandbreite und liefert Ausfallsicherheit, ohne dass RSTP die Ports blockiert.
- **First Hop Redundancy Protocol (FHRP - z. B. VRRP):**  
    Fällt das Standardgateway (der Router) eines Clients aus, erreicht er kein fremdes Netz mehr. **VRRP** schließt mehrere Router zusammen, die sich gegenüber den Clients als **eine einzige virtuelle IP- und MAC-Adresse** ausgeben. Fällt der aktive Router aus, übernimmt der Backup-Router die virtuelle IP völlig geräuschlos für den Client.
    ```mermaid
flowchart TD
    %% Hierarchisches Campus Design
    subgraph Campus [Hierarchisches Campus-Modell]
        Core[Core Layer <br> High-Speed Backbone]
        Dist1[Dist Layer Switch 1]
        Dist2[Dist Layer Switch 2]
        Acc[Access Layer Switch]
        
        Core === Dist1
        Core === Dist2
        Dist1 === Acc
        Dist2 === Acc
    end

    %% Leaf-Spine Design
    subgraph LeafSpine [Rechenzentrum: Leaf-Spine-Architektur]
        S1[Spine Switch 1]
        S2[Spine Switch 2]
        L1[Leaf Switch 1]
        L2[Leaf Switch 2]
        
        L1 === S1
        L1 === S2
        L2 === S1
        L2 === S2
    end

    %% Styling für fehlerfreies Rendering direkt zuweisen
    style Core fill:#1a365d,stroke:#fff,stroke-width:1px,color:#fff
    style Dist1 fill:#2b6cb0,stroke:#fff,stroke-width:1px,color:#fff
    style Dist2 fill:#2b6cb0,stroke:#fff,stroke-width:1px,color:#fff
    style Acc fill:#4a5568,stroke:#fff,stroke-width:1px,color:#fff
    style S1 fill:#2d3748,stroke:#fff,stroke-width:1px,color:#fff
    style S2 fill:#2d3748,stroke:#fff,stroke-width:1px,color:#fff
    style L1 fill:#2f855a,stroke:#fff,stroke-width:1px,color:#fff
    style L2 fill:#2f855a,stroke:#fff,stroke-width:1px,color:#fff

    ```
    
    🚨 Die 3 kritischen IHK-Stolperfallen

- **Verwechslung von Nord-Süd- und Ost-West-Traffic:** Die IHK verlangt in Konzeptfragen die Begründung für Architekturen. Antwort-Falle: Das klassische 3-Schichten-Modell ist optimal für _Nord-Süd-Traffic_ (Client-zu-Internet/Server). Die Leaf-Spine-Architektur ist das exakte Gegenstück für _Ost-West-Traffic_ (Server-zu-Server im RZ). Vertauschst du diese Einsatzzwecke in der Begründung, gibt es harten Punktabzug.
- **LAG-Bündelung ohne LACP-Aktivierung:** Bei der Frage nach der Einrichtung eines redundanten Uplinks zwischen Switches reicht es nicht zu schreiben: _"Ich stecke zwei Kabel ein"_. Du musst den Port-Modus benennen. Wer vergisst zu erwähnen, dass das dynamische Verhandlungsprotokoll **LACP (IEEE 802.3ad)** auf den Ports konfiguriert werden muss (Modus `active`), riskiert, dass RSTP die Verbindung wegen einer Schleife sofort wieder lahmlegt.
- **Falsche Gateway-Zuweisung bei FHRP/VRRP:** Richtest du in einer IHK-Inbetriebnahmesituation zwei Router mit VRRP ein (z. B. Router 1 mit IP `.2`, Router 2 mit IP `.3` und VRRP-Virtuell-IP auf `.1`), scheitern viele bei der Client-Konfiguration. Wenn du den Clients die physische IP von Router 1 als Standardgateway einträgst, hebelst du die Redundanz komplett aus. **Merke:** Die Clients müssen zwingend und ausnahmslos die **virtuelle IP** als Gateway eingetragen bekommen!