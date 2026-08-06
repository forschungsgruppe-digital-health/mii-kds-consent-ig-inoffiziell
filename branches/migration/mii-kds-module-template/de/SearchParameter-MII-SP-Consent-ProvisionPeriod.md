# MII-SP-Consent-ProvisionPeriod - MII Implementation Guide Consent v2026.0.1

* [**Inhaltsverzeichnis**](toc.md)
* [**Artefaktübersicht**](artifacts.md)
* **MII-SP-Consent-ProvisionPeriod**

## SearchParameter: MII-SP-Consent-ProvisionPeriod 

| | |
| :--- | :--- |
| *Offizielle URL*:https://www.medizininformatik-initiative.de/fhir/modul-consent/SearchParameter/mii-sp-consent-provisionperiod | *Version*:2026.0.1 |
| Active Stand: 2023-05-09 | *Maschinenlesbarer Name*:MII_SP_Consent_ProvisionPeriod |

 
Suche im Zeitraum der Provision. Dieser Suchparameter bezieht sich explizit auf die zweite Verschachtelungsebene von provison. 



## Resource Content

```json
{
  "resourceType" : "SearchParameter",
  "id" : "MII-SP-Consent-ProvisionPeriod",
  "url" : "https://www.medizininformatik-initiative.de/fhir/modul-consent/SearchParameter/mii-sp-consent-provisionperiod",
  "version" : "2026.0.1",
  "name" : "MII_SP_Consent_ProvisionPeriod",
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
  "description" : "Suche im Zeitraum der Provision. Dieser Suchparameter bezieht sich explizit auf die zweite Verschachtelungsebene von provison.",
  "jurisdiction" : [{
    "coding" : [{
      "system" : "urn:iso:std:iso:3166",
      "code" : "DE",
      "display" : "Germany"
    }]
  }],
  "code" : "mii-provision-provision-period",
  "base" : ["Consent"],
  "type" : "date",
  "expression" : "Consent.provision.provision.period",
  "multipleOr" : true,
  "multipleAnd" : true
}

```
