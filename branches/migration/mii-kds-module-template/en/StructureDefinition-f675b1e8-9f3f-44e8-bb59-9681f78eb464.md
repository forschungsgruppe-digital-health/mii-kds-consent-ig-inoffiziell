# Profile - MI-I - Consent - Provenance - MII Implementation Guide Consent v2026.0.0

* [**Table of Contents**](toc.md)
* [**Artifacts Summary**](artifacts.md)
* **Profile - MI-I - Consent - Provenance**

## Resource Profile: Profile - MI-I - Consent - Provenance 

| | |
| :--- | :--- |
| *Official URL*:https://www.medizininformatik-initiative.de/fhir/modul-consent/StructureDefinition/mii-pr-consent-provenance | *Version*:2026.0.0 |
| Draft as of 2023-05-09 | *Computable Name*:MII_PR_Consent_Provenance |

 
Dieses Profil beschreibt Herkunftsinformationen zu Einwilligungen in der Medizininformatik-Initiative. 

**TODO:REVIEW (Gate C) — unreviewed machine translation.** The authoritative text of this module is German; this page is an unreviewed machine translation of the German intro note (source guide version 2026.0.0, harvested 2026-08-06). Where the two language variants differ, the German page applies.

Based on the [recommendations](https://ig.fhir.de/einwilligungsmanagement/stable/Provenance.html) of the AG Einwilligungsmanagement, the profile **MIIConsentProvenance** describes the provenance information of a consent document.

The Provenance resource links the consent content — signatures among other things — to the persons involved and to a document scan where one exists; see [UML Diagrams](uml-diagrams.md).

**Usages:**

* Examples for this Profile: [Provenance/55219d12-6245-4de4-8b50-ddf6f16a789b](Provenance-55219d12-6245-4de4-8b50-ddf6f16a789b.md)

You can also check for [usages in the FHIR IG Statistics](https://packages2.fhir.org/xig/resource/de.medizininformatikinitiative.kerndatensatz.consent|current/StructureDefinition/StructureDefinition-f675b1e8-9f3f-44e8-bb59-9681f78eb464.json)

### Formal Views of Profile Content

 [Description of Profiles, Differentials, Snapshots, and their representations](http://build.fhir.org/ig/FHIR/ig-guidance/readingIgs.html#structure-definitions). 

 

Other representations of profile: [CSV](../StructureDefinition-f675b1e8-9f3f-44e8-bb59-9681f78eb464.csv), [Excel](../StructureDefinition-f675b1e8-9f3f-44e8-bb59-9681f78eb464.xlsx), [Schematron](../StructureDefinition-f675b1e8-9f3f-44e8-bb59-9681f78eb464.sch) 

### Notes:

**TODO:REVIEW (Gate C) — unreviewed machine translation.** The authoritative text is the German notes file. Element paths and code values are identifiers and are reproduced verbatim.

**Only the differences from the [base profile](https://ig.fhir.de/einwilligungsmanagement/stable/Provenance.html) are explained below.**

| | |
| :--- | :--- |
| `Provenance.entity.what` | If a document scan is to be attached, the referenced resource has to be of profile type[DocumentReference](StructureDefinition-56375452-bfa1-4111-af7c-5b5ba9a1857c.md), must-support |
| `Provenance.entity.signature.type` | If a base64-encoded signature is to be attached, the kind of signature has to follow[MII_VS_Consent_SignatureTypes](ValueSet-88464c5b-5338-4c2b-9c07-b42fef2ada64.md), must-support |

### Example

* [Example (complete)](Provenance-55219d12-6245-4de4-8b50-ddf6f16a789b.md)

> **TODO:REVIEW (Gate B).** On the rendered source page, embedding exactly this example failed ("File not found"). The example does exist in the module and is rendered by this guide as its own artifact page — the migration therefore fixes a rendering failure of the source. Please confirm it is the same example the source intended to embed.



## Resource Content

```json
{
  "resourceType" : "StructureDefinition",
  "id" : "f675b1e8-9f3f-44e8-bb59-9681f78eb464",
  "url" : "https://www.medizininformatik-initiative.de/fhir/modul-consent/StructureDefinition/mii-pr-consent-provenance",
  "version" : "2026.0.0",
  "name" : "MII_PR_Consent_Provenance",
  "title" : "Profile - MI-I - Consent - Provenance",
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
  "description" : "Dieses Profil beschreibt Herkunftsinformationen zu Einwilligungen in der Medizininformatik-Initiative.",
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
    "identity" : "w3c.prov",
    "uri" : "http://www.w3.org/ns/prov",
    "name" : "W3C PROV"
  },
  {
    "identity" : "w5",
    "uri" : "http://hl7.org/fhir/fivews",
    "name" : "FiveWs Pattern Mapping"
  },
  {
    "identity" : "fhirauditevent",
    "uri" : "http://hl7.org/fhir/auditevent",
    "name" : "FHIR AuditEvent Mapping"
  }],
  "kind" : "resource",
  "abstract" : false,
  "type" : "Provenance",
  "baseDefinition" : "http://fhir.de/ConsentManagement/StructureDefinition/Provenance",
  "derivation" : "constraint",
  "differential" : {
    "element" : [{
      "id" : "Provenance",
      "path" : "Provenance"
    },
    {
      "id" : "Provenance.entity.what",
      "path" : "Provenance.entity.what",
      "type" : [{
        "code" : "Reference",
        "targetProfile" : ["https://www.medizininformatik-initiative.de/fhir/modul-consent/StructureDefinition/mii-pr-consent-documentreference"]
      }]
    },
    {
      "id" : "Provenance.signature.type",
      "path" : "Provenance.signature.type",
      "binding" : {
        "strength" : "required",
        "valueSet" : "https://www.medizininformatik-initiative.de/fhir/modul-consent/ValueSet/mii-vs-consent-signaturetypes"
      }
    }]
  }
}

```
