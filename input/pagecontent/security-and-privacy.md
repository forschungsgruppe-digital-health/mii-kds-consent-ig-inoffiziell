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

### Data protection

Because the FHIR Consent resource likewise carries **no person-identifying
information** about the consenting person, the
[**pseudonymous reference to the person**](https://ig.fhir.de/einwilligungsmanagement/stable/Patient.html)
should be used.

*Technically, Patient resources and derived profiles — for example the profiles of the
[AG Einwilligungsmanagement](https://ig.fhir.de/einwilligungsmanagement/stable/Patient.html) —
can carry identifying data. In the context of the MII Consent module they must not.*

The FHIR Consent resource contains **no document scans and/or signatures**. Where a
transmission is required for a given use case, separate resources are used for it.

> [TODO:REVIEW — Gate B/C. This page is the *Datenschutz-Aspekte* section of the
> guide's Consent profile page, routed here per spec 9 (sections within the fixed
> page set, never a page of their own). The template's original starter content
> for this page was replaced.]
{: .mii-highlight .mii-highlight-grey}
