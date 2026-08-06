<!-- markdownlint-disable MD041 -->
<div class="mii-highlight mii-highlight-orange" markdown="0">
<h5>TODO:REVIEW (Gate C) &mdash; unreviewed machine translation</h5>
<p>The authoritative text of this module is <strong>German</strong>. This English page is an
<strong>unreviewed machine translation</strong> of
<code>input/translations/de/pagecontent/changes.md</code>, migrated from the Simplifier-rendered
guide (version 2026.0.0, harvested 2026-08-06). Consent policy wording, policy display names
and the names of the MII Broad Consent form modules are <strong>deliberately left in
German</strong>: they are legally binding text and identifiers, not prose. Where the two
language variants differ, the German page applies.</p>
</div>

<!-- Default-language (English) page. Structure ported from kerndatensatz-basis
     input/pagecontent/changes.md (branch main) — one section per version,
     newest first — and from the MII IG release-notes template
     (kerndatensatz-meta/implementation-guides/MedizininformatikInitiative-ImplementationGuide-Template/
     MII-IG-Modul--Modul/Release-notes.page.md), which prescribes Keep a Changelog.
     German mirror: input/translations/de/pagecontent/changes.md — both files
     must say the same thing.

     Maintenance rule: add a new `#### Version <x>` section on top for every
     release, in BOTH languages, as part of the release pull request. Never edit
     a released section afterwards. -->

### Changelog

This page records the changes between the released versions of the
**Consent** module, newest version first. It follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and the MII calendar
versioning scheme described on the [Versioning](version-history.html) page.

Each version gets its own section with the release date and the changes grouped
by category:

* **Added** — new profiles, extensions, value sets, search parameters, pages.
* **Changed** — modified constraints, bindings, guidance or documentation.
* **Deprecated** — artifacts that still exist but should no longer be used.
* **Removed** — artifacts that were withdrawn.
* **Fixed** — corrections of defects.
* **Security** — changes with a security or data-protection impact.

Leave out the categories with nothing to report. Where a change is driven by an
issue or a pull request, link it.

<div class="mii-highlight mii-highlight-red">
<h5>Breaking changes MUST be reported and explained</h5>
<p>A version section that contains a breaking change is not complete until it
answers, explicitly and in this changelog:</p>
<ul>
<li><b>What exactly changed</b> between the two versions — the artifact, the
element, the old and the new constraint (not just "profile X was revised").</li>
<li><b>What it means for existing data:</b> does data that conformed to the
previous version still validate against the new one? If not, which resources
and elements are affected, and how does the failure show up?</li>
<li><b>What implementers should do:</b> the authors' recommendation for
migrating existing data to the new version — transformation steps, default
values, re-coding guidance — or an explicit statement that no migration path
is provided and why.</li>
</ul>
<p><b>What counts as breaking</b> — treat a change as breaking if it does any
of the following, even when it looks small: tightens a cardinality
(<code>0..*</code> → <code>1..1</code>), raises a binding strength (example →
required), removes codes from a required value set, removes or renames an
element or a slice, narrows a type, adds an invariant or a must-support
obligation, or changes a canonical URL. When in doubt, report it as
breaking.</p>
<p><b>Breaking for whom:</b> state both perspectives — <i>stored data</i>
(instances valid against the old version) and <i>implementations</i> (clients
and servers built against it; a removed search parameter breaks
implementations while every stored instance stays valid).</p>
<p><b>The version number will not warn anyone.</b> The MII calendar versioning
scheme (<code>YYYY.n.n</code>) carries no major-version signal the way SemVer
does — this changelog section is the <i>only</i> warning a reader gets.</p>
<p><b>Link the technical delta.</b> From the second formal publication on,
enable the IG Publisher's version comparison (<code>version-comparison</code>
in <code>sushi-config.yaml</code> — see the <a href="version-history.html">
Versioning</a> page for the setup and its prerequisites); it publishes a
machine-generated comparison at
<code>comparison-v&lt;previous&gt;/index.html</code>. Link it from the version
section, so the prose explanation and the technical diff sit side by side.</p>
<p>Mark such entries clearly (for example, prefix them with
<b>BREAKING:</b>) so a reader scanning the section cannot miss them.</p>
</div>

---

#### Version 2026.0.0

**Date:** 2025-12-18

* ValueSet *MII\_VS\_Consent\_SignatureTypes* extended by the code
  `1.2.840.10065.1.12.1.5` "Verification Signature"
* CodeSystem *MII Consent: Policy CodeSystem*
  * validity period added per policy (property `period-of-validity` with an ISO
    8601:2004 date string, or 'einmalig')
  * policy `2.16.840.1.113883.3.1937.777.24.5.3.46` "MDAT retrospektiv
    wissenschaftlich nutzen" is now marked deprecated and should no longer be
    used
  * policy `2.16.840.1.113883.3.1937.777.24.5.3.47` "MDAT retrospektiv
    zusammenfuehren Dritte" is now marked deprecated and should no longer be used
  * policy `2.16.840.1.113883.3.1937.777.24.5.3.16` "KKDAT 5J prospektiv
    speichern verarbeiten" is now marked deprecated and should no longer be used
  * policy `2.16.840.1.113883.3.1937.777.24.5.3.17` "KKDAT 5J prospektiv
    wissenschaftlich nutzen" is now marked deprecated and should no longer be
    used
  * a Markdown representation of the code system as a table was created under
    'Terminologie' in the IG
* CodeSystem *mii-cs-consent-version-modules* created for the BC versions and
  additional modules
  * OIDs for refusals added (BC v1.6d and v1.7.2)
* `Consent.provision.period.end` and `Consent.provision.provision.period.end` now
  have cardinality `0..1`, i.e. they are no longer mandatory
* examples revised and extended
* IG: editorial revision, explanations improved
  * new page *Empfehlungen zur praktischen Anwendung* added (ResultType)
  * handling of withdrawals for consents of minors (validity period / expiry of
    the consent)
  * notes on use in the Modellvorhaben Genomsequenzierung (§ 64e)
  * explanation of the new search parameters added

Full changelog:
[2025.0.3…2026.0.0](https://github.com/medizininformatik-initiative/kerndatensatzmodul-consent/compare/2025.0.3...2026.0.0)

#### Version 2025.0.4

**Date:** 2025-06-16

* Terminologies:
  * policy CodeSystem resource: `display` adjusted (abbreviation → meaningful
    designator)
* Bugfix:
  * pagelink error fixed

#### Version 2025.0.3

**Date:** 2025-06-12

* IG/Consent:
  * support for the additional module Fachnetzwerk Infektion – SNID (Z4) added
  * support for the additional module Deutsches Zentrum für Psychische
    Gesundheit – DZPG (Z5) added
  * Consent: list of available MII consents for use in `Consent.policy.uri`
    updated
  * terminologies: policy CodeSystem extended by the SNID and DZPG policies

Full changelog:
[2025.0.0…2025.0.3](https://github.com/medizininformatik-initiative/kerndatensatzmodul-consent/compare/2025.0.0...2025.0.3)

#### Version 2025.0.2

**Date:** 2025-06-11

* IG/Consent:
  * support for the additional module Fachnetzwerk Infektion – SNID (Z4) added
    * Consent: list of available MII consents for use in `Consent.policy.uri`
      updated
    * terminologies: policy CodeSystem extended by the SNID policies

#### Version 2025.0.1

**Date:** 2025-01-21

* IG/Consent:
  * list of available MII consents for use in `Consent.policy.uri` updated:
    * Zusatzmodul ACRIBiS (Z2)
    * Zusatzmodul Patientenbefragung (Z3)

#### Version 2025.0.0

**Date:** 2024-12-17

* Consent resource
  * `Consent.category` → max value `*`
  * `Consent.provision.type` → fixedCode `deny` removed
  * `Consent.provision.provision.type` → fixedCode `permit` removed
  * IG/Consent adjusted accordingly
* IG/Consent
  * list of available MII consents for use in `Consent.policy.uri` updated
    (withdrawals and minors)
* policy CodeSystem: acribis and PROM policies added
* IG/terminology:
  * level information corrected
  * formatting of the note text corrected
  * note 1 (FHIR + policies) corrected

Full changelog:
[1.0.7…2025.0.0](https://github.com/medizininformatik-initiative/kerndatensatzmodul-consent/compare/1.0.7...2025.0.0)

> **TODO:REVIEW (Gate B) — scope and shape of this changelog.** The source guide
> lists exactly these six versions on its *Release Notes* page; older versions
> (up to 1.0.7) are not on it and were therefore not added here either. The
> entries are taken over unchanged and were **not** re-sorted into the Keep a
> Changelog categories (Added/Changed/…): re-sorting would be an editorial
> interpretation. The migration itself is deliberately not a changelog entry — it
> is not a change to the module.
{: .mii-highlight .mii-highlight-grey}
