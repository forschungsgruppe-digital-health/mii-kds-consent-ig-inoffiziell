# Recon: Migration TARGET — mii-kds-module-template v0.13.2 (+ ig-template-mii-kds v1.3.4)

Date: 2026-08-31 · Analyst: Claude (subagent) · ANALYSIS ONLY, read-only on all upstream repos.

**Clone under measurement:** `/private/tmp/claude-503/-Users-marcel-Development-cross-hub-patientportal/9e6d07a4-6adb-4483-b4c7-d44df6dc83fb/scratchpad/recon/template` — created with `git clone --depth 1 --branch v0.13.2 https://github.com/medizininformatik-initiative/mii-kds-module-template`. HEAD = `a2390dea3eacf8139b2231713510f38fa558dad5` ("chore(main): release 0.13.2 (#26)", 2026-08-31 17:03:36 +0200). All `file:line` references below are relative to this clone unless marked otherwise.

**Verification run (MEASURED):** on the clone, `node --test scripts/*.test.mjs` (Node 22 via nvm) → **107 tests, 107 pass, 0 fail**; `node scripts/convention-check.mjs` (dev mode) → `Result: PASS — no hard violation.`

---

## a. What changed v0.13.1 → v0.13.2 — the M6 prerelease fix (Studie-plan gate: CLEARED)

**Release:** v0.13.2 published **2026-08-31T15:03:47Z** (MEASURED: `gh release view v0.13.2 --repo medizininformatik-initiative/mii-kds-module-template`). Release body / `CHANGELOG.md:3-8`: exactly one change — *"fix(convention-check): M6 accepts CalVer prerelease suffixes (#25)"*, commit `3db9de0`.

**Full file delta v0.13.1...v0.13.2** (MEASURED via `gh api repos/…/compare/v0.13.1...v0.13.2`): only 4 files — `.release-please-manifest.json`, `CHANGELOG.md`, `scripts/convention-check.mjs`, `scripts/convention-check.test.mjs`. Nothing else moved.

**The commit message of `3db9de0`** (MEASURED, from the compare API) names the exact contradiction and the trigger:
> The template contradicts itself three ways about prerelease versions: convention-check.mjs:194 rejected every suffix (`^\d{4}\.\d+\.\d+$`); docs/recipes/create-a-new-module.md sanctions '2027.0.0-draft.1'; go-publish.yml's version gate accepts `^[0-9]+\.[0-9]+\.[0-9]+([-.][0-9A-Za-z.-]+)?$`. **Real-world trigger: kerndatensatz-dokument migrates onto this template at its published ballot version 2027.0.0-ballot.rc1, which M6 rejected** …

**Current M6 code** (`scripts/convention-check.mjs:192-195`):

```js
field("M6 version", readTopLevel(sushiConfig, "version"), (v) => {
  if (isPlaceholder(v)) return { ok: true, parameterized: true };
  return { ok: /^\d{4}\.\d+\.\d+(-[0-9A-Za-z.-]+)?$/.test(v), parameterized: false, reason: "version must be CalVer YYYY.n.n with an optional prerelease suffix, e.g. 2027.0.0-draft.1 (modules never use SemVer)" };
});
```

**Regression test** (`scripts/convention-check.test.mjs:134-141`):

```js
test("a CalVer prerelease suffix passes M6 (create-a-new-module.md and go-publish.yml both sanction it)", () => {
  const rc = CONCRETE.replace('version: "2026.0.1"', 'version: "2027.0.0-ballot.rc1"');
  const { findings } = evaluate({ sushiConfig: rc, igIni: CONCRETE_IGINI, release: false });
  assert.ok(!ids(findings, "fail").includes("M6 version"));
  const draft = CONCRETE.replace('version: "2026.0.1"', 'version: "2027.0.0-draft.1"');
  …
```

**Conclusion (MEASURED):** the upstream fix from template issue #24 / PR #25 that the Studie plan was gated on is merged and released. Prerelease CalVer (`2027.0.0-ballot.rc1`, `2026.0.0-rc.1`, …) passes M6; plain SemVer (`1.2.3`) still fails (the `\d{4}` year block). `go-publish.yml:312` independently accepts `^[0-9]+\.[0-9]+\.[0-9]+([-.][0-9A-Za-z.-]+)?$` — note it also allows a `.`-introduced suffix, slightly wider than M6's `-`-only.

---

## b. All convention checks (M1–M11, T1–T4) at v0.13.2 — and Consent pass/fail

One line each, from `scripts/convention-check.mjs` (the single metadata checker; `convention-check.yml:2-15` forbids a second linter):

| Check | Semantics | Evidence | Consent (`modul-consent`, see below) |
|---|---|---|---|
| M1 packageId | must be `de.medizininformatikinitiative.kerndatensatz.` + `[a-z0-9-]+` | mjs:148-149 | PASS (`…kerndatensatz.consent`) |
| M2 id | must be `mii-ig-` + `[a-z0-9-]+`, ≤64 chars | mjs:151-155 | PASS (`mii-ig-consent`) |
| M3 name | must be `MII_IG_` + `[A-Za-z0-9_]+` | mjs:157-158 | PASS (`MII_IG_Consent`) |
| M4 title | must start `MII ` | mjs:160-163 | PASS |
| M5 canonical | `https://www.medizininformatik-initiative.de/fhir/` + module, accepting **three spaces**: bare `…/fhir/<module>`, `…/fhir/ext/<module>`, `…/fhir/core/<module>` (widened in v0.11.2, PR #167 — VERIFIED still present at v0.13.2) | mjs:166-190; tests test.mjs:44-74 | PASS in the **bare** space |
| M6 version | CalVer `YYYY.n.n` + optional `-<prerelease>` suffix (see §a) | mjs:192-195 | PASS (both `2026.0.0` and `2027.0.0-ballot.rc1`) |
| M7 no floating pins | no dependency/`ig.ini template` may be `#current/#latest/#dev/#cibuild` (label set deliberately mirrored in go-publish.yml:283); in `--release` mode a `TODO` template also fails | mjs:197-216, FLOATING regex mjs:88 | PASS (interim URL template line is not floating) |
| M8 demo page | `input/pagecontent/rendering-artifacts.md` present = pass in dev, **fail on release** (must delete page + de mirror + pages: entry + both menu entries + `demo/` + `scripts/gen-rendering-demo.py` + demo-en/de.md + rendering-demo-codes.json) | mjs:222-244, main() mjs:472-474 | n/a — migration deletes it (skill step 3) |
| M9 optional pages | `OPTIONAL-PAGE` marker: asymmetric en/de = fail always; both-marked = pass in dev, fail on release (decide keep/remove per docs/optional-pages.md) | mjs:28, 246-277, scan mjs:358-379 | decision work, not a blocker |
| M10 duplicate headings | first in-page heading repeating the page title, or a heading repeating its parent = fail | mjs:279-286, scan mjs:404-464 | content-dependent |
| M11 illustrative examples | `ILLUSTRATIVE-EXAMPLE` marker (e.g. Person example in security-and-privacy.md): same semantics as M9 | mjs:33, 289-315, scan mjs:382-401 | decision work |
| T1–T4 | template-package repo only (`package/package.json`: name/type/SemVer/pinned base) — **skipped** for a module (no root `package/package.json`) | mjs:317-334 | skip |

**MEASURED simulation with Consent values** (run on the clone, Node 22, `evaluate()` imported directly; sushi fixture: `id: mii-ig-consent`, `canonical: https://www.medizininformatik-initiative.de/fhir/modul-consent`, `name: MII_IG_Consent`, `title: MII Implementation Guide Consent`, `packageId: de.medizininformatikinitiative.kerndatensatz.consent`, ig.ini `template = https://github.com/medizininformatik-initiative/ig-template-mii-kds`, **release mode**):

```
== version 2026.0.0            release-mode ok: true   (M1..M7 all pass)
== version 2027.0.0-ballot.rc1 release-mode ok: true   (M1..M7 all pass)
```

**Which canonical space Consent needs, from the check's perspective:** M5 accepts all three spaces, so the check imposes nothing — but the scaffold and go-publish are shaped for the **bare** space: `sushi-config.yaml:84` templates `…/fhir/modul-{{MODULE_SLUG}}`, the package-source extension repeats it (`sushi-config.yaml:152`), and `go-publish.yml:102` hardcodes `EXPECTED_CANONICAL: "https://www.medizininformatik-initiative.de/fhir/modul-{{MODULE_SLUG}}"`. The pinned context says Consent's canonical is `…/fhir/modul-consent` (bare) — that drops straight in with `MODULE_SLUG=consent`, no manual edits. (Had it been `ext/`/`core/`, `EXPECTED_CANONICAL` and both sushi-config canonical lines would need hand edits; M5 itself would still pass. Confirming from the consent source repo is the source-recon task's job — from this side: NICHT WEITER GEPRÜFT here.)
Per the M5 comment (mjs:166-174), the measured census 2026-08-27 was ext ×14, core ×7, bare ×5; which space a module uses is TF-KDS governance, not the check's business.

---

## c. DE-first: what the scaffold defaults to, and exactly what a DE-FIRST module must patch at v0.13.2

**Scaffold default = EN-default with a German mirror (MEASURED):**
- `sushi-config.yaml:391` — `i18n-default-lang: en`; `:392-393` `i18n-lang: - de`; `:394-395` `translation-sources: - input/translations/de`.
- English source pages under `input/pagecontent/` (23 .md files), German mirror under `input/translations/de/pagecontent/` (same set), German menu `input/translations/de/includes/menu.xml`, IG-level `.po` catalogue `input/translations/de/ImplementationGuide-mii-ig-{{MODULE_SLUG}}.po` (file tree of the clone).

**The 3 CI files a DE-first flip (`i18n-default-lang: de`) must patch — all three exist at v0.13.2 under exactly these names:**

1. **`scripts/language-model-check.sh`** (113 lines — the current name; it exists at v0.13.2 and is run by `convention-check.yml:106-107`). Its entire premise is EN-default (header lines 2-9: *"This IG renders in ENGLISH by default … Prose that calls German the default … fails here"*). The curated `PATTERNS` (lines 34-47) that a DE-first module trips **by configuration alone**:
   - line 46: `'input/translations/en([^A-Za-z]|$)'` — a DE-first module's `translation-sources: - input/translations/en` in sushi-config.yaml is a guaranteed hit (`git grep` scans all tracked text files; only `input/translations/de`, `ig-template/`, and the script itself are excluded, lines 59-62).
   - line 42: `'(^|[^A-Za-z])de-default([^A-Za-z]|$)'` and line 43 `'back to en-default'` — fire on any prose describing the DE-first model in those words.
   - The remediation heredoc (lines 96-109) states "There is no input/translations/en/" — must be rewritten/inverted for DE-first, and the exclusion at line 60 must become `:(exclude)input/translations/en`.
2. **`scripts/convention-check.mjs`** — every hardcoded de-path flips to en (MEASURED grep, all occurrences): scan dirs `:361` and `:385` (`input/translations/de/pagecontent` in `scanOptionalPages`/`scanIllustrativeExamples`), `.po` lookup `:424` + `:427` (`input/translations/de/ImplementationGuide-*.po` for German page titles in `scanDuplicateHeadings`), dirs array `:435` + `:437` (`input/translations/de/pagecontent`, `input/translations/de/intro-notes`), plus message prose `:235`, `:238`, `:271`, `:309` (M8/M9/M11 removal instructions naming the de mirror).
3. **`scripts/convention-check.test.mjs`** — the tests that pin those paths: `:211` and `:214` (M8 message must name `input/translations/de/pagecontent/rendering-artifacts.md` and `input/translations/de/includes/menu.xml`), `:239` (M9 message substrings incl. `input/translations/de/pagecontent`), `:289` (M11 message substrings).

**Why it must be ONE commit (VERIFIED at v0.13.2):** the push/PR workflow `convention-check.yml` runs `node --test scripts/*.test.mjs` **first** (`:70-71`), then `node scripts/convention-check.mjs` (`:100-101`), then `bash scripts/language-model-check.sh` (`:106-107`) — on push + pull_request to dev/main/release/** (`:36-40`). Patching the checker without its tests fails step 1; patching prose without the language script fails step 3. This matches the Dokument/Studie precedent exactly.

**Not part of the patch (VERIFIED):** `scripts/publication-url-consistency.template-test.mjs:78` asserts `i18n-default-lang: en` — but `*.template-test.mjs` runs **only** when the repo name ends `/mii-kds-module-template` (`convention-check.yml:76-78`), so a migrated module never executes it. `scripts/self-check-substitute.test.mjs` builds its own synthetic de-tree fixtures (`:41-51`) and does not read the repo's language layout — it keeps passing untouched (and `self-check-substitute.sh` itself only ever runs on the template repo, `ig-publisher.yml:165`).

Beyond CI, the DE-first content flip itself (pages swapped, menu.xml languages swapped, `.po` direction, sushi-config `:391-395`) is migration content work — the skill's business, not a template patch.

---

## d. Toolchain pins at v0.13.2 — versions, hashes, and where each pin lives

| Pin | Value | Where (evidence) |
|---|---|---|
| IG Publisher | **2.3.2** | `env: PUBLISHER_VERSION` in `ig-publisher.yml:104`, `go-publish.yml:110`, `module-release.yml` (env block), `release-demo.yml` (template-only) |
| Publisher jar SHA-256 | `07c576024df917cc1f879b6b5a64147cd0222d5b4129688e8f0ad9ccce58b1d5` | `ig-publisher.yml:105`, `go-publish.yml:111`; checked at download `ig-publisher.yml:277-279` |
| SUSHI | **3.20.1** | same env blocks (`ig-publisher.yml:106`); 5th copy: `validation.yml` reusable-workflow input `vars.SUSHI_VERSION || '3.20.1'` (asserted by `toolchain-pins.test.mjs:63-77`); dev container `postCreateCommand` `fsh-sushi@3.20.1` (`devcontainer.json:72`) |
| Jekyll | **4.4.1** | same env blocks (`ig-publisher.yml:107`); dev container `devcontainer.json:72` |
| Jekyll **gem** SHA-256 | `4c1144d857a5b2b80d45b8cf5138289579a9f8136aadfa6dd684b31fe2bc18c1` | **only** `go-publish.yml:114` (verified at `:454-456`); explicitly *"covered by no test and not watched by the checker"* — a Jekyll bump missing this checksum fails only at go-publish (`docs/maintenance.md:42`) |
| Ruby | `3.3` (CI floats patch); dev container exact-pins **3.3.12** | `ruby/setup-ruby` steps (`ig-publisher.yml:143-146`); `devcontainer.json:47-49`; go-publish deliberately uses system Ruby (`docs/maintenance.md:43`) |
| JDK for the publisher | temurin **17** | `ig-publisher.yml:133-137`; dev container image `mcr.microsoft.com/devcontainers/java:17-bookworm@sha256:de66e2…` (`devcontainer.json:34`) |
| HL7 validator (comparison demo, template-repo only) | 6.5.7 + SHA-256 `e9ee13…` | `ig-publisher.yml:305-306` |
| nginx tx-proxy image | `nginx:1.30.4-alpine@sha256:97d490c…` | `ig-publisher.yml:244` (same digest in module-release/go-publish per `docs/maintenance.md:48`) |
| SU-TermServ proxy `nginx.conf` | `kerndatensatz-meta` @ commit `1db2e534704d92e5ee0cde663ce3e7ccd8825fa7` | `ig-publisher.yml:231` |

**The "4 pin blocks" doctrine (VERIFIED):** a workflow cannot read another workflow's `env:`, so `PUBLISHER_VERSION` / `PUBLISHER_SHA256` / `SUSHI_VERSION` / `JEKYLL_VERSION` are declared **four times** — `go-publish.yml`, `ig-publisher.yml`, `module-release.yml`, `release-demo.yml` (template-repo-only; the bootstrap removes it, which the test tolerates) — and `scripts/toolchain-pins.test.mjs:17-61` fails the build the moment any two blocks disagree; `:63-77` additionally ties `validation.yml`'s SUSHI fallback literal to them. The prose side is `docs/maintenance.md:31-50` ("Where each pin lives (single source of truth)"), which also lists what is watched by the Monday checker (`dependency-check.yml` + `scripts/check-updates.mjs`) vs. re-resolved by hand.

**`fhir-settings.json`** (`.github/fhir-settings.json:1-11`): allowlists exactly one server — `http://127.0.0.1:8090/fhir`, `authenticationType: none`, `allowHttp: true`, `allowPrivateNetwork: true`. Purpose (`ig-publisher.yml:280-284`): publisher ≥2.3.1 SSRF hardening refuses plain-HTTP/private-network `-tx` targets without it; inert on the tx.fhir.org path.

**tx endpoints + cert fallback (VERIFIED, `ig-publisher.yml:213-257`; same idiom in go-publish/module-release per their headers):** when all three secrets `SU_TERMSERV_CLIENT_CERT` / `_KEY` / `_PASSWORD` are set, CI starts a client-certificate nginx proxy (config pulled from kerndatensatz-meta at the pinned SHA) and uses `-tx http://127.0.0.1:8090/fhir` (= SU-TermServ). Otherwise it **falls back to `https://tx.fhir.org` with a `::notice`** — *"the build must not hard-fail without the cert; some MII-specific value sets may then not fully expand (a QA note)"* (`ig-publisher.yml:37-42`, `:253-256`).

---

## e. ig.ini template reference — interim URL confirmed; what a migrated module must DELETE

**Confirmed (MEASURED):** `ig.ini:42` — `template = https://github.com/medizininformatik-initiative/ig-template-mii-kds`. This is the **interim-URL scaffold default** (introduced in v0.12.0, `CHANGELOG.md:29-34`). `ig.ini:13-40` documents the three forms: (1) INTERIM repository URL — publisher fetches the repo zip of the **default branch = released `main`** at build time; (2) OFFLINE fallback `template = #ig-template` (the vendored folder, synced from the companion's `dev`); (3) ENDGAME `de.medizininformatikinitiative.template#<version>` once the package is registry-published. The interim URL is "the one sanctioned exception to strict pinning" (`ig.ini:36-40`); M7 and go-publish's gate (`go-publish.yml:283-291`) accept it, and reject only `#current/#latest/#dev/#cibuild` and `TODO`.

**Skill doctrine (agent-skills v0.25.0, VERIFIED at the tag):** `skills/mii-ig-migration/references/migration-spec.md:1442-1449` —
> **The migrated module carries NO vendored template copy (decision 2026-08-28).** … the interim form … is KEPT as-is. **Delete from the migrated module** … the `ig-template/` folder, `.github/workflows/sync-ig-template.yml`, `scripts/sync-ig-template.sh` and `scripts/resolve-ig-template-source.sh` — beside a URL reference a vendored copy is dead weight that goes stale invisibly, and check P1 reports the leftover as a divergence.

The template's own `sync-ig-template.yml:23-27` says the same for the endgame switch. `resolve-ig-template-source.sh` is used **only** by `sync-ig-template.yml` (MEASURED grep — `sync-ig-template.yml:60`, `:83`, plus docs), so it dies with the workflow. Provenance to record: both a `5.2 skeleton-vendored … ref=<module-template tag>` line and a `5.2 template-reference url=… release=<latest ig-template release>` line (`migration-spec.md:1450-1452`).

**Companion state:** ig-template-mii-kds latest release **v1.3.4** (2026-08-28T15:49Z, MEASURED via `gh release view` — sole change: "the gh-pages root is a generated plain index (#20)"). Note: the template's vendored `ig-template/package/package.json` still says `"version": "1.3.3"` (vendored from the companion's `dev`); irrelevant once the folder is deleted per doctrine, but it shows the mirror lag the doctrine exists to avoid.

---

## f. Scaffold inventory a migration consumes

**Placeholders:** 19 total — 15 ACTIVE, 4 OPTIONAL — full table in the `sushi-config.yaml:1-66` header. Key ones: `{{MODULE_SLUG}}` (drives packageId/id/canonical and is the **only placeholder appearing in FILE NAMES**), `{{MODULE_NAME}}`, `{{MODULE_TITLE}}`, `{{MODULE_DESCRIPTION}}`, `{{CALVER_VERSION}}`, `{{CALVER_YEAR}}`, `{{RELEASE_DATE}}` (go-publish requires = publication date, `sushi-config.yaml:104-105`), `{{COPYRIGHT_START_YEAR}}`, `{{APPROVAL_DATE}}`, `{{MODULE_AUTHOR_EMAIL}}`, `{{TOPIC_NCI_CODE}}`, `{{GITHUB_ORG}}`/`{{REPO_NAME}}`, `{{RELEASE_DESCRIPTION}}`, `{{REGISTRY_DESCRIPTION}}`; optional `{{SPECIAL_URL_1}}`, `{{CITATION_TEXT}}`/`{{CITATION_URL}}`/`{{CITATION_PUBLICATION_DATE}}`.

**The 3 placeholder-NAMED files that must be RENAMED as well as substituted** (`sushi-config.yaml:20-28`; all present in the clone's file tree):
- `input/translations/de/ImplementationGuide-mii-ig-{{MODULE_SLUG}}.po`
- `input/pagecontent/ImplementationGuide-mii-ig-{{MODULE_SLUG}}.md`
- `input/translations/de/pagecontent/ImplementationGuide-mii-ig-{{MODULE_SLUG}}.md`

**`pages:` structure** (`sushi-config.yaml:300-367`): the TF-KDS-agreed menu structure, one page per artifact type; OPTIONAL (0..1): researcher-guidance, extensions, search-parameters, operations, value-sets, code-systems, metadata (each marked in-file and gated by M9); the demo page `rendering-artifacts.md:366-367` (gated by M8). Every `title:` doubles as a msgid in the IG-level `.po` (`sushi-config.yaml:296-299`). MII-wide Conformance topics and "Datasets and Descriptions" are **menu links, not pages** (`:290-292`).

**menu.xml de/en:** `input/includes/menu.xml` (English source) + `input/translations/de/includes/menu.xml` (mirror) — the only way to a translated menu; never re-add `menu:` to sushi-config (`sushi-config.yaml:466-479`). "Conformance-statement machinery": the Conformance dropdown consists of **link-only entries to the kerndatensatz-meta wiki** (INTERIM until the Meta IG renders; switch documented as a Gate item — menu.xml header comment + Conformance block), plus the module's own `security-and-privacy.md` as the only Conformance-cluster page; capability statements have a scaffold page (`input/pagecontent/capability-statements.md`) + FSH slot (`input/fsh/capabilitystatements/.gitkeep`).

**Workflows** (`.github/workflows/`, 12 files): a module keeps `ig-publisher.yml` (branch preview → `gh-pages/branches/<branch>/`), `module-release.yml` (CalVer release), `go-publish.yml` (gated formal publication), `convention-check.yml`, `validation.yml` (MII reusable dotnet+java validation, SHA-pinned), `dependency-check.yml` (the check-updates Monday tracker), `security-scan.yml`, `cleanup-gh-pages.yml`; `sync-ig-template.yml` is **deleted per §e doctrine**. Template-repo-only (removed by `scripts/first-run-bootstrap.sh:174` in a created module; a migration must equally not carry them): `release-please.yml`, `notify-zulip.yml`, `release-demo.yml` + `release-please-config.json` + `.release-please-manifest.json` + `CHANGELOG.md`.

**.gitignore trap (VERIFIED still present):** `.gitignore:24` is the blanket `*.log` (under "OS / editor noise"), with no negation anywhere in the 24-line file — it **swallows `migration-log/*.log`**; a migration must add an un-ignore (e.g. `!migration-log/*.log`) or the run log never lands in git.

**Root `package.json`: DOES NOT EXIST at v0.13.2** (MEASURED: `ls package.json` → no such file; the only package.json is `ig-template/package/package.json`, which leaves per §e). `docs/maintenance.md:24` phrases Dependabot's npm coverage as "a root npm manifest (**when present**)", and `go-publish.yml:298-300` notes the canonical's single source of truth is sushi-config.yaml, deviating from basis "which duplicates it in a root package.json". A migration must not invent one.

**Skills doctrine:** `skills/` ships only two local skills — `wiki-consistency-check` (bound to convention-check.mjs) and `docs-steward` (`skills/README.md:13-17`). `skills/RETIRED.md` is the tombstone list: `ig-analyze`→`fhir-ig-analysis` and `ig-translate`→`fhir-ig-translation` moved to the FGDH catalog; vendored copies + the whole `sync-skills.sh`/`skills-lock.json`/`sync-skills.yml` machinery were removed 2026-08-28 (v0.13.0, "catalog skills install on demand"; `RETIRED.md:29-32`). Install pinned via `npx skills add …/tree/<release> --skill … --copy` — the `@ref` form silently does NOT pin (`RETIRED.md:41-45`).

**Other scaffold parts consumed:** `input/fsh/rulesets/` (crmi/version/publisher/license/meta-profile/translation… — versioned canonicals pinned by `{{CALVER_VERSION}}`), `input/resources/Parameters-expansion-manifest.json` (slug-free filename; resource id `mii-param-{{MODULE_SLUG}}-manifest`, must agree with `cqf-expansionParameters` + `path-expansion-params` + `pin-manifest`, `sushi-config.yaml:207-216, 431-443`), `qc/custom.rules.yaml`, `advisor.json` (QA suppressions), `publication-request.json`, `tests/profiles/` harness (commented out until placeholders in `tests/` are replaced, `sushi-config.yaml:457-464`), dependencies block pinned to basis parity: `de.basisprofil.r4 1.5.4`, `…kerndatensatz.meta 2026.0.0`, `hl7.fhir.uv.xver-r5.r4 0.1.0`, `hl7.fhir.uv.crmi 2.0.0`, `hl7.terminology.r4 7.3.0` (direct pin, deliberate), `hl7.fhir.uv.extensions.r4 5.3.0` (`sushi-config.yaml:246-270`).

---

## g. template-pages / template-artifacts manifests — the template does NOT ship them; the skill vendors them at stamp v0.11.1

**MEASURED:** the v0.13.2 tree contains **no** template-pages/template-artifacts manifest and no stamping machinery (grep across the clone: the only "manifest" artifacts are the FHIR expansion manifest and `.release-please-manifest.json`). The manifests the migration verifier consumes live **in the skill**: `skills/mii-ig-migration/references/template-pages.tsv` and `template-artifacts.tsv` in `forschungsgruppe-digital-health/agent-skills` **v0.25.0** (MEASURED via `gh api …?ref=v0.25.0`).

- `template-pages.tsv` header: *"Measured, not assumed: `input/pagecontent/` of medizininformatik-initiative/mii-kds-module-template **at tag v0.11.1**, read from the tag's tree on 2026-08-20"*; every data row's third column stamps `v0.11.1` (21 pages: 14 scaffold + 6 optional + 1 demo, with `ImplementationGuide-mii-ig-<slug>` matched by prefix in code).
- The **currency tripwire** (`migration-spec.md:2655`): verify-migration compares the manifest's measurement tag against the run-log `skeleton-vendored ref=`; on mismatch **C5c downgrades to NICHT PRÜFBAR** instead of judging against the wrong page set (the exact defect from the Studie try-run: manifest v0.10.3 vs vendored v0.11.0 → two false DIVERGIERT).
- **Consequence for a Consent migration vendoring v0.13.2:** the tripwire WILL fire (v0.11.1 ≠ v0.13.2) and C5c degrades — *however*, MEASURED via `gh api repos/…/compare/v0.11.1...v0.13.2`: 62 files changed, **zero under `input/`** and `sushi-config.yaml` untouched — the page set is byte-identical between the manifest's tag and v0.13.2. So the manifest content is correct; only the stamp is stale. Options for the plan: accept the documented C5c downgrade, or refresh the skill's manifests' tag column to v0.13.2 (a one-line-per-row skill update, content unchanged) before the run.
- `template-artifacts.tsv` header: one definition of the template's demo artefact tokens (`example-patient`, …) read by both `verify-migration.py` R4 and `autofix-fix.py` (`template-example-link`), so checker and fixer can never disagree about what a template example is.

---

## h. Release/preview machinery a migrated module inherits — and what a Consent migration must adjust

**Inherited and kept:**
- **`ig-publisher.yml`** (branch preview): builds every non-main branch, deploys to `gh-pages/branches/<branch>/`, upserts a preview-URL PR comment; serializes all gh-pages writers via concurrency group `gh-pages-writes` (`:92-96`). The `gen-pages-index.mjs` root-index generator is **guarded to the template repo** (`ig-publisher.yml:453-461`: `case "${REPO}" in */mii-kds-module-template)`) — in a module the site root stays reserved for go-publish output; the script + its test remain in `scripts/` but never run (harmless).
- **`module-release.yml`** (MII CalVer path): reacts to tag glob `v[0-9]+.[0-9]+.[0-9]+*` (accepts `v2027.0.0-ballot.rc1`), builds as buildability gate, attaches `package.tgz` to a DRAFT GitHub release (also feeds `scripts/seed-comparison-cache.sh` for version comparison), and on human publish announces to the MII Zulip **topic "Releases"** (module topic — distinct from the template repos' "Template Releases"; `module-release.yml:405-434`), skip-not-fail without `secrets.ZULIP_API_KEY`. A guard job self-skips while `{{…}}` placeholders remain (`:41-45`).
- **`go-publish.yml`** (formal publication, workflow_dispatch only, `publish:false` = full dry run): env gates `EXPECTED_CANONICAL: "https://www.medizininformatik-initiative.de/fhir/modul-{{MODULE_SLUG}}"` (`:102`), `EXPECTED_PUBLICATION_BASE: "https://{{GITHUB_ORG}}.github.io/{{REPO_NAME}}"` (`:105`, canonical-mismatch by design — never point the canonical at github.io, `sushi-config.yaml:81-84`), `EXPECTED_PACKAGE_ID: "de.medizininformatikinitiative.kerndatensatz.{{MODULE_SLUG}}"` (`:106`); version gate accepts prerelease (`:312`); template-pin gate rejects floating/TODO (`:283-291`); registry handoff is exported as a human-submitted patch; first publication uses `"first": true` in `publication-request.json` (header `:57-64`).
- **Removed** (template maintenance, `first-run-bootstrap.sh:174`): `release-please.yml`, `notify-zulip.yml`, `release-demo.yml`, both release-please JSONs, template `CHANGELOG.md`. A migration replicates this removal (a migrated repo is vendored, not "Use this template"-created, so the bootstrap's removal list is the checklist, not the mechanism).

**Consent-specific adjustments (all by placeholder substitution unless noted):**
- `MODULE_SLUG=consent` ⇒ `id: mii-ig-consent` (`sushi-config.yaml:76`), `packageId de.medizininformatikinitiative.kerndatensatz.consent` (`:99`), canonical `…/fhir/modul-consent` (`:84`) — matches the bare space, so `EXPECTED_CANONICAL` needs **no** manual edit (see §b caveat if the source turns out non-bare).
- The three `{{MODULE_SLUG}}`-named files renamed (§f); `pin-manifest: mii-param-consent-manifest` follows automatically (`sushi-config.yaml:443`).
- **`{{TOPIC_NCI_CODE}}` analog** (`sushi-config.yaml:233-237`): the artifact-topic NCI Thesaurus code has **no sensible default** ("an unreplaced value ships a bogus code", header `:44-49`); Consent needs its own topic code(s) — e.g. an informed-consent concept — a content decision to resolve at migration time, repeating the block per topic. NICHT PRÜFBAR here which code the Consent module should declare; the source IG carries no NCI topic to copy (template-only mechanism).
- `{{GITHUB_ORG}}`/`{{REPO_NAME}}` → the FGDH sandbox (`forschungsgruppe-digital-health/mii-kds-consent-ig-inoffiziell`) for the try-run; `publication-request.json` + go-publish env follow.
- Dependencies: Consent's real pins (basis version, meta, possibly no xver-r5.r4) replace the scaffold parity pins — M7 only cares they are fixed versions.
- Version: Consent's released `2026.0.0` (latest source release, pinned context) passes M6/go-publish both as-is and with any future prerelease suffix (MEASURED §b).

---

## Cross-cutting notables / traps for the plan

1. **The M6 gate the Studie plan waited on is released** (v0.13.2, released TODAY 2026-08-31) — migrations at prerelease CalVer are unblocked at the template level.
2. **Manifest-stamp mismatch is guaranteed** (skill v0.25.0 manifests stamped v0.11.1 vs target v0.13.2) → C5c NICHT PRÜFBAR unless the skill's manifests are re-stamped; page-set content is measured-identical, so re-stamping is safe.
3. **`.gitignore:24` `*.log`** still swallows `migration-log/*.log` — needs the un-ignore line, same as previous runs.
4. **DE-first remains a 3-file, one-commit CI patch** at v0.13.2 (names unchanged: `language-model-check.sh`, `convention-check.mjs`, `convention-check.test.mjs`); the template-only `publication-url-consistency.template-test.mjs` EN assertion does not bite in a module.
5. **Do not vendor `ig-template/`** and delete the 4-part sync machinery (folder + workflow + 2 scripts) — skill doctrine `migration-spec.md:1442-1449`; keep the interim URL `ig.ini:42` as-is.
6. **Zero-network caveat:** the interim URL template means every full IG build (CI and local) fetches the companion repo zip at build time; offline builds need the (deleted) vendored fallback — a deliberate trade the plan should state.
7. The **Jekyll gem SHA** (`go-publish.yml:114`) is the one pin no test watches — any toolchain bump in the migrated module must sweep it manually.
8. The whole workflow set is toggle-gated by repo variables (`ENABLE_CONVENTION_CHECK`, `ENABLE_PREVIEW`, `ENABLE_MODULE_RELEASE`, `ENABLE_ZULIP_ANNOUNCE`, `ENABLE_TEMPLATE_SYNC`, `ENABLE_DEPENDENCY_CHECK`, `ENABLE_SECURITY_SCAN`, `ENABLE_VERSION_COMPARISON`, `PAGES_ACTIONS_ENABLED`) — a sandbox repo can switch off Zulip/publication paths without YAML edits.
