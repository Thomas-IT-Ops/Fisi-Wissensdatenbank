
**Tags:** #[Betriebssysteme] #[Virtualisierung] #[Container] #[FisiPrüfung]

---

### 🗺️ Navigation & Zusammenfassung
* **Vorheriges Thema:** [[07_Sicherheit,_Normen & Green IT]]
* **Nächstes Thema:** [[09_Software-Qualität, Testing & Künstliche Intelligenz]]
* **Verwandte Bausteine:** [[02_Datenspeicher & Sicherheit RAM, Massenspeicher, RAID & Dateisyst...]], [[06_Stromversorgung, USV & Netzformen]]

---

### 🎓 IHK-Prüfungsrelevanz: AP01 & AP02

> [!IMPORTANT] **🟢 IHK Prüfungsrelevanz: AP01 (Teil 1 der gestreckten Abschlussprüfung)**
> * **Relevanz:** Basiswissen für Systeminstallationen und Clientsysteme
> * **Fokus:** In der AP1 musst du grundlegende Aufgaben von Betriebssystemen, Dateisysteme (z. B. NTFS, ext4) sowie hardwarenahe Sicherheitsfunktionen wie UEFI, Secure Boot und TPM 2.0 unterscheiden können.

> [!INFO] **🔵 IHK Prüfungsrelevanz: AP02 (Teil 2 der gestreckten Abschlussprüfung)**
> * **Relevanz:** Kernkompetenz im Bereich Systemintegration & Virtualisierung
> * **Fokus:** Hier wird verlangt, dass du Hypervisor-Typen (Typ 1 vs. Typ 2) sowie VMs und Container konzeptionell gegenüberstellst, Rollout-Strategien (Images, unbemannte Installationen) planst und Lifecycle-Aspekte von Software berücksichtigst.

---

### 📖 Einfache Erklärung & Praxisbeispiele

#### 💡 Das Konzept einfach erklärt
Ein Betriebssystem (OS) fungiert als essenzieller Vermittler zwischen der physischen Hardware und den Anwendungen[cite: 63]. Es verwaltet Prozesse, Arbeitsspeicher, Dateisysteme und steuert über Treiber die Peripherie[cite: 63]. 
* **Firmware & Startvorgang:** Moderne Systeme starten über **UEFI** statt des alten BIOS. Für den sicheren Start sorgen **Secure Boot** (nur signierte Bootloader) und das **TPM 2.0** (Hardware-Sicherheitschip, z. B. zwingend für BitLocker-Verschlüsselung unter Windows 11)[cite: 70].
* **Dateisysteme:** Je nach Einsatzzweck kommen unterschiedliche Systeme zum Einsatz (z. B. *NTFS* für Windows mit feingranularen Rechten, *ext4* als Linux-Standard oder *Btrfs* auf NAS-Systemen mit Snapshots und Prüfsummen)[cite: 72].
* **Virtualisierung & Container:** 
  * *Hypervisor Typ 1 (Bare Metal):* Läuft direkt auf der Hardware (z. B. Proxmox VE, ESXi) und bietet maximale Performance für den Serverbetrieb.
  * *Hypervisor Typ 2 (Hosted):* Läuft auf einem bestehenden Betriebssystem (z. B. VirtualBox) für Tests und Entwicklung[cite: 77].
  * *Container:* Teilen sich im Gegensatz zu virtuellen Maschinen den Kernel des Host-Systems, sind extrem leichtgewichtig (MBs statt GBs) und starten in Sekunden (z. B. via Docker)[cite: 80, 81].

#### 💻 Praxisbeispiel & Technische Umsetzung
Beispielhafter Rollout und Betriebssystem-Setup für die Filiale West (Autohaus Veritas):
* **Clients:** 12 Arbeitsplätze (Mini-PCs und Notebooks) werden standardisiert mit *Windows 11 Pro* ausgestattet, um die Domänenintegration (Entra ID) und BitLocker-Verschlüsselung zu ermöglichen[cite: 65, 66].
* **Rollout-Strategie:** Statt jeden PC manuell einzurichten, wird ein vorkonfiguriertes **Image** erstellt und über das Netzwerk oder USB verteilt[cite: 73].
* **Docker-Container Befehle (CLI):**
  ```bash
# Image herunterladen und Container starten
  docker run -d -p 80:80 --name webserver nginx

  # Laufende Container auflisten
  docker ps

  # Container stoppen
  docker stop webserver
  ```
  
---
### ⚠️ IHK-Prüfungsstolperfallen

- **Stolperfalle 1:** Verwechslung von VM-Snapshots mit einem echten Backup. -> _Lösung:_ Ein Snapshot liegt auf demselben Speicher und sichert nur den Zustand zum Zeitpunkt X; er ersetzt niemals eine unabhängige Datensicherung nach der 3-2-1-Regel.
    
- **Stolperfalle 2:** Annahme, dass Windows 11 Home für Firmennetzwerke ausreicht. -> _Lösung:_ Domänenbeitritt, Gruppenrichtlinien und BitLocker-Laufwerksverschlüsselung setzen zwingend die _Pro_-Edition voraus.
    
- **Stolperfalle 3:** Den Unterschied zwischen Typ-1 und Typ-2 Hypervisoren vertauschen. -> _Lösung:_ Typ 1 läuft direkt auf der leeren Hardware (Enterprise-Server), Typ 2 setzt auf ein bestehendes Betriebssystem auf (Desktop-Testumgebung)