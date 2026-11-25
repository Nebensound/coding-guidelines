# Nebensound Coding Guidelines

The coding and repository guidelines of Nebensound. They are public so that
public repositories can follow and cite them.

> **Notice:** This repository is still being filled. The permanent address of a
> rule, the generator of the reading pages and its checks, and the tagged
> versions do not exist yet. Once versions are given out, the guidelines stay
> below `0.1.0` until the version numbers read the types of
> [The title of a pull request](#the-title-of-a-pull-request).

The guidelines are a catalogue of rules, modelled on the rule catalogue of a
linter, with reading pages for people that embed the rules.

## Kinds of content

Each item (a rule, definition, principle or group) is one YAML file that holds
all of it and is checked against a JSON Schema in [`schemas/`](schemas). No
Markdown file stands beside it: text that needs Markdown, code blocks included,
is a block of text in a field. A page source is a Markdown file with typed YAML
front matter, checked against its schema the same way. The kind decides what
binds; no wording does. A page is not an item: it has no identifier.

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

| Kind       | File                         | Schema                                       |
| ---------- | ---------------------------- | -------------------------------------------- |
| Rule       | `rules/R<number>.yaml`       | [`rule.json`](schemas/rule.json)             |
| Definition | `definitions/D<number>.yaml` | [`definition.json`](schemas/definition.json) |
| Principle  | `principles/P<number>.yaml`  | [`principle.json`](schemas/principle.json)   |
| Group      | `groups/G<number>.yaml`      | [`group.json`](schemas/group.json)           |
| Page       | `pages-src/<name>.md`        | [`page.json`](schemas/page.json)             |

- The fields every item shares (`name`, `status`, `reason`, `replaced-by`), the
  condition that a retired item names its `reason`, and the patterns of the
  identifiers stand once, in [`item.json`](schemas/item.json). The schemas of
  the kinds reference it and hold only what is theirs; a field that neither
  defines is refused.
- Each schema names itself by an `$id` under
  `https://nebensound.github.io/coding-guidelines/schemas/`. A reference from
  one schema to another is resolved to the file beside it in `schemas/`.
- The repository maps each item folder to its schema for the YAML language
  server (the one behind the usual YAML extension of VS Code) in
  [`.vscode/settings.json`](.vscode/settings.json), and recommends that
  extension in [`.vscode/extensions.json`](.vscode/extensions.json). An editor
  with it marks a wrong, missing or unknown field while writing. No item file
  carries a line that names its schema.
- No item has a field that names its kind; the folder and the identifier say it.

## Identifiers

- The identifier is a letter and a running number, for instance `R0042`. It is
  the file name without its ending (`rules/R0042.yaml`) and says nothing about
  position or topic.
- Numbers have four digits and are counted separately per letter (`R0001`,
  `D0001`). A fifth digit follows after `9999`.
- An identifier is taken from the first tagged version that contains it. Before
  that it may still be renumbered or dropped without a trace. Afterwards it is
  never reused, renamed or removed.
- Every item also has a speaking `name`: lowercase words joined by hyphens. It
  may change. A citation reads `R0042 (coverage-gate)`; only the number counts.
- From outside, a rule is cited by the permanent address
  `https://nebensound.github.io/coding-guidelines/r/<identifier>`, for instance
  `https://nebensound.github.io/coding-guidelines/r/R0042`. Neither a citation
  nor the address carries the ending of the file.

## Fields of a rule

The file of a rule has these fields:

- `name`.
- `statement`: the rule as one plain sentence on one line, ending with a full
  stop. Reasons and examples never stand in it.
- `level`: `required` (a deviation needs the deviation process: scope, reason,
  risk and migration target), `recommended` (a deviation needs a reason) or
  `permitted` (states that something is allowed).
- `status`: `planned` (published and citable, binds nobody until a pull request
  makes it `active`), `active` or `retired` (the file stays, with `reason`, and
  `replaced-by` where a rule took its place). No separate register of retired
  identifiers exists.
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
- `next`: optional announcement of a stricter step, a table with `from` and at
  least one of `level` and `existing`: what is to hold from that version on.
  `from` names a version that can carry an incompatible change: `X.0.0`, or
  `0.Y.0` below `1.0.0`. `next` announces the step and changes nothing by
  itself. The pull request that brings the version named in `from` takes the
  step: it rewrites `level` and `existing` to what `next` announced and removes
  `next`, and the fields show it as `stricter`. The check of this repository
  fails while a rule carries a `next` whose `from` is not above the current
  version of the guidelines (the newest tag on `main`, `0.0.0` before the
  first), so an announced step is either taken or its `from` is moved, never
  silently passed.
- `explanation`: optional longer text on how to read and apply the statement,
  as Markdown text. What binds stays the `statement` with `applies-when` and
  `except`; the explanation cannot widen it, and a change of it is editorial.
- `rationale`: the failure the rule prevents or the property it secures, as
  Markdown text.
- `examples`: optional examples, as Markdown text, code blocks included.

The schema requires `statement` and `rationale`, so a rule without a rationale
fails it. Markdown text stands in a YAML block (`|`), has no headings of its own
and needs no inline HTML; the generator writes the headings where it sets an
item into a page.

## Fields of a definition, a principle and a group

Definitions, principles and groups have `name` and `status`, the same `reason`
and `replaced-by` when retired, and no scope fields. Besides:

- A definition has `term`, the word or phrase as it is written, on one line,
  and `meaning`, what it means, as Markdown text. Both are required.
- A principle has `statement`, the principle as one plain sentence in the same
  form as the statement of a rule, and optionally `explanation`, as for a rule.
- A group has `rules`, a list of rule identifiers, and optionally `purpose`,
  what the set of rules is for, as Markdown text. A group holds rules only:
  which principles and definitions belong to it follows from its rules, so they
  are not listed a second time.

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
  lives, in the organization or under a member's personal account; it becomes
  an own repository when it carries the organization's repository declaration.
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
  it. It stays a Markdown file, because it is prose that references items. Its
  front matter has `title` and `summary` (one sentence) and nothing else; a page
  has no scope and no level.
- An item is referenced on a line of its own by an HTML comment of the form
  `<!-- item: R0042 -->`.
- The finished page (`pages/<name>.md`) is written by a generator only: a first
  line that names its source, the `title` as top-level heading, and each
  referenced item set in at its place under a heading of its identifier and
  name, one level below the heading it stands under. A rule shows its statement,
  then its explanation, rationale and examples under the headings
  `Explanation`, `Rationale` and `Examples` one level lower still; a definition
  shows its `term` and `meaning`, a principle its `statement` and
  `explanation`, a group its `purpose` and `rules`.
  The page is committed, so that it reads as continuous text on GitHub.
- The checks for Markdown (format, lint rules, links) run on the generated
  pages, so a broken link in a rationale is found there, and the finding names
  the page.
- Every active rule stands on at least one page, so a person who reads the pages
  has read every rule in the wording the files hold.

The folder [`pages/`](pages) is the index of the pages. The `README.md` in each
folder describes the folder; it is neither an item nor a page.

## Versions

The guidelines follow Semantic Versioning, read for a rulebook. A rulebook
demands; it does not offer. A change is incompatible when a repository that met
every rule before may no longer meet them after. Taking a demand away is never
incompatible.

| Change                                                                                 | Kind        | A repository that met everything | From `1.0.0` |
| -------------------------------------------------------------------------------------- | ----------- | -------------------------------- | ------------ |
| A rule becomes stricter; a new rule, or a planned one made `active`, binds what exists | `stricter`  | may no longer meet it            | major        |
| A new rule, or a planned one made `active`, does not bind what exists                  | `added`     | still meets it                   | minor        |
| A rule is relaxed                                                                      | `relaxed`   | still meets it                   | minor        |
| A rule is retired                                                                      | `retired`   | still meets it                   | minor        |
| A step is announced: a new rule with `status: planned`, or `next` on a rule            | `announced` | still meets it                   | patch        |
| Editorial                                                                              | `editorial` | unaffected                       | patch        |

- A rule binds what exists when its `level` is `required` or `recommended` and
  its `existing` is `required`. With `exempt` or `on-touch` it does not, and a
  `permitted` rule, which cannot be violated, never does.
- Below `1.0.0`: below `0.1.0` every change raises the patch version; from
  `0.1.0` an incompatible change raises the minor version and every other change
  the patch version. `1.0.0` is a deliberate step.
- Announcement before obligation, from `1.0.0` on: an incompatible step is
  announced in an earlier version and binds from the major version that switches
  it on. A rule with `status: planned` binds nobody until a pull request makes
  it `active`. When it binds what exists, that pull request is `stricter` and
  the rule binds from the major version it brings; otherwise it is `added`. The
  `from` of `next` names the major version of the stricter step, and the pull
  request that brings that version takes the step and is `stricter`. An
  announcement asks nothing of anyone yet, so every announcement raises only the
  patch version, whatever it announces. The pull request that fulfils it carries
  the weight: `added` (minor) or `stricter` (major). Relaxing and retiring need
  no announcement.
- Below `1.0.0` nothing has to be announced: an incompatible step binds from the
  version that carries it. `status: planned` and `next` stay available below
  `1.0.0` for whoever wants to announce a step, but nothing requires them.
- A retired rule keeps its file and its identifier is never given again, so a
  citation never points at nothing.

### What a change does to an item

What a pull request does to an item follows from two things: the fields of the
item, compared before and after the pull request, and the title of the pull
request for the free text that carries meaning.

For a rule:

| What changes in the file of a rule                                                                           | Kind                                             |
| ------------------------------------------------------------------------------------------------------------ | ------------------------------------------------ |
| A new rule, `active`, that binds what exists                                                                 | `stricter`                                       |
| A new rule, `active`, that does not bind what exists                                                         | `added`                                          |
| A new rule with `status: planned`                                                                            | `announced`                                      |
| `status` to `active`, from `planned` or from `retired`                                                       | `stricter` if it binds what exists, else `added` |
| `status` to `retired`                                                                                        | `retired`                                        |
| `status` from `active` back to `planned`                                                                     | `relaxed`                                        |
| `status` from `retired` back to `planned`                                                                    | `announced`                                      |
| `level` or `existing` raised                                                                                 | `stricter`                                       |
| `level` or `existing` lowered                                                                                | `relaxed`                                        |
| `addressee` changed                                                                                          | `stricter`                                       |
| `languages` or `repositories` widened: a value added, a node replaced by one above it, or the field removed  | `stricter`                                       |
| `languages` or `repositories` narrowed: a value removed, a node replaced by one below it, or the field added | `relaxed`                                        |
| `next` removed and `level` or `existing` rewritten to what it announced: the step is taken                   | `stricter`                                       |
| `next` added, or changed to announce more or from an earlier version                                         | `announced`                                      |
| `next` changed to announce less or from a later version, or removed without its step being taken             | `relaxed`                                        |
| `statement`, `applies-when` or `except`                                                                      | the kind the title claims                        |
| `explanation`, `rationale`, `examples`, `name`, `enforced-by`, `principles`, `reason` or `replaced-by`       | `editorial`                                      |

For a definition, a principle and a group, which bind nothing by themselves:

| What changes in the file of a definition, principle or group                            | Kind                      |
| --------------------------------------------------------------------------------------- | ------------------------- |
| A new item                                                                              | `added`                   |
| `status` to `retired`                                                                   | `retired`                 |
| Any other change of `status`; `name`, `reason` or `replaced-by`; the `rules` of a group | `editorial`               |
| The `purpose` of a group; the `explanation` of a principle                              | `editorial`               |
| The `term` or the `meaning` of a definition; the `statement` of a principle             | the kind the title claims |

- `level` rises from `permitted` to `recommended` to `required`; `existing`
  rises from `exempt` to `on-touch` to `required`.
- A change of `languages` or `repositories` that widens in one place and narrows
  in another, such as `public` replaced by `internal`, counts as widened.
- A rule with `status: planned` binds nobody, so a change of its fields other
  than `status` that the table reads as `stricter` or `added` is `announced`. A
  rule with `status: retired` binds nobody, so a change of its fields other than
  `status` is `editorial`.
- `next` is removed without its step being taken when the same pull request
  does not rewrite `level` and `existing` to what `next` announced. When it
  does, the step is taken: the raise counts, and the item is `stricter`.
- When several rows apply to one file and one of them is `stricter`, the item
  is `stricter`. Otherwise it counts with each kind its rows show, and with
  `editorial` only when no other kind applies.
- A file is never moved or removed once its identifier is taken. Before that, a
  renumbered item counts as a new item, and a dropped item has no kind, because
  no version contained it.
- A page source binds nothing; a change of it is `editorial`.

### The title of a pull request

The version number is given out from the titles of the merged pull requests,
which follow Conventional Commits. The type of the title names the kind of the
change:

| Type of the title | Kind        |
| ----------------- | ----------- |
| `rule!`           | `stricter`  |
| `rule`            | `added`     |
| `relax`           | `relaxed`   |
| `retire`          | `retired`   |
| `announce`        | `announced` |
| any other type    | `editorial` |

- The breaking marker `!` stands only in `rule!`. The type `feat` is not used:
  a rulebook has no features.
- `rule`, `relax`, `retire` and `announce` are the repository's own types.
  `rule`, `relax` and `retire` raise the minor version from `1.0.0` on.
  `announce` raises the patch version, the same step as an editorial type; it
  is a type of its own so that the list of the version names the announcement.
- The own types are written from the first pull request on. Below `0.1.0` every
  change raises the patch version whatever its type.
- For free text that carries meaning (the `statement` of a rule or a
  principle, `applies-when`, `except`, the `term` and the `meaning` of a
  definition), no program can read whether new wording demands more or only
  reads better. The type of the title is the author's claim about it, and
  review judges the claim.
- The check of this repository holds the title at least as strict as what the
  fields of the changed items show. `rule!` is the strictest, then `rule`,
  `relax` and `retire`, then `announce`, then any other type. A raised `level`
  under a title without `!` fails, and so does an added, relaxed or retired rule
  under `announce`.
- A change of free text that carries meaning under an editorial title passes,
  and the check names the item for the reviewer. A corrected typo in a statement
  stays possible, and a hidden stricter step is seen.

### One kind per pull request

A pull request changes items in one way. A pull request that rewords the
statements of two rules, one to demand more and one only to read better, can
carry only one title, so both would stand in the list of the version as
`stricter`. Two pull requests keep the list true. Changes that the fields show
are not affected; they are read per item.

### Derived data

Since which version an item exists, in which version it last changed in
substance, and the list of changes per version by kind are read from the history
of `main` and the tags, never written by hand. Each touched item counts with the
kind its fields show. Where only its free text that carries meaning changed, it
counts with the kind the title claims. Where both changed, the kind with the
larger version step counts, and the kind the fields show when the steps are
equal. A rule has no version number of its own.

### Through a branch in front of `main`

Once the central pipeline offers branches named `pre` in front of `main`, this
way is recommended:

1. One pull request per change against `pre`. Automatic merging is acceptable
   there; `pre` binds nobody.
2. One pull request from `pre` into `main` that lands the changes together as
   one deliberate version of the rulebook. The landing keeps the single commits
   and their titles, so the list of the version still names the kind per item.
   The review of the landing is where the claims about free text are judged.

Until then every pull request goes to `main`. Nothing in this repository
depends on such a branch.

## A worked example

A rule file, `rules/R0042.yaml`:

```yaml
name: coverage-gate
statement: A change covers every line of code it adds or changes with a test.
status: active
level: required
addressee: change
existing: on-touch
enforced-by:
  - coverage-gate
explanation: |
  A line counts as covered when at least one test runs it. How coverage is
  measured is left to the tools of each language.
rationale: |
  Uncovered code is code nobody has seen run; the gate finds it before a reader
  has to.
```

A definition file, `definitions/D0007.yaml`:

```yaml
name: test
term: test
status: active
meaning: |
  Code that runs other code and fails when that code does not behave as
  expected.
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

### Explanation

A line counts as covered when at least one test runs it. How coverage is
measured is left to the tools of each language.

### Rationale

Uncovered code is code nobody has seen run; the gate finds it before a reader
has to.
```

## Contributing

How the guidelines are changed is described in [`AGENTS.md`](AGENTS.md).

## License

The guidelines, including all documents, are licensed under the
[EUPL-1.2](LICENSE).
