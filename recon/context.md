# Ecosystem + ownership context — MII KDS Consent migration (recon, 2026-08-31)

All work READ-ONLY. Every claim carries an evidence pointer (file:line in a local clone under
`…/9e6d07a4…/scratchpad/recon/`, an exact command, or a URL). MEASURED vs INFERENCE is marked
where it matters; unverifiable items are marked **NICHT PRÜFBAR**.

Local evidence clones (this scratchpad):
- `recon/wiki-meta/` — clone of `https://github.com/medizininformatik-initiative/kerndatensatz-meta.wiki.git`, HEAD `4cbbccec` (2026-08-18 11:32 +0200, "Added LOINC")
- `recon/sandbox-consent/` — clone of `forschungsgruppe-digital-health/mii-kds-consent-ig-inoffiziell`, checked out at `59a1968` (tip of `migration/mii-kds-module-template`)
- `recon/mii-skill-SKILL.md` — the MII org's own migration skill, fetched via `gh api repos/medizininformatik-initiative/mii-kerndatensatz-dev/contents/.claude/skills/mii-ig-publisher-migration/SKILL.md`
- `recon/studie-plan-precedent.md` — copy of today's Studie migration plan (see §f)

---

## a. MII meta wiki guidance (Release 2027, naming conventions)

**Which wiki.** `mii-kerndatensatz-dev.wiki.git` does **not** exist (`git clone` →
`remote: Repository not found`). The guidance wiki is **`kerndatensatz-meta.wiki`**
(cloned to `recon/wiki-meta/`; 14 pages; last wiki commit `4cbbccec` 2026-08-18).

**Release-2027 page** (`recon/wiki-meta/Release-2027.md`, 23 lines total — it is a terse notes
page, not a formal plan). MEASURED content, in full effect:

- Title: "Release Procedure 2027" (line 1).
- "Supporting procedure Migration Simplifier - IG Publisher / possible AI support via Claude Skills"
  naming exactly **two** toolkits (lines 4–7):
  1. `https://github.com/medizininformatik-initiative/mii-kerndatensatz-dev/blob/main/.claude/skills/mii-ig-publisher-migration/SKILL.md` (MII's own skill — see §b)
  2. `https://github.com/forschungsgruppe-digital-health/mii-kds-sample-ig-inoffiziell` (the FGDH reference migration)
- **"IG Umbau - DE First"** (line 9) — the 2027 IG rebuild is mandated DE-first.
- Structure guidance (lines 10–11): rebuild the structure "auf 2Dimensionale Abbildung optimieren
  statt geschachteltem NavBar" (optimize for a 2-dimensional layout instead of a nested navbar);
  "putting Artifact site texts in description / compile explanatory text to extra markdown pages".
- Review needs (lines 14–18): timely review of the **QA report** ("oft treten hier mehr Fehler auf
  als bei SUSHI"), filters, "Zusammenführen der advisor.json / Patrick's Filter Framework für
  complete / mii-testdata".
- Open question: "Dezidierter Kommunikationskanal?" (line 21).
- **Consent-specific rows/timelines/assignments: none.** The page contains no module table, no
  dates, no names. **Ballot timing for 2027: NICHT PRÜFBAR from the wiki** — `grep -iE
  'ballot|2027|termin|deadline|zeitplan|Q[1-4]' Module-Release-Workflow.md` returns nothing, and
  Release-2027.md carries no dates. The only ballot statement anywhere is process-generic:
  ballots are required "nur bei Änderungen am Informationsmodell"
  (`Übersicht-über-Versionen-der-Kerndatensatz‐Module.md:164-166`).

**Naming-conventions page** (`recon/wiki-meta/Namenskonventionen-für-FHIR‐Ressourcen-in-der-MII.md`):
- The agreed module identity for Consent (line 17): **Vollständiger Modulname "Modul Consent" ·
  technischer Modulname (url) `modul-consent` · Abkürzung (title/name/id) `Consent`** — this
  matches the canonical measured in the sandbox
  (`https://www.medizininformatik-initiative.de/fhir/modul-consent`, 12/12 packaged urls agree;
  sandbox `migration-log/identity-claims.tsv` line `canonical`).
- Resource-type prefixes PR/EX/LM etc. (lines 37+).

**Consent rows in the version-overview page**
(`Übersicht-über-Versionen-der-Kerndatensatz‐Module.md:63-67`): 2026.0.0 (veröffentlicht),
2025.0.4 (veröffentlicht), 1.0.7 (veröffentlicht), plus "Arbeitsversion — in Arbeit" pointing at
Simplifier project `medizininformatikinitiative-modulconsent`. **No 2027 row for Consent** —
contrast Mikrobiologie, which has 2027.0.0-alpha1…alpha5 rows in the same table (lines 99–103):
that is what a 2027-active module looks like in this wiki, and Consent does not look like that.

**Terminology policy for v2027** (`Terminology-Version-Policy.md:11,19`): v2027.* pins SNOMED
`http://snomed.info/sct/900000000000207008/version/20260701` and LOINC 2.82.

---

## b. MII's own migration skill — `mii-ig-publisher-migration`

**Location + version (MEASURED).** Lives at
`medizininformatik-initiative/mii-kerndatensatz-dev/.claude/skills/mii-ig-publisher-migration/SKILL.md`
(repo tree listed via `gh api …/git/trees/main?recursive=1`; repo description "Meta-rig coordination
for MII Kerndatensatz development across all modules", default branch `main`, pushedAt
2026-07-15T12:57Z). Frontmatter: **version 1.0.0** (`recon/mii-skill-SKILL.md:2-4`). Single commit
history for the file: `4a3945d5` 2026-04-28 by **Thomas Debertshäuser** ("feat: Add IG Publisher
migration skill") — authored once, never updated since
(`gh api 'repos/…/commits?path=.claude/skills/mii-ig-publisher-migration/SKILL.md'`).
The skill directory contains **only SKILL.md** — no scripts, no references (tree listing).
Sibling skills in the same repo: `fix-ig-export-links`, `mii-package-publishing`,
`mii-testdata-contribution`.

**Scope (MEASURED from SKILL.md).** A knowledge/how-to document: Simplifier-tag replacement tables
(remove/replace/auto-generated), i18n directory layout, `ig.ini`/`sushi-config.yaml` snippets, a
GitHub-Actions workflow recipe, an 8-point post-migration checklist, and a reference-implementation
table (kerndatensatz-basis `main` complete; labor/prozedur/proms on `feat/ig-publisher-migration`
branches — SKILL.md "Existing Reference Implementations").

**Headline differences vs FGDH `mii-ig-migration` (agent-skills, latest v0.25.0 2026-08-28) —
enough for a toolkit choice, not a deep dive:**

| Dimension | MII `mii-ig-publisher-migration` v1.0.0 | FGDH `mii-ig-migration` (agent-skills v0.25.0) |
|---|---|---|
| Nature | prose how-to, no scripts | scripted pipeline with run-log + gates (sandbox run-log invokes `postprocess-gofsh.py`, `fql-scan.sh --strict`, `gen-page-title-po.py`; `migration-report.md:269,440,462`) |
| Language direction | **"English = primary language (`i18n-default-lang: en`)", German = translation** (SKILL.md "Language Strategy") — **contradicts the wiki's "IG Umbau - DE First"** (Release-2027.md:9) | DE-first supported/practiced — Dokument PR #36 is titled "…template v0.13.1, **DE-first**" and its language decision was owner-confirmed (PR comment 2026-08-30, §f) |
| Template | `template = fhir2.base.template#current` — a **floating** pin (SKILL.md "1. ig.ini") | `mii-kds-module-template` pinned by exact version+commit; floating pins (`#current/#latest/#dev`) **fail** the template's convention check (sandbox `ig.ini` comment block, `recon/sandbox-consent/ig.ini`) |
| CI | `ghcr.io/gefyra/ig-publisher-with-snapshot-support:latest` + MII-org mTLS secrets `CDS_DEV_CLIENT_*` (SKILL.md "4. GitHub Actions Workflow") — assumes MII-org shared secrets | pinned toolchain image (`kds-ig-toolchain:v0.4.0`, IG Publisher 2.2.11 sha256-verified; `migration-report.md:480` + "Toolchain" row) |
| Verification | 8-line manual checklist | measured gates A–D, identity tiers P/R/I/T, QA-delta triage, `verify-migration` step (migration-report structure) |
| Freshness | 1 commit, 2026-04-28, v1.0.0 | 34 releases v0.1.0 (2026-07-31) → v0.25.0 (2026-08-28); v0.25.0 headline: "migrated modules reference the IG template by URL - no vendored copy" (`gh release view v0.25.0`) |

**INFERENCE:** the MII skill predates the DE-first decision and is best treated as the org's
statement of *intent + tag-replacement knowledge*, not as the execution toolkit; the wiki itself
lists both side by side as "possible AI support".

---

## c. FGDH sandbox `forschungsgruppe-digital-health/mii-kds-consent-ig-inoffiziell`

**Repo metadata (MEASURED via `gh repo view` / `gh api`):** PUBLIC, created 2026-08-05T20:58Z,
**pushedAt 2026-08-06T19:07Z — no push since**, description "Inoffizielle Demonstration einer
durchgeführten (Test-) Migration für das MII KDS Consent-Modul". Default branch **`develop`**
(a mirror of the source repo's `develop` — its tip `4d44dbe` is a Sebastian-Stäubert commit and
the tree is the Forge layout: `examples/ figures/ ressourcen-profile/ searchparameters/
terminologie/`). Branches: `develop`, `gh-pages`, `migration/mii-kds-module-template`.
PRs: **#3 OPEN** ("feat: migrate KDS Consent onto the MII KDS module template (narrative
harvested, 18/18 pages)", head `migration/mii-kds-module-template`, msusky, 2026-08-06T16:01Z);
#1 CLOSED (the earlier Path-B run, 2026-08-06T00:12Z).

**What the migration branch reflects (MEASURED from `recon/sandbox-consent/` at `59a1968`,
1 migration commit on top of source `4d44dbe`):**
- **Source version:** commit `4d44dbe9` (source `develop`, 2026-08-06); package tier read
  `de.medizininformatikinitiative.kerndatensatz.consent@2026.0.1-rc-4`; rendered guide harvested:
  key `miiigmodulconsent` version 2026.0.0 (published 2025-12-18 01:17); guide harvest 18/18 pages
  (`migration-log/migration-report.md` "Source of record" table; `migration-log/simplifier-guides.tsv`).
- **Template version: v0.6.0** (`7efc8ff8…`), **vendored** as `ig-template/` with
  `template = #ig-template` in `ig.ini` (migration-report.md:6,30; `ig.ini`).
- **Skill version: not stamped in the log** (the run-log's ref line says `ref=<ref>
  ref_source=not recorded`, migration-report.md:500). **INFERENCE from timeline:** PR #3 was
  created 2026-08-06T16:01Z, ~1 h after agent-skills **v0.13.0** (2026-08-06T15:03Z) and after
  v0.12.0 (09:16Z) — the run reflects the v0.12/v0.13-era skill (release list via
  `gh release list -R forschungsgruppe-digital-health/agent-skills`).
- **Language direction: EN-primary** — `sushi-config.yaml:367` `i18n-default-lang: en`, German
  under `input/translations/de/`.
- Build state recorded: SUSHI 0 errors / 9 warnings; qa.txt 98/136/482 with 0 migration-induced
  errors; preview built **locally** and pushed to `gh-pages` because `de.einwilligungsmanagement@
  2.0.3-snapshots` is a LOCAL cache rebuild that "does not resolve in CI or on another machine"
  (migration-report.md L0 block + D4 row + tail "CI preview is disabled for this branch").
- Decision queue D1–D8 fully recorded (canonical kept, license CC-BY-4.0, target version choice
  2026.0.1, approval/topic extensions removed, title per template pattern) —
  migration-report.md ① table.

**Staleness vs skill v0.25.0 + template v0.13.2 (assessment):**
1. Template: v0.6.0 (2026-08-02) vs v0.13.2 (released today 2026-08-31) — 7+ minor releases behind;
   and v0.25.0's headline change ("IG template referenced **by URL — no vendored copy**",
   release notes) makes the sandbox's entire vendored `ig-template/` + `template = #ig-template`
   mechanism obsolete.
2. Language: EN-primary vs the wiki's DE-first mandate and the Dokument PR #36 DE-first precedent.
3. Source: base `4d44dbe` (2026-08-06) is **3 commits behind** source `develop` tip `744f7bab`
   (2026-08-21, Martin Bialke, "slices templateType resultType wieder rein") — and those commits
   touch exactly the `Consent.category` slice area the report used to fingerprint the release.
4. Skill: ~v0.12/0.13-era vs v0.25.0 (≈20 releases of pipeline evolution in between).
5. The repo's own default branch mirror is equally stale (tip `4d44dbe`).

**Verdict: evidence-only, not a reusable starting point.** Re-run the migration fresh (skill
v0.25.0, template v0.13.2, DE-first, current source tip). What IS durable and reusable as
decision input: `migration-log/` (identity-claims.tsv, guide-harvest TSVs incl. per-page routing,
simplifier-guides.tsv, the D1–D8 decisions with their rationale, and the measured
parent-snapshot facts — 21/21 snapshots generate on `de.einwilligungsmanagement@2.0.3` where the
spec measured 3 refusals on 2.0.2; migration-report tail). Note the pinned context's framing
("served as the v0.22.0 harvest-route verification case around 2026-08-23"): consistent with the
repo — that verification left **no trace in the repo** (pushedAt stays 2026-08-06T19:07Z), so it
was read-only against this content; the 18/18 routing was already in PR #3's title on 2026-08-06.

---

## d. Consent module owner activity (source repo `kerndatensatzmodul-consent`)

**People (MEASURED):**
- **Sebastian Stäubert** (`SebStaeubert`, gh profile: "IMISE, Uni-Leipzig", Leipzig) — the
  dominant owner: author/merger of nearly every PR (#122, #105, #96, #78, #76, #31, #22 …;
  `gh pr list --state all`), author of 30 of the 31 open issues, author of almost all commits on
  `develop` and `master`. **Primary D-0 contact.**
- **Martin Bialke** (`mbialke`, gh profile empty) — merged the release PR #104 ("Release v2026:
  Develop -> Main", 2025-12-18) and authored the **most recent develop commits** (3× "slices
  templateType resultType wieder rein", 2026-08-21 — the repo's last push). Affiliation THS/Uni
  Greifswald: INFERENCE from co-authorship with Stäubert on the consent-management publications
  listed in the wiki (`recon/wiki-meta/Home.md`, 2022 + 2023 e-health-com articles "Stäubert, S.,
  Bialke, M., …"). **Secondary contact.**
- Thomas Debertshäuser (`ThomasDeBe`, "BIH / Charité") — authored PR #109 (fix extension
  cardinality, CLOSED unmerged; branch `fix/extension-cardinality-domainreference` still exists)
  and, notably, wrote the MII org's migration skill (§b).
- Governance body: **TF Consent Umsetzung** (PR #22 set publisher/contact to it; issue #94
  "Meta Issue für Help Wanted der TF CU"; issue #128 "TF CU - Beschreibung Enforcement").

**Activity profile (MEASURED):**
- Branches: `develop`, `master`, `fix/extension-cardinality-domainreference`, `renovate/configure`
  — **no 2027 branches, no translation branches** (`gh api …/branches`).
- Top-level tree on `develop`: `.gitignore LICENSE README.md examples figures ressourcen-profile
  searchparameters terminologie` — pure Forge shape, **no `ImplementationGuide-2027*` dirs, no
  `input/`, no sushi-config** (`gh api …/contents/?ref=develop`).
- **Contrast with Studie:** the Studie owner was actively building 2027 DE/EN guide trees;
  **Consent shows NO 2027 guide work at all.** Work since the 2026.0.0 release is steady
  content/terminology maintenance on `develop`: category-slice churn (remove/re-add
  `templateType`/`resultType` slices, 2026-08-03…08-21), SNID module-name corrections (#121/#122,
  merged 2026-06-18), acribis policy label, deprecated-code formatting (#120).
- Open PRs: only Renovate's onboarding PR #55 (open since 2024-12-01) — **no meaningful bot
  dependency churn**.
- Open issues: 31; active ones include **#124 "Consent category prüfen" (updated 2026-08-21 —
  same day as the last push, same topic as the last commits)**, #128 (TF CU enforcement,
  2026-08-06), #123 (FHIR search on updated resources), #126/#125 (testdata). Long-standing
  modernization issues the migration would touch directly: **#63 "github statt simplifier für
  IG-Edit nutzen" (2024-12-19), #64 auto-ig-builder, #66 CI FHIR validator, #69 CS/VS
  translations + displays** (`gh issue list --state open`).
- Releases (GitHub): 2026.0.0 (2025-12-18, latest), 2025.0.3, 2025.0.0 — tags without `v` prefix
  (pinned context). Note the registry knows **2025.0.4** even though GitHub releases stop at
  2025.0.3 (wiki version table also lists 2025.0.4) — releases and GitHub tags are not 1:1 here.

---

## e. Simplifier / registry churn

**Package `de.medizininformatikinitiative.kerndatensatz.consent`** (MEASURED today via
`curl -s https://packages.simplifier.net/de.medizininformatikinitiative.kerndatensatz.consent`):
- Versions: 1.0.0-ballot1, 1.0.1…1.0.7, 2025.0.0-alpha, 2025.0.0…2025.0.4, 2026.0.0,
  **2026.0.1-rc-1 … 2026.0.1-rc-4**. `dist-tags: {latest: 2026.0.0}`.
- **No 2027 version, no new ballot version** (the only "ballot" ever is 1.0.0-ballot1).
- The rc line is unfinished: **no final 2026.0.1**; rc-4 existed by 2026-08-06 (it was the
  package the sandbox harvested; its manifest self-describes as "resync from github branch
  develop" — sandbox `migration-log/identity-claims.tsv`). Registry publish dates per version:
  **NICHT PRÜFBAR** — the registry listing returns no date field (all `?` in our dump).
- **Version-fingerprint gotcha for the plan** (measured in the sandbox report): `dist-tags.latest`
  (2026.0.0) does NOT match current `develop` content; at harvest time only rc-4 matched the
  `Consent.category` slice shape, and rc-4 pins parent `de.einwilligungsmanagement@2.0.3` while
  2026.0.0 pins 2.0.2 (migration-report.md "Which release the source commit corresponds to").
  With develop having moved again on 2026-08-21, even rc-4 no longer provably matches → re-measure
  at execution time.

**Guides (MEASURED probes today):**
- `https://simplifier.net/guide/miiigmodulconsent` → HTTP 200, redirects to `?version=2026.0.0`
  (the default); page version strings contain only `2026.0.0`.
- Guessed 2027 keys 404: `mii-ig-modul-consent-2027`, `mii-ig-modul-consent-2027-de`
  (`curl -w '%{http_code}'`). A 2027 guide under some other key: **NICHT PRÜFBAR** (Simplifier has
  no enumerable public search API from here), but the wiki version table (2026-08-18) lists no
  2027 Consent guide either (§a), and the known guide keys as of 2026-08-06 were exactly three:
  `mii-ig-modul-consent-2025` @2025.0.4, `mii-ig-modul-consent-2026` @2026.0.0,
  `miiigmodulconsent` @2026.0.0 (sandbox `migration-log/simplifier-guides.tsv`).

---

## f. Precedent artifacts on this machine

**Studie plan (earlier today) — readable and copied.**
`/private/tmp/claude-503/-Users-marcel-Development-cross-hub-patientportal/0afac26a-e740-4b1b-ae89-7e9976f6722c/scratchpad/`
is readable. `plan/` contains `studie-migration-plan.md` (32,541 B) + `.html` (45,546 B); `recon/`
contains `guide.md, priorArt.md, source.md, template.md, toolkit.md, verify-skillV.md,
verify-sourceV.md, verify-templateV.md` (+ an empty `summary.md`); the parent dir also holds a
`meta-wiki/` clone (same wiki as §a) and working files. The plan markdown is copied to
**`recon/studie-plan-precedent.md`** in this scratchpad.

**Its section structure (the structural precedent the Consent plan should follow):**
1. Executive summary — 2. Measured starting position (2.1 source repo · 2.2 rendered guides
(Simplifier) · 2.3 toolkit + template versions to pin · 2.4 what is lighter than the Dokument
migration) — 3. Decision queue (nothing is the agent's call) — 4. Execution plan mapped 1:1 onto
skill v0.25.0 run-log steps, Phases 0–9 (preparation · Gate 0 preflight/source-inventory ·
identity/Gate A · skeleton · artefact transfer · narrative/Gate B · bilingual wiring/Gate C ·
build & QA · verification & report · PR & Gates B/C/D) — 5. Risks & mitigations — 6. Effort &
scale estimate — 7. What this plan deliberately does NOT do. (Headings from
`grep '^#' studie-plan-precedent.md`.)

**Dokument migration precedent — real PR in the MII org (MEASURED):**
`medizininformatik-initiative/kerndatensatz-dokument#36` — "Migration: Simplifier → IG Publisher
(mii-kds-module-template v0.13.1, **DE-first**)", author msusky, created 2026-08-30, **state OPEN,
not merged**, 4 comments: a github-actions IG-preview comment (branch
`migration/2027.0.0-ballot.rc1-template-v0.13.1`), msusky's "Language-direction decision (D3) —
normative confirmation" of DE-first (2026-08-30T07:16Z), a status update "owner instructions
applied, nothing merged" with a live branch preview on medizininformatik-initiative.github.io
(09:44Z), and three follow-up work packages applied (17:50Z) (`gh pr view 36 --json comments`).
This is the proof that (i) the FGDH toolkit + template is already running inside the MII org on a
real module, (ii) DE-first is the confirmed direction there, and (iii) the owner-interaction model
(instructions via PR, nothing merged without the owner) works.

---

## Synthesis for the Consent plan (INFERENCE, flagged as such)

- **Toolkit choice:** the wiki names both toolkits; the MII skill is a stale (2026-04-28,
  EN-primary, floating template pin) knowledge doc by a third party (Debertshäuser/BIH), while the
  FGDH pipeline is current (v0.25.0), DE-first-proven (Dokument #36), and already produced this
  module's own 18/18-routed sandbox. Use FGDH `mii-ig-migration`; mine the MII skill's
  tag-replacement tables as a cross-check reference only.
- **The Consent owner is NOT building 2027 guides** (unlike Studie) — the migration would arrive
  on a greenfield 2027 surface, but that also means no owner momentum to attach to: the D-0
  contact (Stäubert, cc Bialke/TF CU) carries more of the project risk here than it did for
  Studie.
- **Moving target:** develop churns in exactly the fingerprint area (category slices, #124,
  2026-08-21); pin the source commit at execution time and re-run the release-fingerprint
  measurement — do not reuse the sandbox's rc-4 finding.
- **The one hard technical blocker known in advance:** the parent package
  `de.einwilligungsmanagement` needs snapshots (2.0.3-snapshots was a local-only rebuild; CI
  cannot resolve it — sandbox D4). The plan needs a CI-resolvable answer (prebuild step, vendored
  rebuilt parent, or registry) before Gate D.
