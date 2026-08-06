<!-- markdownlint-disable MD041 -->
<!--
  MIGRATED NARRATIVE, MACHINE TRANSLATION. English is this IG's default
  language; the module's authored text is German. The German page of the
  same name under input/translations/de/pagecontent/ carries the source
  text and is authoritative until a human confirms this translation.
  Source: the Simplifier-rendered guide miiigmodulconsent, PUBLISHED
  version 2026.0.0 (Default, Read-only, Public, 2025-12-18), harvested
  2026-08-06 (mii-ig-migration, spec 5.1c + 5.1d). Source pages:
    https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile?version=2026.0.0
    https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/WeitererelevanteProfile?version=2026.0.0
  TODO:REVIEW at Gate C (translation) and Gate B (narrative).
-->

### FHIR profiles of this module

The core-dataset specifications build, where possible, on international standards
and terminologies — in particular on the profiling work of the
[AG Einwilligungsmanagement on consent management](https://ig.fhir.de/einwilligungsmanagement/stable/).

All core-dataset elements, adapted to the details and requirements of the Medical
Informatics Initiative's use cases, are described below as FHIR
StructureDefinitions.

The profile-specific description is on **the artifact page of the profile
itself** (`input/intro-notes/`, spec 9), not here:

| Profile | Canonical |
| --- | --- |
| MII\_PR\_Consent\_Einwilligung | `https://www.medizininformatik-initiative.de/fhir/modul-consent/StructureDefinition/mii-pr-consent-einwilligung` |
| MII\_PR\_Consent\_Provenance | `https://www.medizininformatik-initiative.de/fhir/modul-consent/StructureDefinition/mii-pr-consent-provenance` |
| MII\_PR\_Consent\_DocumentReference | `https://www.medizininformatik-initiative.de/fhir/modul-consent/StructureDefinition/mii-pr-consent-documentreference` |

The module's search parameters are described on
[Search Parameters and Operations](search-parameters-and-operations.html).

### Further relevant profiles

Besides Consent, Provenance and DocumentReference, further profiles of the AG
Einwilligungsmanagement are relevant. The following profiles **must** be
supported in order to use this guide:

> The table below is carried over **verbatim** from the German source page:
> its cells are terminology (codes and the displays the code system publishes),
> and translating a published display would falsify the terminology.
{: .mii-highlight .mii-highlight-grey}

| FHIR-Profil | Zur Abbildung von / Verwendung für |

Where the Broad Consent is represented or queried by means of FHIR
Questionnaires, the following profiles should be used in addition:

| --- | --- |
