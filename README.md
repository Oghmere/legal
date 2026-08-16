# Oghmere — official legal documents

This repository holds the **authoritative text** of the legal documents governing the Oghmere
service, and the full history of every change made to them.

Oghmere is operated by **1600978 B.C. LTD.**, a company incorporated under the *Business
Corporations Act* (British Columbia) and carrying on business as Oghmere, with a registered
office at Suite 1008, 3003 Grandview Hwy, Unit 1, Vancouver, BC, Canada V5M 2E4.

## The documents

| Document | File | Governs |
|---|---|---|
| Terms of Service | [`legal/terms-of-service.md`](legal/terms-of-service.md) | your agreement with us |
| Privacy Policy | [`legal/privacy-policy.md`](legal/privacy-policy.md) | what we collect and why |
| Acceptable Use & AI Policy | [`legal/acceptable-use-policy.md`](legal/acceptable-use-policy.md) | what you may and may not do |
| DMCA Policy | [`legal/dmca-policy.md`](legal/dmca-policy.md) | copyright notices |
| Plain-language summary | [`legal/plain-language-summary.md`](legal/plain-language-summary.md) | the above, in English |

The plain-language summary is **not** binding. Where it and a binding document disagree, the
binding document governs.

## Why this repository exists

Policy pages usually change silently. You are told the terms were updated; you are rarely told
what changed, and almost never shown.

The point of this repository is not the files — it is the **diff**. Every change to our legal
text is a commit with an author, a date and a readable difference. You can answer "what did
they change, and when" for yourself, without an account and without taking our word for it.
That is the whole idea, and it is why every change is published as a commit rather than applied as
a silent update.

## Finding the version that applies to you

Each published version of a document is tagged, so a version can be resolved to the exact
immutable text it refers to:

```
terms/2026-08-16
privacy/2026-07-31
aup/2026-07-17
dmca/2026-07-18
```

When you accept our terms, we record the version you accepted. That string maps directly to a tag
here — `git show terms/2026-08-16:legal/terms-of-service.md` prints exactly what you saw. Tags are
never moved once published, and every change from this point forward is a commit you can read.

`legal/versions.json` records the current published version of each document.

## Raising a concern

Write to **legal@oghmere.com**. If you believe a document is unclear, misleading, or contradicts
something we have said elsewhere, we would rather hear it than not — that is the point of
publishing this at all.

Issues and pull requests are closed here, because this repository is a publication rather than a
working copy and a change made here would not reach the documents we actually serve. Email
reaches a person; a pull request would not.

For copyright notices, see the DMCA policy. For abuse reports, **abuse@oghmere.com**.

## Current status

These documents carry a **"Beta — pending legal review"** banner. That banner is accurate and is
there deliberately. The text is under review by counsel and may change before general
availability. We publish it anyway, in this form, because showing you a draft honestly labelled
as a draft is more useful than showing you nothing.
