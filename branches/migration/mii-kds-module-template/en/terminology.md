# Terminology - MII Implementation Guide Consent v2026.0.0

* [**Table of Contents**](toc.md)
* **Terminology**

## Terminology

##### TODO:REVIEW (Gate C) — mixed page: MII-wide English text plus an unreviewed machine translation

The MII-wide notes on the terminology server and on expansions were authored in English (the German mirror is their translation). Everything from **ValueSets** downwards is the opposite direction: its authoritative text is **German**, migrated from the Simplifier-rendered guide (version 2026.0.0, harvested 2026-08-06), and the English wording is an **unreviewed machine translation**. Policy names, code designators and signature descriptions are legally binding German text and are reproduced verbatim.

### Terminology

This page describes the ValueSets and CodeSystems used in the **Consent** module. For general guidance on using codes, see [FHIR Terminology](http://hl7.org/fhir/R4/terminologies.html).

**Important:** CodeSystem resources of external terminologies (e.g. ICD-10-GM, OPS, SNOMED CT) are **not** published in this module; they are obtained from the MII terminology service (SU-TermServ): [https://mii-termserv.de/](https://mii-termserv.de/).

**Expansions:** ValueSet expansions in this guide are produced by a FHIR terminology server — SU-TermServ if the client certificate is configured, otherwise the public HL7 server `tx.fhir.org` (in which case some MII-specific ValueSets may not expand completely).

This module does **not** use SNOMED CT.

### ValueSets

| | |
| :--- | :--- |
| [MII Consent: Policy ValueSet](ValueSet-2.16.840.1.113883.3.1937.777.24.11.36--20230331232804.md) | all codes of the**MII CS Consent Policy**code system |
| [MII Consent: Signature Types](ValueSet-88464c5b-5338-4c2b-9c07-b42fef2ada64.md) | the permitted kinds of signature |
| [MII Consent: Answer ValueSet](ValueSet-2.16.840.1.113883.3.1937.777.24.11.30--20210323234509.md) | the permitted answers in the questionnaire |

Extensions of the policy ValueSet in ART-DECOR will be incorporated into this IG by the TFCU in due course. A new ballot is not required.

#### MII Consent: Signature Types

Per the recommendation of the HL7-D AG Einwilligungsmanagement. Canonical: `https://www.medizininformatik-initiative.de/fhir/modul-consent/ValueSet/mii-vs-consent-signaturetypes`

| | | | |
| :--- | :--- | :--- | :--- |
| Unterschrift der einwilligenden Person | urn:iso-astm:E1762-95:2013 | 1.2.840.10065.1.12.1.7 | Consent Signature |
| Unterschrift der (gesetzlich) vertretenden Person | urn:iso-astm:E1762-95:2013 | 1.2.840.10065.1.12.1.11 | Consent Witness Signature |
| Unterschrift der aufklärenden Person | urn:iso-astm:E1762-95:2013 | 1.2.840.10065.1.12.1.5 | Verification Signature |

**The first column is an explanation added by the guide; it is not part of the ValueSet, which is why it is carried here. It is deliberately not translated.**

#### MII Consent: Answer ValueSet

This ValueSet is used exclusively in the context of questionnaires. How the answers map onto the checkboxes of the form is on [Guidance for Implementers](implementer-guidance.md).

### CodeSystems

| | |
| :--- | :--- |
| [MII CS Consent Policy](CodeSystem-2.16.840.1.113883.3.1937.777.24.5.3--20251211153003.md) | the consent policy codes operationalising the MII Broad Consent |
| [MII Consent Version and Modules](CodeSystem-mii-cs-consent-version-modules.md) | the OIDs of the Broad Consent versions and additional modules |
| [MII Consent: Answer CodeSystem](CodeSystem-2.16.840.1.113883.3.1937.777.24.5.2--20210423105554.md) | gültig / nicht gültig / unbekannt |

#### MII CS Consent Policy

**Note**: the concept of **nested provision elements** in the MII context works with two levels. The parent provision element, the level-1 provision, represents a question in the consent and specifies, via `Provision.Type=DENY` (opt-in model), that everything is forbidden unless it is explicitly permitted in the form of child provision elements, the level-2 provisions. That is: to interpret whether permission exists for a particular use (collect, store, use) of specific data (IDAT, MDAT, BIOMAT, …), the elements of the level-2 provisions have to be evaluated.

Partial withdrawals can likewise cause changes on the level-2 provisions. For example, collection may be forbidden while storage and use remain unaffected ("MDAT erheben" = `deny`, but "MDAT wissenschaftlich nutzen EU DSGVO NIVEAU" = `permit`).

**Attention: only policy codes are intended for use in level-2 provisions** (in the concept table, the second-level concepts, i.e. the child concepts of a module).

Policies with the status "deprecated/inactive" should no longer be added to newly created Consent resources in the future. Such policies should also no longer be evaluated (enforcement).

The code system `urn:oid:2.16.840.1.113883.3.1937.777.24.5.3` contains 101 concepts. The full table — level (module/policy, via the hierarchy), display, code, validity period (property `period-of-validity`) and status (properties `status`/`inactive`) — is on the artifact page [MII CS Consent Policy](CodeSystem-2.16.840.1.113883.3.1937.777.24.5.3--20251211153003.md) and is generated by the IG Publisher from the resource itself.

> **TODO:REVIEW (Gate B) — the policy table was not copied.** The source guide carries this table as roughly 124 rows of hand-maintained Markdown on its terminology page. It is **not** reproduced here, because the same information is in this module's CodeSystem resource and is rendered by the IG Publisher; a second, hand-maintained copy would drift apart the next time a policy is added. Please check on the generated artifact page that validity period and status are in fact visible — otherwise the table has to come back onto this page. (In the build of 2026-08-06 they were: level, display, code, `P30Y`/`P5Y` and "Deprecated" are all on the generated page.) **One phrase had to be re-pointed:** the source's parenthetical "(Siehe nachstehende Tabelle, Spalte Lvl mit Wert 2)" refers to a table that no longer exists here; it now points at the concept level of the generated table. The same reference in substance, but please proof-read it.

