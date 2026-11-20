# Nebensound Coding Guidelines

The coding and repository guidelines of Nebensound. They are public so that
public repositories can follow and cite them.

> **Notice:** This repository is still being filled. The permanent address of a
> rule and the generator of the reading pages do not exist yet.

The guidelines are a catalogue of rules, modelled on the rule catalogue of a
linter, with reading pages for people that embed the rules.

## Kinds of content

Each item is one Markdown file with typed YAML front matter that is checked
against a JSON Schema in [`schemas/`](schemas). The kind decides what binds; no
wording does.

| Kind         | What it is                                                                  | Identifier     | Binds               |
| ------------ | --------------------------------------------------------------------------- | -------------- | ------------------- |
| Rule         | exactly one requirement that can be followed or violated                    | `R` and number | yes, by its `level` |
| Definition   | exactly one term and its meaning                                            | `D` and number | no                  |
| Principle    | an attitude rules follow from; not decidable for a single change            | `P` and number | no                  |
| Group        | a named set of rules, for instance a definition of done                     | `G` and number | through its rules   |
| Reading page | a text for people: headings, order and connecting sentences, rules embedded | its file name  | never               |

- Only a rule binds. The text of a reading page explains and orders; it demands
  nothing.
- Rule or principle: if two people looking at the same change agree whether it
  is met, it is a rule (checked by review where no program can check it); if
  they would not, it is a principle.
- A description of what a mechanism does (a pipeline, a tool) is not content of
  the guidelines. It lives in the reference of the repository that owns the
  mechanism.

| Kind       | Folder         | Schema                                       |
| ---------- | -------------- | -------------------------------------------- |
| Rule       | `rules/`       | [`rule.json`](schemas/rule.json)             |
| Definition | `definitions/` | [`definition.json`](schemas/definition.json) |
| Principle  | `principles/`  | [`principle.json`](schemas/principle.json)   |
| Group      | `groups/`      | [`group.json`](schemas/group.json)           |
| Page       | `pages-src/`   | [`page.json`](schemas/page.json)             |

## Identifiers

- The identifier is a letter and a running number, for instance `R0042`. It is
  the file name (`rules/R0042.md`) and says nothing about position or topic.
- Numbers have four digits and are counted separately per letter (`R0001`,
  `D0001`). A fifth digit follows after `9999`.
- An identifier is taken from the first tagged version that contains it. Before
  that it may still be renumbered or dropped without a trace. Afterwards it is
  never reused, renamed or removed.
- Every item also has a speaking `name`: lowercase words joined by hyphens. It
  may change. A citation reads `R0042 (coverage-gate)`; only the number counts.
- From outside, a rule is cited by the permanent address
  `https://nebensound.github.io/coding-guidelines/r/<identifier>`.

## Fields of a rule

The statement of the rule is the body of the file. The front matter has:

- `name`.
- `level`: `required` (a deviation needs the deviation process: scope, reason,
  risk and migration target), `recommended` (a deviation needs a reason) or
  `permitted` (states that something is allowed).
- `status`: `planned` (published and citable, binds nobody yet), `active` or
  `retired` (the file stays, with `reason`, and `replaced-by` where a rule took
  its place). No separate register of retired identifiers exists.
- `addressee`: `change`, `repository` or `organization`.
- `languages` and `repositories`: optional lists of fixed values that the schema
  names. Within a field one value must fit, between fields all must. An absent
  field means every value. A value is added to the schema by the pull request
  that brings the first item needing it. The values of `repositories` are places
  in a tree, described in [Where a rule holds](#where-a-rule-holds).
- `applies-when` and `except`: optional text for a condition and an exception.
- `existing`: what holds for what was there before the rule: `exempt`,
  `on-touch` (brought in line when it is touched anyway) or `required`.
- `enforced-by`: a list whose values are `review` or the name of an automated
  check as its owner calls it (lowercase words, hyphens, slashes). The schema
  fixes the form, not the names.
- `principles`: optional list of the principles the rule follows from.
- `next`: optional announcement of a change, a table with `from` (the version,
  `X.Y.Z`) and at least one of `level` and `existing`: what holds from that
  version on.

The body of a rule starts with the statement as one plain sentence in one
paragraph, followed by `## Rationale` (required) and `## Examples` (optional).
Reasons and examples never stand in the statement.

Definitions and principles have `name` and `status` (and `reason` and
`replaced-by` when retired), no scope fields and a body of plain text. A group
has `name`, `status` and `rules`, a list of rule identifiers, and the same
`reason` and `replaced-by` when retired. An item file has no top-level heading;
the generator writes the heading where it sets the item into a page. An item
file needs no inline HTML.

## Where a rule holds

Rules hold in layers, and the lowest layer binds wherever a member of the
organization works, also in someone else's project. The field `repositories`
therefore names a place in a tree:

```text
everywhere (the field is absent)   whatever a member of the organization works on
├── foreign                        someone else's project: a fork, a pull request upstream
└── own                            the organization's repositories and a member's own repositories under a personal account
    ├── public                     its open source
    └── internal                   private
        └── customer               a customer can see it
```

- A rule names the node from which it holds and holds for everything below it.
  With several nodes, one must fit. A rule without the field holds everywhere, a
  fork included.
- `public`, `internal` and `customer` are what an own repository declares as its
  audience. `foreign` is declared nowhere: it follows from the project being
  someone else's. A fork of someone else's project stays foreign wherever it
  lives, in the organization or under a member's personal account.
- The `addressee` decides what can hold in someone else's project at all. A rule
  addressed to the `change` can. A rule addressed to the `repository` or the
  `organization` cannot, so it names `own` or a node below it, and the schema
  refuses it without one.
- A sandbox repository has no place of its own in the tree. It is an own
  repository and every rule holds for it as for any other, with one difference:
  a rule that names a node (`own` or below) counts there as `recommended`
  whatever its `level`. A rule without the field keeps its level everywhere, a
  sandbox included. Whether a repository is a sandbox is given by the
  organization's repository property `lifecycle`.
- A member's own repository under a personal account is an own repository,
  `public` or `internal` by its visibility. Every rule holds for it except the
  rules addressed to the `organization`.
- What a repository produces (a library, a service, firmware, a document) is
  stated as text in `applies-when`.

## Reading pages

- A page source (`pages-src/<name>.md`) is written by hand: headings,
  connecting sentences and, at each place where an item stands, a reference to
  it. Its front matter has `title` and `summary` (one sentence) and nothing
  else; a page has no scope and no level.
- An item is referenced on a line of its own by an HTML comment of the form
  `<!-- item: R0042 -->`.
- The finished page (`pages/<name>.md`) is written by a generator only, with
  each referenced item set in at its place under a heading of its identifier
  and name, its own headings one level lower. It is committed, so that it reads
  as continuous text on GitHub, and it names its source at the top.
- Every active rule stands on at least one page, so a person who reads the pages
  has read every rule in the wording the files hold.

The folder [`pages/`](pages) is the index of the pages.

## Versions

- The guidelines are versioned like every repository. A version says whether a
  repository that conformed still conforms.
- Every pull request that touches an item says, typed, what it does to it:
  `added`, `stricter`, `relaxed`, `editorial` or `retired`. `stricter` and
  `retired` raise the major version, `added` and `relaxed` the minor,
  `editorial` the patch. A new required rule whose `existing` is `exempt` or
  `on-touch` counts as `added`. Below `1.0.0` a major change raises the minor
  version.
- A stricter rule is announced first (`next`, or `status: planned`) and becomes
  binding with the major version named.
- The version in which a rule exists, and the one in which it last changed in
  substance, is derived from these records and the tags, never written by hand.
  A rule has no version number of its own.

### The record of a change

One TOML file per pull request lies under [`changes/`](changes), named freely.
It lists, per touched item, its identifier and the kind of change, as described
by [`change.json`](schemas/change.json):

```toml
[[changes]]
item = "R0042"
kind = "added"
```

The files stay. The lists per version are derived from them and the tags.

## A worked example

A rule file, `rules/R0042.md`:

```markdown
---
name: coverage-gate
status: active
level: required
addressee: change
existing: on-touch
enforced-by:
  - coverage-gate
---

A change covers every line of code it adds or changes with a test.

## Rationale

Uncovered code is code nobody has seen run; the gate finds it before a reader
has to.
```

A page source, `pages-src/testing.md`, that embeds it:

```markdown
---
title: Testing
summary: How a change is tested and what the tests must cover.
---

Tests show that a change does what it claims. The rule below says how much of
the code they must reach.

<!-- item: R0042 -->
```

The resulting page, `pages/testing.md`, written by the generator:

```markdown
<!-- Generated from pages-src/testing.md. Do not edit. -->

# Testing

Tests show that a change does what it claims. The rule below says how much of
the code they must reach.

## R0042 (coverage-gate)

A change covers every line of code it adds or changes with a test.

### Rationale

Uncovered code is code nobody has seen run; the gate finds it before a reader
has to.
```

## Contributing

How the guidelines are changed is described in [`AGENTS.md`](AGENTS.md).

## License

The guidelines, including all documents, are licensed under the
[EUPL-1.2](LICENSE).
