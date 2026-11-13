```dataviewjs
const container = dv.container;
container.empty();

// Style für volle Breite & saubere Tabellenformatierung
const style = document.createElement('style');
style.textContent = `
  .dashboard-table {
    width: 100% !important;
    table-layout: fixed !important;
    border-collapse: collapse !important;
  }
  .dashboard-table th, .dashboard-table td {
    word-wrap: break-word !important;
    white-space: normal !important;
    padding: 10px 8px !important;
    vertical-align: top !important;
    border-bottom: 1px solid var(--background-modifier-border) !important;
  }
  .dashboard-table th:nth-child(1) { width: 28%; text-align: left; }
  .dashboard-table th:nth-child(2) { width: 54%; text-align: left; }
  .dashboard-table th:nth-child(3) { width: 18%; text-align: center; }
  .dashboard-table td:nth-child(3) { text-align: center; }
  
  .badge-ap1 { color: #2e7d32; font-weight: bold; }
  .badge-ap2 { color: #1565c0; font-weight: bold; }
`;
container.appendChild(style);

// Abfrage aller Notizen im Vault
const pages = dv.pages('""')
  .where(p => p.file.name !== "00 📊 Dashboard" && p.file.folder !== "");

// Gruppierung nach Ordner / Modul
const groups = pages.groupBy(p => p.file.folder).sort(g => g.key, 'asc');

const tableData = groups.map(g => {
  const folderName = g.key;
  
  // Alle Themen-Links im Ordner
  const fileLinks = g.rows.file.link.array().map(link => "• " + link).join("<br>");
  
  // Exakte IHK-Analyse pro Datei
  const apBadges = g.rows.map(r => {
    const f = r.file.folder.toLowerCase();
    const name = r.file.name.toLowerCase();
    
    // 1. Expliziter Frontmatter-Eintrag (falls vorhanden)
    if (r.ihk_phase) {
      const val = String(r.ihk_phase).toUpperCase();
      if (val.includes("AP01") && val.includes("AP02")) return '<span class="badge-ap1">🟢 AP01</span> / <span class="badge-ap2">🔵 AP02</span>';
      if (val.includes("AP01")) return '<span class="badge-ap1">🟢 AP01</span>';
      if (val.includes("AP02")) return '<span class="badge-ap2">🔵 AP02</span>';
    }
    
    // 2. Zuordnung nach IHK VO 2020 Rahmenlehrplan:
    
    // Modul 01: BWL
    if (f.includes("01")) {
      if (name.includes("prozess") || name.includes("controlling") || name.includes("marketing") || name.includes("organisation")) {
        return '<span class="badge-ap2">🔵 AP02</span>';
      }
      return '<span class="badge-ap1">🟢 AP01</span>';
    }
    
    // Modul 02: Systemtechnik
    if (f.includes("02")) {
      if (name.includes("betriebssysteme") || name.includes("software-qualität") || name.includes("blockchain")) {
        return '<span class="badge-ap2">🔵 AP02</span>';
      }
      return '<span class="badge-ap1">🟢 AP01</span>';
    }
    
    // Modul 03: Fachbezogenes Rechnen
    if (f.includes("03")) {
      return '<span class="badge-ap1">🟢 AP01</span>';
    }
    
    // Modul 04: Programmierung (Grundlagen vs. OOP/UML)
    if (f.includes("04")) {
      if (name.includes("01_") || name.includes("02_") || name.includes("03_programmiergrundlagen") || name.includes("04_python")) {
        return '<span class="badge-ap1">🟢 AP01</span>';
      }
      return '<span class="badge-ap2">🔵 AP02</span>';
    }
    
    // Modul 05: Datenbanken (Einführung/SQL-Basics vs. Normalisierung)
    if (f.includes("05")) {
      if (name.includes("01_") || name.includes("grundlagen")) {
        return '<span class="badge-ap1">🟢 AP01</span>';
      }
      return '<span class="badge-ap2">🔵 AP02</span>';
    }
    
    // Modul 06: Netzwerke & Protokolle
    if (f.includes("06")) {
      if (name.includes("01_") || name.includes("02_") || name.includes("osi") || name.includes("ipv4")) {
        return '<span class="badge-ap1">🟢 AP01</span>';
      }
      return '<span class="badge-ap2">🔵 AP02</span>';
    }
    
    // Modul 07: Security & Datenschutz
    if (f.includes("07")) {
      if (name.includes("01_") || name.includes("02_") || name.includes("dsgvo") || name.includes("schutzziele")) {
        return '<span class="badge-ap1">🟢 AP01</span>';
      }
      return '<span class="badge-ap2">🔵 AP02</span>';
    }
    
    // Modul 08: Service- & Projektmanagement
    if (f.includes("08")) {
      if (name.includes("präsentation") || name.includes("repetitorium")) {
        return '<span class="badge-ap1">🟢 AP01</span> / <span class="badge-ap2">🔵 AP02</span>';
      }
      return '<span class="badge-ap2">🔵 AP02</span>';
    }
    
    // Modul 09, 10, 11
    if (f.includes("09") || f.includes("10") || f.includes("11")) {
      return '<span class="badge-ap1">🟢 AP01</span>';
    }
    
    return '<span class="badge-ap1">🟢 AP01</span>';
  }).array().join("<br>");

  return [folderName, fileLinks, apBadges];
});

dv.table(["Modul / Ordner", "Themen & Inhalte", "IHK / Phase"], tableData);
```


