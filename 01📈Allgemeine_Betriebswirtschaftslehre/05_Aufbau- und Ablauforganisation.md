tags: [fisi, ihk, lernsheet]
## 🧭 Navigation & Zusammenhänge
- **Vorausgesetztes Thema:** [[04_Sicherheit_und_Ergnomie]]
- **Nächstes Thema:** [[06_Prozessmodellierung]]
- **Verwandte Bausteine:** [[01_Einführung_Allgemeine_BWL]], [[07_Controlling]]
---

🎯 IHK-Prüfungsrelevanz

> [!IMPORTANT] AP01 / WiSo: Grundlagen der Betriebs- und Arbeitsorganisation
> 
> - **Relevanz:** Hoch
> - **Fokus:** Die IHK prüft regelmäßig die Abgrenzung von **Aufbauorganisation** und **Ablauforganisation**. Ebenfalls prüfungsrelevant: Die Anwendung des **Kongruenzprinzips** bei der Stellenbildung und das Lesen/Erstellen von **Organigrammen** und **Funktionsdiagrammen** (RACI).

> [!WARNING] AP02: Konzeption, Administration & Netzwerke
> 
> - **Relevanz:** Mittel
> - **Fokus:** Verständnis von Leitungssystemen (Einlinien- vs. Mehrliniensystem), Matrixstrukturen in Systemhäusern sowie die Analyse und Reduktion von Zeitkomponenten (Durchlaufzeiten) bei IT-Prozessen.
>     

---

📖 Einfache Erklärung & Praxisbeispiele

Die betriebliche Organisationslehre sorgt für Stabilität, Effizienz und Vorhersehbarkeit bei wiederkehrenden Betriebsvorgängen. Sie unterteilt sich in das statische Gerüst (**Aufbauorganisation**) und den dynamischen Prozessfluss (**Ablauforganisation**).

Unterthemen & Anschauliche Beispiele:

- **Organisation, Disposition & Improvisation:**
    - **Organisation:** Dauerhafte, feste Regelungen für wiederkehrende Vorgänge.
        - 💡 **Praxisbeispiel:** Das tägliche automatisierte Einspielen von Sicherheits-Patches um 03:00 Uhr nachts.
    - **Disposition:** Fallweise Regelungen innerhalb eines bestehenden Rahmens.
        - 💡 **Praxisbeispiel:** Zuweisung eines dringenden Support-Tickets an den Techniker, der heute am wenigsten Auslastung hat.
    - **Improvisation:** Vorläufige Regelung für unvorhergesehene Ereignisse (Krisen/Notfälle).
        - 💡 **Praxisbeispiel:** Spontanes Aufsetzen eines Ersatz-Routers über LTE, weil der Haupt-Glasfaseranschluss durch Baggerarbeiten durchtrennt wurde.
- **Die Stelle und das Kongruenzprinzip:** Die Stelle ist die kleinste organisatorische Basiseinheit. Nach dem **Kongruenzprinzip** müssen **Aufgabe** (Was ist zu tun?), **Kompetenz** (Was darf entschieden werden?) und **Verantwortung** (Wofür gerade stehen?) eine harmonische Einheit bilden.
    - 💡 **Praxisbeispiel (Inkongruenz):** Du erhältst als Systemadministrator die _Aufgabe_, den neuen Core-Switch zu konfigurieren, besitzt aber nicht die administrativen _Kompetenzen_ (Rechte) für das System. Du bist handlungsunfähig.
- **Klassische Leitungssysteme (IHK-Dauerbrenner):**
    - **Einliniensystem:** Jeder Mitarbeiter hat exakt _einen_ Vorgesetzten (Einheit der Auftragserteilung).
        - 👍 _Vorteil:_ Maximale Transparenz und eindeutige Berichtswege.
        - 👎 _Nachteil:_ Lange Instanzenwege ("Dienstweg") verlangsamen Entscheidungen.
    - **Mehrliniensystem:** Mitarbeiter erhalten Weisungen von mehreren Fachvorgesetzten (Prinzip des kürzesten Weges).
        - 👍 _Vorteil:_ Schnelle Entscheidungen durch direkte Fachkompetenz.
        - 👎 _Nachteil:_ Hohe Gefahr von Kompetenzkonflikten und unklaren Prioritäten für den Mitarbeiter.
    - **Stab-Linien-System:** Linieninstanzen werden durch spezialisierte _Stabsstellen_ ohne eigene Weisungsbefugnis unterstützt.
        - 💡 **IT-Praxisbeispiel:** Der _IT-Sicherheitsbeauftragte_ (CISO) oder _Datenschutzbeauftragte_ berät die Geschäftsführung direkt als Stabstelle, darf den Technikern aber keine direkten Befehle erteilen.
- **Organisationsmodelle (Von Funktional bis Agile):**
    - **Funktionalorganisation:** Gliederung nach Tätigkeiten/Verrichtungen (Zentraler Einkauf, IT, Vertrieb). Typisch für KMUs. Gefahr von Silo-Denken.
    - **Spartenorganisation (Divisional):** Gliederung nach Objekten (Produkte, Regionen, Kundengruppen wie "Großkunden" vs. "Behörden"). Sparten agieren oft als eigenständige Profit-Center.
    - **Matrixorganisation:** Mehrdimensionale Struktur. Mitarbeiter berichten an einen Disziplinarvorgesetzten (z. B. IT-Abteilungsleiter) UND an einen Projektleiter. Typisch für IT-Systemhäuser, birgt aber hohes Konfliktpotenzial bei Ressourcenknappheit.
    - **Agile Organisation:** Rollen statt starre Stellen. Interdisziplinäre, selbstorganisierte Teams (Squads/Tribes) mit festen Rollen wie _Product Owner_ oder _Scrum Master_.
- **Zentralisation vs. Dezentralisation:**
    - **Zentralisation:** Ein zentraler IT-Einkauf für den gesamten Konzern bündelt Mengen und senkt Kosten (_Economies of Scale_).
    - **Dezentralisation:** IT-Administratoren sitzen direkt vor Ort in den jeweiligen Fachabteilungen (schnellere Reaktion, hohe Fachnähe).
- **Ablauforganisation und Zeitkomponenten (Durchlaufzeit):** Ordnet Handlungen nach Raum, Zeit und Sachmitteln, um Prozesse zu optimieren. Die **Durchlaufzeit** eines IT-Prozesses setzt sich zusammen aus:
    - _Bearbeitungszeit_ (Echte Wertschöpfung, z. B. Code schreiben).
    - _Rüstzeit_ (Vorbereitung, z. B. Server-Setup bereitstellen).
    - _Liegezeit_ (Inproduktives Warten auf den nächsten Schritt).
    - _Transportzeit_ (Übermittlung von Daten/Material).
- **Instrumente der Dokumentation:**
    - **Organigramm:** Grafische Darstellung der vertikalen Hierarchiestruktur (Leitungstiefe) und Weisungswege eines Betriebs.
    - **Funktionsdiagramm (Verantwortungsmatrix / RACI):** Stellt Aufgaben den zuständigen Stellen gegenüber und definiert über Kürzel (z. B. **E**ntscheidung, **M**itarbeit, **I**nformation) die genauen Kompetenzen, um Unklarheiten in komplexen Projekten zu vermeiden.

---

📊 Visuelle Darstellung (Mermaid.js)

mermaid

```
graph TD
    subgraph OrgaFormen [Aufbauorganisation: Statische Struktur]
        Einlinie[Einliniensystem: 1 Vorgesetzter]
        Mehrlinie[Mehrliniensystem: Mehrere Fachvorgesetzte]
        StabLinie[Stab-Linien-System: Beratung ohne Weisungsrecht]
    end

    subgraph Dualitaet [Betriebliche Regelungen]
        Org[Organisation: Dauerhafte Regelung] --> Disp[Disposition: Fallweise Regelung]
        Disp --> Imp[Improvisation: Vorlaeufige Notfall-Regelung]
    end

    subgraph Durchlaufzeit [Ablauforganisation: Prozess-Komponenten]
        B[Bearbeitungszeit] --> R[Ruestzeit]
        R --> L[Liegezeit]
        L --> T[Transportzeit]
    end
```

Verwende Code mit Vorsicht.

---

Um das Lernsheet optimal abzurunden, lass mich wissen:

- Sollen wir ein **konkretes IHK-Rechenbeispiel zur Optimierung von Durchlaufzeiten** ergänzen?
- Möchtest du eine interaktive Übung zur **Erstellung einer RACI-Matrix (Funktionsdiagramm)** für ein IT-Projekt einbauen?
- Sollen wir die Vor- und Nachteile von **Matrixorganisationen** in einer übersichtlichen Prüfungstabelle gegenüberstellen?

KI-Antworten können Fehler enthalten. Aufgrund aktueller Einschränkungen kann nur ein Teil des Dokuments für diese Antwort verwendet werden. [Weitere Informationen](https://support.google.com/websearch?p=aimode)