<!-- markdownlint-disable MD041 -->
<!-- Source: kerndatensatz-basis input/pagecontent/translationinfo.md; the
     mechanism is documented in docs/recipes/add-translation.md. German mirror:
     input/translations/de/pagecontent/translationinfo.md. -->
### Translation Information

This guide is written in **English** (the default language); **German** is the
translation. English is therefore both the base rendering of the guide and the
`/en/` rendering; use the language switcher at the top right to move between
`/en/` and `/de/`.

Translated pages live under `input/translations/de/pagecontent/` (same file name
as the English page); resource translations are `.po` files under
`input/translations/de/`. Details:
`docs/recipes/add-translation.md` in this repository.

<div class="mii-highlight mii-highlight-orange" markdown="0">
<h5>TODO:REVIEW (Gate C) &mdash; the language direction of THIS module is inverted</h5>
<p>English is the guide's default rendering language, but this module's
<b>authoritative text is German</b>: the narrative was migrated from the
German Simplifier guide (version 2026.0.0, harvested 2026-08-06). The German pages under
<code>input/translations/de/pagecontent/</code> are therefore the <b>source of record</b>, and
the English pages that carry migrated content are <b>unreviewed machine translations</b> of
them. Each such page says so at the top.</p>
<p>Consent policy wording, policy display names, the names of the MII Broad Consent form
modules and the code designators (<code>g&uuml;ltig</code> / <code>nicht g&uuml;ltig</code> /
<code>unbekannt</code>) are deliberately left in German everywhere: they are legally binding
text and identifiers.</p>
<p>Pages that carry MII-wide template text rather than migrated narrative &mdash; General
Requirements, Must Support, Handling Missing Data, Metadata, Downloads, Versioning &mdash; run
in the normal direction (English authored, German translated); the pages that mix both say so
in their own banner. Page titles in the navigation are translated through the
IG-level catalogue <code>input/translations/de/ImplementationGuide-mii-ig-consent.po</code>.</p>
<p><b>Nothing on the English side has been reviewed by a human yet.</b> That review is Gate C
of the migration.</p>
</div>
