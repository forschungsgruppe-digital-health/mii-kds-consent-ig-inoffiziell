# Resource MII Implementation Guide Consent



## Resource Content

```json
{
  "resourceType" : "ImplementationGuide",
  "id" : "mii-ig-consent",
  "meta" : {
    "profile" : ["http://hl7.org/fhir/uv/crmi/StructureDefinition/crmi-shareableimplementationguide",
    "http://hl7.org/fhir/uv/crmi/StructureDefinition/crmi-publishableimplementationguide",
    "http://hl7.org/fhir/uv/crmi/StructureDefinition/crmi-implementationguide"]
  },
  "language" : "en",
  "extension" : [{
    "url" : "http://hl7.org/fhir/StructureDefinition/cqf-knowledgeCapability",
    "valueCode" : "shareable"
  },
  {
    "url" : "http://hl7.org/fhir/StructureDefinition/cqf-knowledgeCapability",
    "valueCode" : "publishable"
  },
  {
    "url" : "http://hl7.org/fhir/StructureDefinition/artifact-versionPolicy",
    "valueCodeableConcept" : {
      "coding" : [{
        "system" : "http://terminology.hl7.org/CodeSystem/artifact-version-policy-codes",
        "code" : "package",
        "display" : "Package"
      }]
    }
  },
  {
    "extension" : [{
      "url" : "packageId",
      "valueId" : "de.medizininformatikinitiative.kerndatensatz.consent"
    },
    {
      "url" : "version",
      "valueString" : "2026.0.1"
    },
    {
      "url" : "uri",
      "valueUri" : "https://www.medizininformatik-initiative.de/fhir/modul-consent"
    }],
    "url" : "http://hl7.org/fhir/StructureDefinition/package-source"
  },
  {
    "url" : "http://hl7.org/fhir/StructureDefinition/resource-effectivePeriod",
    "valuePeriod" : {
      "start" : "2026"
    }
  },
  {
    "url" : "http://hl7.org/fhir/StructureDefinition/artifact-author",
    "valueContactDetail" : {
      "telecom" : [{
        "system" : "email",
        "value" : "office@medizininformatik-initiative.de"
      }]
    }
  },
  {
    "url" : "http://hl7.org/fhir/StructureDefinition/artifact-editor",
    "valueContactDetail" : {
      "name" : "Taskforce Core Data Set"
    }
  },
  {
    "url" : "http://hl7.org/fhir/StructureDefinition/artifact-reviewer",
    "valueContactDetail" : {
      "name" : "Interoperability Working Group",
      "telecom" : [{
        "system" : "url",
        "value" : "https://www.medizininformatik-initiative.de/en/collaboration/interoperability-working-group"
      }]
    }
  },
  {
    "url" : "http://hl7.org/fhir/StructureDefinition/artifact-reviewer",
    "valueContactDetail" : {
      "name" : "National Steering Committee",
      "telecom" : [{
        "system" : "url",
        "value" : "https://www.medizininformatik-initiative.de/en/collaboration/national-steering-committee"
      }]
    }
  },
  {
    "url" : "http://hl7.org/fhir/StructureDefinition/artifact-endorser",
    "valueContactDetail" : {
      "name" : "Interoperability Working Group",
      "telecom" : [{
        "system" : "url",
        "value" : "https://www.medizininformatik-initiative.de/en/collaboration/interoperability-working-group"
      }]
    }
  },
  {
    "url" : "http://hl7.org/fhir/StructureDefinition/artifact-endorser",
    "valueContactDetail" : {
      "name" : "National Steering Committee",
      "telecom" : [{
        "system" : "url",
        "value" : "https://www.medizininformatik-initiative.de/en/collaboration/national-steering-committee"
      }]
    }
  },
  {
    "url" : "http://hl7.org/fhir/StructureDefinition/cqf-expansionParameters",
    "valueReference" : {
      "reference" : "Parameters/mii-param-consent-manifest"
    }
  },
  {
    "url" : "http://hl7.org/fhir/StructureDefinition/artifact-versionAlgorithm",
    "valueCoding" : {
      "system" : "http://hl7.org/fhir/version-algorithm",
      "code" : "semver"
    }
  },
  {
    "url" : "http://hl7.org/fhir/StructureDefinition/artifact-usage",
    "valueMarkdown" : "Use this ImplementationGuide resource as a computable definition of all the parts of the corresponding module of the Medical Informatics Initiative core data set."
  },
  {
    "url" : "http://hl7.org/fhir/StructureDefinition/artifact-purpose",
    "valueMarkdown" : "Provide the computable publication unit for the MII Core Dataset Consent module, enabling implementers to discover, validate, version, and apply the specification consistently."
  }],
  "url" : "https://www.medizininformatik-initiative.de/fhir/modul-consent/ImplementationGuide/mii-ig-consent",
  "version" : "2026.0.1",
  "name" : "MII_IG_Consent",
  "title" : "MII Implementation Guide Consent",
  "_title" : {
    "extension" : [{
      "extension" : [{
        "url" : "lang",
        "valueCode" : "de"
      },
      {
        "url" : "content",
        "valueString" : "MII Implementierungsleitfaden Consent"
      }],
      "url" : "http://hl7.org/fhir/StructureDefinition/translation"
    }]
  },
  "status" : "active",
  "experimental" : false,
  "date" : "2026-08-06",
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
  "description" : "Medizininformatik Initiative - Modul Consent - Implementation Guide",
  "jurisdiction" : [{
    "coding" : [{
      "system" : "urn:iso:std:iso:3166",
      "code" : "DE",
      "display" : "Germany"
    }]
  }],
  "packageId" : "de.medizininformatikinitiative.kerndatensatz.consent",
  "license" : "CC-BY-4.0",
  "fhirVersion" : ["4.0.1"],
  "dependsOn" : [{
    "id" : "hl7tx",
    "extension" : [{
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/implementationguide-dependency-comment",
      "valueMarkdown" : "Automatically added as a dependency - all IGs depend on HL7 Terminology"
    }],
    "uri" : "http://terminology.hl7.org/ImplementationGuide/hl7.terminology",
    "packageId" : "hl7.terminology.r4",
    "version" : "7.3.0"
  },
  {
    "id" : "hl7ext",
    "extension" : [{
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/implementationguide-dependency-comment",
      "valueMarkdown" : "Automatically added as a dependency - all IGs depend on the HL7 Extension Pack"
    }],
    "uri" : "http://hl7.org/fhir/extensions/ImplementationGuide/hl7.fhir.uv.extensions",
    "packageId" : "hl7.fhir.uv.extensions.r4",
    "version" : "5.3.0"
  },
  {
    "id" : "de_einwilligungsmanagement",
    "uri" : "http://fhir.org/packages/de.einwilligungsmanagement/ImplementationGuide/de.einwilligungsmanagement",
    "packageId" : "de.einwilligungsmanagement",
    "version" : "2.0.3-snapshots"
  },
  {
    "id" : "hl7_fhir_uv_crmi",
    "uri" : "http://hl7.org/fhir/uv/crmi/ImplementationGuide/hl7.fhir.uv.crmi",
    "packageId" : "hl7.fhir.uv.crmi",
    "version" : "2.0.0"
  }],
  "definition" : {
    "extension" : [{
      "extension" : [{
        "url" : "code",
        "valueString" : "copyrightyear"
      },
      {
        "url" : "value",
        "valueString" : "2019+"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "releaselabel"
      },
      {
        "url" : "value",
        "valueString" : "Release"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "i18n-default-lang"
      },
      {
        "url" : "value",
        "valueString" : "en"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "i18n-lang"
      },
      {
        "url" : "value",
        "valueString" : "de"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "translation-sources"
      },
      {
        "url" : "value",
        "valueString" : "input/translations/de"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "excludexml"
      },
      {
        "url" : "value",
        "valueString" : "false"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "excludejson"
      },
      {
        "url" : "value",
        "valueString" : "false"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "excludettl"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "excludemap"
      },
      {
        "url" : "value",
        "valueString" : "false"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "logging"
      },
      {
        "url" : "value",
        "valueString" : "init"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "logging"
      },
      {
        "url" : "value",
        "valueString" : "progress"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "logging"
      },
      {
        "url" : "value",
        "valueString" : "context"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "logging"
      },
      {
        "url" : "value",
        "valueString" : "html"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "logging"
      },
      {
        "url" : "value",
        "valueString" : "tx"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "pin-canonicals"
      },
      {
        "url" : "value",
        "valueString" : "pin-all"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "path-expansion-params"
      },
      {
        "url" : "value",
        "valueString" : "../../input/resources/Parameters-expansion-manifest.json"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "pin-manifest"
      },
      {
        "url" : "value",
        "valueString" : "mii-param-consent-manifest"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "suppress-mappings"
      },
      {
        "url" : "value",
        "valueString" : "http://hl7.org/v3"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "suppress-mappings"
      },
      {
        "url" : "value",
        "valueString" : "http://hl7.org/v3/cda"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "autoload-resources"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "path-liquid"
      },
      {
        "url" : "value",
        "valueString" : "template/liquid"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "path-liquid"
      },
      {
        "url" : "value",
        "valueString" : "input/liquid"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "path-qa"
      },
      {
        "url" : "value",
        "valueString" : "temp/qa"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "path-temp"
      },
      {
        "url" : "value",
        "valueString" : "temp/pages"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "path-output"
      },
      {
        "url" : "value",
        "valueString" : "output"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "path-suppressed-warnings"
      },
      {
        "url" : "value",
        "valueString" : "input/ignoreWarnings.txt"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "path-history"
      },
      {
        "url" : "value",
        "valueString" : "https://www.medizininformatik-initiative.de/fhir/modul-consent/history.html"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "template-html"
      },
      {
        "url" : "value",
        "valueString" : "template-page.html"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "template-md"
      },
      {
        "url" : "value",
        "valueString" : "template-page-md.html"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "apply-contact"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "apply-context"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "apply-copyright"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "apply-jurisdiction"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "apply-license"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "apply-publisher"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "apply-version"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "apply-wg"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "active-tables"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "fmm-definition"
      },
      {
        "url" : "value",
        "valueString" : "http://hl7.org/fhir/versions.html#maturity"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "propagate-status"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "excludelogbinaryformat"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "tabbed-snapshots"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "wantGen-ttl"
      },
      {
        "url" : "value",
        "valueString" : "false"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueString" : "wantGen-ttl-html"
      },
      {
        "url" : "value",
        "valueString" : "false"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/expansion-parameters",
      "valueReference" : {
        "reference" : "Parameters/expansion-parameters"
      }
    },
    {
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-internal-dependency",
      "valueCode" : "hl7.fhir.uv.tools.r4#1.1.2"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "copyrightyear"
      },
      {
        "url" : "value",
        "valueString" : "2019+"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "releaselabel"
      },
      {
        "url" : "value",
        "valueString" : "Release"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "i18n-default-lang"
      },
      {
        "url" : "value",
        "valueString" : "en"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "i18n-lang"
      },
      {
        "url" : "value",
        "valueString" : "de"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "translation-sources"
      },
      {
        "url" : "value",
        "valueString" : "input/translations/de"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "excludexml"
      },
      {
        "url" : "value",
        "valueString" : "false"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "excludejson"
      },
      {
        "url" : "value",
        "valueString" : "false"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "excludettl"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "excludemap"
      },
      {
        "url" : "value",
        "valueString" : "false"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "logging"
      },
      {
        "url" : "value",
        "valueString" : "init"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "logging"
      },
      {
        "url" : "value",
        "valueString" : "progress"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "logging"
      },
      {
        "url" : "value",
        "valueString" : "context"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "logging"
      },
      {
        "url" : "value",
        "valueString" : "html"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "logging"
      },
      {
        "url" : "value",
        "valueString" : "tx"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "pin-canonicals"
      },
      {
        "url" : "value",
        "valueString" : "pin-all"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "path-expansion-params"
      },
      {
        "url" : "value",
        "valueString" : "../../input/resources/Parameters-expansion-manifest.json"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "pin-manifest"
      },
      {
        "url" : "value",
        "valueString" : "mii-param-consent-manifest"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "suppress-mappings"
      },
      {
        "url" : "value",
        "valueString" : "http://hl7.org/v3"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "suppress-mappings"
      },
      {
        "url" : "value",
        "valueString" : "http://hl7.org/v3/cda"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "autoload-resources"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "path-liquid"
      },
      {
        "url" : "value",
        "valueString" : "template/liquid"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "path-liquid"
      },
      {
        "url" : "value",
        "valueString" : "input/liquid"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "path-qa"
      },
      {
        "url" : "value",
        "valueString" : "temp/qa"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "path-temp"
      },
      {
        "url" : "value",
        "valueString" : "temp/pages"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "path-output"
      },
      {
        "url" : "value",
        "valueString" : "output"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "path-suppressed-warnings"
      },
      {
        "url" : "value",
        "valueString" : "input/ignoreWarnings.txt"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "path-history"
      },
      {
        "url" : "value",
        "valueString" : "https://www.medizininformatik-initiative.de/fhir/modul-consent/history.html"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "template-html"
      },
      {
        "url" : "value",
        "valueString" : "template-page.html"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "template-md"
      },
      {
        "url" : "value",
        "valueString" : "template-page-md.html"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "apply-contact"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "apply-context"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "apply-copyright"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "apply-jurisdiction"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "apply-license"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "apply-publisher"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "apply-version"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "apply-wg"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "active-tables"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "fmm-definition"
      },
      {
        "url" : "value",
        "valueString" : "http://hl7.org/fhir/versions.html#maturity"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "propagate-status"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "excludelogbinaryformat"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "tabbed-snapshots"
      },
      {
        "url" : "value",
        "valueString" : "true"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "wantGen-ttl"
      },
      {
        "url" : "value",
        "valueString" : "false"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    },
    {
      "extension" : [{
        "url" : "code",
        "valueCode" : "wantGen-ttl-html"
      },
      {
        "url" : "value",
        "valueString" : "false"
      }],
      "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-parameter"
    }],
    "resource" : [{
      "extension" : [{
        "url" : "http://hl7.org/fhir/tools/StructureDefinition/resource-information",
        "valueString" : "Consent"
      },
      {
        "url" : "http://hl7.org/fhir/StructureDefinition/implementationguide-page",
        "valueUri" : "Consent-34150a23-b1c8-404f-874f-e042a30435d2.html"
      }],
      "reference" : {
        "reference" : "Consent/34150a23-b1c8-404f-874f-e042a30435d2"
      },
      "name" : "34150a23-b1c8-404f-874f-e042a30435d2",
      "exampleCanonical" : "https://www.medizininformatik-initiative.de/fhir/modul-consent/StructureDefinition/mii-pr-consent-einwilligung"
    },
    {
      "extension" : [{
        "url" : "http://hl7.org/fhir/tools/StructureDefinition/resource-information",
        "valueString" : "Consent"
      },
      {
        "url" : "http://hl7.org/fhir/StructureDefinition/implementationguide-page",
        "valueUri" : "Consent-5143266b-8d60-4b28-8ee9-635140ffa5bb.html"
      }],
      "reference" : {
        "reference" : "Consent/5143266b-8d60-4b28-8ee9-635140ffa5bb"
      },
      "name" : "5143266b-8d60-4b28-8ee9-635140ffa5bb",
      "exampleCanonical" : "https://www.medizininformatik-initiative.de/fhir/modul-consent/StructureDefinition/mii-pr-consent-einwilligung"
    },
    {
      "extension" : [{
        "url" : "http://hl7.org/fhir/tools/StructureDefinition/resource-information",
        "valueString" : "Provenance"
      },
      {
        "url" : "http://hl7.org/fhir/StructureDefinition/implementationguide-page",
        "valueUri" : "Provenance-55219d12-6245-4de4-8b50-ddf6f16a789b.html"
      }],
      "reference" : {
        "reference" : "Provenance/55219d12-6245-4de4-8b50-ddf6f16a789b"
      },
      "name" : "55219d12-6245-4de4-8b50-ddf6f16a789b",
      "exampleCanonical" : "https://www.medizininformatik-initiative.de/fhir/modul-consent/StructureDefinition/mii-pr-consent-provenance"
    },
    {
      "extension" : [{
        "url" : "http://hl7.org/fhir/tools/StructureDefinition/resource-information",
        "valueString" : "DocumentReference"
      },
      {
        "url" : "http://hl7.org/fhir/StructureDefinition/implementationguide-page",
        "valueUri" : "DocumentReference-8a3d1799-2463-405e-b49c-6a16c8692b01.html"
      }],
      "reference" : {
        "reference" : "DocumentReference/8a3d1799-2463-405e-b49c-6a16c8692b01"
      },
      "name" : "8a3d1799-2463-405e-b49c-6a16c8692b01",
      "exampleCanonical" : "https://www.medizininformatik-initiative.de/fhir/modul-consent/StructureDefinition/mii-pr-consent-documentreference"
    },
    {
      "extension" : [{
        "url" : "http://hl7.org/fhir/tools/StructureDefinition/resource-information",
        "valueString" : "Consent"
      },
      {
        "url" : "http://hl7.org/fhir/StructureDefinition/implementationguide-page",
        "valueUri" : "Consent-Example-MII-Consent-ResultType-document.html"
      }],
      "reference" : {
        "reference" : "Consent/Example-MII-Consent-ResultType-document"
      },
      "name" : "Example-MII-Consent-ResultType-document",
      "exampleCanonical" : "https://www.medizininformatik-initiative.de/fhir/modul-consent/StructureDefinition/mii-pr-consent-einwilligung"
    },
    {
      "extension" : [{
        "url" : "http://hl7.org/fhir/tools/StructureDefinition/resource-information",
        "valueString" : "CodeSystem"
      },
      {
        "url" : "http://hl7.org/fhir/StructureDefinition/implementationguide-page",
        "valueUri" : "CodeSystem-mii-cs-consent-version-modules.html"
      }],
      "reference" : {
        "reference" : "CodeSystem/mii-cs-consent-version-modules"
      },
      "name" : "MII Consent Version and Modules CodeSystem",
      "description" : "Dieses Code System enthält die OIDs der verschiedenen Versionen und Zusatzmodule des Broad Consent der Medizininformatik Initiative.",
      "exampleBoolean" : false
    },
    {
      "extension" : [{
        "url" : "http://hl7.org/fhir/tools/StructureDefinition/resource-information",
        "valueString" : "CodeSystem"
      },
      {
        "url" : "http://hl7.org/fhir/StructureDefinition/implementationguide-page",
        "valueUri" : "CodeSystem-2.16.840.1.113883.3.1937.777.24.5.2--20210423105554.html"
      }],
      "reference" : {
        "reference" : "CodeSystem/2.16.840.1.113883.3.1937.777.24.5.2--20210423105554"
      },
      "name" : "MII Consent: Answer CodeSystem",
      "description" : "This CodeSystem contains the possible answers to the questions of the MII Consent.",
      "exampleBoolean" : false
    },
    {
      "extension" : [{
        "url" : "http://hl7.org/fhir/tools/StructureDefinition/resource-information",
        "valueString" : "ValueSet"
      },
      {
        "url" : "http://hl7.org/fhir/StructureDefinition/implementationguide-page",
        "valueUri" : "ValueSet-2.16.840.1.113883.3.1937.777.24.11.30--20210323234509.html"
      }],
      "reference" : {
        "reference" : "ValueSet/2.16.840.1.113883.3.1937.777.24.11.30--20210323234509"
      },
      "name" : "MII Consent: Answer ValueSet",
      "description" : "This ValueSet contains the possible answers to the questions of the MII Consent.",
      "exampleBoolean" : false
    },
    {
      "extension" : [{
        "url" : "http://hl7.org/fhir/tools/StructureDefinition/resource-information",
        "valueString" : "CodeSystem"
      },
      {
        "url" : "http://hl7.org/fhir/StructureDefinition/implementationguide-page",
        "valueUri" : "CodeSystem-2.16.840.1.113883.3.1937.777.24.5.3--20251211153003.html"
      }],
      "reference" : {
        "reference" : "CodeSystem/2.16.840.1.113883.3.1937.777.24.5.3--20251211153003"
      },
      "name" : "MII Consent: Policy CodeSystem",
      "description" : "Codesystem mit Consent-Policy-Codes zur interoperablen Operationalisierung bzw. Durchsetzung (Enforcement) von Consent Informationen des MII Broad Consent",
      "exampleBoolean" : false
    },
    {
      "extension" : [{
        "url" : "http://hl7.org/fhir/tools/StructureDefinition/resource-information",
        "valueString" : "ValueSet"
      },
      {
        "url" : "http://hl7.org/fhir/StructureDefinition/implementationguide-page",
        "valueUri" : "ValueSet-2.16.840.1.113883.3.1937.777.24.11.36--20230331232804.html"
      }],
      "reference" : {
        "reference" : "ValueSet/2.16.840.1.113883.3.1937.777.24.11.36--20230331232804"
      },
      "name" : "MII Consent: Policy ValueSet",
      "description" : "\n**Disclaimer** \n\n (Punkte übernommen aus der Policy Liste ([MII SharePoint, TF Consent Umsetzung](https://tmfev.sharepoint.com/:f:/r/sites/tmf/mi-i/Taskforce%20Consent%20Umsetzung/02_Dokumente/Policies?csf=1&web=1&e=C0xLim \"\")))\n1. Diese Liste fasst erforderliche\n                    Einwilligungsmodule und zugeordnete Einwilligungspolicies für die technische Abbildung der \"MII Mustertexte Patienteneinwilligung\" in den aktuell verfügbaren Versionen zusammen. \n2. Für die Abbildung der Policies im Art Decor werden ausschließlich die Spalten [Policybezeichner], [Bedeutung/Kontext] und [OID] verwendet. \n3. Die Formulierung in\n                    der Spalte [Bedeutung/Kontext] dient ausschließlich administrativen Zwecken und der Verständnisbildung für die jeweilige Policy. \n4. Eine Darstellung der jeweiligen Formulierung innerhalb von Formularen oder digitalen Einwilligungsdokumenten ist nicht intendiert. \n5. Die Spalte [Weitere Hinweise Enforcement-Seite] nennt zusätzliche\n                    Randbedingungen, die auf der datenverarbeitenden Seite über die reine Einwilligungsinformation hinaus zu berücksichtigen sind. Die Gewährleistung der Einhaltung dieser weiteren Hinweise geht über den Wirkungsraum der Task Force Consent Umsetzung hinaus. \n\n **Hinweis 1 - Verwendung in FHIR:** Siehe [Implementation Guide](https://ig.fhir.de/einwilligungsmanagement/stable/Consent.html \"consent.provision Hierarchie ist noch in Arbeit\").  \n\n **Hinweis 2 - Verwendung in IHE BPPC:** \nUm die in diesem ValueSet enthaltenen Codes in IHE BPPC verwenden zu können, ist eine Kombination mit dem [MII Consent: Answer ValueSet](https://art-decor.org/art-decor/decor-valuesets--mide-?id=2.16.840.1.113883.3.1937.777.24.11.30&effectiveDate=2021-03-23T23:45:09&language=de-DE \"\") möglich (evtl. sogar erforderlich).  \n\n  Beispiel 1:  \n\n Patient hat dem Erheben der IDAT (Policy: 2.16.840.1.113883.3.1937.777.24.5.3.2 \"IDAT_erheben\") zugestimmt:\n                            2.16.840.1.113883.3.1937.777.24.5.3.2**.1** (.1 wird aus dem [MII Consent: Answer ValueSet](https://art-decor.org/art-decor/decor-valuesets--mide-?id=2.16.840.1.113883.3.1937.777.24.11.30&effectiveDate=2021-03-23T23:45:09&language=de-DE \"\") angehängt)  \n\n Beispiel 2:  \n\n 2.16.840.1.113883.3.1937.777.24.5.3.4.2\n                    bedeutet, dass der Patient der Policy IDAT_zusammenfuehren_Dritte nicht zugestimmt hat.",
      "exampleBoolean" : false
    },
    {
      "extension" : [{
        "url" : "http://hl7.org/fhir/tools/StructureDefinition/resource-information",
        "valueString" : "ValueSet"
      },
      {
        "url" : "http://hl7.org/fhir/StructureDefinition/implementationguide-page",
        "valueUri" : "ValueSet-88464c5b-5338-4c2b-9c07-b42fef2ada64.html"
      }],
      "reference" : {
        "reference" : "ValueSet/88464c5b-5338-4c2b-9c07-b42fef2ada64"
      },
      "name" : "MII Consent: Signature Types",
      "description" : "Dieses ValueSet enthält die zulässigen Werte für den Signaturtyp im Kontext des MI-I Consent.",
      "exampleBoolean" : false
    },
    {
      "extension" : [{
        "url" : "http://hl7.org/fhir/tools/StructureDefinition/resource-information",
        "valueString" : "Parameters"
      },
      {
        "url" : "http://hl7.org/fhir/StructureDefinition/implementationguide-page",
        "valueUri" : "Parameters-mii-param-consent-manifest.html"
      }],
      "reference" : {
        "reference" : "Parameters/mii-param-consent-manifest"
      },
      "name" : "mii-param-consent-manifest",
      "exampleBoolean" : false
    },
    {
      "extension" : [{
        "url" : "http://hl7.org/fhir/tools/StructureDefinition/resource-information",
        "valueString" : "SearchParameter"
      },
      {
        "url" : "http://hl7.org/fhir/StructureDefinition/implementationguide-page",
        "valueUri" : "SearchParameter-MII-SP-Consent-PolicyUri.html"
      }],
      "reference" : {
        "reference" : "SearchParameter/MII-SP-Consent-PolicyUri"
      },
      "name" : "MII-SP-Consent-PolicyUri",
      "description" : "Suche in der Policy URI (versionsspezifische Policy / Broad Consent)",
      "exampleBoolean" : false
    },
    {
      "extension" : [{
        "url" : "http://hl7.org/fhir/tools/StructureDefinition/resource-information",
        "valueString" : "SearchParameter"
      },
      {
        "url" : "http://hl7.org/fhir/StructureDefinition/implementationguide-page",
        "valueUri" : "SearchParameter-MII-SP-Consent-ProvisionCode.html"
      }],
      "reference" : {
        "reference" : "SearchParameter/MII-SP-Consent-ProvisionCode"
      },
      "name" : "MII-SP-Consent-ProvisionCode",
      "description" : "Suche im Code der Provison",
      "exampleBoolean" : false
    },
    {
      "extension" : [{
        "url" : "http://hl7.org/fhir/tools/StructureDefinition/resource-information",
        "valueString" : "SearchParameter"
      },
      {
        "url" : "http://hl7.org/fhir/StructureDefinition/implementationguide-page",
        "valueUri" : "SearchParameter-MII-SP-Consent-ProvisionCodePeriod.html"
      }],
      "reference" : {
        "reference" : "SearchParameter/MII-SP-Consent-ProvisionCodePeriod"
      },
      "name" : "MII-SP-Consent-ProvisionCodePeriod",
      "description" : "Composite-Suche nach Zeitraum (period) einer bestimmten, durch einen Code definierten, Provision.",
      "exampleBoolean" : false
    },
    {
      "extension" : [{
        "url" : "http://hl7.org/fhir/tools/StructureDefinition/resource-information",
        "valueString" : "SearchParameter"
      },
      {
        "url" : "http://hl7.org/fhir/StructureDefinition/implementationguide-page",
        "valueUri" : "SearchParameter-MII-SP-Consent-ProvisionCodeType.html"
      }],
      "reference" : {
        "reference" : "SearchParameter/MII-SP-Consent-ProvisionCodeType"
      },
      "name" : "MII-SP-Consent-ProvisionCodeType",
      "description" : "Composite-Suche nach Typ (type) einer bestimmten, durch einen Code definierten, Provision.",
      "exampleBoolean" : false
    },
    {
      "extension" : [{
        "url" : "http://hl7.org/fhir/tools/StructureDefinition/resource-information",
        "valueString" : "SearchParameter"
      },
      {
        "url" : "http://hl7.org/fhir/StructureDefinition/implementationguide-page",
        "valueUri" : "SearchParameter-MII-SP-Consent-ProvisionPeriod.html"
      }],
      "reference" : {
        "reference" : "SearchParameter/MII-SP-Consent-ProvisionPeriod"
      },
      "name" : "MII-SP-Consent-ProvisionPeriod",
      "description" : "Suche im Zeitraum der Provision. Dieser Suchparameter bezieht sich explizit auf die zweite Verschachtelungsebene von provison.",
      "exampleBoolean" : false
    },
    {
      "extension" : [{
        "url" : "http://hl7.org/fhir/tools/StructureDefinition/resource-information",
        "valueString" : "SearchParameter"
      },
      {
        "url" : "http://hl7.org/fhir/StructureDefinition/implementationguide-page",
        "valueUri" : "SearchParameter-MII-SP-Consent-ProvisionType.html"
      }],
      "reference" : {
        "reference" : "SearchParameter/MII-SP-Consent-ProvisionType"
      },
      "name" : "MII-SP-Consent-ProvisionType",
      "description" : "Suche im Typ der Provison (permit, deny).",
      "exampleBoolean" : false
    },
    {
      "extension" : [{
        "url" : "http://hl7.org/fhir/tools/StructureDefinition/resource-information",
        "valueString" : "StructureDefinition:resource"
      },
      {
        "url" : "http://hl7.org/fhir/StructureDefinition/implementationguide-page",
        "valueUri" : "StructureDefinition-56375452-bfa1-4111-af7c-5b5ba9a1857c.html"
      }],
      "reference" : {
        "reference" : "StructureDefinition/56375452-bfa1-4111-af7c-5b5ba9a1857c"
      },
      "name" : "Profile - MI-I - Consent - DocumentReference",
      "description" : "Dieses Profil beschreibt die Abbildung von Originaldokumenten zu Einwilligungen in der Medizininformatik-Initiative.\nDiese müssen im PDF-Format vorliegen.",
      "exampleBoolean" : false
    },
    {
      "extension" : [{
        "url" : "http://hl7.org/fhir/tools/StructureDefinition/resource-information",
        "valueString" : "StructureDefinition:resource"
      },
      {
        "url" : "http://hl7.org/fhir/StructureDefinition/implementationguide-page",
        "valueUri" : "StructureDefinition-e0e166b4-0f77-478d-9062-de0034d98ce0.html"
      }],
      "reference" : {
        "reference" : "StructureDefinition/e0e166b4-0f77-478d-9062-de0034d98ce0"
      },
      "name" : "Profile - MI-I - Consent - Einwilligung",
      "description" : "Dieses Profil beschreibt eine Einwilligung in der Medizininformatik-Initiative.",
      "exampleBoolean" : false
    },
    {
      "extension" : [{
        "url" : "http://hl7.org/fhir/tools/StructureDefinition/resource-information",
        "valueString" : "StructureDefinition:resource"
      },
      {
        "url" : "http://hl7.org/fhir/StructureDefinition/implementationguide-page",
        "valueUri" : "StructureDefinition-f675b1e8-9f3f-44e8-bb59-9681f78eb464.html"
      }],
      "reference" : {
        "reference" : "StructureDefinition/f675b1e8-9f3f-44e8-bb59-9681f78eb464"
      },
      "name" : "Profile - MI-I - Consent - Provenance",
      "description" : "Dieses Profil beschreibt Herkunftsinformationen zu Einwilligungen in der Medizininformatik-Initiative.",
      "exampleBoolean" : false
    }],
    "page" : {
      "extension" : [{
        "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-page-name",
        "valueUrl" : "toc.html"
      }],
      "nameUrl" : "toc.html",
      "title" : "Table of Contents",
      "_title" : {
        "extension" : [{
          "extension" : [{
            "url" : "lang",
            "valueCode" : "de"
          },
          {
            "url" : "content",
            "valueString" : "Inhaltsverzeichnis"
          }],
          "url" : "http://hl7.org/fhir/StructureDefinition/translation"
        }]
      },
      "generation" : "html",
      "page" : [{
        "extension" : [{
          "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-page-name",
          "valueUrl" : "index.html"
        }],
        "nameUrl" : "index.html",
        "title" : "Home",
        "_title" : {
          "extension" : [{
            "extension" : [{
              "url" : "lang",
              "valueCode" : "de"
            },
            {
              "url" : "content",
              "valueString" : "Startseite"
            }],
            "url" : "http://hl7.org/fhir/StructureDefinition/translation"
          }]
        },
        "generation" : "markdown"
      },
      {
        "extension" : [{
          "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-page-name",
          "valueUrl" : "guidance.html"
        }],
        "nameUrl" : "guidance.html",
        "title" : "Guidance",
        "_title" : {
          "extension" : [{
            "extension" : [{
              "url" : "lang",
              "valueCode" : "de"
            },
            {
              "url" : "content",
              "valueString" : "Anleitung"
            }],
            "url" : "http://hl7.org/fhir/StructureDefinition/translation"
          }]
        },
        "generation" : "markdown",
        "page" : [{
          "extension" : [{
            "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-page-name",
            "valueUrl" : "researcher-guidance.html"
          }],
          "nameUrl" : "researcher-guidance.html",
          "title" : "Guidance for Researchers",
          "_title" : {
            "extension" : [{
              "extension" : [{
                "url" : "lang",
                "valueCode" : "de"
              },
              {
                "url" : "content",
                "valueString" : "Anleitung für Forschende"
              }],
              "url" : "http://hl7.org/fhir/StructureDefinition/translation"
            }]
          },
          "generation" : "markdown"
        },
        {
          "extension" : [{
            "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-page-name",
            "valueUrl" : "implementer-guidance.html"
          }],
          "nameUrl" : "implementer-guidance.html",
          "title" : "Guidance for Implementers",
          "_title" : {
            "extension" : [{
              "extension" : [{
                "url" : "lang",
                "valueCode" : "de"
              },
              {
                "url" : "content",
                "valueString" : "Anleitung für Implementierende"
              }],
              "url" : "http://hl7.org/fhir/StructureDefinition/translation"
            }]
          },
          "generation" : "markdown"
        },
        {
          "extension" : [{
            "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-page-name",
            "valueUrl" : "datasets-and-descriptions.html"
          }],
          "nameUrl" : "datasets-and-descriptions.html",
          "title" : "Datasets and Descriptions",
          "_title" : {
            "extension" : [{
              "extension" : [{
                "url" : "lang",
                "valueCode" : "de"
              },
              {
                "url" : "content",
                "valueString" : "Datensätze und Beschreibungen"
              }],
              "url" : "http://hl7.org/fhir/StructureDefinition/translation"
            }]
          },
          "generation" : "markdown"
        },
        {
          "extension" : [{
            "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-page-name",
            "valueUrl" : "uml-diagrams.html"
          }],
          "nameUrl" : "uml-diagrams.html",
          "title" : "UML Diagrams",
          "_title" : {
            "extension" : [{
              "extension" : [{
                "url" : "lang",
                "valueCode" : "de"
              },
              {
                "url" : "content",
                "valueString" : "UML-Diagramme"
              }],
              "url" : "http://hl7.org/fhir/StructureDefinition/translation"
            }]
          },
          "generation" : "markdown"
        }]
      },
      {
        "extension" : [{
          "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-page-name",
          "valueUrl" : "conformance.html"
        }],
        "nameUrl" : "conformance.html",
        "title" : "Conformance",
        "_title" : {
          "extension" : [{
            "extension" : [{
              "url" : "lang",
              "valueCode" : "de"
            },
            {
              "url" : "content",
              "valueString" : "Konformität"
            }],
            "url" : "http://hl7.org/fhir/StructureDefinition/translation"
          }]
        },
        "generation" : "markdown",
        "page" : [{
          "extension" : [{
            "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-page-name",
            "valueUrl" : "general-requirements.html"
          }],
          "nameUrl" : "general-requirements.html",
          "title" : "General Requirements",
          "_title" : {
            "extension" : [{
              "extension" : [{
                "url" : "lang",
                "valueCode" : "de"
              },
              {
                "url" : "content",
                "valueString" : "Allgemeine Anforderungen"
              }],
              "url" : "http://hl7.org/fhir/StructureDefinition/translation"
            }]
          },
          "generation" : "markdown"
        },
        {
          "extension" : [{
            "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-page-name",
            "valueUrl" : "must-support.html"
          }],
          "nameUrl" : "must-support.html",
          "title" : "Must Support",
          "_title" : {
            "extension" : [{
              "extension" : [{
                "url" : "lang",
                "valueCode" : "de"
              },
              {
                "url" : "content",
                "valueString" : "Must-Support"
              }],
              "url" : "http://hl7.org/fhir/StructureDefinition/translation"
            }]
          },
          "generation" : "markdown"
        },
        {
          "extension" : [{
            "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-page-name",
            "valueUrl" : "missing-data.html"
          }],
          "nameUrl" : "missing-data.html",
          "title" : "Handling Missing Data",
          "_title" : {
            "extension" : [{
              "extension" : [{
                "url" : "lang",
                "valueCode" : "de"
              },
              {
                "url" : "content",
                "valueString" : "Umgang mit fehlenden Daten"
              }],
              "url" : "http://hl7.org/fhir/StructureDefinition/translation"
            }]
          },
          "generation" : "markdown"
        },
        {
          "extension" : [{
            "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-page-name",
            "valueUrl" : "security-and-privacy.html"
          }],
          "nameUrl" : "security-and-privacy.html",
          "title" : "Security and Privacy",
          "_title" : {
            "extension" : [{
              "extension" : [{
                "url" : "lang",
                "valueCode" : "de"
              },
              {
                "url" : "content",
                "valueString" : "Sicherheit und Datenschutz"
              }],
              "url" : "http://hl7.org/fhir/StructureDefinition/translation"
            }]
          },
          "generation" : "markdown"
        }]
      },
      {
        "extension" : [{
          "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-page-name",
          "valueUrl" : "profiles-and-extensions.html"
        }],
        "nameUrl" : "profiles-and-extensions.html",
        "title" : "Profiles and Extensions",
        "_title" : {
          "extension" : [{
            "extension" : [{
              "url" : "lang",
              "valueCode" : "de"
            },
            {
              "url" : "content",
              "valueString" : "Profile und Extensions"
            }],
            "url" : "http://hl7.org/fhir/StructureDefinition/translation"
          }]
        },
        "generation" : "markdown"
      },
      {
        "extension" : [{
          "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-page-name",
          "valueUrl" : "search-parameters-and-operations.html"
        }],
        "nameUrl" : "search-parameters-and-operations.html",
        "title" : "Search Parameters and Operations",
        "_title" : {
          "extension" : [{
            "extension" : [{
              "url" : "lang",
              "valueCode" : "de"
            },
            {
              "url" : "content",
              "valueString" : "Suchparameter und Operationen"
            }],
            "url" : "http://hl7.org/fhir/StructureDefinition/translation"
          }]
        },
        "generation" : "markdown"
      },
      {
        "extension" : [{
          "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-page-name",
          "valueUrl" : "terminology.html"
        }],
        "nameUrl" : "terminology.html",
        "title" : "Terminology",
        "_title" : {
          "extension" : [{
            "extension" : [{
              "url" : "lang",
              "valueCode" : "de"
            },
            {
              "url" : "content",
              "valueString" : "Terminologie"
            }],
            "url" : "http://hl7.org/fhir/StructureDefinition/translation"
          }]
        },
        "generation" : "markdown"
      },
      {
        "extension" : [{
          "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-page-name",
          "valueUrl" : "capability-statements.html"
        }],
        "nameUrl" : "capability-statements.html",
        "title" : "Capability Statements",
        "_title" : {
          "extension" : [{
            "extension" : [{
              "url" : "lang",
              "valueCode" : "de"
            },
            {
              "url" : "content",
              "valueString" : "CapabilityStatements"
            }],
            "url" : "http://hl7.org/fhir/StructureDefinition/translation"
          }]
        },
        "generation" : "markdown"
      },
      {
        "extension" : [{
          "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-page-name",
          "valueUrl" : "logical-models.html"
        }],
        "nameUrl" : "logical-models.html",
        "title" : "Logical Models",
        "_title" : {
          "extension" : [{
            "extension" : [{
              "url" : "lang",
              "valueCode" : "de"
            },
            {
              "url" : "content",
              "valueString" : "Logische Modelle"
            }],
            "url" : "http://hl7.org/fhir/StructureDefinition/translation"
          }]
        },
        "generation" : "markdown"
      },
      {
        "extension" : [{
          "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-page-name",
          "valueUrl" : "examples.html"
        }],
        "nameUrl" : "examples.html",
        "title" : "Examples",
        "_title" : {
          "extension" : [{
            "extension" : [{
              "url" : "lang",
              "valueCode" : "de"
            },
            {
              "url" : "content",
              "valueString" : "Beispiele"
            }],
            "url" : "http://hl7.org/fhir/StructureDefinition/translation"
          }]
        },
        "generation" : "markdown"
      },
      {
        "extension" : [{
          "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-page-name",
          "valueUrl" : "downloads.html"
        }],
        "nameUrl" : "downloads.html",
        "title" : "Downloads",
        "_title" : {
          "extension" : [{
            "extension" : [{
              "url" : "lang",
              "valueCode" : "de"
            },
            {
              "url" : "content",
              "valueString" : "Downloads"
            }],
            "url" : "http://hl7.org/fhir/StructureDefinition/translation"
          }]
        },
        "generation" : "markdown"
      },
      {
        "extension" : [{
          "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-page-name",
          "valueUrl" : "version-history.html"
        }],
        "nameUrl" : "version-history.html",
        "title" : "Versioning",
        "_title" : {
          "extension" : [{
            "extension" : [{
              "url" : "lang",
              "valueCode" : "de"
            },
            {
              "url" : "content",
              "valueString" : "Versionierung"
            }],
            "url" : "http://hl7.org/fhir/StructureDefinition/translation"
          }]
        },
        "generation" : "markdown",
        "page" : [{
          "extension" : [{
            "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-page-name",
            "valueUrl" : "changes.html"
          }],
          "nameUrl" : "changes.html",
          "title" : "Changelog",
          "_title" : {
            "extension" : [{
              "extension" : [{
                "url" : "lang",
                "valueCode" : "de"
              },
              {
                "url" : "content",
                "valueString" : "Änderungshistorie"
              }],
              "url" : "http://hl7.org/fhir/StructureDefinition/translation"
            }]
          },
          "generation" : "markdown"
        }]
      },
      {
        "extension" : [{
          "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-page-name",
          "valueUrl" : "translationinfo.html"
        }],
        "nameUrl" : "translationinfo.html",
        "title" : "Translation Information",
        "_title" : {
          "extension" : [{
            "extension" : [{
              "url" : "lang",
              "valueCode" : "de"
            },
            {
              "url" : "content",
              "valueString" : "Hinweise zur Übersetzung"
            }],
            "url" : "http://hl7.org/fhir/StructureDefinition/translation"
          }]
        },
        "generation" : "markdown"
      },
      {
        "extension" : [{
          "url" : "http://hl7.org/fhir/tools/StructureDefinition/ig-page-name",
          "valueUrl" : "metadata.html"
        }],
        "nameUrl" : "metadata.html",
        "title" : "Metadata Overview",
        "_title" : {
          "extension" : [{
            "extension" : [{
              "url" : "lang",
              "valueCode" : "de"
            },
            {
              "url" : "content",
              "valueString" : "Metadaten"
            }],
            "url" : "http://hl7.org/fhir/StructureDefinition/translation"
          }]
        },
        "generation" : "markdown"
      }]
    },
    "parameter" : [{
      "code" : "path-resource",
      "value" : "input/predefined-resources"
    },
    {
      "code" : "path-pages",
      "value" : "input/intro-notes"
    },
    {
      "code" : "path-resource",
      "value" : "input/capabilities"
    },
    {
      "code" : "path-resource",
      "value" : "input/examples"
    },
    {
      "code" : "path-resource",
      "value" : "input/extensions"
    },
    {
      "code" : "path-resource",
      "value" : "input/models"
    },
    {
      "code" : "path-resource",
      "value" : "input/operations"
    },
    {
      "code" : "path-resource",
      "value" : "input/profiles"
    },
    {
      "code" : "path-resource",
      "value" : "input/resources"
    },
    {
      "code" : "path-resource",
      "value" : "input/vocabulary"
    },
    {
      "code" : "path-resource",
      "value" : "input/testing"
    },
    {
      "code" : "path-resource",
      "value" : "input/history"
    },
    {
      "code" : "path-resource",
      "value" : "fsh-generated/resources"
    },
    {
      "code" : "path-pages",
      "value" : "template/config"
    },
    {
      "code" : "path-pages",
      "value" : "input/images"
    },
    {
      "code" : "path-tx-cache",
      "value" : "input-cache/txcache"
    }]
  }
}

```
