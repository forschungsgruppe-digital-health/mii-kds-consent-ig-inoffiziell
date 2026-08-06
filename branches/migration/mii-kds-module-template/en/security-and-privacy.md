# Security and Privacy - MII Implementation Guide Consent v2026.0.1

* [**Table of Contents**](toc.md)
* [**Conformance**](conformance.md)
* **Security and Privacy**

## Security and Privacy

### Data protection

Because the FHIR Consent resource likewise carries **no person-identifying information** about the consenting person, the [**pseudonymous reference to the person**](https://ig.fhir.de/einwilligungsmanagement/stable/Patient.html) should be used.

**Technically, Patient resources and derived profiles — for example the profiles of the [AG Einwilligungsmanagement](https://ig.fhir.de/einwilligungsmanagement/stable/Patient.html) — can carry identifying data. In the context of the MII Consent module they must not.**

The FHIR Consent resource contains **no document scans and/or signatures**. Where a transmission is required for a given use case, separate resources are used for it.

> [TODO:REVIEW — Gate B/C. This page is the **Datenschutz-Aspekte** section of the guide's Consent profile page, routed here per spec 9 (sections within the fixed page set, never a page of their own). The template's original starter content for this page was replaced.]

