<!-- markdownlint-disable MD041 -->
<div class="mii-highlight mii-highlight-orange" markdown="0">
<h5>TODO:REVIEW (Gate B) &mdash; starter page, narrative not yet migrated</h5>
<p>This is the <strong>MII KDS module template's starter page</strong>, carried over as-is.
It is <strong>not</strong> the narrative of the MII KDS Modul Consent.</p>
<p>The module's guide text exists only as a rendered Simplifier guide
(<code>simplifier.net/guide/miiigmodulconsent</code>); it is <strong>not in the source
repository</strong>, so there was nothing to migrate into this page and nothing was
invented for it. The page <em>structure</em>, the menu and the artifact rendering below are
real; the prose is a placeholder until the narrative is migrated from Simplifier.</p>
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

> [TODO: Describe the data categories your module carries and the applicable
> purpose limitation / legal basis in the MII context.]
{: .mii-highlight .mii-highlight-grey}

#### Security considerations

Security is risk management against risks to confidentiality, integrity and
availability.

> [TODO: Name the attacks/risks considered and the countermeasures — e.g. FHIR
> API access control, pseudonymisation, transport encryption, audit logging.]
{: .mii-highlight .mii-highlight-grey}

#### Module-specific conformance requirements

> [TODO: If your module defines security- or privacy-related SHALL/SHOULD/MAY
> requirements, list them here and say which risk each one addresses.]
{: .mii-highlight .mii-highlight-grey}

#### Residual risks

> [TODO: Name risks NOT addressed by this specification, which must therefore be
> handled in system design, deployment or policy.]
{: .mii-highlight .mii-highlight-grey}
