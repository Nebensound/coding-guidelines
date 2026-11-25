# Working with the guidelines and changing them

This file is for whoever works with the Nebensound Coding Guidelines or changes
them. What the guidelines consist of and how they work is written once, in
[`README.md`](README.md); this file links there and adds only what to do.

The guidelines hold for this repository itself: a change here meets the rules
in force like a change in any other repository.

## Working with the guidelines

- Find the rules that apply to the case by their `languages` and
  `repositories`, as described in [Fields of a rule](README.md#fields-of-a-rule)
  and [Where a rule holds](README.md#where-a-rule-holds). What binds is
  described in [Kinds of content](README.md#kinds-of-content).
- Read the rules in context on the reading pages, from the start page named in
  [Reading pages](README.md#reading-pages).
- Cite a rule as described in [Identifiers](README.md#identifiers).
- Work that is checked against the guidelines names the version of the
  guidelines it was checked against.

## Changing the guidelines

This applies to every change, whoever makes it.

- Split a sentence that holds two requirements, which can be followed or
  violated separately, into two rules. Decide between rule and principle as
  described in [Kinds of content](README.md#kinds-of-content).
- Write the fields as described in
  [Fields of a rule](README.md#fields-of-a-rule) and
  [Fields of a definition, a principle and a group](README.md#fields-of-a-definition-a-principle-and-a-group).
  A rationale that only says "best practice" is not one.
- Refer to an item in the short form described in
  [References](README.md#references).
- Give a new item the next free number of its letter. When an identifier is
  taken and what then holds for it is described in
  [Identifiers](README.md#identifiers).
- Set a new rule in, by the long form, on a reading page in the same change,
  and link a new page from a page the start page reaches, as described in
  [Reading pages](README.md#reading-pages).
- Never edit `pages/` by hand: change the page source or the item and run the
  generator.
- Check item files in an editor with the recommended YAML extension, which uses
  the mapping described in [Kinds of content](README.md#kinds-of-content).
- Give the pull request the title type that fits what it does to each item, as
  described in
  [What a change does to an item](README.md#what-a-change-does-to-an-item) and
  [The title of a pull request](README.md#the-title-of-a-pull-request), and
  change items in one way per pull request, as described in
  [One kind per pull request](README.md#one-kind-per-pull-request).
- Announce a stricter step as described in
  [Announcing a step](README.md#announcing-a-step).
- Once branches named `pre` in front of `main` exist, follow
  [Through a branch in front of `main`](README.md#through-a-branch-in-front-of-main).
- Nothing internal is named: no private repositories, internal hosts, internal
  services, credentials or customers, in files, commits, pull requests, issues
  or comments. Describe a need generically.
- Everything is English. Commit messages and pull request titles are
  Conventional Commits. Files follow the repository's Prettier configuration and
  Markdown its markdownlint configuration; run both over the changed files
  before pushing.
