<!-- markdownlint-disable MD041 -->
<div class="mii-highlight mii-highlight-orange" markdown="0">
<h5>TODO:REVIEW (Gate C) &mdash; mixed page: MII-wide English text plus an unreviewed machine translation</h5>
<p>The authoritative text of this module is <strong>German</strong>. This English page is an
<strong>unreviewed machine translation</strong> of
<code>input/translations/de/pagecontent/security-and-privacy.md</code>, migrated from the Simplifier-rendered
guide (version 2026.0.0, harvested 2026-08-06). Consent policy wording, policy display names
and the names of the MII Broad Consent form modules are <strong>deliberately left in
German</strong>: they are legally binding text and identifiers, not prose. Where the two
language variants differ, the German page applies.</p>
</div>

<!-- English rendering of input/pagecontent/security-and-privacy.md. -->

### Security and Privacy

This section addresses security and privacy experts. It explains which attacks
and risks were considered for the **Consent** module and which
countermeasures apply.

General requirements are in the FHIR core specification —
[Security & Privacy Module](https://build.fhir.org/secpriv-module.html) and the
[security checklist](https://build.fhir.org/security.html). This section does not
repeat them; it states only what is **specific to this module**.

#### Privacy principles

Processing of personal data follows transparency, purpose limitation, data
minimisation, accuracy, storage limitation and integrity/confidentiality
(GDPR Art. 5). In the MII context, use is based on the MII Broad Consent.

##### Privacy aspects of the Consent resource

*Migrated from the source guide — source of record: the German page, harvested
from `.../TechnischeImplementierung/FHIRProfile/Consent`, section
"Datenschutz-Aspekte" (version 2026.0.0, 2026-08-06). Linked from the profile
page [MII\_PR\_Consent\_Einwilligung](StructureDefinition-e0e166b4-0f77-478d-9062-de0034d98ce0.html).*

Because the FHIR Consent resource likewise contains **no person-identifying
information** about the consenting person, the
[**pseudonymous person reference**](https://ig.fhir.de/einwilligungsmanagement/stable/Patient.html)
should be established through corresponding
[**pseudonymous identifiers**](https://ig.fhir.de/einwilligungsmanagement/stable/ContextIdentifier.html).
Any person-identifying information (e.g. date of birth, sex, address), as well as
references — for example to clear-text patient profiles — should be replaced
suitably before export.

*Technically, Patient resources and derived profiles may be used, such as the
profiles of the
[AG Einwilligungsmanagement](https://ig.fhir.de/einwilligungsmanagement/stable/Patient.html)
or of the
[MII](https://simplifier.net/medizininformatikinitiative-modulperson/sdmiipersonpatientpseudonymisiert).*
Independently of that, in order to distinguish pseudonyms, case numbers and so
on, the identifier used has to be categorised by means of
[`Patient.identifier.type`](https://ig.fhir.de/einwilligungsmanagement/stable/ContextIdentifierType.html).

The FHIR Consent resource contains **no document scans and/or signatures**. Where
transmitting them is required for a given use case, separate resources have to be
created per the
[requirements of the AG Einwilligungsmanagement](https://ig.fhir.de/einwilligungsmanagement/stable/DocumentReference.html)
(consent bundles) — in this module the profiles
[Provenance](StructureDefinition-f675b1e8-9f3f-44e8-bb59-9681f78eb464.html) and
[DocumentReference](StructureDefinition-56375452-bfa1-4111-af7c-5b5ba9a1857c.html).

#### Security considerations

Security is risk management against risks to confidentiality, integrity and
availability.

<div class="mii-highlight mii-highlight-grey" markdown="0">
<h5>TODO:REVIEW (Gate B) &mdash; not present in the source guide</h5>
<p>The migrated source guide contains no attack or risk analysis. Nothing was invented; the
gap is recorded in the migration report. Everything the source says about data protection is
in the section above.</p>
</div>

#### Module-specific conformance requirements

<div class="mii-highlight mii-highlight-grey" markdown="0">
<h5>TODO:REVIEW (Gate B) &mdash; not present in the source guide</h5>
<p>The source guide states no security or privacy conformance statements as such. The
pseudonymisation guidance above is phrased as a recommendation, not as SHALL/SHOULD/MAY; it
was not rewritten into conformance statements.</p>
</div>

#### Residual risks

<div class="mii-highlight mii-highlight-grey" markdown="0">
<h5>TODO:REVIEW (Gate B) &mdash; not present in the source guide</h5>
<p>The source guide names no residual risks. Not supplied.</p>
</div>
