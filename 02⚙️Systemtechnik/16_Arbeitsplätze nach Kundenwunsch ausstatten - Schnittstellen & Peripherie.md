**Tags:** #Systemtechnik #SchnittstellenPeripherie #Ergonomie #FisiPrüfung #Lernfeld2

---

### 🗺️ Navigation & Zusammenfassung
* **Vorheriges Thema:** [[01_Das Unternehmen und die eigene Rolle im Betrieb beschreiben]]
* **Nächstes Thema:** [[03_Clients in Netzwerke einbinden]]
* **Verwandte Bausteine:** [[Hardwarekomponenten]], [[Ergonomie am Arbeitsplatz]], [[Nutzwertanalyse]]

---

### 🎓 IHK-Prüfungsrelevanz: AP01 & AP02

> [!IMPORTANT] **🟢 IHK Prüfungsrelevanz: AP01 (Teil 1 der gestreckten Abschlussprüfung)**
> **Relevanz:** Sehr hoch / Basiswissen
> **Fokus:** In der AP01 musst du Peripheriegeräte und deren Schnittstellen anhand von technischen Datenblättern vergleichen können. Typisch sind Rechenaufgaben zu Übertragungsraten sowie Fragen zu passenden Kabeltypen, Steckverbindungen und maximalen Leitungslängen.

> [!INFO] **🔵 IHK Prüfungsrelevanz: AP02 (Teil 2 der gestreckten Abschlussprüfung)**
> **Relevanz:** Ergänzend
> **Fokus:** In der AP02 bildet dieses Wissen das Fundament, wenn komplexe Arbeitsplätze (z. B. für CAD-Entwickler oder Videoschnitt) konzipiert werden müssen. Hier stehen die Wirtschaftlichkeit, zukunftssichere Bandbreiten und die Einhaltung ergonomischer Vorgaben im Vordergrund.

---

### 📖 Einfache Erklärung & Praxisbeispiele

#### 💡 Das Konzept einfach erklärt
Stell dir einen PC wie ein Gehirn vor. Damit es mit der Außenwelt kommunizieren kann, braucht es Sinnesorgane und Gliedmaßen – das ist die **Peripherie** (Maus, Tastatur, Monitor, Drucker). Die **Schnittstellen** (Ports oder Anschlüsse) sind die Nervenbahnen, über die die Daten transportiert werden. 

Es gibt zwei grundlegende Arten der Datenübertragung:
* **Serielle Schnittstelle:** Die Datenbits werden nacheinander (in einer Reihe) über eine einzige Leitung geschickt. Moderne Schnittstellen wie USB oder PCIe nutzen dieses Prinzip extrem schnell.
* **Parallele Schnittstelle:** Mehrere Bits werden gleichzeitig nebeneinander über mehrere parallele Leitungen geschickt. Dies ist extern wegen Signalstörungen (Skew) veraltet.

#### 💻 Praxisbeispiel & Technische Umsetzung
Ein Kunde benötigt einen modernen Arbeitsplatz für Data Analytics. Du musst zwei 4K-Monitore ($$3840 \times 2160$$ Pixel bei 60 Hz) an ein Notebook anschließen. 

Du prüfst die Datenübertragungsrate (Bandbreite) für einen Monitor mit unkomprimiertem Videosignal (8-Bit Farbtiefe pro RGB-Kanal = 24 Bit):

$$Bandbreite = 3840 \times 2160 \times 60 \times 24 \approx 11,94 \text{ Gbit/s}$$

Unter Berücksichtigung des Protokoll-Overheads benötigt ein Monitor knapp **12,5 Gbit/s**, zwei Monitore folglich **25 Gbit/s**.

Du vergleichst die Schnittstellen auf dem Datenblatt des Notebooks:
* **HDMI 2.0:** Unterstützt bis zu 18 Gbit/s (reicht nicht für beide Monitore parallel).
* **Thunderbolt 4 / USB4:** Unterstützt bis zu **40 Gbit/s**.

*Entscheidung:* Du bindest die Monitore über eine Thunderbolt 4 Dockingstation an das Notebook an, da die Bandbreite locker für beide unkomprimierten 4K-Signale ausreicht.

---

### 📊 Schnittstellen-Vergleichstabelle (IHK-Prüfungswissen)

| Schnittstelle | Version / Spezifikation | Max. Bruttobandbreite | Hauptsächliche Verwendung & IHK-Merkmale |
| :--- | :--- | :--- | :--- |
| **USB 2.0** | High Speed | **480 Mbit/s** ($$60 \text{ MB/s}$$) | Maus, Tastatur, ältere Drucker. Nutzt 4 Adern. |
| **USB 3.0 / 3.2 Gen 1** | SuperSpeed | **5 Gbit/s** ($$625 \text{ MB/s}$$) | Externe SSDs, Standard-Docks. Typisch blauer Stecker (Typ-A). |
| **USB 3.1 / 3.2 Gen 2** | SuperSpeed+ | **10 Gbit/s** ($$1,25 \text{ GB/s}$$) | Schnelle Speichergeräte, Gigabit-Netzwerkadapter. |
| **USB 3.2 Gen 2x2** | SuperSpeed+ (Multi-Lane) | **20 Gbit/s** ($$2,5 \text{ GB/s}$$) | Nutzt zwei Lanes, setzt zwingend den **Typ-C-Stecker** voraus. |
| **USB4 / Thunderbolt 4** | USB4 Gen 3x2 / TB4 | **40 Gbit/s** ($$5 \text{ GB/s}$$) | Universelle Dockingstations, externe Grafikkarten (eGPUs). |
| **HDMI 2.0** | Ultra High Speed Baseline | **18 Gbit/s** | Monitore/TVs. Reicht für $$4\text{K @ 60 Hz}$$. |
| **HDMI 2.1** | Ultra High Speed | **48 Gbit/s** | Moderne Displays. Unterstützt $$8\text{K @ 60 Hz}$$ oder $$4\text{K @ 120 Hz}$$. |
| **DisplayPort 1.4** | HBR3 (High Bit Rate 3) | **32,4 Gbit/s** | IT-Arbeitsplätze. Unterstützt **MST** (Daisy-Chaining von Monitoren). |
| **DisplayPort 2.1** | UHBR20 | **80 Gbit/s** | High-End Workstations für extrem hohe Auflösungen. |

---

### 🪑 Ergonomie am Bildschirmarbeitsplatz

Bei der physischen Ausstattung des Arbeitsplatzes müssen gesetzliche Vorgaben (z.B. die Arbeitsstättenverordnung - ArbStättV) und ergonomische Richtlinien beachtet werden, um gesundheitliche Schäden der Anwender zu verhindern.

> [!INFO] **📏 Bildschirmabstand & Größe** 
> * **Richtwert:** Der optimale Abstand zwischen Auge und Display beträgt **50 bis 80 cm** (je nach Bildschirmdiagonale). > * **Daumenregel für die Praxis:** Bei standardmäßigen 24-Zoll-Büromonitoren sind ca. **60 bis 70 cm** ideal. Höhere Auflösungen (wie 4K) erfordern trotz schärferem Bild oft Anpassungen bei der Skalierung der Benutzeroberfläche, um Ermüdung vorzubeugen.


 > [!TIP] **👁️ Sehachsen & Blickwinkel** 
 > > * **Höhenausrichtung:** Die **Oberkante des Monitors** sollte sich maximal auf **Augenhöhe** befinden (oder leicht darunter). > * **Neigung der Sehachse:** Der Blick sollte bei entspannter Kopfhaltung leicht nach unten fallen (**15° bis 20° Neigung**). Das schont die Nackenmuskulatur und verhindert ein Austrocknen der Augen, da das Augenlid leicht geschlossen bleibt. > * **Platzierung:** Der Monitor muss zentriert im Blickfeld stehen (Vermeidung von dauerhaftem Verdrehen des Kopfes).


> [!ATTENTION] **💡 Beleuchtung & Vermeidung von Reflexionen** 
> > * **Beleuchtungsstärke:** Am Bildschirmarbeitsplatz sind mindestens **500 Lux** vorgeschrieben. > * **Anordnung im Raum:** Die Sehleitung muss **parallel zum Fenster** verlaufen. > * *Warum?* Steht das Fenster im Rücken des Nutzers, spiegelt sich das Licht im Display (**Reflexion**). Steht der Monitor direkt vor dem Fenster, wird das Auge durch den extremen Helligkeitskontrast geblendet (**Direktblendung**). > * **Entspiegelung:** Büromonitore müssen zwingend mattiert/entspiegelt sein (Zertifizierungen wie TCO oder TÜV Ergonomie prüfen).

```mermaid graph TD A[Schnittstellen & Peripherie] --> B[Schnittstellentypen] A --> C[Peripheriegeräte] A --> H[Physische Ergonomie] B --> B1[Intern] B --> B2[Extern] B1 --> D1[PCIe - Grafikkarte/NVMe] B1 --> D2[SATA - Legacy SSD/HDD] B2 --> E1[USB-C / Thunderbolt] B2 --> E2[DisplayPort / HDMI] B2 --> E3[RJ-45 - Netzwerk] C --> F1[Eingabe: Maus, Tastatur] C --> F2[Ausgabe: Monitor, Drucker] H --> H1[Sehachse & Abstand: 50-80cm] H --> H2[Beleuchtung: min. 500 Lux] H --> H3[Reflexionsschutz: Parallel zum Fenster] ```


