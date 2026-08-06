# Profile - MI-I - Consent - DocumentReference - MII Implementation Guide Consent v2026.0.0

* [**Table of Contents**](toc.md)
* [**Artifacts Summary**](artifacts.md)
* **Profile - MI-I - Consent - DocumentReference**

## Resource Profile: Profile - MI-I - Consent - DocumentReference 

| | |
| :--- | :--- |
| *Official URL*:https://www.medizininformatik-initiative.de/fhir/modul-consent/StructureDefinition/mii-pr-consent-documentreference | *Version*:2026.0.0 |
| Draft as of 2023-05-09 | *Computable Name*:MII_PR_Consent_DocumentReference |

 
Dieses Profil beschreibt die Abbildung von Originaldokumenten zu Einwilligungen in der Medizininformatik-Initiative. Diese müssen im PDF-Format vorliegen. 

**TODO:REVIEW (Gate C) — unreviewed machine translation.** The authoritative text of this module is German; this page is an unreviewed machine translation of the German intro note (source guide version 2026.0.0, harvested 2026-08-06). Where the two language variants differ, the German page applies.

Based on the [recommendations](https://ig.fhir.de/einwilligungsmanagement/stable/DocumentReference.html) of the AG Einwilligungsmanagement, the profile **MIIConsentDocumentReference** targets a real, existing document related to the consent document.

It is, however, restricted to scans of consent documents in PDF format.

**Usages:**

* Refer to this Profile: [Profile - MI-I - Consent - Provenance](StructureDefinition-f675b1e8-9f3f-44e8-bb59-9681f78eb464.md)
* Examples for this Profile: [DocumentReference/8a3d1799-2463-405e-b49c-6a16c8692b01](DocumentReference-8a3d1799-2463-405e-b49c-6a16c8692b01.md)

You can also check for [usages in the FHIR IG Statistics](https://packages2.fhir.org/xig/resource/de.medizininformatikinitiative.kerndatensatz.consent|current/StructureDefinition/StructureDefinition-56375452-bfa1-4111-af7c-5b5ba9a1857c.json)

### Formal Views of Profile Content

 [Description of Profiles, Differentials, Snapshots, and their representations](http://build.fhir.org/ig/FHIR/ig-guidance/readingIgs.html#structure-definitions). 

 

Other representations of profile: [CSV](../StructureDefinition-56375452-bfa1-4111-af7c-5b5ba9a1857c.csv), [Excel](../StructureDefinition-56375452-bfa1-4111-af7c-5b5ba9a1857c.xlsx), [Schematron](../StructureDefinition-56375452-bfa1-4111-af7c-5b5ba9a1857c.sch) 

### Notes:

**TODO:REVIEW (Gate C) — unreviewed machine translation.** The authoritative text is the German notes file.

| | |
| :--- | :--- |
| `DocumentReference.content.attachment.contentType` | fixed value`application/pdf`, must-support |

### Example

* [Example (complete)](DocumentReference-8a3d1799-2463-405e-b49c-6a16c8692b01.md)



## Resource Content

```json
{
  "resourceType" : "StructureDefinition",
  "id" : "56375452-bfa1-4111-af7c-5b5ba9a1857c",
  "url" : "https://www.medizininformatik-initiative.de/fhir/modul-consent/StructureDefinition/mii-pr-consent-documentreference",
  "version" : "2026.0.0",
  "name" : "MII_PR_Consent_DocumentReference",
  "title" : "Profile - MI-I - Consent - DocumentReference",
  "status" : "draft",
  "date" : "2023-05-09",
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
  "description" : "Dieses Profil beschreibt die Abbildung von Originaldokumenten zu Einwilligungen in der Medizininformatik-Initiative.\nDiese müssen im PDF-Format vorliegen.",
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
    "identity" : "fhircomposition",
    "uri" : "http://hl7.org/fhir/composition",
    "name" : "FHIR Composition"
  },
  {
    "identity" : "w5",
    "uri" : "http://hl7.org/fhir/fivews",
    "name" : "FiveWs Pattern Mapping"
  },
  {
    "identity" : "v2",
    "uri" : "http://hl7.org/v2",
    "name" : "HL7 v2 Mapping"
  },
  {
    "identity" : "xds",
    "uri" : "http://ihe.net/xds",
    "name" : "XDS metadata equivalent"
  }],
  "kind" : "resource",
  "abstract" : false,
  "type" : "DocumentReference",
  "baseDefinition" : "http://fhir.de/ConsentManagement/StructureDefinition/DocumentReference",
  "derivation" : "constraint",
  "differential" : {
    "element" : [{
      "id" : "DocumentReference",
      "path" : "DocumentReference"
    },
    {
      "id" : "DocumentReference.content.attachment.contentType",
      "path" : "DocumentReference.content.attachment.contentType",
      "patternCode" : "application/pdf"
    }]
  }
}

```
