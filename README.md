# Nebensound Coding Guidelines

The coding and repository guidelines of Nebensound. They are public so that
public repositories can follow and cite them.

This repository is being filled in several reviewed pull requests. Until a page
is listed in the [index](#index-of-pages), its rules are not published here.

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

Pages are created as they are moved. A page that is not in the index does not
exist yet.

## Pages and their header

Every page of rules starts with YAML front matter that is checked against
[`schemas/page.json`](schemas/page.json), the one place that names the allowed
values:

- `title`: the title of the page.
- `summary`: one sentence, at most 200 characters.
- `applies-to`: a non-empty list of fixed values, starting with `all`. A
  further value, such as a language or a kind of repository, is added to the
  schema by the pull request that moves the first page needing it.
- `kind`: `binding` or `informative`.

This `README.md` and `AGENTS.md` are not pages of rules and carry no header.

## Citing a rule

Every heading that states a citable rule carries an identifier: an anchor
element on its own line directly above the heading. Identifiers are lowercase
words joined by hyphens, speak for themselves and are unique across the
repository. The wording of a heading may change; its identifier never does.

A rule is cited by its identifier, never by a number or by the wording of its
heading. Inside the repository the citation is a relative link to the page with
the identifier as fragment. From outside it is the permanent address
`https://nebensound.github.io/coding-guidelines/r/<identifier>`, which leads to
the rule where it stands now, or to what happened to it. The site that answers
this address does not exist yet, so the address does not resolve yet; the
address itself is fixed.

An identifier that has been on `main` never disappears. When its rule moves or
is dropped, the identifier is entered in [`identifiers.toml`](identifiers.toml),
the register of retired identifiers.

An invented example (no such page exists), with the rule as it is written on its
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

| Page | Topic                       |
| ---- | --------------------------- |
| none | No page has been moved yet. |

## Contributing

How the guidelines are changed is described in [`AGENTS.md`](AGENTS.md).

## License

The guidelines, including all documents, are licensed under the
[EUPL-1.2](LICENSE).
