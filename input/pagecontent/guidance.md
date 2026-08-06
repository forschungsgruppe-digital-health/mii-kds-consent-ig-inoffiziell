<!-- markdownlint-disable MD041 -->
<!-- Source: kerndatensatz-basis input/pagecontent/guidance.md (MII module page set).
     "Guidance" overview page. Replace the [TODO] prompts; the sub-page structure
     follows kerndatensatz-basis. German mirror:
     input/translations/de/pagecontent/guidance.md — keep both in step. -->

This section collects the domain guidance for implementing and using the
**Consent** module.

### General Implementation Guidance

* **[Datasets and Descriptions](datasets-and-descriptions.html)** — detailed
  description of the module's data elements / logical models.
* **[UML Diagrams](uml-diagrams.html)** — visual representation of the data
  models and their relationships.

### Audience-Specific Guidance

* **[Guidance for Researchers](researcher-guidance.html)** — for researchers
  using the module's data.
* **[Guidance for Implementers](implementer-guidance.html)** — technical
  guidance for DIC implementers.

The module's focus is the operationalisation (enforcement) of the consent filled
in by the patient, on the basis of the consent policies. The delimitation the
source guide draws: using *all* of the profiles developed in the AG
Einwilligungsmanagement is not mandatory, and the FHIR Consent resource carries
neither person-identifying information nor document scans or signatures. See
[Guidance for Implementers](implementer-guidance.html) and
[Security and Privacy](security-and-privacy.html).

---
For conformance requirements see [Conformance](conformance.html); for the
technical artifacts see [Profiles and Extensions](profiles-and-extensions.html).
