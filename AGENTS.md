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
- A rule states its rationale: the failure it prevents or the property it
  secures. A rationale that only says "best practice" is not one. Keep rules
  decidable; if two people would not agree whether a change meets it, it is a
  principle, not a rule.
- An identifier is never reused, renamed or removed once a tagged version
  contains it. A retired item stays as a file with `reason` and, where an item
  of the same kind took its place, `replaced-by`.
- A new rule gets a place on a reading page in the same change.
- A pull request that touches an item adds a record of the change under
  [`changes/`](changes) that says, per item, whether it is `added`, `stricter`,
  `relaxed`, `retired`, `announced` or `editorial`, as described in
  [The record of a change](README.md#the-record-of-a-change). Its title fits the
  record, as described in [Versions](README.md#versions): `rule!` for a
  `stricter` entry; `rule`, `relax`, `retire` or `announce` for an `added`,
  `relaxed`, `retired` or `announced` one; any other type for `editorial` only
  or for a pull request without a record. The marker `!` stands only with a
  `stricter` entry. The type `feat` is not used.
- An incompatible step (a stricter rule, or a new rule that binds what exists)
  is announced in an earlier version, by `next` or by `status: planned`, and
  binds from the major version that switches it on. Relaxing and retiring need
  no announcement.
- Front matter validates against the schema of its kind. A value of `languages`
  or `repositories` is added to the schema by the pull request that brings the
  first item needing it.
- Reading pages in `pages/` are never edited by hand; they are generated from
  `pages-src/`.
- Nothing internal is named: no private repositories, internal hosts, internal
  services, credentials or customers, in files, commits, pull requests, issues
  or comments. Describe a need generically.
- Everything is English. Commit messages and pull request titles are
  Conventional Commits. Markdown follows the repository's Prettier and
  markdownlint configuration; run both over the changed files before pushing.
