# Home - MII Implementation Guide Consent v2026.0.1

* [**Table of Contents**](toc.md)
* **Home**

## Home

| | |
| :--- | :--- |
| *Official URL*:https://www.medizininformatik-initiative.de/fhir/modul-consent/ImplementationGuide/mii-ig-consent | *Version*:2026.0.1 |
| Active as of 2026-08-06 | *Computable Name*:MII_IG_Consent |

### Introduction

This specification describes the FHIR representation of the Core Dataset (CDS) module **Consent** of the Medical Informatics Initiative (MII). It covers the module's use cases and the associated FHIR profiles, extensions and terminology resources in their normative form. The MII Core Dataset enables the standardized secondary use of routine clinical data for medical research.

> The Consent module is a base module of the MII Core Dataset. It describes how consent information is represented uniformly as FHIR resources for processing in a local trusted third party and/or a data integration centre, so that a patient's current consent status can be taken into account in cross-site feasibility enquiries and data releases. It builds on the FHIR profiles of the HL7-D/IHE-D Interop-Forum working group on consent management and constrains them to the MII's requirements. — migrated from the guide's **Beschreibung Modul Consent** page. TODO:REVIEW at Gate B/C.

| | |
| :--- | :--- |
| Date | **not set — see the migration report, decision queue** |
| Version | 2026.0.1 (CalVer`YYYY.n.n`) |
| Status | active |
| Realm | DE |

### Target audience

##### Implementers

Data Integration Centers (DIC), software developers and system architects building FHIR-based solutions.
 → see [Profiles and Extensions](profiles-and-extensions.md) and [Logical Models](logical-models.md).

##### Researchers

Scientists using MII data for medical research.
 → see [Guidance for Researchers](researcher-guidance.md).

### Contents

* **[Guidance](guidance.md)** — getting started and domain notes.
* **[Conformance](conformance.md)** — normative requirements, Must-Support and handling missing data.
* **[Profiles and Extensions](profiles-and-extensions.md)** and **[Terminology](terminology.md)** — the technical artifacts.
* **[Examples](examples.md)** — example instances.

### Related guides

This module is part of the MII Core Dataset; the other KDS modules and their dependencies are described at [medizininformatik-initiative.de](https://www.medizininformatik-initiative.de/).

> This module formally depends on `de.einwilligungsmanagement` (the FHIR profiles of the HL7-D/IHE-D working group on consent management, [ig.fhir.de/einwilligungsmanagement](https://ig.fhir.de/einwilligungsmanagement/stable/)), from which its three profiles derive, and on `hl7.fhir.uv.crmi`. The module relates to the MII base module **Person** for the pseudonymous person identifier — see [Guidance for Implementers](implementer-guidance.md). Further references are on that page.

More FHIR implementation guides can be found in the official **[FHIR IG Registry](https://fhir.org/guides/registry/)** (source: [`FHIR/ig-registry`](https://github.com/FHIR/ig-registry)).

### Imprint

This guide was created within the Medical Informatics Initiative and is subject, by its governance process, to the coordination procedure of the Interoperability Forum and the technical committees of HL7 Germany.

### Contact

Questions about this publication can be asked on the HL7 FHIR Zulip [chat.fhir.org](https://chat.fhir.org) in the `german/mi-initiative` stream, or on the MII Zulip [mii.zulipchat.com](https://mii.zulipchat.com/) in the `MII-Kerndatensatz` stream. Comments and issues are welcome as **Issues** on [GitHub](https://github.com/forschungsgruppe-digital-health/mii-kds-consent-ig-inoffiziell/issues).

> Content responsibility for this module lies with the **MII Taskforce Consent Umsetzung**. Module lead: Sebastian Stäubert, Martin Bialke. Technical implementation: Stefan Lang (FHIR profiles and implementation guides), Martin Bialke (implementation guides). Contact at the TMF: Karoline Buckow. Questions may also be sent informally to `office@medizininformatik-initiative.de`.

### Authors (in alphabetical order)

> The module was created with the collaboration of Martin Bialke, Sebastian Stäubert, Angela Merzweiler, Lars Geidel, Jörg Römhild, Raffael Bild, Fabian Prasser and Stefan Lang (HL7 Deutschland, technical committee FHIR, Gefyra GmbH, Lang Health IT Consulting). — migrated from the guide's **Autoren und Ansprechpartner** section; institutions per person are not stated in the source. TODO:REVIEW at Gate B.

### Copyright and License

© 2019+ TMF e. V., Charlottenstraße 42, 10117 Berlin

This work is licensed under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).

For the usage rights of the underlying FHIR technology, see the FHIR base specification.

Some of the code systems used are published and maintained by other organizations; the copyright of the respective publishers applies.

### Disclaimer

The content of this document is public. Please note that parts of this document are based on FHIR version R4, which is copyrighted by HL7 International.

Although this publication was prepared with the greatest care, the authors cannot accept any liability for direct or indirect damage that may arise from the content of this specification.

