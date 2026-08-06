# MII-SP-Consent-ProvisionCodePeriod - MII Implementation Guide Consent v2026.0.0

* [**Table of Contents**](toc.md)
* [**Artifacts Summary**](artifacts.md)
* **MII-SP-Consent-ProvisionCodePeriod**

## SearchParameter: MII-SP-Consent-ProvisionCodePeriod 

| | |
| :--- | :--- |
| *Official URL*:https://www.medizininformatik-initiative.de/fhir/modul-consent/SearchParameter/mii-sp-consent-provisioncodeperiod | *Version*:2026.0.0 |
| Active as of 2023-05-09 | *Computable Name*:MII_SP_Consent_ProvisionCodePeriod |

 
Composite-Suche nach Zeitraum (period) einer bestimmten, durch einen Code definierten, Provision. 



## Resource Content

```json
{
  "resourceType" : "SearchParameter",
  "id" : "MII-SP-Consent-ProvisionCodePeriod",
  "url" : "https://www.medizininformatik-initiative.de/fhir/modul-consent/SearchParameter/mii-sp-consent-provisioncodeperiod",
  "version" : "2026.0.0",
  "name" : "MII_SP_Consent_ProvisionCodePeriod",
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
  "description" : "Composite-Suche nach Zeitraum (period) einer bestimmten, durch einen Code definierten, Provision.",
  "jurisdiction" : [{
    "coding" : [{
      "system" : "urn:iso:std:iso:3166",
      "code" : "DE",
      "display" : "Germany"
    }]
  }],
  "code" : "mii-provision-provision-code-period",
  "base" : ["Consent"],
  "type" : "composite",
  "expression" : "Consent.provision.provision",
  "component" : [{
    "definition" : "https://www.medizininformatik-initiative.de/fhir/modul-consent/SearchParameter/mii-sp-consent-provisioncode",
    "expression" : "code"
  },
  {
    "definition" : "https://www.medizininformatik-initiative.de/fhir/modul-consent/SearchParameter/mii-sp-consent-provisionperiod",
    "expression" : "period"
  }]
}

```
