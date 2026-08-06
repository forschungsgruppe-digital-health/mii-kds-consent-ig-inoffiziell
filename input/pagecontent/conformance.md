<!-- markdownlint-disable MD041 -->
<!--
  MIGRATED NARRATIVE, MACHINE TRANSLATION. English is this IG's default
  language; the module's authored text is German. The German page of the
  same name under input/translations/de/pagecontent/ carries the source
  text and is authoritative until a human confirms this translation.
  Source: the Simplifier-rendered guide miiigmodulconsent, PUBLISHED
  version 2026.0.0 (Default, Read-only, Public, 2025-12-18), harvested
  2026-08-06 (mii-ig-migration, spec 5.1c + 5.1d). Source pages:
    https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung?version=2026.0.0
  TODO:REVIEW at Gate C (translation) and Gate B (narrative).
-->

### Technical implementation

This section describes the syntactic and semantic requirements for implementing
the Consent module.

Search parameters are also defined, which the respective systems must implement
when the FHIR RESTful API is used. In principle, logical AND and OR combinations
of search parameters are supported.

The foundations and further detail on searching and on the FHIR RESTful API were
being worked out in the base modules at the time this implementation guide was
written, and may be added or refined at a later point.

### Conformance pages of this guide

- **[General Requirements](general-requirements.html)** — use cases and scenarios.
- **[Must Support](must-support.html)** — handling of mandatory and Must-Support elements.
- **[Handling Missing Data](missing-data.html)**.
- **[Security and Privacy](security-and-privacy.html)** — data-protection aspects of the Consent resource.
