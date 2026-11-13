
```dataviewjs
const container = dv.container;
container.empty();

// Suchfeld erstellen
const input = container.createEl("input", {
    type: "text",
    placeholder: "Suchbegriff eingeben (z.B. Hardware, http, Netzwerk)..."
});
input.style.width = "100%";
input.style.padding = "8px 12px";
input.style.marginBottom = "15px";
input.style.borderRadius = "6px";
input.style.border = "1px solid var(--background-modifier-border)";
input.style.backgroundColor = "var(--background-secondary)";
input.style.color = "var(--text-normal)";

// Container für die HTML-Tabelle
const tableWrapper = container.createEl("div");
tableWrapper.style.overflowX = "auto";

async function init() {
    try {
        const file = app.workspace.getActiveFile();
        if (!file) {
            tableWrapper.setText("⚠️ Keine aktive Datei gefunden.");
            return;
        }

        const content = await app.vault.read(file);
        const lines = content.split("\n");
        const tableRows = lines.filter(line => line.trim().startsWith("|") && line.trim().endsWith("|"));

        if (tableRows.length < 3) {
            tableWrapper.setText("⚠️ Keine gültige Tabelle in dieser Notiz gefunden.");
            return;
        }

        const headers = tableRows[0].split("|").slice(1, -1).map(c => c.trim());
        const rows = tableRows.slice(2).map(row => 
            row.split("|").slice(1, -1).map(cell => cell.trim())
        );

        function renderTable(filter = "") {
            tableWrapper.innerHTML = "";
            const term = filter.toLowerCase().trim();

            const filteredRows = rows.filter(row => 
                row.some(cell => cell.toLowerCase().includes(term))
            );

            if (filteredRows.length === 0) {
                const noResult = tableWrapper.createEl("div");
                noResult.style.padding = "10px";
                noResult.style.color = "var(--text-muted)";
                noResult.setText("Keine Treffer für: " + filter);
                return;
            }

            // Native HTML Tabelle aufbauen
            const table = tableWrapper.createEl("table");
            table.className = "dataview table-view-table";
            table.style.width = "100%";
            table.style.borderCollapse = "collapse";

            // Header rendern
            const thead = table.createEl("thead");
            const headerTr = thead.createEl("tr");
            headers.forEach(h => {
                const th = headerTr.createEl("th");
                th.textContent = h.replace(/\*\*/g, '');
                th.style.textAlign = "left";
                th.style.padding = "8px 12px";
                th.style.borderBottom = "2px solid var(--background-modifier-border)";
            });

            // Zeilen rendern
            const tbody = table.createEl("tbody");
            filteredRows.forEach(r => {
                const tr = tbody.createEl("tr");
                r.forEach(cellText => {
                    const td = tr.createEl("td");
                    td.textContent = cellText.replace(/\*\*/g, '');
                    td.style.padding = "8px 12px";
                    td.style.borderBottom = "1px solid var(--background-modifier-border)";
                });
            });
        }

        // Initiale Ansicht (alles anzeigen)
        renderTable();

        // Live-Suche bei jedem Tippen
        input.addEventListener("input", (e) => {
            renderTable(e.target.value);
        });

    } catch (err) {
        tableWrapper.setText("Fehler beim Laden: " + err.message);
    }
}

init();
```





```


| Fachbegriff                                    | Kategorie                   | Einfache Erklärung für Einsteiger (AP1-relevant)                                                                                                                                                                                                                               |
| :--------------------------------------------- | :-------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Hardware**                                   | Grundlagen                  | Alle anfassbaren, physischen Teile eines Computers (Prozessor, Kabel, Monitor, Tastatur).                                                                                                                                                                                      |
| **Software**                                   | Grundlagen                  | Alle Programme, Apps und Daten, die auf einem Computer laufen und die man nicht anfassen kann.                                                                                                                                                                                 |
| **Betriebssystem**                             | Software                    | Die Grund-Software (z. B. Windows, Linux), die den Computer bedienbar macht und die Hardware für andere Programme verwaltet.                                                                                                                                                   |
| **Filesystem / Dateisystem**                   | Betriebssysteme             | Regelt, wie Daten auf einer Festplatte gespeichert, benannt und wiedergefunden werden (z. B. NTFS, FAT32, ext4).                                                                                                                                                               |
| **Partitionierung**                            | Betriebssysteme             | Das Aufteilen einer Festplatte in mehrere logische Bereiche (z. B. Laufwerk C: und D:).                                                                                                                                                                                        |
| **Host**                                       | Netzwerk / Grundlagen       | Jedes Gerät, das eine eigene IP-Adresse hat und aktiv im Netzwerk kommuniziert (z. B. dein PC, ein Drucker oder ein Server).                                                                                                                                                   |
| **Client**                                     | Netzwerk / Grundlagen       | Ein Computer oder Programm, das einen Dienst anfordert (z. B. dein Browser, der eine Webseite von einem Server anfordert).                                                                                                                                                     |
| **Server**                                     | Netzwerk / Grundlagen       | Ein leistungsstarker Computer, der im Netzwerk bereitsteht und Daten oder Dienste für andere (Clients) zur Verfügung stellt.                                                                                                                                                   |
| **CPU (Prozessor)**                            | Hardware                    | Der Hauptrechenbaustein ("das Gehirn") des Computers. Er führt alle Befehle aus und steuert die Rechenoperationen.                                                                                                                                                             |
| **RAM (Arbeitsspeicher)**                      | Hardware                    | Der flüchtige Kurzzeitspeicher des Computers. Hier liegen Daten, während Programme laufen. Beim Ausschalten wird er gelöscht.                                                                                                                                                  |
| **SSD / HDD**                                  | Hardware                    | Der dauerhafte Datenspeicher. **SSD**: Sehr schnell, elektronisch ohne bewegliche Teile. **HDD**: Langsamer, hat mechanische Magnet-Scheiben, aber günstig.                                                                                                                    |
| **Cache**                                      | Hardware                    | Ein winziger, extrem schneller Zwischenspeicher direkt auf dem Prozessor für Daten, die im Sekundentakt wiedergebraucht werden.                                                                                                                                                |
| **Schnittstelle (Interface)**                  | Hardware / Software         | Ein Übergangspunkt oder Anschluss zwischen zwei Systemen (z. B. USB-Anschluss für Hardware oder API für Software).                                                                                                                                                             |
| **BIOS / UEFI**                                | Hardware                    | Ein fest eingebautes Mini-Programm auf der Hauptplatine. Es prüft beim Einschalten die Hardware und startet danach das Betriebssystem.                                                                                                                                         |
| **PAN (Personal Area Network)**                | Netzwerk                    | Ein persönliches Netzwerk im engsten Umkreis (wenige Meter, z. B. Smartphone verbunden mit Bluetooth-Kopfhörern).                                                                                                                                                              |
| **LAN (Local Area Network)**                   | Netzwerk                    | Ein lokales Netzwerk auf begrenztem Raum (z. B. in einem Zimmer, einer Wohnung oder einem Bürogebäude).                                                                                                                                                                        |
| **WLAN (Wireless LAN)**                        | Netzwerk                    | Ein lokales Netzwerk, das Daten kabellos über Funkwellen überträgt.                                                                                                                                                                                                            |
| **MAN (Metropolitan Area Network)**            | Netzwerk                    | Ein stadtweites Netzwerk, das mehrere Gebäude oder Stadtteile miteinander verbindet (größer als LAN, kleiner als WAN).                                                                                                                                                         |
| **WAN (Wide Area Network)**                    | Netzwerk                    | Ein weitreichendes Netzwerk über Länder oder Kontinente hinweg (das bekannteste WAN ist das Internet).                                                                                                                                                                         |
| **DAN (Desk Area Network)**                    | Netzwerk                    | Ein Mini-Netzwerk direkt am Schreibtisch (z. B. PC, Maus, Tastatur und Drucker miteinander verbunden).                                                                                                                                                                         |
| **CAN (Campus Area Network)**                  | Netzwerk                    | Ein Netzwerk, das mehrere Gebäude auf einem geschlossenen Gelände verbindet (z. B. ein Firmen- oder Uni-Gelände).                                                                                                                                                              |
| **VLAN (Virtual LAN)**                         | Netzwerk                    | Ein logisch unterteiltes Netzwerk. Ein echtes Kabelnetzwerk wird per Software in mehrere getrennte Bereiche aufgeteilt (z. B. für Gäste und Mitarbeiter).                                                                                                                      |
| **VPN (Virtual Private Network)**              | Netzwerk                    | Ein verschlüsselter Tunnel durch das unsichere Internet, damit man von außen sicher auf das Firmennetzwerk zugreifen kann.                                                                                                                                                     |
| **Router**                                     | Netzwerk                    | Verbindet Geräte mit dem Internet. Arbeitet auf Schicht 3 und nutzt IP-Adressen.                                                                                                                                                                                               |
| **Switch**                                     | Netzwerk                    | Verbindet Geräte in einem Netzwerk. Arbeitet auf Schicht 2 und nutzt Mac-Adressen.                                                                                                                                                                                             |
| **Access Point**                               | Netzwerk                    | Ein Sendegerät, das drahtlose Geräte (WLAN) mit einem kabelgebundenen Netzwerk verbindet.                                                                                                                                                                                      |
| **IP-Adresse**                                 | Netzwerk                    | Die eindeutige "Postadresse" eines Geräts im Netzwerk, damit Datenpakete den Weg dorthin finden (z. B. `192.168.1.1`).                                                                                                                                                         |
| **IPv4 vs. IPv6**                              | Netzwerk                    | Das Format von IP-Adressen. **IPv4**: Alter Standard (4 Zahlenblöcke)1 Oktett=8Bit. **IPv6**: Neuer, moderner Standard mit gigantisch viel mehr Adressraum. Zahlen von 0-255 erlaubt                                                                                           |
| **Subnetzmaske**                               | Netzwerk                    | Eine Zahlenkette (z. B. `255.255.255.0`), die der IP-Adresse hilft zu erkennen, welcher Teil der Adresse das Netzwerk und welcher das Endgerät beschreibt.                                                                                                                     |
| Broadcast-Adresse                              | Netzwerk                    | Die Broadcast-Adresse ist wie eine **Megafon-Durchsage an alle Bewohner des Wohnblocks gleichzeitig**. Jedes Gerät im selben Subnetz hört diese Nachricht. Sie ist immer die aller letzte Adresse in diesem Bereich zb. .255 ist die letzte also ist die letzte broadcast .254 |
| **Standard-Gateway**                           | Netzwerk                    | Die "Tür nach draußen" im Netzwerk (meist die IP des Routers). Dorthin schickt ein PC Daten, wenn das Ziel außerhalb des eigenen Netzwerks liegt.                                                                                                                              |
| Default-Gateway                                | Netzwerk                    |                                                                                                                                                                                                                                                                                |
| **MAC-Adresse**                                | Netzwerk                    | Die weltweit einmalige, fest in die Netzwerkkarte eingebrannte Hardware-Nummer (kann im Normalfall nicht geändert werden).                                                                                                                                                     |
| **Domain**                                     | Netzwerk                    | Der lesbare Name einer Website oder eines Servers im Internet (z. B. `example.com`), den sich Menschen leicht merken können.                                                                                                                                                   |
| **DNS (Domain Name System)**                   | Netzwerk                    | Das "Telefonbuch" des Internets. Übersetzt lesbare Domain-Namen (z. B. `google.de`) blitzschnell in die echten IP-Adressen.                                                                                                                                                    |
| **DHCP**                                       | Netzwerk                    | Ein automatischer Dienst im Netzwerk, der angeschlossenen Geräten (wie Smartphones oder PCs) eigenständig eine freie IP-Adresse zuweist.                                                                                                                                       |
| **OSI-Schichtenmodell**                        | Netzwerk                    | Ein standardisiertes Schichtenmodell mit 7 Ebenen, das beschreibt, wie Datenübertragung in Netzwerken theoretisch abläuft.                                                                                                                                                     |
| **TCP**                                        | Netzwerk                    | Ein verbindungsorientiertes Übertragungsprotokoll (Schicht 4): Garantiert, dass Daten fehlerfrei, vollständig und in Reihenfolge ankommen (mit Empfangsbestätigung).                                                                                                           |
| **UDP**                                        | Netzwerk                    | Ein verbindungsloses Übertragungsprotokoll (Schicht 4): Sendet Daten extrem schnell ohne Rückmeldung raus (ideal für Livestreams oder Online-Spiele).                                                                                                                          |
| **HTTP / HTTPS**                               | Netzwerk                    | Protokolle zum Laden von Webseiten. **HTTP**: Unverschlüsselt. **HTTPS**: Sicher und verschlüsselt (mit TLS/SSL abgesichert).                                                                                                                                                  |
| **FTP / SFTP**                                 | Netzwerk                    | Protokolle zur Übertragung von Dateien über ein Netzwerk (SFTP ist die sichere, verschlüsselte Variante).                                                                                                                                                                      |
| **SMTP / IMAP / POP3**                         | Netzwerk                    | E-Mail-Protokolle. SMTP sendet E-Mails ab; IMAP und POP3 rufen E-Mails vom Server ab (IMAP lässt sie auf dem Server, POP3 lädt sie herunter).                                                                                                                                  |
| **Protokoll**                                  | Netzwerk                    | Eine feste Vereinbarung oder "Regelsprache", nach der sich zwei Systeme unterhalten, damit sie einander verstehen.                                                                                                                                                             |
| **Ping / Traceroute**                          | Netzwerk / Diagnose         | Diagnose-Befehle: `ping` prüft, ob ein Gerät erreichbar ist; `traceroute` zeigt den exakten Weg der Datenpakete über Router hinweg.                                                                                                                                            |
| **Firewall**                                   | IT-Sicherheit               | Ein digitaler Filter am Netzwerkeingang. Prüft ein- und ausgehenden Datenverkehr anhand von Regeln und blockiert Angriffe.                                                                                                                                                     |
| **TOM (Technisch-Organisatorische Maßnahmen)** | IT-Sicherheit / Datenschutz | Konkrete Vorschriften und Vorkehrungen (z. B. Passwörter, Alarmanlagen, Rechtevergabe), um Daten sicher zu schützen.                                                                                                                                                           |
| **Backup / Datensicherung**                    | IT-Sicherheit               | Das Erstellen von Sicherheitskopien wichtiger Daten, um sie bei Verlust oder Beschädigung wiederherstellen zu können (z. B. Großvater-Vater-Sohn-Prinzip).                                                                                                                     |
| **Symmetrische Verschlüsselung**               | IT-Sicherheit               | Ein Verfahren, bei dem Sender und Empfänger **denselben** geheimen Schlüssel zum Ver- und Entschlüsseln nutzen.                                                                                                                                                                |
| **Asymmetrische Verschlüsselung**              | IT-Sicherheit               | Ein Verfahren mit einem **Schlüsselpaar**: Ein öffentlicher Schlüssel (Public Key) verschlüsselt, und nur der private Schlüssel (Private Key) kann es wieder entschlüsseln.                                                                                                    |
| **Hybride Verschlüsselung**                    | IT-Sicherheit               | Die Kombination aus symmetrischer und asymmetrischer Verschlüsselung (wird z. B. bei HTTPS genutzt, da es schnell und sicher ist).                                                                                                                                             |
| **Hash-Verfahren (Hashing)**                   | IT-Sicherheit               | Eine mathematische Einweg-Funktion, die Daten in eine feste Zeichenkette (Hashwert) umwandelt. Perfekt, um zu prüfen, ob Daten manipuliert wurden.                                                                                                                             |
| **Digitale Signatur**                          | IT-Sicherheit               | Eine elektronische Unterschrift, die die Echtheit und Integrität einer Nachricht oder Software garantiert.                                                                                                                                                                     |
| **Schutzziele (CIA-Dreieck)**                  | IT-Sicherheit               | Die 3 Grundpfeiler: **C**onfidentiality (Vertraulichkeit), **I**ntegrity (Integrität/Unversehrtheit), **A**vailability (Verfügbarkeit).                                                                                                                                        |
| **Virtuelle Maschine (VM)**                    | Betriebssysteme             | Ein "Computer im Computer". Eine Software simuliert einen eigenständigen Rechner, auf dem ein separates Betriebssystem läuft.                                                                                                                                                  |
| **Container (z.B. Docker)**                    | Betriebssysteme             | Eine leichtere Variante der Virtualisierung: Teilt sich den Kern des Hauptbetriebssystems, läuft aber isoliert und extrem schnell.                                                                                                                                             |
| **Hypervisor**                                 | Betriebssysteme             | Die Steuerungs-Software, die virtuelle Maschinen (VMs) verwaltet und die Hardware-Ressourcen des Hauptrechners aufteilt (Typ 1 direkt auf Hardware, Typ 2 auf Betriebssystem).                                                                                                 |
| **Prozess**                                    | Betriebssysteme             | Ein eigenständiges, aktiv laufendes Programm auf dem Computer mitsamt seinem eigenen Speicherbereich.                                                                                                                                                                          |
| **Thread**                                     | Betriebssysteme             | Ein kleiner Teilbereich innerhalb eines Prozesses. Ein Programm kann mehrere Threads gleichzeitig ausführen (z. B. Musik spielen und laden).                                                                                                                                   |
| **Datenbank**                                  | Datenbanken                 | Ein strukturiertes elektronisches System zur geordneten, dauerhaften und sicheren Speicherung großer Datenmengen.                                                                                                                                                              |
| **Redundanz**                                  | Datenbanken / IT            | Das mehrfache Vorhandensein derselben Information. In Datenbanken unerwünscht (wird normalisiert); in Hardware gewollt für Ausfallsicherheit.                                                                                                                                  |
| **ERM (Entity-Relationship-Modell)**           | Datenbanken                 | Ein grafischer Entwurf für eine Datenbank, der zeigt, welche Datentabellen (Entitäten) existieren und wie sie miteinander verknüpft sind.                                                                                                                                      |
| **Normalisierung**                             | Datenbanken                 | Das schrittweise Aufteilen und Bereinigen von Tabellen nach festen Regeln, um Daten-Doppelungen (Redundanzen) zu vermeiden (1., 2., 3. Normalform).                                                                                                                            |
| **Primärschlüssel (Primary Key)**              | Datenbanken                 | Ein eindeutiges Erkennungsmerkmal für genau eine Zeile in einer Tabelle (z. B. eine einmalige Kundennummer, darf sich nicht wiederholen).                                                                                                                                      |
| **Fremdschlüssel (Foreign Key)**               | Datenbanken                 | Ein Verweis auf den Primärschlüssel einer *anderen* Tabelle, um logische Beziehungen zwischen den Tabellen herzustellen.                                                                                                                                                       |
| **SQL**                                        | Datenbanken                 | Die standardisierte Abfragesprache (Structured Query Language), mit der man relationale Datenbanken steuert und abfragt.                                                                                                                                                       |
| **UML (Unified Modeling Language)**            | Softwareentwicklung         | Eine standardisierte grafische Zeichensprache, um Software-Systeme, Abläufe oder Klassen übersichtlich darzustellen (z. B. Klassendiagramm, Aktivitätsdiagramm, Use-Case-Diagramm).                                                                                            |
| **Struktogramm / Nassi-Shneiderman**           | Softwareentwicklung         | Ein Flussdiagramm in Kastenform zur grafischen Darstellung der Programmlogik (Schleifen, Verzweigungen).                                                                                                                                                                       |
| **Verifikation**                               | Qualitätssicherung          | *"Haben wir das System richtig gebaut?"* – Prüft, ob das Produkt exakt nach den vorgegebenen technischen Spezifikationen umgesetzt wurde.                                                                                                                                      |
| **Validierung**                                | Qualitätssicherung          | *"Haben wir das richtige System gebaut?"* – Prüft, ob das Produkt im Alltag den echten Nutzen für den Anwender erfüllt.                                                                                                                                                        |
| **Statische Prüfverfahren**                    | Qualitätssicherung          | Prüfung von Dokumenten oder Code **ohne** Programmausführung (z. B. durch reines Lesen und Analysieren).                                                                                                                                                                       |
| **Dynamische Prüfverfahren**                   | Qualitätssicherung          | Prüfung des Systems **während** es läuft und in einer Testumgebung ausgeführt wird.                                                                                                                                                                                            |
| **Reviews / Walkthroughs / Inspektionen**      | Qualitätssicherung          | Statische Prüfmethoden: Vom gemeinsamen Durchlesen (Review) über Autorendurchgänge (Walkthrough) bis zur strengen, formellen Experten-Prüfung (Inspektion).                                                                                                                    |
| **Statische Codeanalyse**                      | Qualitätssicherung          | Ein automatisiertes Software-Tool scannt den Quellcode nach Fehlern oder schlechtem Stil, ohne den Code zu starten.                                                                                                                                                            |
| **Funktionstest**                              | Qualitätssicherung          | Ein Test, der prüft, ob eine konkrete Funktion (z. B. ein Login-Button) fehlerfrei das tut, was sie soll.                                                                                                                                                                      |
| **Last- & Performancetest**                    | Qualitätssicherung          | Prüft die Reaktionsgeschwindigkeit und Stabilität eines Systems, wenn viele Nutzer gleichzeitig darauf zugreifen.                                                                                                                                                              |
| **Sicherheitstest**                            | Qualitätssicherung          | Gezieltes Suchen nach Schwachstellen, um zu testen, ob das System gegen Angriffe von außen geschützt ist.                                                                                                                                                                      |
| **Schreibtischtest**                           | Qualitätssicherung          | Manueller "Trockenlauf" eines Algorithmus oder Codes mit Stift und Papier, um Logikfehler im Kopf durchzuspielen.                                                                                                                                                              |
| **Framework**                                  | Projekt / Software          | Ein vorgefertigtes, strukturiertes Gerüst aus Werkzeugen und Regeln, auf dem man aufbauen kann, statt alles neu zu erfinden.                                                                                                                                                   |
| **Algorithmus**                                | Softwareentwicklung         | Eine präzise Schritt-für-Schritt-Anleitung zur Lösung eines bestimmten Problems (wie ein Kochrezept).                                                                                                                                                                          |
| **Quellcode (Source Code)**                    | Softwareentwicklung         | Der von Menschen lesbare Programmiertext, den Entwickler in einer Programmiersprache schreiben.                                                                                                                                                                                |
| **Open Source vs. Proprietary**                | Softwareentwicklung / Recht | **Open Source**: Quellcode ist frei zugänglich und veränderbar. **Proprietary**: Kommerzielle Software, bei der der Quellcode unter Verschluss bleibt.                                                                                                                         |
| **First- / Second- / Third-Level-Support**     | Support & Service           | Die Stufen des Kundendienstes: 1. Level = Hotline/Standardhilfe, 2. Level = Techniker für Spezialfragen, 3. Level = Hersteller/Entwickler.                                                                                                                                     |
| **Ticketsystem**                               | Support & Service           | Eine Software zur strukturierten Erfassung, Verteilung und Bearbeitung von Kundenanfragen oder IT-Problemen.                                                                                                                                                                   |
| **Make-or-Buy-Entscheidung**                   | Projektmanagement / BWL     | Die betriebswirtschaftliche Entscheidung, ob eine Software/Hardware selbst entwickelt/gekauft oder extern beschafft werden soll.                                                                                                                                               |
| **Nutzwertanalyse**                            | Projektmanagement           | Eine Methode, um verschiedene Handlungsalternativen (z. B. mehrere Software-Angebote) anhand von Gewichtungen objektiv zu vergleichen.                                                                                                                                         |
| **Netzplan / Gantt-Diagramm**                  | Projektmanagement           | Grafische Werkzeuge zur Projektplanung: Gantt zeigt Balken-Zeitpläne, der Netzplan zeigt logische Abfolge und kritische Pfade von Aufgaben.                                                                                                                                    |
| **Agil**                                       | Projektmanagement           | Eine flexible Arbeitsweise in kleinen Schritten. Anforderungen können während des Projekts laufend angepasst werden.                                                                                                                                                           |
| **Wasserfallmodell**                           | Projektmanagement           | Ein klassisches, starres Projektmodell: Eine Phase (z. B. Planung) muss zu 100 % fertig sein, bevor die nächste beginnt.                                                                                                                                                       |
| **Lastenheft**                                 | Projektmanagement           | Das Dokument vom **Kunden**: Beschreibt die Anforderungen, Wünsche und das *Was* des gewünschten Projekts.                                                                                                                                                                     |
| **Pflichtenheft**                              | Projektmanagement           | Das Dokument vom **Auftragnehmer/Entwickler**: Beschreibt die genaue technische Umsetzung und das *Wie* auf Basis des Lastenhefts.                                                                                                                                             |
| **Scrum**                                      | Projektmanagement           | Ein agiles Framework für Teamarbeit mit festen Rollen (Product Owner, Scrum Master, Team) und kurzen Arbeitszyklen (Sprints).                                                                                                                                                  |
| **Sprint**                                     | Projektmanagement           | Ein fester, kurzer Zeitraum (z. B. 2 bis 4 Wochen) bei Scrum, in dem ein fertiges Teilprodukt entwickelt wird.                                                                                                                                                                 |
| **DSGVO**                                      | IT-Recht                    | Die Europäische Datenschutz-Grundverordnung; regelt streng und verbindlich den Umgang mit personenbezogenen Daten.                                                                                                                                                             |
| **Urheberrecht**                               | IT-Recht                    | Schützt das geistige Eigentum von Schöpfern (z. B. selbst geschriebener Quellcode, Dokumentationen, Designs) vor unbefugtem Kopieren.                                                                                                                                          |
| CIDR-Notation                                  | Netzwerk                    | Sagt uns wie groß ein Netzwerk ist. `/26` zeigt wieviele bits reserviert sind. Berechnung: 32Bits(gesamt Bits)-26 Bits (reservierte Bits)= 6 Bit für den Host-Anteil.                                                                                                          |
