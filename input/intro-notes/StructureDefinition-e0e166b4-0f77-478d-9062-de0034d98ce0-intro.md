<!-- markdownlint-disable MD041 -->
<!--
  MIGRATED NARRATIVE, MACHINE TRANSLATION. English is this IG's default
  language; the module's authored text is German. The German page of the
  same name under input/translations/de/pagecontent/ carries the source
  text and is authoritative until a human confirms this translation.
  Source: the Simplifier-rendered guide miiigmodulconsent, PUBLISHED
  version 2026.0.0 (Default, Read-only, Public, 2025-12-18), harvested
  2026-08-06 (mii-ig-migration, spec 5.1c + 5.1d). Source pages:
    https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/Consent?version=2026.0.0
  TODO:REVIEW at Gate C (translation) and Gate B (narrative).
-->

This profile describes an operationalized, automatically produced and processable
consent within the Medical Informatics Initiative.

When a person is enrolled in a study (including an MII use case), a consent is
created for that person on the basis of the
[MII Broad Consent model texts](https://www.medizininformatik-initiative.de/de/mustertext-zur-patienteneinwilligung).
The FHIR Consent resource is then generated automatically from those consent
documents.

The resource must be created before the person takes part in cross-site
feasibility enquiries and data releases.

#### Interoperability

To ensure that the operationalized consent content can be exchanged beyond FHIR
as well, a uniform policy code system was agreed with the **MII AG Consent**.

*Using this code system is mandatory for the KDS Consent module.*

Data-protection aspects of this profile are on
[Security and Privacy](security-and-privacy.html).
