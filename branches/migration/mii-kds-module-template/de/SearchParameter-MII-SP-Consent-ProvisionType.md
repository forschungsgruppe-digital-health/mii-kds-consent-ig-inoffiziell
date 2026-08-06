# MII-SP-Consent-ProvisionType - MII Implementation Guide Consent v2026.0.1

* [**Inhaltsverzeichnis**](toc.md)
* [**Artefaktübersicht**](artifacts.md)
* **MII-SP-Consent-ProvisionType**

## SearchParameter: MII-SP-Consent-ProvisionType 

| | |
| :--- | :--- |
| *Offizielle URL*:https://www.medizininformatik-initiative.de/fhir/modul-consent/SearchParameter/mii-sp-consent-provisiontype | *Version*:2026.0.1 |
| Active Stand: 2023-05-09 | *Maschinenlesbarer Name*:MII_SP_Consent_ProvisionType |

 
Suche im Typ der Provison (permit, deny). 



## Resource Content

```json
{
  "resourceType" : "SearchParameter",
  "id" : "MII-SP-Consent-ProvisionType",
  "url" : "https://www.medizininformatik-initiative.de/fhir/modul-consent/SearchParameter/mii-sp-consent-provisiontype",
  "version" : "2026.0.1",
  "name" : "MII_SP_Consent_ProvisionType",
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
  "description" : "Suche im Typ der Provison (permit, deny).",
  "jurisdiction" : [{
    "coding" : [{
      "system" : "urn:iso:std:iso:3166",
      "code" : "DE",
      "display" : "Germany"
    }]
  }],
  "code" : "mii-provision-provision-type",
  "base" : ["Consent"],
  "type" : "token",
  "expression" : "Consent.provision.provision.type",
  "multipleOr" : true,
  "multipleAnd" : true
}

```
