---
tags: [fisi, ihk, lernsheet]
---
## 🧭 Navigation & Zusammenhänge
- **Vorausgesetztes Thema:** [[07_Finanzierung & Buchführung]]
- **Nächstes Thema:** [[09_Präsentationstechniken & Digitale Werkzeuge]]
- **Verwandte Bausteine:** [[08_Kundenberatung und Marketing in der IT]], [[02_Change Management & IT-Kommunikation]]
---

## 🎯 IHK-Prüfungsrelevanz
> [!IMPORTANT] AP01: Einrichten eines IT-gestützten Arbeitsplatzes
> - **Relevanz:** Niedrig bis Mittel
> - **Fokus:** Grundlagen der kundenorientierten Gesprächsführung bei First-Level-Supportanfragen und die Dokumentation von Ticket-Eingängen.

> [!WARNING] AP02: Konzeption, Administration & Netzwerke
> - **Relevanz:** Extrem Hoch (Prüfungsgarant)
> - **Fokus:** Dieses Thema verknüpft Kernkompetenzen für die schriftliche Prüfung (WiSo/Projektmanagement) mit der mündlichen Abschlussprüfung (Teil 3: Projektpräsentation und Fachgespräch). Die IHK fordert die präzise Anwendung von Kommunikationsmodellen (Schulz von Thun, Watzlawick, Eisberg) zur Deeskalation bei Reklamationen. Zudem sind operative vs. analytische CRM-Systeme, DSGVO-Regeln (BCC, Authentifizierung) und Compliance-Richtlinien im Kundenkontakt feste Prüfungsbestandteile.

---

## 📖 Einfache Erklärung & Praxisbeispiele
Fachinformatiker für Systemintegration arbeiten längst nicht mehr im "stillen Kämmerlein", sondern besetzen eine zentrale **Schnittstellenfunktion**. Sie übersetzen komplexe technische Sachverhalte in verständliche Kundensprache. Professionelle Kommunikation basiert auf bewährten theoretischen Modellen, strukturierten Gesprächsphasen sowie der Nutzung von Customer Relationship Management (CRM) Systemen zur langfristigen Kundenbindung.

### Unterthemen & Anschauliche Beispiele:
- **Die wichtigsten Kommunikationsmodelle im IT-Umfeld:**
  - **Sender-Empfänger-Modell (Shannon & Weaver):** Nachricht wird codiert, via Kanal (E-Mail, Telefon) übermittelt und decodiert. *Erkenntnis:* Fachbegriffe und Lärm wirken als Störquellen (*Noise*). "Gesagt ist nicht gehört, gehört ist nicht verstanden".
  - **4-Seiten-Modell (Schulz von Thun):** Jede Nachricht hat vier Seiten: *Sachinhalt* (Fakten), *Selbstoffenbarung* (Ich-Botschaft), *Beziehungshinweis* (Tonfall) und *Appell* (Handlungsaufforderung).
  - **5 Axiome nach Paul Watzlawick:** 1. Man kann nicht *nicht* kommunizieren. 2. Jede Kommunikation hat Inhalts- und Beziehungsaspekte. 4. Sie läuft digital (Worte) und analog (Körpersprache) ab.
  - **Eisberg-Modell (Sigmund Freud):** Nur ca. 20% sind sichtbar auf der *Sachebene* (Daten, Fakten). Die restlichen 80% liegen unsichtbar auf der *Beziehungsebene* (Ängste, Werte, Gefühle). Konflikte auf der Sachebene sind oft ungelöste Beziehungskonflikte.
- **Die Phasen des Beratungsgesprächs & Nutzenargumentation:**
  - Der Ablauf folgt einer klaren Struktur: **Vorbereitung** (Zielsetzung) $\rightarrow$ **Eröffnung** (Small Talk als Eisbrecher) $\rightarrow$ **Bedarfsanalyse** (mittels offenen W-Fragen: "Wer fragt, der führt!") $\rightarrow$ **Lösungsphase** (Präsentation) $\rightarrow$ **Abschlussphase** (Action Items definieren).
  - 💡 **Praxisbeispiel (Merkmal vs. Nutzen):** Vermeide "Feature Fucking" (reines Aufzählen technischer Details). Nutze stattdessen die Formel *Merkmal + Brücke + Nutzen*. **Schlecht:** "Die Server-Infrastruktur besitzt NVMe-SSDs im RAID-10." **IHK-konform:** "Durch die verbauten Highspeed-Festplatten (*Merkmal*) profitiert Ihr Team von extrem kurzen Ladezeiten (*Vorteil*), sodass Ihre Mitarbeiter morgens ohne Wartezeiten sofort produktiv arbeiten können (*Nutzen*)."
- **Customer Relationship Management (CRM):**
  - **Operatives CRM:** Unterstützt das tägliche Kundengeschäft (Erfassung von Kontakten, Angeboten und Support-Tickets im Ticketsystem).
  - **Analytisches CRM:** Wertet gesammelte Daten systematisch aus (Data Mining, ABC-Kundenbewertung), um Potenziale zu erkennen.
- **Compliance, DSGVO & Social Engineering:**
  - **Compliance (Regeltreue):** Schützt das Unternehmen vor Strafen. Bei Geschenken gilt die interne Wertgrenze (oft max. 35 €) – Transparenz zum Vorgesetzten schützt vor Korruptionsverdacht ("Anfüttern" vermeiden).
  - **DSGVO-Regeln:** Datensparsamkeit einhalten. Bei Rundmails zwingend **BCC** (Blindkopie) statt CC nutzen, um Mailadressen zu schützen. Am Telefon vor einer Datenauskunft immer erst die Identität des Anrufers authentifizieren.
  - **Social Engineering:** Die gezielte Manipulation von Mitarbeitern (z. B. Phishing, CEO-Fraud), um sensible Passwörter oder Daten zu erpressen. *Schutz:* Gesunde Skepsis und Autorisierung über etablierte Rückrufe.

---

## 📊 Visuelle Darstellung (Mermaid.js)
```mermaid
flowchart TD
    %% Die Kommunikationsebenen
    subgraph Theorie [Kommunikationsmodelle für das Fachgespräch]
        direction TB
        S_E[Sender-Empfänger] -->|Codierung / Decodierung| Noise{Störquellen / Noise <br> Lärm, Fachchinesisch}
        
        Schulz[4-Seiten-Modell] --> Sach[1. Sachinhalt: Reine Fakten]
        Schulz --> Offen[2. Selbstoffenbarung: Ich-Botschaft]
        Schulz --> Bez[3. Beziehung: Tonfall]
        Schulz --> App[4. Appell: Handlungsaufforderung]
        
        Eisberg[Eisberg-Modell] --> S_Ebene[Sachebene: ca. 20% sichtbar]
        Eisberg --> B_Ebene[Beziehungsebene: ca. 80% unsichtbar]
    end

    %% Beratungsgespräch Phasen
    subgraph Beratung [Der professionelle Beratungszyklus]
        direction TB
        B1[1. Vorbereitung <br> CEO oder Admin? Ziel festlegen] --> B2[2. Eröffnung <br> Small Talk als Eisbrecher + Agenda]
        B2 --> B3[3. Bedarfsanalyse <br> Offene W-Fragen sammeln]
        B3 --> B4[4. Lösung & Einwand <br> Merkmal-Brücke-Nutzen Methode]
        B4 --> B5[5. Abschluss <br> Action Items: Wer macht was bis wann?]
    end

    %% CRM und Recht
    subgraph Sicherheit [CRM & Compliance Framework]
        direction LR
        CRM{CRM-System} -->|Tagesgeschäft| Op[Operativ: Tickets, Kontakte]
        CRM -->|Datenanalyse| An[Analytisch: ABC-Analyse]
        
        Comp[Compliance & DSGVO] --> DS[Datensparsamkeit & BCC Pflicht]
        Comp --> SE[Social Engineering Abwehr <br> Identität prüfen / Rückruf]
    end

    %% Logische Verknüpfungen
    B3 -.->|Datenpflege in| CRM
    B4 -->|Argumentation via| Schulz
    SE -.-> S_E

    %% Styling
    style Noise fill:#9b2c2c,stroke:#fff,stroke-width:1px,color:#fff
    style Sach fill:#4a5568,stroke:#fff,stroke-width:1px,color:#fff
    style Offen fill:#4a5568,stroke:#fff,stroke-width:1px,color:#fff
    style Bez fill:#4a5568,stroke:#fff,stroke-width:1px,color:#fff
    style App fill:#4a5568,stroke:#fff,stroke-width:1px,color:#fff
    style B4 fill:#2b6cb0,stroke:#fff,stroke-width:1px,color:#fff
    style B5 fill:#2f855a,stroke:#fff,stroke-width:1px,color:#fff
    style Comp fill:#d69e2e,stroke:#fff,stroke-width:2px,color:#000
```
