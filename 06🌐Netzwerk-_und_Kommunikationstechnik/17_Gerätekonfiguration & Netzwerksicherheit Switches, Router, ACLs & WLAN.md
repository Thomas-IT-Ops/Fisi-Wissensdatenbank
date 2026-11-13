tags: [fisi, ihk, lernsheet]
## 🧭 Navigation & Zusammenhänge
- **Vorausgesetztes Thema:** [[16_DNS-Strukturen, administrative Steuerung & Security Deep Dive]]
- **Nächstes Thema:** [[18_Netzwerksicherheit & Firewalls Firewall-Typen, DMZ, VPNs & NAC (802.1X)]]
- **Verwandte Bausteine:** [[11_Netzwerksegmentierung Virtual Local Area Networks (VLANs)]], [[14_Routing-Grundlagen Tabellenstruktur, statisches & dynamisches Routing]]
---

🎯 IHK-Prüfungsrelevanz

> [!IMPORTANT] AP01: Einrichten eines IT-gestützten Arbeitsplatzes
> 
> - **Relevanz:** Hoch
> - **Fokus:** Portbasierte Zugangskontrolle und WLAN-Einbindung. Du musst wissen, wie Endgeräte über **Access Ports** angebunden werden, wie **Port Security** unbefugte Hardware blockiert und wie Arbeitsplatzgeräte sicher mit verschlüsselten Funknetzen (**WPA2/WPA3-PSK**) verbunden werden.

> [!WARNING] AP02: Konzeption, Administration & Netzwerke
> 
> - **Relevanz:** Überlebenswichtig (Absoluter IHK-Kernbereich für FISIs!)
> - **Fokus:** Eines der am intensivsten geprüften Themen überhaupt! In der Prüfung musst du Cisco-IOS-Konfigurationsbefehle für Switches und Router interpretieren oder selbst niederschreiben können. Ein massiver Schwerpunkt liegt auf Sicherheitsarchitekturen: Du musst **Standard- und Extended Access Control Lists (ACLs)** mitsamt Wildcard-Masken berechnen und platzieren können. Ebenso elementar ist das Verständnis von Adressübersetzungen (**SNAT/Masquerading** für den Internet-Uplink und **DNAT/Port-Forwarding** für Serverbereitstellungen) sowie die strategische **WLAN-Kanalplanung** im Unternehmen.

---

📖 Einfache Erklärung & Praxisbeispiele

1. Grundlagen der Switch- & Router-Konfiguration (Cisco IOS)

Während **Unmanaged Switches** reine, nicht konfigurierbare Plug-and-Play-Geräte sind, bieten **Managed Switches** volle administrative Kontrolle über Performance und Sicherheit. Der Erstzugriff erfolgt physisch per _Konsolenkabel_, der spätere Remote-Zugriff aus Sicherheitsgründen verschlüsselt via _SSH_.

- **Management-IP (SVI):** Damit ein Switch per SSH erreichbar ist, benötigt er eine IP-Adresse auf einem virtuellen Interface (Switched Virtual Interface) – meist in einem isolierten Management-VLAN.
    
    cfg
    
    ```
    interface Vlan99
     ip address 192.168.99.10 255.255.255.0
     no shutdown
    exit
    ip default-gateway 192.168.99.1
    ```

- **Port Security (Layer 2 Absicherung):** Verhindert, dass Angreifer unbefugte Geräte an freie Netzwerkdosen anstecken. Der Switch limitiert die Anzahl erlaubter MAC-Adressen pro Port. Über den Befehl `mac-address sticky` lernt der Switch die MAC des legitimen Geräts automatisch und trägt sie fest in die Konfiguration ein.
    - **Violation Modi:** Tritt ein Verstoß auf, entscheidet der konfigurierte Modus:
        - `shutdown`: Der Port wird sofort komplett deaktiviert und wechselt in den Zustand _Err-disabled_ (Sicherster IHK-Standard). Er muss manuell per `shutdown` und `no shutdown` reaktiviert werden.
        - `restrict`: Der Port bleibt aktiv, unbefugte Pakete werden verworfen, ein Syslog-Alarm wird ausgelöst und der Fehlerzähler hochgezählt.
        - `protect`: Pakete unbefugter Geräte werden lautlos verworfen – ohne Benachrichtigung.

2. Access Control Lists (ACLs) – Filtern auf Schicht 3 & 4

ACLs sind sequentielle Filterlisten, die Datenverkehr erlauben (`permit`) oder verbieten (`deny`). **Wichtigste IHK-Regel:** Am Ende _jeder_ ACL steht ein unsichtbares, **implizites `deny all`**. Trifft keine Regel zu, wird das Paket verworfen. Die Verarbeitung stoppt beim ersten Treffer (_First Match_).

- **Standard-ACLs (Bereich 1–99):** Filtern **ausschließlich nach der Quell-IP-Adresse**. Sie werden so nah wie möglich am _Ziel_ platziert.  
    `cfg access-list 10 permit 192.168.10.0 0.0.0.255`
- **Extended-ACLs (Bereich 100–199):** Filtern nach **Quelle, Ziel, Protokoll (IP, TCP, UDP, ICMP) und Portnummer**. Sie werden so nah wie möglich an der _Quelle_ platziert, um unzulässigen Traffic frühzeitig zu blockieren.  
    `cfg access-list 101 permit tcp any host 10.1.1.1 eq 80 access-list 101 permit tcp any host 10.1.1.1 eq 443`
- _Aktivierung:_ Eine ACL filtert erst, wenn sie an ein Interface gebunden wird: `ip access-group 101 in`.

3. Network Address Translation (NAT)

NAT übersetzt private (nicht im Internet routbare) IP-Adressen in öffentliche IPs.

- **SNAT (Source NAT / Masquerading / PAT):** Der Standard für jeden Internet-Uplink. Verlässt ein Paket das LAN, ersetzt der Router die private Quell-IP durch seine öffentliche IP. Bei **PAT (Port Address Translation)** nutzt er zusätzlich wechselnde Quellports, damit tausende interne Clients gleichzeitig über _eine einzige_ öffentliche IP surfen können.
- **DNAT (Destination NAT / Port Forwarding):** Ändert die Ziel-IP eines eingehenden Pakets. So können interne Server (z. B. ein Webserver im LAN) unter der einen öffentlichen IP-Adresse des Unternehmens aus dem Internet erreichbar gemacht werden.

4. WLAN-Design & Enterprise-Sicherheit

Drahtlose Funknetze (IEEE 802.11) nutzen Access Points (APs) als Brücke zum physischen Kabelnetz.

- **Frequenzbänder & Kanalplanung:**
    - **2,4 GHz (Wi-Fi 4 / 802.11n):** Hohe Reichweite, aber extrem störanfällig. Es gibt nur **drei überlappungsfreie Kanäle (1, 6 und 11)**. Benachbarte APs müssen zwingend auf unterschiedlichen Kanälen funken, um Funkinterferenzen (Co-Channel-Interferenz) zu vermeiden.
    - **5 GHz (Wi-Fi 5 / 802.11ac):** Geringere Reichweite, aber wesentlich mehr Kanäle, höhere Datenraten und kaum Interferenzen.
    - **6 GHz (Wi-Fi 6E/7 / 802.11ax):** Ultraschnell, maximale Kanalbreiten, exklusiv für modernste Hardware.
- **Sicherheitsmodi:**
    - _WPA2-Personal (PSK):_ Ein gemeinsames Passwort für alle. Absolut unsicher für Firmen, da bei Mitarbeiter-Austritt das Passwort überall geändert werden müsste.
    - _WPA3:_ Pflicht ab Wi-Fi 6, schützt effektiv gegen Brute-Force-Angriffe.
    - _WPA2/3-Enterprise (EAP):_ Der Firmenstandard. Jeder Benutzer authentifiziert sich mit eigenen Benutzerdaten oder Zertifikaten an einem zentralen **RADIUS-Server**.
- **Gastnetze & Client Isolation:** Gäste-WLANs werden über eine eigene SSID und ein separates VLAN strikt vom Firmennetz isoliert. Die Aktivierung von **Client Isolation (AP Isolation)** auf dem AP verhindert, dass drahtlose Clients im Gästenetzwerk untereinander kommunizieren können (Schutz vor internen Angriffen).

📊 Diagnose- & Monitoring-Toolmatrix

Um Netzwerke zu überwachen (_Monitoring_) und Fehler gezielt zu analysieren (_Diagnose_), nutzt ein FISI folgende Werkzeuge:

|Tool|Ebene (OSI)|Kernfunktion|IHK-Praxisanwendungsfall|
|---|---|---|---|
|**`ping`**|Layer 3|Sendet ICMP Echo Requests und erwartet Echo Replies.|Schnelle Verifizierung der grundlegenden Netzwerk-Erreichbarkeit.|
|**`traceroute` / `tracert`**|Layer 3|Identifiziert jeden Router-Hop auf dem Weg zum Ziel über ICMP-Time-Exceeded-Meldungen.|Lokalisierung des exakten Routers, an dem ein Paket verloren geht oder wo Latenzprobleme auftreten.|
|**`netstat` / `ss`**|Layer 4|Listet alle aktiven Sockets, offenen TCP/UDP-Ports und verknüpfte Prozess-IDs (PIDs) auf.|Prüfen, ob ein lokaler Server-Dienst (z. B. `httpd` auf Port 80) überhaupt aktiv lauscht.|
|**`nmap`**|Layer 3 & 4|Extrem mächtiger Netzwerk- und Portscanner.|Sicherheitsaudit: Aufdecken von unerwünscht geöffneten Ports in einem Subnetz.|
|**`wireshark`**|Layer 2 bis 7|Paket-Sniffer zur Aufzeichnung und Tiefenanalyse von Protokoll-Headern.|Detaillierte Fehlersuche bei Verbindungsabbrüchen. _Achtung:_ Erfordert auf Switches die Einrichtung von **Port Mirroring (SPAN)**.|
|**SNMP**|Layer 7|Standardprotokoll (Simple Network Management Protocol) für zentrale Monitoring-Server (Zabbix, PRTG).|Kontinuierliche Überwachung von Systemressourcen (CPU-Last, Schnittstellen-Bandbreitennutzung) via MIB-Abfragen.|

---

🚨 Die 3 kritischen IHK-Stolperfallen

- **Die "Hidden SSID"-Sicherheitsillusion:** Die IHK stellt gerne Fangfragen zur Absicherung von Funknetzen. Schlag auf keinen Fall vor, das Verstecken der SSID (_Hidden Network_) als Sicherheitsmaßnahme zu nutzen. APs senden permanent _Beacon Frames_. Ein unsichtbares WLAN sendet seinen Namen unverschlüsselt, sobald ein Client sich verbinden will. Es ist reine Scheinsicherheit (_Security through Obscurity_). Die einzig korrekte IHK-Antwort für Firmen ist **WPA2/3-Enterprise mit RADIUS**.
- **Falsche Platzierung von Standard- vs. Extended-ACLs:** Platzierst du eine Standard-ACL nahe an der Quelle, blockierst du den Client komplett für das gesamte Netzwerk, da sie nur nach der Quell-IP filtert. **IHK-Faustregel:** Standard-ACLs gehören so nah wie möglich an das **Ziel**. Extended-ACLs hingegen filtern präzise nach Ports und Ziel-IPs – sie müssen so nah wie möglich an die **Quelle** gebunden werden, um unnötigen Traffic gar nicht erst durch das Core-Netzwerk zu routen.
    
- **Vergessen des "no shutdown"-Befehls bei Cisco-Interfaces:** In praktischen Cisco-Konfigurationsaufgaben verlangt die IHK das Aufschreiben der Befehlskette zur Interface-Einrichtung. Viele Prüflinge wechseln in das Interface, weisen IP und Maske zu und springen direkt zum nächsten Schritt. Bei Cisco-Geräten sind Router-Schnittstellen ab Werk administrativ deaktiviert (_administratively down_). Vergisst du den Befehl **`no shutdown`**, bleibt das Interface offline und die Aufgabe erhält erhebliche Punktabzüge.
