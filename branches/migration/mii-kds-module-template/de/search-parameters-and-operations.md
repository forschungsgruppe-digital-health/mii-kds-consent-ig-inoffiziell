# Suchparameter und Operationen - MII Implementation Guide Consent v2026.0.0

* [**Inhaltsverzeichnis**](toc.md)
* **Suchparameter und Operationen**

## Suchparameter und Operationen

 Diese Seite enthält Übersetzungen aus der Originalsprache, in der der Leitfaden verfasst wurde. Informationen zu diesen Übersetzungen und Anweisungen zum Abgeben von Feedback zu den Übersetzungen finden Sie [hier](translationinfo.md). 

### Suchparameter und Operationen

Bei Verwendung der FHIR RESTful API müssen die hier aufgeführten Suchparameter durch die jeweiligen Systeme implementiert werden. Grundsätzlich werden logische AND- und OR-Verknüpfungen der FHIR-Search unterstützt, vgl. [hl7.org/fhir/search.html](http://www.hl7.org/fhir/search.html).

Dieses Modul definiert **keine eigenen Operationen**.

#### Kategorie

Im Kontext dieses Leitfadens muss der Standard-Suchparameter **`Consent.category`** unterstützt werden (vgl. [hl7.org/fhir/consent.html#search](http://www.hl7.org/fhir/consent.html#search)).

Beispiel hierzu:

```
GET [base]/Consent?category=2.16.840.1.113883.3.1937.777.24.2.184

```

findet alle (gültigen und nicht mehr gültigen) Consent-Ressourcen zum Zeitpunkt der Anfrage, die einer beliebigen Version des MII Broad Consent (z. B. 1.6d, 1.7.2 usw.) entsprechen.

#### Modul-eigene Suchparameter

| | | | |
| :--- | :--- | :--- | :--- |
| [`mii-provision-provision-code`](SearchParameter-MII-SP-Consent-ProvisionCode.md) | token | `Consent.provision.provision.code` | Provision-Code |
| [`mii-provision-provision-type`](SearchParameter-MII-SP-Consent-ProvisionType.md) | token | `Consent.provision.provision.type` | Typ der Provision (`permit`,`deny`) |
| [`mii-provision-provision-code-type`](SearchParameter-MII-SP-Consent-ProvisionCodeType.md) | composite | `Consent.provision.provision` | Typ der Provision einer bestimmten, durch einen Code definierten Provision |
| [`mii-provision-provision-period`](SearchParameter-MII-SP-Consent-ProvisionPeriod.md) | date | `Consent.provision.provision.period` | Provisions-Zeitraum |
| [`mii-provision-provision-code-period`](SearchParameter-MII-SP-Consent-ProvisionCodePeriod.md) | composite | `Consent.provision.provision` | Provisions-Zeitraum einer bestimmten, durch einen Code definierten Provision |
| [`mii-policy-uri`](SearchParameter-MII-SP-Consent-PolicyUri.md) | uri | `Consent.policy.uri` | Policy-URI (versionsspezifischer MII Broad Consent) |

Beispiele je Suchparameter:

```
GET [base]/Consent?mii-provision-provision-code=urn:oid:2.16.840.1.113883.3.1937.777.24.5.3|2.16.840.1.113883.3.1937.777.24.5.3.8

GET [base]/Consent?mii-provision-provision-type=permit

GET [base]/Consent?mii-provision-provision-code-type=urn:oid:2.16.840.1.113883.3.1937.777.24.5.3|2.16.840.1.113883.3.1937.777.24.5.3.8$permit

GET [base]/Consent?mii-provision-provision-period=2020-12-15

GET [base]/Consent?mii-provision-provision-code-period=urn:oid:2.16.840.1.113883.3.1937.777.24.5.3|2.16.840.1.113883.3.1937.777.24.5.3.8$2020-12-15

GET [base]/Consent?mii-policy-uri=urn:oid:2.16.840.1.113883.3.1937.777.24.2.1791

```

#### Mitgeltende Suchparameter gemäß HL7-D Standard Einwilligungsmanagement

Im Kontext der Suche nach Consent-Ressourcen sind nach dem [HL7-D Standard für Einwilligungsmanagement](https://ig.fhir.de/einwilligungsmanagement/stable/Consent.html) (Version 2.0) folgende Suchparameter zur Filterung von Consent-Ressourcen definiert. Diese werden ebenfalls durch den MII KDS Consent unterstützt. Konkrete Beispiele sind im IG der HL7-D-Arbeitsgruppe dokumentiert.

| | |
| :--- | :--- |
| `domain` | Einwilligungsdomäne. Insbesondere wird empfohlen, logische Referenzen (Reference by Identifier, im Suchparameter: Modifier`:identifier`) zu unterstützen. |
| `category` | Art des Dokuments (Einwilligung, Widerruf usw.); ResultType (Dokument, Consent-Status usw.) |
| `patient.identifier` | Die betroffene Person, identifiziert über einen Identifier |

**Anmerkung: Da eine Dependency auf das Paket der HL7-D AG Einwilligungsmanagement besteht, existiert der Suchparameter `domain` automatisch und muss nicht explizit für das KDS-Modul definiert werden. Er wird technisch ‚einfach übernommen‘.**

#### Komplexere Beispiele (Suchanfragen)

```
GET [base]/Consent?mii-provision-provision-type=permit&mii-provision-provision-code=urn:oid:2.16.840.1.113883.3.1937.777.24.5.3|2.16.840.1.113883.3.1937.777.24.5.3.8&mii-provision-provision-code=urn:oid:2.16.840.1.113883.3.1937.777.24.5.3|2.16.840.1.113883.3.1937.777.24.5.3.9

```

findet alle Consent-Ressourcen mit Permit-Provision, bei denen sowohl der Provision-Code `2.16.840.1.113883.3.1937.777.24.5.3.8` als auch der Provision-Code `2.16.840.1.113883.3.1937.777.24.5.3.9` gesetzt sind.

```
GET [base]/Consent?mii-provision-provision-type=permit&mii-provision-provision-code=urn:oid:2.16.840.1.113883.3.1937.777.24.5.3|2.16.840.1.113883.3.1937.777.24.5.3.8,mii-provision-provision-code=urn:oid:2.16.840.1.113883.3.1937.777.24.5.3|2.16.840.1.113883.3.1937.777.24.5.3.9

```

findet alle Consent-Ressourcen mit Permit-Provision, bei denen der Provision-Code `2.16.840.1.113883.3.1937.777.24.5.3.8` oder der Provision-Code `2.16.840.1.113883.3.1937.777.24.5.3.9` gesetzt ist.

```
GET [base]/Consent?domain:identifier=MII&category=http://fhir.de/ConsentManagement/CodeSystem/TemplateType|CONSENT-OPT-IN&category=http://fhir.de/ConsentManagement/CodeSystem/ResultType|document

```

findet alle Consent-Ressourcen vom Typ „Einwilligung“ in einer Domäne `mii`. Eine Consent-Ressource je Einwilligungsdokument. `Bundle.total` gibt Aufschluss über die Anzahl der Einwilligungen.

```
GET [base]/Consent?category=http://fhir.de/ConsentManagement/CodeSystem/TemplateType|WITHDRAWAL&category=http://fhir.de/ConsentManagement/CodeSystem/ResultType|document

```

findet alle Consent-Ressourcen vom Typ „Widerruf“. Eine Consent-Ressource je Widerrufsdokument. `Bundle.total` gibt Aufschluss über die Anzahl der Widerrufe.

```
GET [base]/Consent?category=http://fhir.de/ConsentManagement/CodeSystem/TemplateType|REFUSAL&category=http://fhir.de/ConsentManagement/CodeSystem/ResultType|document

```

findet alle Consent-Ressourcen vom Typ „Ablehnung“. Eine Consent-Ressource je Ablehnungsdokument. `Bundle.total` gibt Aufschluss über die Anzahl der Ablehnungen.

```
GET [base]/Consent?domain:identifier=MII&category=http://fhir.de/ConsentManagement/CodeSystem/ResultType|consent-status

```

findet alle Consent-Ressourcen in der Domäne `mii`. Jede Consent-Ressource **berücksichtigt alle relevanten Einwilligungs-, Widerrufs- und Ablehnungsdokumente für einen (!) Patienten**. Die Consent-Ressource mit ResultType `consent-status` aggregiert Einwilligungsinformationen, bezieht sich auf exakt einen Patienten und repräsentiert den aktuellen Einwilligungsstand des Patienten. Gleichzeitig entspricht `Bundle.total` der Anzahl der Patienten, für die mindestens ein Dokument mit Einwilligungsinformationen (Einwilligung, Widerruf, Ablehnung) vorliegt.

