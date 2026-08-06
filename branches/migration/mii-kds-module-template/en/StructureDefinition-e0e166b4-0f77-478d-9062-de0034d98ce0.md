# Profile - MI-I - Consent - Einwilligung - MII Implementation Guide Consent v2026.0.0

* [**Table of Contents**](toc.md)
* [**Artifacts Summary**](artifacts.md)
* **Profile - MI-I - Consent - Einwilligung**

## Resource Profile: Profile - MI-I - Consent - Einwilligung 

| | |
| :--- | :--- |
| *Official URL*:https://www.medizininformatik-initiative.de/fhir/modul-consent/StructureDefinition/mii-pr-consent-einwilligung | *Version*:2026.0.0 |
| Active as of 2025-12-03 | *Computable Name*:MII_PR_Consent_Einwilligung |

 
Dieses Profil beschreibt eine Einwilligung in der Medizininformatik-Initiative. 

**TODO:REVIEW (Gate C) — unreviewed machine translation.** The authoritative text of this module is German. This page is an unreviewed machine translation of the German intro note, migrated from the Simplifier-rendered guide (version 2026.0.0, harvested 2026-08-06). Consent policy wording and policy display names are left in German on purpose: they are legally binding text and identifiers. Where the two language variants differ, the German page applies.

This profile describes an operationalised, automatically generated and processable consent within the Medical Informatics Initiative.

When a person is enrolled in a study (including an MII use case), a consent is obtained for that person on the basis of the [MII Broad Consent model texts](https://www.medizininformatik-initiative.de/de/mustertext-zur-patienteneinwilligung), and the corresponding consent document is documented in a structured way at the respective site, following the [requirements of the MII Task Force Consent Umsetzung](https://art-decor.org/art-decor/decor-datasets--mide-?id=2.16.840.1.113883.3.1937.777.24.1.1&effectiveDate=2018-06-05T12%3A44%3A12&conceptId=2.16.840.1.113883.3.1937.777.24.2.184&conceptEffectiveDate=2018-06-29T16%3A26%3A50&language=de-DE).

The FHIR Consent resource is generated automatically on the basis of these consent documents. The [project context](https://ig.fhir.de/einwilligungsmanagement/stable/DomainReference.html) is preserved.

The resource must be created before participating in cross-site feasibility requests and data releases. Further obligations and adaptations have to be checked for each use case.

**Privacy aspects** of this profile — pseudonymous person reference, handling of person-identifying information, no document scans in the Consent resource — are on [Security and Privacy](security-and-privacy.md).

### Interoperability

To ensure that the operationalised consent content can be exchanged beyond FHIR as well, a uniform policy value set for the **semantic representation** of the statements contained in the MII Broad Consent was agreed with the **MII AG Consent** in December 2021 and documented in [ART-DECOR](http://art-decor.org/decor/services/RetrieveValueSet?id=2.16.840.1.113883.3.1937.777.24.11.36&effectiveDate=2021-04-23T10:55:54&prefix=mide-&format=html&collapsable=true&language=de-DE&ui=en-US) (policy OIDs).

**Using this code system is mandatory for the CDS module Consent.**

**Usages:**

* Examples for this Profile: [Consent/34150a23-b1c8-404f-874f-e042a30435d2](Consent-34150a23-b1c8-404f-874f-e042a30435d2.md), [Consent/5143266b-8d60-4b28-8ee9-635140ffa5bb](Consent-5143266b-8d60-4b28-8ee9-635140ffa5bb.md) and [Consent/Example-MII-Consent-ResultType-document](Consent-Example-MII-Consent-ResultType-document.md)

You can also check for [usages in the FHIR IG Statistics](https://packages2.fhir.org/xig/resource/de.medizininformatikinitiative.kerndatensatz.consent|current/StructureDefinition/StructureDefinition-e0e166b4-0f77-478d-9062-de0034d98ce0.json)

### Formal Views of Profile Content

 [Description of Profiles, Differentials, Snapshots, and their representations](http://build.fhir.org/ig/FHIR/ig-guidance/readingIgs.html#structure-definitions). 

 

Other representations of profile: [CSV](../StructureDefinition-e0e166b4-0f77-478d-9062-de0034d98ce0.csv), [Excel](../StructureDefinition-e0e166b4-0f77-478d-9062-de0034d98ce0.xlsx), [Schematron](../StructureDefinition-e0e166b4-0f77-478d-9062-de0034d98ce0.sch) 

### Notes:

**TODO:REVIEW (Gate C) — unreviewed machine translation.** The authoritative text is the German notes file. Element paths, code values, OIDs and the German policy display names below are **identifiers**: they are reproduced verbatim and are not translated. Where the two language variants differ, the German page applies.

### Basic use of the FHIR Consent profile

**Only the differences from the base profile are explained below.**

| | |
| :--- | :--- |
| `Consent.id` | must-support, but optional |
| `Consent.meta` | must-support, but optional |
| `Consent.meta.source` | must-support, but optional |
| `Consent.meta.profile` | must-support, but optional |
| `Consent.extension:domainReference` | must-support per the requirements of the[AG Einwilligungsmanagement](https://ig.fhir.de/einwilligungsmanagement/stable/ResearchStudy.html), but optional |
| `Consent.identifier` | Contains one or more external IDs of the consent from an external system. This can be, for example, the IHE ID of the CDA document or the ID of the document in an external trusted third party. The identifier should always be given as the pair "system" and "value". Optional. |
| `Consent.scope.coding.system` | fixed value:`http://terminology.hl7.org/CodeSystem/consentscope` |
| `Consent.scope.coding.code` | The representation of the MII consent places the context clearly on research. Fixed value:`research` |
| `Consent.category.coding` | must-support.**At least two categories**are mandatory, each with at least one coding for the consent categories, so that consents of type "MII Einwilligung" can be searched for:**(1)**per[valueset-consent-category](https://www.hl7.org/fhir/valueset-consent-category.html)— fixed system`http://loinc.org`, fixed code for 'Privacy policy acknowledgement Document'`57016-8`;**(2)**identification of the MII Broad Consent — fixed code`2.16.840.1.113883.3.1937.777.24.2.184`. Further additional entries are not prevented. |
| `Consent.category:templateType.coding` | ResultType per[ResultType](https://ig.fhir.de/einwilligungsmanagement/stable/ResultType.html). At least`document`and`consent-status`should be supported. If`document`is given as the ResultType, the kind of (source) document must also be given in the`templateType`slice. |
| `Consent.category:templateType.coding` | Categorisation per[TemplateType](https://ig.fhir.de/einwilligungsmanagement/stable/TemplateType.html). Serves as an informal element to differentiate between consent, withdrawal, objection and refusal. |
| `Consent.patient.reference` | Reference to the patient the Consent resource refers to, as a literal reference, relative reference, internal reference or absolute URL, must-support.`Consent.patient.reference`should be filled where possible, i.e. where a corresponding Patient resource exists. Otherwise the patient reference has to be established via`Consent.patient.identifier`. |
| `Consent.patient.identifier` | The person reference as an identifier, must-support. See`Consent.patient.reference`. The reference to the patient should preferably be established via`Consent.patient.reference`;`Consent.patient.identifier`may be used as an alternative or in addition. |
| `Consent.patient.identifier.system` | If the person reference is given by identifier, the system (as a URI) is mandatory, must-support |
| `Consent.patient.identifier.value` | If the person reference is given by identifier, the value (as a string) is mandatory, must-support |
| `Consent.policy.uri` | Reference to the version of the MII Broad Consent document underlying the Consent resource, per the table below — e.g.**MII Broad Consent version 1.7.2**`urn:oid:2.16.840.1.113883.3.1937.777.24.2.2079`or**MII Broad Consent version 1.7.2 incl. Zusatzmodul Acribis**`urn:oid:2.16.840.1.113883.3.1937.777.24.2.4031`, must-support |

> **TODO:REVIEW (Gate B) — two rows under the same slice name.** The rendered source page lists both category rows under `Consent.category:templateType.coding`, although the first describes the ResultType. Both rows are reproduced unchanged (nothing corrected, nothing added). In addition, this profile slices `Consent.category` into the slices `loinc` and `mii`; the slice names `templateType`/`resultType` come from the base profile of the AG Einwilligungsmanagement. Please check against the StructureDefinition and have the source corrected.

### Unique identification of the MII Broad Consent

To filter FHIR Consent resources for consents based on the MII Broad Consent, a mandatory URI is used for `Consent.policy.uri`. The TFCU has created ART-DECOR representations for the different versions of the MII Broad Consent. They can be referenced by a unique OID (see the table below). The version labels are the German designations of the consent forms and are not translated.

| | |
| :--- | :--- |
| 1.6d | 2.16.840.1.113883.3.1937.777.24.2.1790 |
| 1.6d Ablehnung | 2.16.840.1.113883.3.1937.777.24.2.4053 |
| 1.6d Komplettwiderruf | 2.16.840.1.113883.3.1937.777.24.2.2718 |
| 1.6d Teilwiderruf | 2.16.840.1.113883.3.1937.777.24.2.2719 |
| 1.6f | 2.16.840.1.113883.3.1937.777.24.2.1791 |
| 1.6f Komplettwiderruf | 2.16.840.1.113883.3.1937.777.24.2.2720 |
| 1.6f Teilwiderruf | 2.16.840.1.113883.3.1937.777.24.2.2721 |
| 1.7.2 | 2.16.840.1.113883.3.1937.777.24.2.2079 |
| 1.7.2 Ablehnung | 2.16.840.1.113883.3.1937.777.24.2.4054 |
| 1.7.2 Komplettwiderruf | 2.16.840.1.113883.3.1937.777.24.2.2722 |
| 1.7.2 Teilwiderruf | 2.16.840.1.113883.3.1937.777.24.2.2723 |
| 1.7.2 (Eltern und Sorgeberechtigte für Minderjährige v1.1) | 2.16.840.1.113883.3.1937.777.24.2.3542 |
| 1.7.2 (7–11 Minderjährige v1.1) | 2.16.840.1.113883.3.1937.777.24.2.3543 |
| 1.7.2 (12–17 Minderjährige v1.1) | 2.16.840.1.113883.3.1937.777.24.2.3544 |
| Zusatzmodul ACRIBiS (Z2) | 2.16.840.1.113883.3.1937.777.24.2.4031 |
| Zusatzmodul Patientenbefragung (Z3) | 2.16.840.1.113883.3.1937.777.24.2.4036 |
| Zusatzmodul Fachnetzwerk Infektion – SNID (Z4) | 2.16.840.1.113883.3.1937.777.24.2.4037 |
| Zusatzmodul Deutsches Zentrum für Psychische Gesundheit – DZPG (Z5) | 2.16.840.1.113883.3.1937.777.24.2.4048 |

### Nested provision elements

The FHIR Consent resource follows the GDPR requirement of **opt-in**: only what was explicitly consented to at a particular point in time (the time of consent) is permitted. This is realised through nested provision elements.

In opt-in scenarios the **parent provision element** (→ **level-1 provision**) denies everything (`Provision.Type=DENY`) unless it is explicitly permitted in the form of **child provision elements** (→ **level-2 provision**). Child provisions therefore have to use provision elements with `Provision.Type=PERMIT`. For additional information, level-2 provisions with `Provision.Type=DENY` are possible.

The general validity period of the consent is likewise realised through the parent provision element by means of `provision.period` (for the MII Broad Consent: 30 years).

Should individual parts of the consent expire earlier, these exceptions can be defined as part of child provisions referring to the relevant part of the consent by means of `provision.provision.period` (e.g. the provision with code `2.16.840.1.113883.3.1937.777.24.5.3.6` for the policy "MDAT erheben" expires after 5 years).

**Parent provision (`Consent.provision`)**

| | |
| :--- | :--- |
| `Consent.provision.type` | value`DENY`or`PERMIT`, must-support |
| `Consent.provision.period.start` | mandatory start of the validity of the consent. Unless specified otherwise this is typically the date on which the data subject signed the consent, must-support |
| `Consent.provision.period.end` | mandatory end of the validity of the consent. This is typically the point at which the consent period defined for the MII expires (30 years from the date of signature), must-support |
| `Consent.provision.action` | actions are not permitted, not supported |
| `Consent.provision.code` | codes are not permitted in the parent provision, not supported |
| `Consent.provision.provision` | list of child provision elements explicitly permitting (data processing) activities, must-support |

**Child provision elements (`Consent.provision.provision`)**

**Exactly one child provision element should be used per consent policy.**

| | |
| :--- | :--- |
| `Consent.provision.provision.type` | value`PERMIT`or`DENY`, must-support |
| `Consent.provision.provision.period.start` | mandatory start of the validity of the consent policy, must-support |
| `Consent.provision.provision.period.end` | mandatory end of the validity of the consent policy, must-support |
| `Consent.provision.provision.code` | 1..n statements on the semantics of the consent policy.**At least per the MII TFCU concept**(cf.[MII Consent: Policy ValueSet](ValueSet-2.16.840.1.113883.3.1937.777.24.11.36--20230331232804.md)), must-support |
| `Consent.provision.provision.code.coding.system` | system, ideally per the**MII TFCU concept**(cf.[MII Consent: Policy ValueSet](ValueSet-2.16.840.1.113883.3.1937.777.24.11.36--20230331232804.md)):`urn:oid:2.16.840.1.113883.3.1937.777.24.5.3`, must-support |
| `Consent.provision.provision.code.coding.code` | code, ideally per the**MII TFCU concept**(cf.[MII Consent: Policy ValueSet](ValueSet-2.16.840.1.113883.3.1937.777.24.11.36--20230331232804.md)), e.g.`2.16.840.1.113883.3.1937.777.24.5.3.6`, must-support |
| `Consent.provision.provision.code.coding.display` | optional display, ideally per the**MII TFCU concept**(cf.[MII Consent: Policy ValueSet](ValueSet-2.16.840.1.113883.3.1937.777.24.11.36--20230331232804.md)), e.g. "MDAT erheben" |
| `Consent.provision.provision.action` | actions are not permitted, not supported |
| `Consent.provision.provision.provision` | further nesting levels of provisions are not permitted, not supported |

### End of the consent, and Consent resources in the context of withdrawal, refusal or objection

Per the requirements of the MII AG Consent, a patient's consent generally ends after 30 years. Consents of **minors** (the person the consent concerns) are a special case: where such consents were filled in on their behalf by those with custody, **the consent ends when the data subject reaches the age of majority**. This has to be implemented technically. [Reference implementations](https://www.ths-greifswald.de/dezember-release-2025-neue-versionen-von-e-pix-gpas-und-gics-verfuegbar/) exist.

The [withdrawal template (compatible with MII BC 1.7.2)](https://www.medizininformatik-initiative.de/sites/default/files/2025-01/MII_BC_Formular-Komplettwiderruf.pdf) is also intended for withdrawing consents of minors, as these too are usually filled in by those with custody.

For Consent resources created in connection with withdrawals (full or partial), refusals or objections, the [recommendations of the HL7-D AG Einwilligungsmanagement](https://simplifier.net/guide/Einwilligungsmanagement/Consent?version=current) generally apply (cf. the section **Angepasste Empfehlungen zur Verwendung von Consent und Consent-Provisions nach Dokumentenart und Szenario**):

**Level-2 provisions should therefore always be given where possible.** If a document has no conceptually defined end (for example a withdrawal, refusal or objection), `period.end` may accordingly be omitted from the provisions.



## Resource Content

```json
{
  "resourceType" : "StructureDefinition",
  "id" : "e0e166b4-0f77-478d-9062-de0034d98ce0",
  "url" : "https://www.medizininformatik-initiative.de/fhir/modul-consent/StructureDefinition/mii-pr-consent-einwilligung",
  "version" : "2026.0.0",
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
  "baseDefinition" : "http://hl7.org/fhir/StructureDefinition/Consent",
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
      "id" : "Consent.extension",
      "path" : "Consent.extension",
      "slicing" : {
        "discriminator" : [{
          "type" : "value",
          "path" : "url"
        }],
        "rules" : "open"
      }
    },
    {
      "id" : "Consent.extension:domainReference",
      "path" : "Consent.extension",
      "sliceName" : "domainReference",
      "min" : 0,
      "max" : "*",
      "type" : [{
        "code" : "Extension",
        "profile" : ["http://fhir.de/ConsentManagement/StructureDefinition/DomainReference"]
      }],
      "mustSupport" : true
    },
    {
      "id" : "Consent.extension:domainReference.extension:domain",
      "path" : "Consent.extension.extension",
      "sliceName" : "domain",
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
      "path" : "Consent.status",
      "mustSupport" : true
    },
    {
      "id" : "Consent.scope",
      "path" : "Consent.scope",
      "comment" : "Wird im Kontext des Einwilligungsmanagment-Leitfadens nicht näher definiert.\r\nBei Bedarf kann das ValueSet erweitert oder ggf. ein NullFlavor-Code eingetragen werden."
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
      "slicing" : {
        "discriminator" : [{
          "type" : "pattern",
          "path" : "$this"
        }],
        "rules" : "open"
      },
      "min" : 2,
      "mustSupport" : true
    },
    {
      "id" : "Consent.category:loinc",
      "path" : "Consent.category",
      "sliceName" : "loinc",
      "min" : 1,
      "max" : "1",
      "patternCodeableConcept" : {
        "coding" : [{
          "system" : "http://loinc.org",
          "code" : "57016-8"
        }]
      },
      "mustSupport" : true
    },
    {
      "id" : "Consent.category:loinc.coding",
      "path" : "Consent.category.coding",
      "min" : 1,
      "max" : "1",
      "mustSupport" : true
    },
    {
      "id" : "Consent.category:loinc.coding.system",
      "path" : "Consent.category.coding.system",
      "min" : 1,
      "mustSupport" : true
    },
    {
      "id" : "Consent.category:loinc.coding.code",
      "path" : "Consent.category.coding.code",
      "min" : 1,
      "mustSupport" : true
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
      "id" : "Consent.patient",
      "path" : "Consent.patient",
      "min" : 1,
      "type" : [{
        "code" : "Reference",
        "targetProfile" : ["http://fhir.de/ConsentManagement/StructureDefinition/Patient"]
      }],
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
      "definition" : "Dieser Zeitpunkt sollte in der Praxis, zumindest bei vollelektronischer Verarbeitung, identisch mit dem Unterschriftsdatum des Fragebogens sein (Provenance.signature.when des Patienten)",
      "comment" : "Dieser Zeitpunkt sollte in der Praxis, zumindest bei vollelektronischer Verarbeitung, identisch mit dem Unterschriftsdatum des Fragebogens sein (Provenance.signature.when des Patienten)",
      "min" : 1,
      "mustSupport" : true
    },
    {
      "id" : "Consent.organization",
      "path" : "Consent.organization",
      "short" : "Organisation, in der die Einwilligung erfasst wurde.",
      "definition" : "Dies ist die Organisation, die den Consent erfasst hat.",
      "mustSupport" : true
    },
    {
      "id" : "Consent.source[x]",
      "path" : "Consent.source[x]",
      "type" : [{
        "code" : "Reference",
        "targetProfile" : ["http://fhir.de/ConsentManagement/StructureDefinition/QuestionnaireResponse"]
      }],
      "mustSupport" : true
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
      "path" : "Consent.source[x].reference",
      "min" : 1,
      "mustSupport" : true
    },
    {
      "id" : "Consent.policy",
      "path" : "Consent.policy",
      "min" : 1,
      "mustSupport" : true
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
      "path" : "Consent.policy.uri",
      "min" : 1,
      "mustSupport" : true
    },
    {
      "id" : "Consent.policyRule",
      "path" : "Consent.policyRule",
      "mustSupport" : true
    },
    {
      "id" : "Consent.policyRule.extension:xacml",
      "path" : "Consent.policyRule.extension",
      "sliceName" : "xacml",
      "min" : 0,
      "max" : "1",
      "type" : [{
        "code" : "Extension",
        "profile" : ["http://fhir.de/ConsentManagement/StructureDefinition/Xacml"]
      }],
      "mustSupport" : true
    },
    {
      "id" : "Consent.provision",
      "path" : "Consent.provision",
      "mustSupport" : true
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
      "min" : 1,
      "mustSupport" : true
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
