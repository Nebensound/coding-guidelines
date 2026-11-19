# Nebensound Coding Guidelines

The coding and repository guidelines of Nebensound. They are public so that
public repositories can follow and cite them.

> **Notice:** This repository is still being filled in reviewed pull requests,
> and the site behind the permanent address of a rule does not exist yet, so
> that address does not resolve yet.

## Scope and priority

The guidelines are the quality standard for the projects of the `Nebensound`
GitHub organization. For other projects they are a reference that can be
followed and cited.

They rank as follows:

1. Mandatory law and binding security and data protection requirements.
2. Approved domain specifications and contracts of the specific project.
3. These guidelines.
4. Project-specific rules (`AGENTS.md`, `CONTRIBUTING.md`, the project's
   `README.md`). They may clarify or strengthen the guidelines, never silently
   weaken them.

When rules of equal priority conflict, the stricter rule applies. A deviation
is documented as described in
[Changing the guidelines](AGENTS.md#a-deviation-names-scope-reason-risk-and-migration-target).

## Structure

One page per topic:

- `general/` holds the rules that apply in every project.
- `github/` holds the rules about repositories, pull requests, issues, Actions
  and releases.
- `languages/` holds the rules per language.
- `definition-of-done.md` holds the Definition of Done.

## Pages and their header

Every page of rules starts with YAML front matter that is checked against
[`schemas/page.json`](schemas/page.json), the one place that names the allowed
values:

- `title`: the title of the page, on one line. A page repeats it as its first
  heading.
- `summary`: one sentence on one line, ending with a full stop, at most 200
  characters.
- `languages` and `repositories`: optional lists of fixed values, one field
  per dimension of scope. Within a field the page applies when one of its
  values fits the case; between fields all must fit. A field that is absent
  means every value of that dimension, so a page without both fields applies
  everywhere. The schema names the allowed values and starts with empty value
  lists; a value is added by the pull request that adds the first page needing
  it.
- `kind`: `binding` or `informative`.

Until the CI validates headers, the pull request that adds or changes a page
states the result of validating the page's front matter against the schema with
a JSON Schema 2020-12 validator.

This `README.md` and `AGENTS.md` are not pages of rules and carry no header.

## Citing a rule

Every heading that states a citable rule carries an identifier: an anchor
element on its own line before the heading, separated from it by one blank
line. Identifiers are lowercase words joined by hyphens, speak for themselves,
are unique across the repository and differ from every heading slug on their
page. The wording of a heading may change; its identifier never does.

A rule is cited by its identifier, never by a number or by the wording of its
heading. Links between `README.md` and `AGENTS.md` point to their section
headings; these two files hold no citable rules. Inside the repository the
citation is a relative link to the page with the identifier as fragment. The
path depends on where the citing page sits; the example below is written from a
page in one of the topic directories. From outside it is the permanent address
`https://nebensound.github.io/coding-guidelines/r/<identifier>`, which leads to
the rule where it stands now, or to what happened to it.

An identifier that has been on `main` never disappears. A rule that moves to
another page keeps its identifier; only the internal links to it change. When a
rule is merged into another one or dropped, its identifier is entered in
[`identifiers.toml`](identifiers.toml), the register of retired identifiers. A
retired identifier is never given to another rule, so an identifier is free only
if it is in neither a page nor the register.

An example, with the rule as it is written on its
page:

```markdown
<a id="coverage-gate"></a>

## The coverage gate

...
```

An internal citation of it from another page:

```markdown
See [the coverage gate](../general/testing.md#coverage-gate).
```

The permanent address of it:

```text
https://nebensound.github.io/coding-guidelines/r/coverage-gate
```

## Index of pages

| Page | Topic |
| ---- | ----- |
| none | none  |

## Contributing

How the guidelines are changed is described in [`AGENTS.md`](AGENTS.md).

## License

The guidelines, including all documents, are licensed under the
[EUPL-1.2](LICENSE).
