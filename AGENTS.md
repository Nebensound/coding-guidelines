# Working with the guidelines and changing them

This repository holds the Nebensound Coding Guidelines. This file has two
parts: how to work with the guidelines, and how to change them. The model of the
content is described in [`README.md`](README.md).

## Working with the guidelines

### Find what applies

- Read the rules whose `languages` and `repositories` fit the case, as described
  in [Fields of a rule](README.md#fields-of-a-rule). An absent field fits every
  value; within a field one value must fit, between fields all must.
- A rule without `repositories` holds wherever a member of the organization
  works, someone else's project included. How the named places nest, and what
  changes in a sandbox or under a personal account, is described in
  [Where a rule holds](README.md#where-a-rule-holds).
- Only a rule binds, by its `level`. Definitions, principles and the text of
  reading pages explain and demand nothing.
- The reading pages in [`pages/`](pages) show the rules in context.

### Cite a rule

- Cite a rule by its identifier and its name, `R0042 (coverage-gate)`; only the
  number counts. From outside, use the permanent address described in
  [Identifiers](README.md#identifiers).

### Name the version

- Work that is checked against the guidelines names the version of the
  guidelines it was checked against.

## Changing the guidelines

The rules below apply to every change, whoever makes it.

- One rule states one requirement. If a sentence holds two requirements that can
  be followed or violated separately, it is two rules.
- A rule states its rationale in `rationale`: the failure it prevents or the
  property it secures. A rationale that only says "best practice" is not one.
  Keep rules decidable; if two people would not agree whether a change meets
  it, it is a principle, not a rule.
- An identifier is never reused, renamed or removed once a tagged version
  contains it. A retired item stays as a file with `reason` and, where an item
  of the same kind took its place, `replaced-by`.
- A new rule gets a place on a reading page in the same change.
- What a change does to an item (`stricter`, `added`, `relaxed`, `retired`,
  `announced` or `editorial`) follows from the fields of the item, as described
  in [What a change does to an item](README.md#what-a-change-does-to-an-item).
  For the `statement` of a rule, `applies-when`, `except` and the `text` of a
  definition or a principle, the type of the title claims it, and review judges
  the claim.
- The type of the title names the kind, as described in
  [The title of a pull request](README.md#the-title-of-a-pull-request): `rule!`
  for `stricter`; `rule`, `relax`, `retire` or `announce` for `added`,
  `relaxed`, `retired` or `announced`; any other type for `editorial`. The title
  is at least as strict as what the fields show. The marker `!` stands only in
  `rule!`. The type `feat` is not used.
- A pull request changes items in one way, as described in
  [One kind per pull request](README.md#one-kind-per-pull-request).
- Once branches named `pre` in front of `main` exist, the recommended way is one
  pull request per change against `pre`, landed in `main` together, as described
  in
  [Through a branch in front of `main`](README.md#through-a-branch-in-front-of-main).
  Until then every pull request goes to `main`.
- From `1.0.0` on, an incompatible step (a stricter rule, or a new rule that
  binds what exists) is announced in an earlier version, by `next` or by
  `status: planned`, and binds from the major version that switches it on.
  Below `1.0.0` nothing has to be announced: a stricter step binds from the
  version that carries it, and `next` and `status: planned` stay available but
  nothing requires them. Relaxing and retiring need no announcement.
- An announcement raises the patch version, under the type `announce`. The pull
  request that fulfils it carries the weight: `rule` when the rule does not bind
  what exists, `rule!` when it does.
- `next` announces a step and changes nothing by itself. The pull request that
  brings the version named in `from` takes the step: it rewrites `level` and
  `existing` to what `next` announced and removes `next`, and the fields show
  it as `stricter`. The check fails while a rule carries a `next` whose `from`
  is not above the current version, so the step is either taken or its `from`
  is moved.
- An item is one YAML file, `<folder>/<identifier>.yaml`, and validates against
  the schema of its kind; the front matter of a page source validates against
  `page.json`. An editor with the YAML language server checks item files while
  writing, through the mapping in `.vscode/settings.json`; the extension behind
  it is recommended in `.vscode/extensions.json`. A field every kind shares is
  changed in `item.json`, not in the schema of a kind. A value of
  `languages` or `repositories` is added to the schema by the pull request that
  brings the first item needing it.
- Reading pages in `pages/` are never edited by hand; they are generated from
  `pages-src/`.
- Nothing internal is named: no private repositories, internal hosts, internal
  services, credentials or customers, in files, commits, pull requests, issues
  or comments. Describe a need generically.
- Everything is English. Commit messages and pull request titles are
  Conventional Commits. Files follow the repository's Prettier configuration and
  Markdown its markdownlint configuration; run both over the changed files
  before pushing.
