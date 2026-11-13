---
tags: [fisi, ihk, lernsheet]
---
## 🧭 Navigation & Zusammenhänge
- **Vorausgesetztes Thema:** [[18_Tabellenstrukturen mit Datentypen & Constraints physisch anlegen]]
- **Nächstes Thema:** [[02_Das ISO, OSI-Referenzmodell & TCP, IP-Schichtenmodell]]
- **Verwandte Bausteine:** [[13_Core-Dienste auf Anwendungsebene DHCP, DNS & E-Mail-Infrastruktur]], [[19_Netzwerkprotokolle, Kern-Dienste & IHK-Portmatrix]]
---

## 🎯 IHK-Prüfungsrelevanz
> [!IMPORTANT] AP01: Einrichten eines IT-gestützten Arbeitsplatzes
> - **Relevanz:** Mittel
> - **Fokus:** Verständnis über den grundlegenden Aufbau des Internets, globale physische Infrastrukturen (Seekabel) sowie die zuständigen nationalen Stellen (z. B. DENIC für .de-Domains) beim Einrichten von Netzwerkanbindungen.

> [!WARNING] AP02: Konzeption, Administration & Netzwerke
> - **Relevanz:** Hoch
> - **Fokus:** In Netzwerktechnik-Aufgaben verlangt die IHK oft die genaue Zuordnung von Internetorganisationen (wie RIPE NCC für Europa) oder die Interpretation von Internet-Standards (RFCs). Besonders wichtig für die strukturierte IP-Adressvergabe und das Verständnis, wie globale IP-Blöcke hierarchisch verteilt werden.

---

## 📖 Einfache Erklärung & Praxisbeispiele
Das Internet ist kein zentral gesteuertes System, sondern ein weltweiter Zusammenschluss autonomer Netzwerke. Damit Datenpakete global fehlerfrei übertragen werden können, basiert die gesamte Infrastruktur auf standardisierten **Normen und Standards**, einer hierarchischen **Ressourcenverwaltung** sowie physischen Knotenpunkten.

### Unterthemen & Anschauliche Beispiele:

- **Physische Infrastruktur (Seekabel & IXPs):**
  Daten fließen global über interkontinentale Unterseekabel. Lokale und regionale Netze tauschen ihren Traffic an zentralen Internetknotenpunkten, sogenannten **Internet Exchanges (IXPs)** wie dem DE-CIX in Frankfurt oder kleineren regionalen Knoten (z. B. DO-CIX, Stuttgart-IX), effizient aus.
  - 💡 **Praxisbeispiel:** Wenn ein Unternehmen in Dortmund Clouddienste nutzt, läuft der Datenverkehr oft über den regionalen Dortmund Internet eXchange (DO-CIX), statt den Umweg über Frankfurt zu nehmen, was Latenzen minimiert.

- **Normen & RFCs (IETF):**
  Die **Internet Engineering Task Force (IETF)** entwickelt technische Standards. Diese werden als **RFC (Request for Comments)** veröffentlicht. RFCs nutzen standardisierte Keywords nach RFC 2119 (wie `MUST` für absolute Pflichten oder `SHOULD` für dringende Empfehlungen).
  - 💡 **Praxisbeispiel:** Bei der Konfiguration eines Mailservers (SMTP) richtet sich der Systemintegrator nach den Vorgaben von RFC 5321. Hält sich die Software nicht an die `MUST`-Vorgaben, verweigern andere Mailserver weltweit die Annahme der E-Mails.

- **Globale Adress- und Namensverwaltung (ICANN / IANA):**
  Die **ICANN** verwaltet zusammen mit der **IANA** die absolute Wurzel des Internets: die DNS-Root-Zone und die Vergabe zentraler IP-Adressblöcke sowie Top-Level-Domains (TLDs) wie `.de` oder `.com`.
  - 💡 **Praxisbeispiel:** Ein FISI registriert für einen Kunden die Domain `firma.de`. Die ICANN/IANA delegiert die Verwaltung der TLD `.de` an das deutsche Network Information Center (**DENIC**), welches die Domain final in die Nameserver einträgt.

- **Hierarchische IP-Verteilung (RIRs):**
  Die IANA teilt riesige IP-Adressblöcke an die fünf **Regional Internet Registries (RIR)** auf. Für Europa und den Nahen Osten ist das **RIPE NCC** zuständig. Dieses vergibt die IP-Blöcke an lokale Provider (LIRs).
  - 💡 **Praxisbeispiel:** Ein Systemintegrator beantragt für das neue Firmennetzwerk ein eigenes, providerunabhängiges IPv6-Präfix. Der Antrag wird nach den Richtlinien des RIPE NCC bearbeitet, damit das Netz global geroutet werden kann.

---

## 📊 Visuelle Darstellung (Mermaid.js)
```mermaid
flowchart TD
    %% Globale Ebene
    ICANN[ICANN / IANA <br>Globale Verwaltung von IPs, TLDs & DNS-Root]:::global
    
    %% Regionale Ebene (RIRs)
    subgraph RIR_Ebene [Regional Internet Registries RIR]
        direction LR
        RIPE[RIPE NCC <br>Europa / Nahost]:::rir
        ARIN[ARIN <br>Nordamerika]:::rir
        APNIC[APNIC <br>Asien-Pazifik]:::rir
        LACNIC[LACNIC <br>Lateinamerika]:::rir
        AFRINIC[AfriNIC <br>Afrika]:::rir
    </style>
    
    %% Nationale / Lokale Ebene
    DENIC[DENIC <br>Nationale Registry für .de]:::national
    ISP[Lokale Internet Provider <br>LIRs / AS-Betreiber]:::local
    
    %% Infrastruktur-Komponenten
    IXP[Internet Exchanges <br>DE-CIX, DO-CIX, Stuttgart-IX]:::infra
    CABLE[Physische Backbone-Infrastruktur <br>Unterseekabel & Glasfaser-Trassen]:::infra

    %% Verknüpfungen IP/Domain-Hierarchie
    ICANN -->|verteilt IP-Großblöcke an| RIPE
    ICANN -->|delegiert TLDs an| DENIC
    RIPE -->|weist IP-Netze zu an| ISP
    DENIC -->|koordiniert Domains für| ISP
    
    %% Datenfluss Infrastruktur
    ISP <-->|tauscht Traffic an| IXP
    IXP <-->|nutzt globale Transportwege| CABLE

    %% Styling
    classDef global fill:#1a365d,stroke:#fff,stroke-width:2px,color:#fff;
    classDef rir fill:#2b6cb0,stroke:#fff,color:#fff;
    classDef national fill:#4a5568,stroke:#fff,color:#fff;
    classDef local fill:#2d3748,stroke:#fff,color:#fff;
    classDef infra fill:#2f855a,stroke:#fff,color:#fff;
```

---

## 🚨 Die 3 kritischen IHK-Stolperfallen

- **Verwechslung von Zuständigkeiten:** In Prüfungen werden gerne die Aufgaben von ICANN/IANA, RIPE NCC und DENIC durcheinandergewürfelt. Merkregel: ICANN/IANA steuert das große Ganze global, RIPE NCC teilt IP-Adressen regional für Europa zu und die DENIC verwaltet ausschließlich die deutsche Länderendung `.de`.
- **Falsche Interpretation von RFC-Keywords:** Wer in einer IHK-Dokumentation oder -Prüfung ein `SHOULD` (Sollte-Vorschrift) mit einem `MUST` (Muss-Vorschrift) gleichsetzt, verliert Punkte. Die IHK fordert hier präzise Einhaltung der technischen Spezifikationen nach RFC 2119.
- **Annahme, das Internet sei rein virtuell:** Technische Zeichnungen verleiten dazu, das Internet als "Wolke" zu sehen. Die IHK fragt jedoch gezielt nach Ausfallsicherheit (Redundanz). Fällt ein zentraler IXP oder eine wichtige Seekabel-Trasse aus, müssen alternative Routingwege über andere Autonome Systeme (AS) bereitstehen.
