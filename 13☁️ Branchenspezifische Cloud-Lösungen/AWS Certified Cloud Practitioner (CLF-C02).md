# Themenblock 1: Cloud-Konzepte & Sicherheit

> **Modul:** AWS Certified Cloud Practitioner (CLF-C02)  
> **Thema:** Cloud-Konzepte, Vorteile der AWS Cloud & Modell der geteilten Verantwortung  
> **Ziel:** Fundamentales Verständnis für die Prüfung (Prüfungsziel ≥ 90 %)

---

## 1. Cloud-Computing & Finanzmodelle

### On-Demand & Pay-as-you-go
* **On-Demand:** IT-Ressourcen (Server, Speicher, Datenbanken) werden bei Bedarf per Mausklick in Sekunden/Minuten bereitgestellt.
* **Pay-as-you-go:** Abrechnung erfolgt nur für die exakt genutzte Laufzeit (sekunden- oder minutengenau). Wird die Ressource gestoppt, entfallen die Kosten für die Rechenleistung.

### CAPEX vs. OPEX

| Eigenschaft | On-Premises (Klassische IT) | AWS Cloud |
| :--- | :--- | :--- |
| **Finanzmodell** | **CAPEX** (Capital Expenditures / Kapitalausgaben) | **OPEX** (Operational Expenditures / Betriebsausgaben) |
| **Investition** | Hohe Vorabinvestitionen in physische Hardware & Rechenzentren. | Variable Kosten basierend auf dem tatsächlichen Verbrauch. |
| **Risiko** | Hohes Risiko durch Kapazitäts-Fehlplanungen (Über- oder Unterdimensionierung). | Flexibel anpassbar; keine langfristigen Bindungen erforderlich. |

> [!TIP] **FiSi-Metapher:**  
> **CAPEX** ist der Kauf eines Autos inklusive Garagenmiete und Instandhaltung für die nächsten 5 Jahre.  
> **OPEX** ist Carsharing: Du zahlst nur die gefahrenen Minuten.

---

## 2. Die Kernvorteile der AWS Cloud

1. **Degressionsgewinn (Economies of Scale):**  
   Durch die Bündelung von Hunderttausenden Kunden weltweit erzielt AWS massive Skaleneffekte. Dies führt zu niedrigeren Einkaufspreisen für Hardware, die in Form von regelmäßigen Preissenkungen an Kunden weitergegeben werden.
2. **Keine Mutmaßung von Kapazitäten (Stop Guessing Capacity):**  
   Ressourcen werden automatisch basierend auf dem tatsächlichen Bedarf skaliert. Keine ungenutzten Brachflächen mehr.
3. **Erhöhte Geschwindigkeit und Agilität:**  
   Entwickler und Admins können Ressourcen in Minuten testen und bereitstellen, statt Wochen auf Hardware-Lieferungen zu warten.
4. **Fokus auf Kerngeschäft (Business Value):**  
   Verlagerung des Aufwands für das "Heavy Lifting" (Server-Racks montieren, Strom, Kühlung, physische Absicherung) auf AWS.
5. **Globale Reichweite in Minuten:**  
   Anwendungen können mit wenigen Klicks weltweit nahe an den Endbenutzern bereitgestellt werden (geringe Latenzen).

---

## 3. Skalierbarkeit vs. Elastizität (Prüfungsfokus!)

```
[ Last steigt ]
   ├── Vertikale Skalierbarkeit (Scaling Up):  [ Server ] -> [ Dickerer Server (mehr RAM/CPU) ]
   └── Horizontale Skalierbarkeit (Scaling Out): [ Server ] -> [ Server ] + [ Server ] + [ Server ]

[ Last schwankt ]
   └── Elastizität (Elasticity): Automatische Anpassung (Rein & Raus) je nach Traffic.
```

* **Skalierbarkeit (Scalability):** Die Fähigkeit eines Systems, steigende Lasten durch Hinzufügen von Ressourcen zu bewältigen.
  * **Vertikal (Scaling Up / Down):** Einem bestehenden Server mehr/weniger Ressourcen (CPU, RAM) zuweisen.
  * **Horizontal (Scaling Out / In):** Dem System weitere Server-Instanzen hinzufügen oder entfernen.
* **Elastizität (Elasticity):** Die Fähigkeit, Ressourcen **vollautomatisch** je nach Nachfrage hoch- und wieder **herunterzuskalieren**.

---

## 4. AWS-Modell der geteilten Verantwortung (Shared Responsibility Model)

> [!IMPORTANT] **Goldene Regel für die Prüfung:**  
> **AWS** ist verantwortlich für die Sicherheit **DER** Cloud (*Security OF the Cloud*).  
> **Der Kunde** ist verantwortlich für die Sicherheit **IN** der Cloud (*Security IN the Cloud*).

### Zuständigkeiten im Überblick

```
┌─────────────────────────────────────────────────────────────────┐
│                    VERANTWORTUNG DES KUNDEN                      │
│   (Daten, IAM-Rechte, Gast-Betriebssystem, OS-Patches, FW)       │
├─────────────────────────────────────────────────────────────────┤
│                     VERANTWORTUNG VON AWS                       │
│   (Physische Rechenzentren, Hardware, Hypervisor, Netze)        │
└─────────────────────────────────────────────────────────────────┘
```

* **Verantwortung von AWS:**
  * Physische Sicherheit der Rechenzentren (Zutrittskontrollen, Strom, Kühlung).
  * Wartung der physischen Hardware (Server, Festplatten, Switche).
  * Host-Betriebssystem und Virtualisierungsschicht (Hypervisor).
* **Verantwortung des Kunden:**
  * Kunden-Daten und Verschlüsselung (At-Rest und In-Transit).
  * Identitäts- und Zugriffsverwaltung (IAM) & Passwortrichtlinien.
  * Betriebssystem-Patches auf virtuellen Servern (**Amazon EC2**).
  * Konfiguration von Firewalls (**Security Groups**, Network ACLs).

### Abgrenzung: Unmanaged vs. Managed Services

* **IaaS (z. B. Amazon EC2):** Höchste Kontrolle für den Kunden. Der Kunde muss das Gast-Betriebssystem selbst patchen und konfigurieren.
* **PaaS / Managed Services (z. B. Amazon RDS):** AWS übernimmt zusätzlich das Betriebssystem-Patching, Software-Updates und automatisierte Backups. Der Kunde verwaltet nur noch Daten und Tabellenrechte.

---

## 5. Glossar (AWS CLF-C02 Key Terms)

* **Availability Zone (AZ):** Ein oder mehrere isolierte, physisch getrennte Rechenzentren innerhalb einer AWS-Region mit redundanter Stromversorgung und Netzwerkanbindung.
* **AWS Region:** Ein geografisches Gebiet weltweit, das mehrere isolierte Availability Zones enthält.
* **CAPEX (Capital Expenditures):** Investitionsausgaben für physische Anlagen (z. B. Kauf von Server-Hardware im Voraus).
* **EC2 (Elastic Compute Cloud):** Virtuelle Server in der AWS Cloud (IaaS).
* **Elasticity (Elastizität):** Automatische dynamische Skalierung von IT-Ressourcen je nach aktuellem Bedarf.
* **Managed Service:** Ein von AWS verwalteter Dienst (z. B. RDS), bei dem AWS administrative Aufgaben wie Wartung, Patching und Backups übernimmt.
* **OPEX (Operational Expenditures):** Laufende Betriebsausgaben für die Nutzung von Diensten (Pay-as-you-go).
* **RDS (Relational Database Service):** Verwalteter relationaler Datenbankdienst von AWS (PaaS).
* **Scalability (Skalierbarkeit):** Die Eigenschaft eines Systems, durch Hinzufügen von Leistung mit höheren Anforderungen mitzuwachsen.
* **Shared Responsibility Model:** Regelwerk, das festlegt, welche Sicherheitsaufgaben bei AWS und welche beim Kunden liegen.