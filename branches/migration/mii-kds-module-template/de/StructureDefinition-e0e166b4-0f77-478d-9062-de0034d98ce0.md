# Profile - MI-I - Consent - Einwilligung - MII Implementation Guide Consent v2026.0.1

* [**Inhaltsverzeichnis**](toc.md)
* [**Artefaktübersicht**](artifacts.md)
* **Profile - MI-I - Consent - Einwilligung**

## Ressourcenprofil: Profile - MI-I - Consent - Einwilligung 

| | |
| :--- | :--- |
| *Offizielle URL*:https://www.medizininformatik-initiative.de/fhir/modul-consent/StructureDefinition/mii-pr-consent-einwilligung | *Version*:2026.0.1 |
| Active Stand: 2025-12-03 | *Maschinenlesbarer Name*:MII_PR_Consent_Einwilligung |

 
Dieses Profil beschreibt eine Einwilligung in der Medizininformatik-Initiative. 

Dieses Profil beschreibt eine operationalisierte, automatisch erzeugte und prozessierbare Einwilligung in der Medizininformatik-Initiative.

Beim Einschluss einer Person in eine Studie (auch in einen MII-Use Case) wird eine Einwilligung für diese Person auf Basis der [MII Broad Consent Mustertexte](https://www.medizininformatik-initiative.de/de/mustertext-zur-patienteneinwilligung) erhoben und entsprechende Einwilligungsdokument am jeweiligen Standort strukturiert dokumentiert gemäß den [Vorgaben der MII Task Force Consent Umsetzung](https://art-decor.org/art-decor/decor-datasets--mide-?id=2.16.840.1.113883.3.1937.777.24.1.1&effectiveDate=2018-06-05T12%3A44%3A12&conceptId=2.16.840.1.113883.3.1937.777.24.2.184&conceptEffectiveDate=2018-06-29T16%3A26%3A50&language=de-DE).

Auf Grundlage dieser Einwilligungsdokumente wird die FHIR Consent Ressource automatisiert erzeugt. Der [Projektkontext](https://ig.fhir.de/einwilligungsmanagement/stable/DomainReference.html) bleibt erhalten.

Die Erstellung der Ressource muss vor der Teilnahme an Standort-übergreifenden Feasability-Anfragen und Datenherausgaben erfolgen. Weitere Pflichten und Anpassungen sind für jeden Use Case zu prüfen.

### Interoperabilität

Um die Austauschbarkeit der operationalisierten Einwilligungsinhalte auch über FHIR hinaus sicherzustellen, wurde mit der **MII AG Consent** ein einheitliches PolicyValueSet zur **semantischen Abbildung** der im MII Broad Consent enthaltenen Aussagen im Dezember 2021 abgestimmt und im [ART-DECOR](http://art-decor.org/decor/services/RetrieveValueSet?id=2.16.840.1.113883.3.1937.777.24.11.36&effectiveDate=2021-04-23T10:55:54&prefix=mide-&format=html&collapsable=true&language=de-DE&ui=en-US) (Policy-OIDs) dokumentiert.

**Die Verwendung dieses Codesystems ist bezogen auf das KDS-Modul Consent verpflichtend.**

**Usages:**

* Examples for this Profile: [Consent/34150a23-b1c8-404f-874f-e042a30435d2](Consent-34150a23-b1c8-404f-874f-e042a30435d2.md), [Consent/5143266b-8d60-4b28-8ee9-635140ffa5bb](Consent-5143266b-8d60-4b28-8ee9-635140ffa5bb.md) and [Consent/Example-MII-Consent-ResultType-document](Consent-Example-MII-Consent-ResultType-document.md)

You can also check for [usages in the FHIR IG Statistics](https://packages2.fhir.org/xig/resource/de.medizininformatikinitiative.kerndatensatz.consent|current/StructureDefinition/StructureDefinition-e0e166b4-0f77-478d-9062-de0034d98ce0.json)

### Formale Ansichten des Profilinhalts

 [Beschreibung von Profilen, Differentials, Snapshots und deren Repräsentationen](http://build.fhir.org/ig/FHIR/ig-guidance/readingIgs.html#structure-definitions). 

*  [Schlüsselelemente-Tabelle](#tabs-key) 
*  [Differential-Tabelle](#tabs-diff) 
*  [Snapshot-Tabelle](#tabs-snap) 
*  [Statistiken/Referenzen](#tabs-summ) 
*  [Alle](#tabs-all) 

#### Terminology Bindings

#### Constraints

Diese Struktur ist abgeleitet von [ConsentManagementConsent](https://simplifier.net/resolve?scope=de.einwilligungsmanagement@2.0.3-snapshots&canonical=http://fhir.de/ConsentManagement/StructureDefinition/Consent) 

#### Terminology Bindings (Differential)

#### Terminology Bindings

#### Constraints

Diese Struktur ist abgeleitet von [ConsentManagementConsent](https://simplifier.net/resolve?scope=de.einwilligungsmanagement@2.0.3-snapshots&canonical=http://fhir.de/ConsentManagement/StructureDefinition/Consent) 

** Summary **

Mandatory: 8 elements(12 nested mandatory elements)
 Must-Support: 24 elements
 Fixed: 2 elements
 Prohibited: 4 elements

 **Schlüsselelemente-Ansicht** 

#### Terminology Bindings

#### Constraints

 **Differential-Ansicht** 

Diese Struktur ist abgeleitet von [ConsentManagementConsent](https://simplifier.net/resolve?scope=de.einwilligungsmanagement@2.0.3-snapshots&canonical=http://fhir.de/ConsentManagement/StructureDefinition/Consent) 

#### Terminology Bindings (Differential)

 **Snapshot-AnsichtView** 

#### Terminology Bindings

#### Constraints

Diese Struktur ist abgeleitet von [ConsentManagementConsent](https://simplifier.net/resolve?scope=de.einwilligungsmanagement@2.0.3-snapshots&canonical=http://fhir.de/ConsentManagement/StructureDefinition/Consent) 

** Summary **

Mandatory: 8 elements(12 nested mandatory elements)
 Must-Support: 24 elements
 Fixed: 2 elements
 Prohibited: 4 elements

 

Weitere Repräsentationen des Profils: [CSV](../StructureDefinition-e0e166b4-0f77-478d-9062-de0034d98ce0.csv), [Excel](../StructureDefinition-e0e166b4-0f77-478d-9062-de0034d98ce0.xlsx), [Schematron](../StructureDefinition-e0e166b4-0f77-478d-9062-de0034d98ce0.sch) 



## Resource Content

```json
{
  "resourceType" : "StructureDefinition",
  "id" : "e0e166b4-0f77-478d-9062-de0034d98ce0",
  "url" : "https://www.medizininformatik-initiative.de/fhir/modul-consent/StructureDefinition/mii-pr-consent-einwilligung",
  "version" : "2026.0.1",
  "name" : "MII_PR_Consent_Einwilligung",
  "title" : "Profile - MI-I - Consent - Einwilligung",
  "status" : "active",
  "date" : "2025-12-03",
  "publisher" : "Medical Informatics Initiative (MII)",
  "_publisher" : {
    "extension" : [{
      "extension" : [{
        "url" : "lang",
        "valueCode" : "de"
      },
      {
        "url" : "content",
        "valueString" : "Medizininformatik-Initiative (MII)"
      }],
      "url" : "http://hl7.org/fhir/StructureDefinition/translation"
    }]
  },
  "contact" : [{
    "name" : "Medical Informatics Initiative (MII)",
    "telecom" : [{
      "system" : "url",
      "value" : "https://www.medizininformatik-initiative.de"
    }]
  }],
  "description" : "Dieses Profil beschreibt eine Einwilligung in der Medizininformatik-Initiative.",
  "jurisdiction" : [{
    "coding" : [{
      "system" : "urn:iso:std:iso:3166",
      "code" : "DE",
      "display" : "Germany"
    }]
  }],
  "fhirVersion" : "4.0.1",
  "mapping" : [{
    "identity" : "workflow",
    "uri" : "http://hl7.org/fhir/workflow",
    "name" : "Workflow Pattern"
  },
  {
    "identity" : "v2",
    "uri" : "http://hl7.org/v2",
    "name" : "HL7 v2 Mapping"
  },
  {
    "identity" : "w5",
    "uri" : "http://hl7.org/fhir/fivews",
    "name" : "FiveWs Pattern Mapping"
  }],
  "kind" : "resource",
  "abstract" : false,
  "type" : "Consent",
  "baseDefinition" : "http://fhir.de/ConsentManagement/StructureDefinition/Consent",
  "derivation" : "constraint",
  "differential" : {
    "element" : [{
      "id" : "Consent",
      "path" : "Consent"
    },
    {
      "id" : "Consent.id",
      "path" : "Consent.id",
      "mustSupport" : true
    },
    {
      "id" : "Consent.meta",
      "path" : "Consent.meta",
      "mustSupport" : true
    },
    {
      "id" : "Consent.meta.source",
      "path" : "Consent.meta.source",
      "mustSupport" : true
    },
    {
      "id" : "Consent.meta.profile",
      "path" : "Consent.meta.profile",
      "mustSupport" : true
    },
    {
      "id" : "Consent.status",
      "extension" : [{
        "url" : "http://hl7.org/fhir/StructureDefinition/structuredefinition-standards-status",
        "valueCode" : "normative"
      },
      {
        "url" : "http://hl7.org/fhir/StructureDefinition/structuredefinition-normative-version",
        "valueCode" : "4.0.0"
      }],
      "path" : "Consent.status"
    },
    {
      "id" : "Consent.scope.coding",
      "path" : "Consent.scope.coding",
      "min" : 1,
      "max" : "1"
    },
    {
      "id" : "Consent.scope.coding.system",
      "path" : "Consent.scope.coding.system",
      "min" : 1,
      "fixedUri" : "http://terminology.hl7.org/CodeSystem/consentscope"
    },
    {
      "id" : "Consent.scope.coding.code",
      "path" : "Consent.scope.coding.code",
      "min" : 1,
      "fixedCode" : "research"
    },
    {
      "id" : "Consent.category",
      "path" : "Consent.category",
      "min" : 2
    },
    {
      "id" : "Consent.category:consentCategory",
      "path" : "Consent.category",
      "sliceName" : "consentCategory",
      "max" : "1",
      "patternCodeableConcept" : {
        "coding" : [{
          "system" : "http://loinc.org",
          "code" : "57016-8"
        }]
      }
    },
    {
      "id" : "Consent.category:consentCategory.coding",
      "path" : "Consent.category.coding",
      "max" : "1"
    },
    {
      "id" : "Consent.category:mii",
      "path" : "Consent.category",
      "sliceName" : "mii",
      "min" : 1,
      "max" : "1",
      "patternCodeableConcept" : {
        "coding" : [{
          "system" : "https://www.medizininformatik-initiative.de/fhir/modul-consent/CodeSystem/mii-cs-consent-version-modules",
          "code" : "2.16.840.1.113883.3.1937.777.24.2.184"
        }]
      },
      "mustSupport" : true
    },
    {
      "id" : "Consent.category:mii.coding",
      "path" : "Consent.category.coding",
      "min" : 1,
      "max" : "1",
      "mustSupport" : true
    },
    {
      "id" : "Consent.category:mii.coding.system",
      "path" : "Consent.category.coding.system",
      "min" : 1,
      "mustSupport" : true
    },
    {
      "id" : "Consent.category:mii.coding.code",
      "path" : "Consent.category.coding.code",
      "min" : 1,
      "mustSupport" : true
    },
    {
      "id" : "Consent.patient.reference",
      "extension" : [{
        "url" : "http://hl7.org/fhir/StructureDefinition/structuredefinition-standards-status",
        "valueCode" : "normative"
      },
      {
        "url" : "http://hl7.org/fhir/StructureDefinition/structuredefinition-normative-version",
        "valueCode" : "4.0.0"
      }],
      "path" : "Consent.patient.reference",
      "mustSupport" : true
    },
    {
      "id" : "Consent.patient.identifier",
      "path" : "Consent.patient.identifier",
      "mustSupport" : true
    },
    {
      "id" : "Consent.patient.identifier.system",
      "path" : "Consent.patient.identifier.system",
      "min" : 1,
      "mustSupport" : true
    },
    {
      "id" : "Consent.patient.identifier.value",
      "path" : "Consent.patient.identifier.value",
      "min" : 1,
      "mustSupport" : true
    },
    {
      "id" : "Consent.dateTime",
      "extension" : [{
        "url" : "http://hl7.org/fhir/StructureDefinition/structuredefinition-standards-status",
        "valueCode" : "normative"
      },
      {
        "url" : "http://hl7.org/fhir/StructureDefinition/structuredefinition-normative-version",
        "valueCode" : "4.0.0"
      }],
      "path" : "Consent.dateTime",
      "short" : "Erstellungszeitpunkt der Einwilligung",
      "definition" : "Dieser Zeitpunkt sollte in der Praxis, zumindest bei vollelektronischer Verarbeitung, identisch mit dem Unterschriftsdatum des Fragebogens sein (Provenance.signature.when des Patienten)"
    },
    {
      "id" : "Consent.source[x].reference",
      "extension" : [{
        "url" : "http://hl7.org/fhir/StructureDefinition/structuredefinition-standards-status",
        "valueCode" : "normative"
      },
      {
        "url" : "http://hl7.org/fhir/StructureDefinition/structuredefinition-normative-version",
        "valueCode" : "4.0.0"
      }],
      "path" : "Consent.source[x].reference"
    },
    {
      "id" : "Consent.policy",
      "path" : "Consent.policy",
      "min" : 1
    },
    {
      "id" : "Consent.policy.uri",
      "extension" : [{
        "url" : "http://hl7.org/fhir/StructureDefinition/structuredefinition-standards-status",
        "valueCode" : "normative"
      },
      {
        "url" : "http://hl7.org/fhir/StructureDefinition/structuredefinition-normative-version",
        "valueCode" : "4.0.0"
      }],
      "path" : "Consent.policy.uri"
    },
    {
      "id" : "Consent.provision.type",
      "path" : "Consent.provision.type",
      "min" : 1,
      "mustSupport" : true
    },
    {
      "id" : "Consent.provision.period",
      "path" : "Consent.provision.period",
      "min" : 1
    },
    {
      "id" : "Consent.provision.period.start",
      "path" : "Consent.provision.period.start",
      "min" : 1,
      "mustSupport" : true
    },
    {
      "id" : "Consent.provision.period.end",
      "path" : "Consent.provision.period.end",
      "mustSupport" : true
    },
    {
      "id" : "Consent.provision.action",
      "path" : "Consent.provision.action",
      "max" : "0"
    },
    {
      "id" : "Consent.provision.code",
      "path" : "Consent.provision.code",
      "max" : "0"
    },
    {
      "id" : "Consent.provision.provision",
      "path" : "Consent.provision.provision",
      "type" : [{
        "code" : "BackboneElement"
      }],
      "mustSupport" : true
    },
    {
      "id" : "Consent.provision.provision.type",
      "path" : "Consent.provision.provision.type",
      "min" : 1,
      "mustSupport" : true
    },
    {
      "id" : "Consent.provision.provision.period",
      "path" : "Consent.provision.provision.period",
      "min" : 1,
      "mustSupport" : true
    },
    {
      "id" : "Consent.provision.provision.period.start",
      "path" : "Consent.provision.provision.period.start",
      "min" : 1,
      "mustSupport" : true
    },
    {
      "id" : "Consent.provision.provision.period.end",
      "path" : "Consent.provision.provision.period.end",
      "mustSupport" : true
    },
    {
      "id" : "Consent.provision.provision.action",
      "path" : "Consent.provision.provision.action",
      "max" : "0"
    },
    {
      "id" : "Consent.provision.provision.code",
      "path" : "Consent.provision.provision.code",
      "min" : 1,
      "mustSupport" : true,
      "binding" : {
        "strength" : "required",
        "valueSet" : "https://www.medizininformatik-initiative.de/fhir/modul-consent/ValueSet/mii-vs-consent-policy"
      }
    },
    {
      "id" : "Consent.provision.provision.code.coding",
      "path" : "Consent.provision.provision.code.coding",
      "min" : 1,
      "mustSupport" : true
    },
    {
      "id" : "Consent.provision.provision.code.coding.system",
      "path" : "Consent.provision.provision.code.coding.system",
      "min" : 1,
      "mustSupport" : true
    },
    {
      "id" : "Consent.provision.provision.code.coding.code",
      "path" : "Consent.provision.provision.code.coding.code",
      "min" : 1,
      "mustSupport" : true
    },
    {
      "id" : "Consent.provision.provision.provision",
      "path" : "Consent.provision.provision.provision",
      "max" : "0"
    }]
  }
}

```
