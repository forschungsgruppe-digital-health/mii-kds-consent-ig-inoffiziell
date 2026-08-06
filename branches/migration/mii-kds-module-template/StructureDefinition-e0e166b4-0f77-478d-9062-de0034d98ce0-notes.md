<!--
  MII_PR_Consent_Einwilligung — notes, ENGLISH (translation).
  Source of record: input/translations/de/intro-notes/<same file name>, which also
  records where the source page's search-parameter and example sections went.
-->

{:.bg-warning}
**TODO:REVIEW (Gate C) — unreviewed machine translation.** The authoritative text
is the German notes file. Element paths, code values, OIDs and the German policy
display names below are **identifiers**: they are reproduced verbatim and are not
translated. Where the two language variants differ, the German page applies.

### Basic use of the FHIR Consent profile

*Only the differences from the base profile are explained below.*

| FHIR element | Explanation |
| --- | --- |
| `Consent.id` | must-support, but optional |
| `Consent.meta` | must-support, but optional |
| `Consent.meta.source` | must-support, but optional |
| `Consent.meta.profile` | must-support, but optional |
| `Consent.extension:domainReference` | must-support per the requirements of the [AG Einwilligungsmanagement](https://ig.fhir.de/einwilligungsmanagement/stable/ResearchStudy.html), but optional |
| `Consent.identifier` | Contains one or more external IDs of the consent from an external system. This can be, for example, the IHE ID of the CDA document or the ID of the document in an external trusted third party. The identifier should always be given as the pair "system" and "value". Optional. |
| `Consent.scope.coding.system` | fixed value: `http://terminology.hl7.org/CodeSystem/consentscope` |
| `Consent.scope.coding.code` | The representation of the MII consent places the context clearly on research. Fixed value: `research` |
| `Consent.category.coding` | must-support. **At least two categories** are mandatory, each with at least one coding for the consent categories, so that consents of type "MII Einwilligung" can be searched for: **(1)** per [valueset-consent-category](https://www.hl7.org/fhir/valueset-consent-category.html) — fixed system `http://loinc.org`, fixed code for 'Privacy policy acknowledgement Document' `57016-8`; **(2)** identification of the MII Broad Consent — fixed code `2.16.840.1.113883.3.1937.777.24.2.184`. Further additional entries are not prevented. |
| `Consent.category:templateType.coding` | ResultType per [ResultType](https://ig.fhir.de/einwilligungsmanagement/stable/ResultType.html). At least `document` and `consent-status` should be supported. If `document` is given as the ResultType, the kind of (source) document must also be given in the `templateType` slice. |
| `Consent.category:templateType.coding` | Categorisation per [TemplateType](https://ig.fhir.de/einwilligungsmanagement/stable/TemplateType.html). Serves as an informal element to differentiate between consent, withdrawal, objection and refusal. |
| `Consent.patient.reference` | Reference to the patient the Consent resource refers to, as a literal reference, relative reference, internal reference or absolute URL, must-support. `Consent.patient.reference` should be filled where possible, i.e. where a corresponding Patient resource exists. Otherwise the patient reference has to be established via `Consent.patient.identifier`. |
| `Consent.patient.identifier` | The person reference as an identifier, must-support. See `Consent.patient.reference`. The reference to the patient should preferably be established via `Consent.patient.reference`; `Consent.patient.identifier` may be used as an alternative or in addition. |
| `Consent.patient.identifier.system` | If the person reference is given by identifier, the system (as a URI) is mandatory, must-support |
| `Consent.patient.identifier.value` | If the person reference is given by identifier, the value (as a string) is mandatory, must-support |
| `Consent.policy.uri` | Reference to the version of the MII Broad Consent document underlying the Consent resource, per the table below — e.g. **MII Broad Consent version 1.7.2** `urn:oid:2.16.840.1.113883.3.1937.777.24.2.2079` or **MII Broad Consent version 1.7.2 incl. Zusatzmodul Acribis** `urn:oid:2.16.840.1.113883.3.1937.777.24.2.4031`, must-support |

> **TODO:REVIEW (Gate B) — two rows under the same slice name.** The rendered
> source page lists both category rows under
> `Consent.category:templateType.coding`, although the first describes the
> ResultType. Both rows are reproduced unchanged (nothing corrected, nothing
> added). In addition, this profile slices `Consent.category` into the slices
> `loinc` and `mii`; the slice names `templateType`/`resultType` come from the
> base profile of the AG Einwilligungsmanagement. Please check against the
> StructureDefinition and have the source corrected.
{: .mii-highlight .mii-highlight-grey}

### Unique identification of the MII Broad Consent

To filter FHIR Consent resources for consents based on the MII Broad Consent, a
mandatory URI is used for `Consent.policy.uri`. The TFCU has created ART-DECOR
representations for the different versions of the MII Broad Consent. They can be
referenced by a unique OID (see the table below). The version labels are the
German designations of the consent forms and are not translated.

| Version of the MII Broad Consent | Unique OID per the [TFCU specification](https://art-decor.org/decor/services/RetrieveDataSet?conceptId=2.16.840.1.113883.3.1937.777.24.2.184) |
| --- | --- |
| 1.6d | 2.16.840.1.113883.3.1937.777.24.2.1790 |
| 1.6d Ablehnung | 2.16.840.1.113883.3.1937.777.24.2.4053 |
| 1.6d Komplettwiderruf | 2.16.840.1.113883.3.1937.777.24.2.2718 |
| 1.6d Teilwiderruf | 2.16.840.1.113883.3.1937.777.24.2.2719 |
| 1.6f | 2.16.840.1.113883.3.1937.777.24.2.1791 |
| 1.6f Komplettwiderruf | 2.16.840.1.113883.3.1937.777.24.2.2720 |
| 1.6f Teilwiderruf | 2.16.840.1.113883.3.1937.777.24.2.2721 |
| 1.7.2 | 2.16.840.1.113883.3.1937.777.24.2.2079 |
| 1.7.2 Ablehnung | 2.16.840.1.113883.3.1937.777.24.2.4054 |
| 1.7.2 Komplettwiderruf | 2.16.840.1.113883.3.1937.777.24.2.2722 |
| 1.7.2 Teilwiderruf | 2.16.840.1.113883.3.1937.777.24.2.2723 |
| 1.7.2 (Eltern und Sorgeberechtigte für Minderjährige v1.1) | 2.16.840.1.113883.3.1937.777.24.2.3542 |
| 1.7.2 (7–11 Minderjährige v1.1) | 2.16.840.1.113883.3.1937.777.24.2.3543 |
| 1.7.2 (12–17 Minderjährige v1.1) | 2.16.840.1.113883.3.1937.777.24.2.3544 |
| Zusatzmodul ACRIBiS (Z2) | 2.16.840.1.113883.3.1937.777.24.2.4031 |
| Zusatzmodul Patientenbefragung (Z3) | 2.16.840.1.113883.3.1937.777.24.2.4036 |
| Zusatzmodul Fachnetzwerk Infektion – SNID (Z4) | 2.16.840.1.113883.3.1937.777.24.2.4037 |
| Zusatzmodul Deutsches Zentrum für Psychische Gesundheit – DZPG (Z5) | 2.16.840.1.113883.3.1937.777.24.2.4048 |

### Nested provision elements

The FHIR Consent resource follows the GDPR requirement of **opt-in**: only what
was explicitly consented to at a particular point in time (the time of consent)
is permitted. This is realised through nested provision elements.

In opt-in scenarios the **parent provision element** (→ **level-1 provision**)
denies everything (`Provision.Type=DENY`) unless it is explicitly permitted in the
form of **child provision elements** (→ **level-2 provision**). Child provisions
therefore have to use provision elements with `Provision.Type=PERMIT`. For
additional information, level-2 provisions with `Provision.Type=DENY` are
possible.

The general validity period of the consent is likewise realised through the
parent provision element by means of `provision.period` (for the MII Broad
Consent: 30 years).

Should individual parts of the consent expire earlier, these exceptions can be
defined as part of child provisions referring to the relevant part of the consent
by means of `provision.provision.period` (e.g. the provision with code
`2.16.840.1.113883.3.1937.777.24.5.3.6` for the policy "MDAT erheben" expires
after 5 years).

**Parent provision (`Consent.provision`)**

| FHIR element | Explanation |
| --- | --- |
| `Consent.provision.type` | value `DENY` or `PERMIT`, must-support |
| `Consent.provision.period.start` | mandatory start of the validity of the consent. Unless specified otherwise this is typically the date on which the data subject signed the consent, must-support |
| `Consent.provision.period.end` | mandatory end of the validity of the consent. This is typically the point at which the consent period defined for the MII expires (30 years from the date of signature), must-support |
| `Consent.provision.action` | actions are not permitted, not supported |
| `Consent.provision.code` | codes are not permitted in the parent provision, not supported |
| `Consent.provision.provision` | list of child provision elements explicitly permitting (data processing) activities, must-support |

**Child provision elements (`Consent.provision.provision`)**

*Exactly one child provision element should be used per consent policy.*

| FHIR element | Explanation |
| --- | --- |
| `Consent.provision.provision.type` | value `PERMIT` or `DENY`, must-support |
| `Consent.provision.provision.period.start` | mandatory start of the validity of the consent policy, must-support |
| `Consent.provision.provision.period.end` | mandatory end of the validity of the consent policy, must-support |
| `Consent.provision.provision.code` | 1..n statements on the semantics of the consent policy. **At least per the MII TFCU concept** (cf. [MII Consent: Policy ValueSet](ValueSet-2.16.840.1.113883.3.1937.777.24.11.36--20230331232804.html)), must-support |
| `Consent.provision.provision.code.coding.system` | system, ideally per the **MII TFCU concept** (cf. [MII Consent: Policy ValueSet](ValueSet-2.16.840.1.113883.3.1937.777.24.11.36--20230331232804.html)): `urn:oid:2.16.840.1.113883.3.1937.777.24.5.3`, must-support |
| `Consent.provision.provision.code.coding.code` | code, ideally per the **MII TFCU concept** (cf. [MII Consent: Policy ValueSet](ValueSet-2.16.840.1.113883.3.1937.777.24.11.36--20230331232804.html)), e.g. `2.16.840.1.113883.3.1937.777.24.5.3.6`, must-support |
| `Consent.provision.provision.code.coding.display` | optional display, ideally per the **MII TFCU concept** (cf. [MII Consent: Policy ValueSet](ValueSet-2.16.840.1.113883.3.1937.777.24.11.36--20230331232804.html)), e.g. "MDAT erheben" |
| `Consent.provision.provision.action` | actions are not permitted, not supported |
| `Consent.provision.provision.provision` | further nesting levels of provisions are not permitted, not supported |

### End of the consent, and Consent resources in the context of withdrawal, refusal or objection

Per the requirements of the MII AG Consent, a patient's consent generally ends
after 30 years. Consents of **minors** (the person the consent concerns) are a
special case: where such consents were filled in on their behalf by those with
custody, **the consent ends when the data subject reaches the age of majority**.
This has to be implemented technically.
[Reference implementations](https://www.ths-greifswald.de/dezember-release-2025-neue-versionen-von-e-pix-gpas-und-gics-verfuegbar/)
exist.

The
[withdrawal template (compatible with MII BC 1.7.2)](https://www.medizininformatik-initiative.de/sites/default/files/2025-01/MII_BC_Formular-Komplettwiderruf.pdf)
is also intended for withdrawing consents of minors, as these too are usually
filled in by those with custody.

For Consent resources created in connection with withdrawals (full or partial),
refusals or objections, the
[recommendations of the HL7-D AG Einwilligungsmanagement](https://simplifier.net/guide/Einwilligungsmanagement/Consent?version=current)
generally apply (cf. the section *Angepasste Empfehlungen zur Verwendung von
Consent und Consent-Provisions nach Dokumentenart und Szenario*):

*Level-2 provisions should therefore always be given where possible.* If a
document has no conceptually defined end (for example a withdrawal, refusal or
objection), `period.end` may accordingly be omitted from the provisions.
