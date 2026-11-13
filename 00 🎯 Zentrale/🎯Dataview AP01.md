```dataviewjs
// AP01 IHK Rahmenlehrplan Struktur (Lernfelder 1 - 5)
const curriculumAP01 = [
  {
    lf: "Lernfeld 1: Unternehmen & Rolle mitgestalten",
    topics: [
      { name: "01 Einführung / Allgemeine BWL", kw: "bwl" },
      { name: "02 Management & Arbeitsplatz-Ergonomie", kw: "management" },
      { name: "Vertragsrecht & Ausbildungsvertrag", kw: "vertrag" },
      { name: "Arbeitsschutz & Green IT", kw: "arbeitsschutz" }
    ]
  },
  {
    lf: "Lernfeld 2: Arbeitsplätze ausstatten",
    topics: [
      { name: "Hardware-Komponenten & Architektur", kw: "hardware" },
      { name: "Betriebssysteme", kw: "betriebssystem" },
      { name: "Schnittstellen & Peripherie", kw: "schnittstelle" },
      { name: "Handelskalkulation (LEP, ZEP, BVP)", kw: "kalkulation" }
    ]
  },
  {
    lf: "Lernfeld 3: Clients in Netzwerke einbinden",
    topics: [
      { name: "Netzwerk-Grundlagen & Topologien", kw: "topologie" },
      { name: "OSI-Modell & TCP/IP", kw: "osi" },
      { name: "IPv4-Adressierung & Subnetting Basics", kw: "ipv4" },
      { name: "Netzwerkprotokolle (DHCP, DNS)", kw: "protokoll" }
    ]
  },
  {
    lf: "Lernfeld 4: Schutzbedarf & IT-Sicherheit",
    topics: [
      { name: "Schutzziele (CIA) & IT-Sicherheit", kw: "schutzziele" },
      { name: "Datenschutz (DSGVO)", kw: "dsgvo" },
      { name: "Datensicherung & Backup-Strategien", kw: "backup" },
      { name: "Schutzbedarfsanalyse", kw: "schutzbedarf" }
    ]
  },
  {
    lf: "Lernfeld 5: Software & Skripte entwickeln",
    topics: [
      { name: "Programmiergrundlagen", kw: "programmier" },
      { name: "Skripting & Automatisierung", kw: "skript" },
      { name: "Datenbank-Grundlagen & ERM", kw: "datenbank" },
      { name: "SQL-Abfragen", kw: "sql" }
    ]
  }
];

// Notizen aus dem Vault abfragen
const allPages = dv.pages('""').where(p => p.file.folder !== "");

const rows = [];

for (const group of curriculumAP01) {
  for (const topic of group.topics) {
    const matchedNote = allPages.find(p => {
      const name = p.file.name.toLowerCase();
      return name.includes(topic.kw);
    });

    if (matchedNote) {
      rows.push([
        group.lf,
        matchedNote.file.link,
        matchedNote.file.folder,
        "🟢 Vorhanden"
      ]);
    } else {
      rows.push([
        group.lf,
        topic.name,
        "-",
        "🔴 Hinzufügen"
      ]);
    }
  }
}

dv.table(["IHK Lernfeld (AP01)", "Thema / Notiz", "Ordner", "Status"], rows);
```
