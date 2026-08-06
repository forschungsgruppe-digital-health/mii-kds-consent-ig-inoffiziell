# Search Parameters and Operations - MII Implementation Guide Consent v2026.0.1

* [**Table of Contents**](toc.md)
* **Search Parameters and Operations**

## Search Parameters and Operations

### Search parameters of this module

Search parameters are defined which the respective systems must implement when the FHIR RESTful API is used. In principle, logical AND and OR combinations of search parameters are supported.

The foundations and further detail on searching and on the FHIR RESTful API were being worked out in the base modules at the time this implementation guide was written, and may be added or refined at a later point.

This module defines six search parameters on the Consent resource. They are listed, with their canonicals and expressions, in the generated artifact list — see the **Artifacts Summary**.

> [TODO:REVIEW — Gate A/B. The six SearchParameter resources carry **no `id` in the source**; goFSH minted one for each during the migration (`MII-SP-Consent-PolicyUri`, `-ProvisionCode`, `-ProvisionCodePeriod`, `-ProvisionCodeType`, `-ProvisionPeriod`, `-ProvisionType`). Those minted ids become the module's ids and must be confirmed by a human.]

