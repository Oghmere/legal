# Legal documents — authoring & the language axis

Canonical legal text lives here and is baked into a typed module
(`src/legal/content.generated.ts`) by `scripts/generate-legal.mjs`. Consumers import the
built content via `@oghma/shared-admin/legal` — one reviewed source for oghma, oghma-web and
gaia (oghma-shared#110, design oghmere-design#9).

## Layout

- **English (canonical):** `legal/<doc>.md` — e.g. `legal/privacy-policy.md`. These paths are
  the source of truth and never move.
- **Translations:** `legal/<lang>/<doc>.md`, using the **same filename** as the English
  document — e.g. `legal/fr-CA/privacy-policy.md`. `<lang>` is a BCP-47 tag.
- **`versions.json`** — the effective-date map, keyed by document. Flat and English-dated;
  it is what the public mirror tags from and what oghma's consent guard parses. Its shape is
  unchanged by the language axis.
- **`translations.json`** — the registry of available translations, keyed by language:
  ```json
  { "fr-CA": ["terms", "privacy"] }
  ```
  Listing a `(language, document)` pair here (and dropping the matching
  `legal/<lang>/<doc>.md` file) is all it takes: the codegen picks it up, `LEGAL_DOCS_BY_LANG`
  gains the language, and the mirror tags it. No consumer code changes.

## Consuming the language axis

`LEGAL_DOCS[key]` is unchanged — it is still the English string. The language axis is
additive:

- `LEGAL_DOCS_BY_LANG[key][lang]` — markdown keyed by document then BCP-47 language. Every
  document always carries `en`.
- `resolveLegalDoc(key, lang)` — returns `{ text, language, requestedLanguage, fellBack }`.
  A missing `(document, language)` pair resolves to English with `fellBack: true`, so a
  caller can render a "shown in English" notice (oghma#5455). The fallback is **observable**,
  never silent.

## Is a translation a new consent version?

**No.** A translation of *unchanged* English text does not create a new consent version and
does not fire re-consent. The English effective date in `versions.json` is authoritative and
unchanged, so a translation inherits it — which is why `translations.json` carries no
per-language dates. This is consistent with the entity-identifier-correction precedent
(oghma-shared#174): text that does not change the substance of what a user agreed to does not
re-arm the consent gate.

This is a **mechanism** decision, not a legal one. If counsel later decides a given
translation *is* materially different, the language axis is exactly what makes that
expressible — bump the affected document's English effective date (which re-consents everyone)
or introduce a per-language date at that point. Until then, translations are a content drop
into an existing shape, not a consent event.

## Mirror

`.github/workflows/mirror-legal.yml` publishes this tree one-way to `Oghmere/legal` on
release. It tags each `(document, date)` as `<doc>/<date>` (unchanged, never moved) and, for
the language axis, `<doc>/<lang>/<date>` — so a `consent_records` row resolves to exactly one
immutable blob. English is tagged under both the legacy `<doc>/<date>` scheme and the new
`<doc>/en/<date>` scheme.
