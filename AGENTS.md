# Working with the guidelines and changing them

This repository holds the Nebensound Coding Guidelines. This file has two parts
that last: how to work with the guidelines, and how to change them.

## Working with the guidelines

### Find the pages that apply

- The [index](README.md#index-of-pages) lists every page.
- A page applies to a case as described in
  [Pages and their header](README.md#pages-and-their-header): by its
  `languages` and `repositories` fields. Read every page that applies to the
  languages and the kind of repository of the case.

### Cite a rule

- Cite a rule by its identifier, as described in
  [Citing a rule](README.md#citing-a-rule).

### Name the version

- Work that is checked against the guidelines names the version of the
  guidelines it was checked against.

## Changing the guidelines

The rules below apply to every change, whoever makes it.

### One mechanism, one place

- A mechanism, a term or a requirement is described in exactly one place. Every
  other page cites it by its identifier, as described in
  [Citing a rule](README.md#citing-a-rule).
- Do not repeat a rule in a second page "for convenience". A copy drifts, and
  then two pages say different things.
- A page covers one topic. Put a rule on the page of its topic and do not
  create a page for a single rule.
- When a page is moved, or a rule is merged into another one or dropped, every
  citation of it is updated in the same change: to the new place, to the rule it
  was merged into, or removed together with the text that relied on it.

### An identifier is never renamed or removed

- A new rule gets its identifier with its heading. Identifiers follow
  [Citing a rule](README.md#citing-a-rule): once on `main`, an identifier is
  never renamed or removed, and a merged or dropped rule is entered in
  `identifiers.toml`. A retired identifier is never reused.

### A new page arrives with its header

- A new page starts with the front matter described in
  [Pages and their header](README.md#pages-and-their-header), including how a
  new value of `languages` or `repositories` is added and how the header is
  validated.
- A new page is entered in the [index](README.md#index-of-pages) in the same
  change, and the row of a moved or removed page changes with it.

### A new rule names its reason

- Every new or stricter rule states why it exists: the failure it prevents or
  the property it secures.
- A rule without a reason is not added. A reason that only says "best
  practice" is not a reason.
- Keep rules checkable. If nobody can tell whether a change follows the rule,
  rewrite it until somebody can.

### A deviation names scope, reason, risk and migration target

A deviation from a rule, in this repository or in a project that follows it, is
written down with:

- **Scope**: what exactly deviates, and where.
- **Reason**: the technical or domain reason that makes the rule unworkable.
- **Risk**: what the deviation costs or endangers.
- **Migration target**: how and when the deviation ends, or why it cannot.

A deviation that does not name all four is not a deviation but a violation.

### Nothing internal is named

This repository is public.

- Do not name, link or quote private repositories, internal hosts, internal
  services, credentials or customers, in files, commits, pull requests, issues
  or comments.
- Describe a need generically. A rule must be understandable and usable by
  someone outside the organization.

### Language and format

- Everything is English: documents, comments, commit messages, pull requests,
  issues.
- Markdown follows the repository's Prettier and markdownlint configuration.
  Run both over the changed files before pushing.
- Commit messages and pull request titles are Conventional Commits.
