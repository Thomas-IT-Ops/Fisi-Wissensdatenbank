tags: [fisi, ihk, lernsheet]
## 🧭 Navigation & Zusammenhänge
- **Vorausgesetztes Thema:** [[18_Netzwerksicherheit & Firewalls Firewall-Typen, DMZ, VPNs & NAC (802.1X)]]
- **Nächstes Thema:** [[01_Grundlagen der IT-Sicherheit & Schutzziele]] *(Übergang zu Modul 07)*
- **Verwandte Bausteine:** [[13_Core-Dienste auf Anwendungsebene DHCP, DNS & E-Mail-Infrastruktur]], [[15_Transportschicht im Detail TCP- vs. UDP-Protokolle, Header & Handshakes]]
---

🎯 IHK-Prüfungsrelevanz

> [!IMPORTANT] AP01: Einrichten eines IT-gestützten Arbeitsplatzes
> 
> - **Relevanz:** Hoch
> - **Fokus:** Portgenaue Anbindung und Fehlerdiagnose am Client. Du musst die Standard-Anwendungsports im Schlaf beherrschen, um Verbindungsprobleme (z. B. blockierter E-Mail-Abruf über **IMAP/POP3** oder fehlschlagende Namensauflösung via **DNS**) auf Betriebssystemebene oder an lokalen Client-Firewalls zu lokalisieren.

> [!WARNING] AP02: Konzeption, Administration & Netzwerke
> 
> - **Relevanz:** Extrem Hoch (Pflicht-Punktelieferant in jeder Prüfung!)
> - **Fokus:** Die IHK fordert in fast jeder Netzwerkaufgabe das Ausfüllen oder Analysieren von Firewall-Tabellen und ACLs. Hierfür musst du die Zuordnung von **Diensten, Portnummern und dem zugrundeliegenden Layer-4-Protokoll (TCP oder UDP)** fehlerfrei beherrschen. Regelmäßig werden zudem die konzeptionellen Unterschiede zwischen den Mail-Protokollen (IMAP vs. POP3) sowie die sichere Remoteverwaltung von Serverlandschaften (**SSH** und **RDP**) abgefragt.

---

📖 Einfache Erklärung & Praxisbeispiele

1. Die IHK-Kern-Dienste im Steckbrief

- **DNS (Domain Name System):** Übersetzt für Menschen lesbare Domainnamen in maschinenlesbare IP-Adressen. Es nutzt standardmäßig **Port 53 via UDP** für schnelle, kleine Anfragen (bei großen Zonentransfers oder DNSSEC-Validierungen wechselt es zu TCP).
- **DHCP (Dynamic Host Configuration Protocol):** Versorgt Endgeräte beim Netzwerkbeitritt vollautomatisch mit IP-Adressen, Subnetzmasken, Standardgateways und DNS-Servern. Es arbeitet verbindungslos auf den **Ports 67 und 68 über UDP Broadcasts**.
- **SSH (Secure Shell) vs. RDP (Remote Desktop Protocol):** Beide dienen der Fernwartung. **SSH (Port 22/tcp)** ist der verschlüsselte Standard für die textbasierte CLI-Administration (z. B. Linux-Server oder Switche). **RDP (Port 3389/tcp)** ist das proprietäre Protokoll von Microsoft zur Übertragung einer vollständigen grafischen Benutzeroberfläche (GUI) für Windows-Systeme.
- **HTTP vs. HTTPS:** Protokolle zur Übertragung von Webseiteninhalten. Während **HTTP (Port 80/tcp)** unverschlüsselt und damit anfällig für Lauschangriffe ist, sichert **HTTPS (Port 443/tcp)** die Kommunikation über eine **TLS-Verschlüsselung** kryptografisch ab.

2. Das E-Mail-Protokolltrio (Der IHK-Klassiker)

In der Prüfung musst du strikt zwischen dem Mail-**Versand** und dem Mail-**Abruf** unterscheiden:

- **Versand ➔ SMTP (Simple Mail Transfer Protocol):** Wird _ausschließlich_ zum Versenden von E-Mails (vom Client zum Server oder zwischen Mailservern) auf **Port 25/tcp** verwendet (bzw. Port 587/tcp für gesichertes Einliefern).
- **Abruf Option A ➔ IMAP (Internet Message Access Protocol):** Synchronisiert die E-Mails direkt auf dem Server. Die Nachrichten verbleiben dort; Ordnerstrukturen und gelesen-Status sind auf allen Endgeräten identisch. Arbeitet auf **Port 143/tcp**.
- **Abruf Option B ➔ POP3 (Post Office Protocol v3):** Lädt die E-Mails stur vom Server herunter und löscht sie dort im Standardfall. Ein synchroner Abruf mit mehreren Geräten ist nicht möglich. Arbeitet auf **Port 110/tcp**.

---

📊 Das IHK-Referenzgitter (Wichtige Ports & Protokolle)

Dieses Gitter fasst die im Lernzettel genannten Dienste strukturiert zusammen. Du solltest diese Tabelle für die Prüfung auswendig zeichnen können:

|Dienst|Port|Layer-4-Protokoll|Übertragungsart & Hauptaufgabe|
|---|---|---|---|
|**FTP**|`20 / 21`|**TCP**|Dateiübertragung (Steuerkanal auf 21, Datenkanal auf 20)|
|**SSH**|`22`|**TCP**|Verschlüsselte, textbasierte Fernwartung (CLI)|
|**SMTP**|`25`|**TCP**|Zuverlässiger E-Mail-Versand (Server-zu-Server)|
|**DNS**|`53`|**UDP** _(& TCP)_|Namensauflösung (Domainname ➔ IP-Adresse)|
|**DHCP**|`67 / 68`|**UDP**|Automatische IP-Konfiguration (67 Server, 68 Client)|
|**HTTP**|`80`|**TCP**|Unverschlüsselte Übertragung von Webseiten|
|**POP3**|`110`|**TCP**|Lokales Herunterladen von E-Mails (keine Synchronisation)|
|**IMAP**|`143`|**TCP**|Serverbasierte E-Mail-Synchronisation (Multi-Device-fähig)|
|**HTTPS**|`443`|**TCP**|TLS-verschlüsselte Webseitenübertragung (Standard)|
|**RDP**|`3389`|**TCP**|Grafische Fernsteuerung von Windows-Systemen (GUI)|

---

🚨 Die 3 kritischen IHK-Stolperfallen

- **Das falsche Transportprotokoll in Firewall-Regeln eintragen:** Ein verheerender Leichtsinnsfehler. In Aufgaben zu Paketfiltern musst du neben der Portnummer auch das Protokoll angeben. Schreibst du für eine DNS-Anfrage fälschlicherweise `53/tcp` statt `53/udp` oder für den Webserver `80/udp` statt `80/tcp`, blockiert die Firewall den Traffic komplett. **Merke:** Infrastruktur-Dienste (DNS, DHCP) nutzen primär **UDP**; Anwendungsdienste (Web, Mail, Remote-Zugriff) setzen zwingend auf die Zuverlässigkeit von **TCP**.
- **FTP-Datenkanal (Port 20) in ACLs vergessen:** Wenn eine Aufgabe fordert, einen FTP-Zugang durch eine Firewall zu tunneln, tragen Prüflinge oft nur Port 21 (Steuerkanal) ein. Der Effekt: Der Client kann sich zwar anmelden und Befehle senden, sieht aber keine Verzeichnisse und kann keine Dateien übertragen. **Merke:** Für klassisches, aktives FTP müssen **immer beide Ports (21 für Befehle, 20 für Nutzdaten)** freigegeben werden.
- **IMAP und POP3 beim Einsatzzweck vertauschen:** Die IHK beschreibt oft Kundenszenarien (z. B. _"Außendienstmitarbeiter muss seine Mails auf Smartphone und Laptop parallel verwalten"_). Wer hier **POP3** als Lösung vorschlägt, kassiert null Punkte, da POP3 die Mails lokal herunterlädt und die Geräte asynchron laufen lässt. Für moderne Multi-Device-Umgebungen ist **IMAP** die einzig richtige Prüfungsantwort.