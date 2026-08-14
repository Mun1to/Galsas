# Galsas

A Claude Code skill that audits the **legal hygiene of a software product** by reading the
repository, and writes a `LEGAL.md` with what you are breaking today, ranked by severity, each
finding carrying its article, its official link and the concrete fix in your code.

**Scope: Spain and the EU.** The AI Act module applies to anyone shipping into the European market;
the consumer, cookie and tax modules are Spanish law. If you sell from elsewhere, treat those as a
checklist of questions, not answers.

**This is not legal advice**, and the skill says so in every report it writes. It finds problems and
tells you which ones need an actual lawyer.

## Install

Inside Claude Code, two lines:

```
/plugin marketplace add Mun1to/Vibeset
/plugin install galsas@vibeset
```

<details>
<summary>Prefer to install it by hand?</summary>

```bash
git clone https://github.com/Mun1to/Galsas.git
ln -s "$(pwd)/Galsas" ~/.claude/skills/galsas
```

On Windows, with PowerShell:

```powershell
New-Item -ItemType Junction -Path "$env:USERPROFILE\.claude\skills\galsas" -Target "C:\path\to\Galsas"
```
</details>

## Use it

Ask for it in plain words: "revisa lo legal antes de publicar", "¿esta licencia me deja cobrar?",
"¿tengo que avisar de que es una IA?", "¿necesito banner de cookies?", or run `/galsas`.

It starts by reading your repo, not by asking you questions: dependencies, forms, payment flow,
where data ends up, whether anything talks to a person or generates content. Then it only audits the
modules that actually apply.

## What it covers

| Module | What it catches |
|---|---|
| **AI Act, article 50** | Missing "you're talking to an AI" notice, unlabelled synthetic content, and the exemptions that mean you owe nothing, the part no summary gets right |
| **Dependency licences** | Copyleft (GPL, AGPL) inside a commercial product, source-available licences that ban SaaS, `UNKNOWN` licences, missing attribution files, statically linked LGPL |
| **GDPR and LSSI** | Legal notice fields, privacy policy vs. the destinations actually present in the code, cookie banner rules, analytics writing before consent, marketing email, minors |
| **Consumer sales** | Withdrawal rights for digital products, the payment button wording that decides whether the contract binds at all, price-with-tax, reviews, auto-renewal notice |
| **Accessibility** | European Accessibility Act, e-commerce, and the microenterprise exemption that most guides forget exists |

## Why it is different from asking an AI "is this legal?"

Because the failure mode of that question is a confident, well-formatted answer copied from blog
posts. This skill is built around not doing that:

- Nothing is asserted without a link to the **official** source: BOE, EUR-Lex, AEPD, the Commission.
- Articles are cited by number, so you can check the claim in ten seconds.
- Bills in progress are never presented as law in force.
- Everything that could not be verified goes into its own section of the report, with the URL where
  to check it. An honest list of holes beats a complete-looking report that invented the gaps.
- Every reference file carries a verification date, and stale data must be re-checked before use.

It also ships the two corrections that catch almost everyone: the LSSI fines everybody quotes come
from a **repealed** decree, and the EU online dispute platform everybody links to **shut down in
July 2025**.

## The cheap fixes it always proposes

1. The AI notice lives **inside the chat component**, not in your terms.
2. Everything generated leaves the product through **one export function**, so signing it later is a
   patch and not a rewrite.
3. Log **which model produced what, and when**. Free on day one, impossible to reconstruct later.

## License

MIT, see [LICENSE](LICENSE).

> **ES:** Esto no es asesoramiento jurídico. Es una revisión técnica que lee tu repositorio y te
> dice qué incumples hoy, con el artículo y el enlace oficial de cada cosa, y qué tienes que
> preguntarle a un abogado de verdad.
