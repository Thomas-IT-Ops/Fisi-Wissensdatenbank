```dataviewjs
// AP02 IHK Rahmenlehrplan Struktur (Lernfelder 6 - 11)
const curriculumAP02 = [
  {
    lf: "Lernfeld 6: Serviceanfragen bearbeiten (ITIL & SLA)",
    topics: [
      { name: "Service Desk, Incident Management & ITIL Basics", kw: "itil" },
      { name: "Service Level Agreements (SLA) & Pönale", kw: "sla" },
      { name: "Fehleranalyse & Remote-Support Tools", kw: "support" }
    ]
  },
  {
    lf: "Lernfeld 7: Cyber-physische Systeme ergänzen",
    topics: [
      { name: "IoT-Infrastruktur, Sensorik & Aktorik", kw: "iot" },
      { name: "Industrielle Schnittstellen & Protokolle (MQTT, OPC UA)", kw: "mqtt" }
    ]
  },
  {
    lf: "Lernfeld 8: Datensysteme bedarfsgerecht bereitstellen",
    topics: [
      { name: "Erweiterte Datenbanken & ER-Modellierung", kw: "datenbank" },
      { name: "Komplexe SQL-Abfragen & Normalisierung (1NF - 3NF)", kw: "sql" },
      { name: "NoSQL vs. Relationale Datenbanken", kw: "nosql" }
    ]
  },
  {
    lf: "Lernfeld 9: Netzwerke und Dienste bereitstellen",
    topics: [
      { name: "VLSM, Advanced Subnetting & IP-Routing", kw: "subnetting" },
      { name: "VLAN-Konfiguration & Trunking (802.1Q)", kw: "vlan" },
      { name: "Serverdienste (DNS, DHCP, Webserver, Mailserver)", kw: "serverdienste" },
      { name: "Firewall-Regeln, NAT & VPN-Tunnel (IPsec/OpenVPN)", kw: "firewall" }
    ]
  },
  {
    lf: "Lernfeld 10: Serverdienste & Netzwerke administrieren",
    topics: [
      { name: "Verzeichnisdienste (Active Directory, LDAP, GPO)", kw: "active directory" },
      { name: "Virtualisierung (Hyper-V, Proxmox, VMware)", kw: "virtualisierung" },
      { name: "Speichersysteme (NAS, SAN, RAID 0/1/5/6/10)", kw: "raid" },
      { name: "Cloud-Infrastruktur (IaaS, PaaS, SaaS, Hybrid Cloud)", kw: "cloud" }
    ]
  },
  {
    lf: "Lernfeld 11: IT-Systeme nachhaltig betreiben & sichern",
    topics: [
      { name: "Monitoring & Log-Analyse (Nagios, Zabbix, PRTG)", kw: "monitoring" },
      { name: "Ausfallsicherheit, USV-Dimensionierung & High Availability", kw: "usv" },
      { name: "Investitionsrechnung, TCO & CapEx vs. OpEx", kw: "tco" },
      { name: "IT-Notfallplanung, Backup-Strategien & Disaster Recovery", kw: "disaster" }
    ]
  }
];

// Notizen aus dem Vault abfragen
const allPages = dv.pages('""').where(p => p.file.folder !== "");

const rows = [];

for (const group of curriculumAP02) {
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

dv.table(["IHK Lernfeld (AP02)", "Thema / Notiz", "Ordner", "Status"], rows);
```
