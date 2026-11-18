# Changing the guidelines

This repository holds the Nebensound Coding Guidelines. The rules below say how
they are changed. They apply to every change, whoever makes it.

## One mechanism, one place

- A mechanism, a term or a requirement is described in exactly one place. Every
  other page cites it by its identifier, as described in
  [Citing a rule](README.md#citing-a-rule).
- Do not repeat a rule in a second page "for convenience". A copy drifts, and
  then two pages say different things.
- A page covers one topic. Put a rule on the page of its topic and do not
  create a page for a single rule.
- When a page is moved or a rule is dropped, every citation of it is updated in
  the same change.

## An identifier is never renamed or removed

- Every heading that states a citable rule carries an identifier, as described
  in [Citing a rule](README.md#citing-a-rule). A new rule gets its identifier
  with its heading.
- An identifier is never renamed and never removed. The wording of a heading may
  change.
- When a rule moves or is dropped, its identifier is entered in
  `identifiers.toml`, in the form that fits (`moved-to`, or `removed-since` with
  a `reason`).

## A new page arrives with its header

- A new page starts with the front matter described in
  [Pages and their header](README.md#pages-and-their-header) and passes
  `schemas/page.json`.
- A value of `applies-to` that the schema does not know yet is added to the
  schema in the same pull request.

## A new rule names its reason

- Every new or stricter rule states why it exists: the failure it prevents or
  the property it secures.
- A rule without a reason is not added. A reason that only says "best
  practice" is not a reason.
- Keep rules checkable. If nobody can tell whether a change follows the rule,
  rewrite it until somebody can.

## A deviation names scope, reason, risk and migration target

A deviation from a rule, in this repository or in a project that follows it, is
written down with:

- **Scope**: what exactly deviates, and where.
- **Reason**: the technical or domain reason that makes the rule unworkable.
- **Risk**: what the deviation costs or endangers.
- **Migration target**: how and when the deviation ends, or why it cannot.

A deviation that does not name all four is not a deviation but a violation.

## Nothing internal is named

This repository is public.

- Do not name, link or quote private repositories, internal hosts, internal
  services, credentials or customers, in files, commits, pull requests, issues
  or comments.
- Describe a need generically. A rule must be understandable and usable by
  someone outside the organization.

## Language and format

- Everything is English: documents, comments, commit messages, pull requests,
  issues.
- Markdown follows the repository's Prettier and markdownlint configuration.
  Run both over the changed files before pushing.
- Commit messages and pull request titles are Conventional Commits.
- Cite other pages as described in [Citing a rule](README.md#citing-a-rule). Do
  not link to a heading by its number.
