# MII-SP-Consent-ProvisionCode - MII Implementation Guide Consent v2026.0.1

* [**Table of Contents**](toc.md)
* [**Artifacts Summary**](artifacts.md)
* **MII-SP-Consent-ProvisionCode**

## SearchParameter: MII-SP-Consent-ProvisionCode 

| | |
| :--- | :--- |
| *Official URL*:https://www.medizininformatik-initiative.de/fhir/modul-consent/SearchParameter/mii-sp-consent-provisioncode | *Version*:2026.0.1 |
| Active as of 2023-05-09 | *Computable Name*:MII_SP_Consent_ProvisionCode |

 
Suche im Code der Provison 



## Resource Content

```json
{
  "resourceType" : "SearchParameter",
  "id" : "MII-SP-Consent-ProvisionCode",
  "url" : "https://www.medizininformatik-initiative.de/fhir/modul-consent/SearchParameter/mii-sp-consent-provisioncode",
  "version" : "2026.0.1",
  "name" : "MII_SP_Consent_ProvisionCode",
  "status" : "active",
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
  "description" : "Suche im Code der Provison",
  "jurisdiction" : [{
    "coding" : [{
      "system" : "urn:iso:std:iso:3166",
      "code" : "DE",
      "display" : "Germany"
    }]
  }],
  "code" : "mii-provision-provision-code",
  "base" : ["Consent"],
  "type" : "token",
  "expression" : "Consent.provision.provision.code",
  "multipleOr" : true,
  "multipleAnd" : true
}

```
