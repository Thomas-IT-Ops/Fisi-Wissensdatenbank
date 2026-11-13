---
tags: [fisi, ihk, lernsheet]
---
## 🧭 Navigation & Zusammenhänge
- **Vorausgesetztes Thema:** [[02_Das ISO, OSI-Referenzmodell & TCP, IP-Schichtenmodell]]
- **Nächstes Thema:** [[04_Ethernet-Grundlagen, MAC-Adressen & Rahmenstrukturen]]
- **Verwandte Bausteine:** [[05_IPv4-Grundlagen, Subnetting & Adressbereiche]], [[04_Hexadezimalsystem, MAC-Adressen & Nibbles]]
---

## 🎯 IHK-Prüfungsrelevanz
> [!IMPORTANT] AP01: Einrichten eines IT-gestützten Arbeitsplatzes
> - **Relevanz:** Hoch
> - **Fokus:** Zuordnung von Hardwarekomponenten (z. B. Kabel, Netzwerkkarte) und Medientypen zu den untersten Schichten (Schicht 1 und 2) beim physischen Aufbau von Arbeitsplätzen.

> [!WARNING] AP02: Konzeption, Administration & Netzwerke
> - **Relevanz:** Extrem Hoch (Absolutes IHK-Standardthema!)
> - **Fokus:** Du musst in fast jeder Prüfung Protokolle (wie TCP, UDP, IP), Hardware (Router, Switches, Hubs) oder logische Adresseinheiten (Pakete, Frames, Bits) fehlerfrei den 7 Schichten des OSI-Modells oder den 4 Schichten des TCP/IP-Modells zuordnen können. Ein weiterer Schwerpunkt ist das Verständnis der Datenverkapselung über die Schichten hinweg.

---

## 📖 Einfache Erklärung & Praxisbeispiele
Das **ISO/OSI-Referenzmodell** beschreibt die netzwerkbasierte Kommunikation zwischen unterschiedlichen technischen Systemen anhand von **sieben übereinanderliegenden Schichten** mit eng begrenzten Schwerpunkten. Jede Schicht nutzt die Dienste der darunterliegenden Schicht und stellt der darüberliegenden Schicht eigene Dienste bereit. Das **TCP/IP-Modell** fasst diese für die Praxis des Internet-Protokollstapels in **vier Schichten** zusammen.

### Unterthemen & Anschauliche Beispiele:

- **Die Bitübertragungsschicht (Layer 1 - Physical Layer):**
  Verwaltet die rein physikalische Übertragung über mechanische oder elektrische Hilfsmittel (Kupferkabel, Glasfaser, WLAN-Wellen) als reine Punkt-zu-Punkt-Verbindung.
  - 💡 **Praxisbeispiel:** Ein FISI crimpt ein Cat6-Twisted-Pair-Kabel. Die elektrischen Signale, die durch die Adern fließen, bewegen sich rein auf Schicht 1.

- **Die Sicherungsschicht (Layer 2 - Data Link Layer):**
  Regelt den Zugriff auf das Übertragungsmedium, fügt Prüfsummen zur Fehlererkennung hinzu und verpackt Daten in Blöcke, sogenannte **Frames** (Rahmen). Hier arbeiten MAC-Adressen und Switches.
  - 💡 **Praxisbeispiel:** Ein Switch liest die Ziel-MAC-Adresse aus einem eintreffenden Ethernet-Frame aus, um zu entscheiden, an welchen Port das Datenpaket exakt weitergeleitet werden muss.

- **Die Vermittlungsschicht (Layer 3 - Network Layer):**
  Zuständig für die netzübergreifende **Ende-zu-Ende-Vermittlung** und das **Routing** von Datenpaketen über mehrere Zwischenstationen (Hops) hinweg. Hier greift das Internet-Protokoll (IP) mit IP-Adressen.
  - 💡 **Praxisbeispiel:** Ein Router analysiert die Ziel-IP-Adresse eines Pakets und ermittelt anhand seiner Routingtabelle das nächste Standardgateway, um die Netzwerkgrenze zu überbrücken.

- **Die Transportschicht (Layer 4 - Transport Layer):**
  Steuert die Segmentierung des Datenstroms und ordnet Datenpakete über **Ports** einem konkreten Dienst auf dem System zu. Die Kernprotokolle sind TCP (verbindungsorientiert) und UDP (verbindungslos).
  - 💡 **Praxisbeispiel:** Wenn auf einem Server gleichzeitig ein Webserver (Port 80/443) und ein SSH-Dienst (Port 22) laufen, sorgt Schicht 4 dafür, dass die eingehenden TCP-Segmente der richtigen Anwendung zugeordnet werden.

- **Die anwendungsorientierten Schichten (Layer 5 bis 7):**
  Die Schichten Sitzung (Layer 5), Darstellung (Layer 6 - Kompression/Verschlüsselung) und Anwendung (Layer 7 - Ein-/Ausgabe für UI) regeln die logische Verbindung und Datenaufbereitung direkt für die Software-Applikationen.
  - 💡 **Praxisbeispiel:** Das Protokoll HTTPS nutzt TLS auf Schicht 6, um Daten zu verschlüsseln, bevor die eigentliche Website-Anzeige über HTTP auf Schicht 7 im Browser (UI) ausgegeben wird.

---

## 📊 Visuelle Darstellung (Mermaid.js)
```mermaid
flowchart LR
    subgraph OSI [ISO/OSI-Referenzmodell (7 Schichten)]
        direction TB
        O7[Schicht 7: Anwendungsschicht <br>Application Layer]:::app
        O6[Schicht 6: Darstellungsschicht <br>Presentation Layer]:::app
        O5[Schicht 5: Sitzungsschicht <br>Session Layer]:::app
        O4[Schicht 4: Transportschicht <br>Transport Layer]:::trans
        O3[Schicht 3: Vermittlungsschicht <br>Network Layer]:::net
        O2[Schicht 2: Sicherungsschicht <br>Data Link Layer]:::link
        O1[Schicht 1: Bitübertragungsschicht <br>Physical Layer]:::phys
        
        O7 --> O6 --> O5 --> O4 --> O3 --> O2 --> O1
    end

    subgraph TCP [TCP/IP-Modell (4 Schichten)]
        direction TB
        T4[Schicht 4: Anwendung <br>Application]:::app
        T3[Schicht 3: Transport <br>Transport]:::trans
        T2[Schicht 2: Internet <br>Internet]:::net
        T1[Schicht 1: Netzzugang <br>Network Access]:::link
        
        T4 --> T3 --> T2 --> T1
    end

    %% Mappings zwischen den Modellen
    O7 -.-> T4
    O6 -.-> T4
    O5 -.-> T4
    O4 -.-> T3
    O3 -.-> T2
    O2 -.-> T1
    O1 -.-> T1

    %% Styling
    classDef app fill:#2d3748,stroke:#fff,color:#fff;
    classDef trans fill:#2b6cb0,stroke:#fff,color:#fff;
    classDef net fill:#2f855a,stroke:#fff,color:#fff;
    classDef link fill:#4a5568,stroke:#fff,color:#fff;
    classDef phys fill:#1a365d,stroke:#fff,color:#fff;
```

---

## 🚨 Die 3 kritischen IHK-Stolperfallen

- **Verwechslung von Protokolleinheiten (PDU):** Die IHK zieht in Prüfungsfragen gezielte Punktabzüge ab, wenn du die Begriffe vermischt. Merkregel: Auf Schicht 2 sprechen wir von **Frames (Rahmen)**, auf Schicht 3 von **Paketen** und auf Schicht 4 von **Segmenten** (bei TCP) bzw. **Datagrammen** (bei UDP).
- **Falsche Zuordnung von Hardwarekomponenten:** Ein klassischer Fehler ist die Annahme, ein Router arbeite auf Schicht 2 oder ein Switch auf Schicht 3. Standard-Switches arbeiten strikt auf **Schicht 2** (MAC-Ebene), Router strikt auf **Schicht 3** (IP-Ebene). *Ausnahme:* Schicht-3-Switches, diese müssen in der Prüfung aber explizit so benannt werden.
- **Modell-Verschmelzung bei TCP/IP:** Wer im TCP/IP-Modell nach der "Sicherungsschicht" oder dem "Internet-Layer im OSI-Modell" sucht, scheitert. Präge dir das Mapping genau ein: Schicht 1 und 2 des OSI-Modells verschmelzen im TCP/IP-Modell zur Schicht **Netzzugang**. Die OSI-Schichten 5, 6 und 7 werden in TCP/IP flach als reine **Anwendungsschicht** zusammengefasst.
