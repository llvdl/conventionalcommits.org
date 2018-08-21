---
title: Conventionele Commits 1.0.0-beta.2
language: nl-NL
---

# Conventional Commits 1.0.0-beta.2

## Samenvatting

Als een open source onderhouder, squash ik feature branches op `master` en
schrijf ik ondertussen een gestandaardiseerd commit bericht.

Het commit bericht zou als volgt gestructureerd moeten zijn:

---

```
<type>[optionele scope]: <omschrijving>

[optionele body]

[optionele footer]
```
---

<br />
De commit bevat de volgende structurele elementen om de intentie duidelijk te
maken aan de gebruikers van de bibliotheek:

1. **fix:** een commit van het _type_ `fix` corrigeert een bug in de codebase
(dit komt overeen met [`PATCH`](http://semver.org/#summary) in semantic
versioning).
2. **feat:** een commit van het _type_ `feat` introduceert een nieuwe functie
in de codebase (dit komt overeen met [`MINOR`](http://semver.org/#summary) in
semantic versioning).
3. **BREAKING CHANGE:** een commit met een body of footer die begint met
`BREAKING CHANGE:` introduceert een API verandering die niet compatibel is met
de vorige versie. Een breaking change kan onderdeel zijn commits van elk _type_.
Bijvoorbeeld `fix:`, `feat:` en `chore:` types zijn valide, net als ieder ander
_type_.
4. Overig: andere commit _types_, naast `fix:` en `feat:`, zijn toegestaan.
Bijvoorbeeld `chore:`, `docs:`, `style:`, `refactor:`, `perf:`, `test:` en
andere types aanbevolen door [commitlint-config-conventional](https://github.com/marionebl/commitlint/tree/master/%40commitlint/config-conventional)
(gebaseerd op
[de Angular conventie](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines)).
Wij bevelen ook `improvement` aan voor commits die de huidige implementatie
verbeteren zijn een nieuwe functie toe te voegen of een bug te herstellen. Deze
types zijn niet verplicht volgens de conventionele commits specificatie en
hebben geen impliciet effect in semantic versioning (tenzij ze een BREAKING
CHANGE bevatten, wat NIET aanbevolen is).
<br />
Een scope kan worden toegevoegd aan een commit type om additionele contextuele
informatie toe te voegen. De scope staat tussen haakjes, bijvoorbeeld:
`feat(parser): add ability to parse arrays`.

## Voorbeelden

### Commit message with description and breaking change in body
```
feat: allow provided config object to extend other configs

BREAKING CHANGE: `extends` key in config file is now used for extending other config files
```

### Commit message with no body
```
docs: correct spelling of CHANGELOG
```

### Commit message with scope
```
feat(lang): added polish language
```

### Commit message for a fix using an (optional) issue number.
```
fix: minor typos in code

see the issue for details on the typos fixed

fixes issue #12
```

## Introduction

In software development, it's been my experience that bugs are most often introduced
at the boundaries between applications. Unit testing works great for testing the interactions
that an open-source maintainer knows about, but do a poor job of capturing all the
interesting, often unexpected, ways that a community puts a library to use.

Anyone who has upgraded to a new patch version of a dependency, only to watch their
application start throwing a steady stream of 500 errors, knows how important
a readable commit history (and [ideally a well maintained CHANGELOG](http://keepachangelog.com/en/0.3.0/)) is to the ensuing
forensic process.

The Conventional Commits specification proposes introducing a standardized lightweight
convention on top of commit messages. This convention dovetails with [SemVer](http://semver.org),
asking software developers to describe in commit messages, features, fixes, and breaking
changes that they make.

By introducing this convention, we create a common language that makes it easier to
debug issues across project boundaries.

## Conventional Commits Specification

The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

1. Commits MUST be prefixed with a type, which consists of a noun, `feat`, `fix`, etc.,
   followed by a colon and a space.
2. The type `feat` MUST be used when a commit adds a new feature to your application
  or library.
3. The type `fix` MUST be used when a commit represents a bug fix for your application.
4. An optional scope MAY be provided after a type. A scope is a phrase describing
  a section of the codebase enclosed in parenthesis, e.g., `fix(parser):`
5. A description MUST immediately follow the type/scope prefix.
  The description is a short description of the code changes, e.g.,
  _fix: array parsing issue when multiple spaces were contained in string._
6. A longer commit body MAY be provided after the short description, providing additional contextual information about the code changes. The body MUST begin one blank line after the description.
7. A footer MAY be provided one blank line after the body (or after the description if body is missing).
  The footer SHOULD contain additional issue references about the code changes (such as the issues it fixes, e.g.,`Fixes #13`).
8. Breaking changes MUST be indicated at the very beginning of the footer or body section of a commit. A breaking change MUST consist of the uppercase text `BREAKING CHANGE`, followed by a colon and a space.
9. A description MUST be provided after the `BREAKING CHANGE: `, describing what
  has changed about the API, e.g., _BREAKING CHANGE: environment variables now take precedence over config files._
10. The footer MUST only contain `BREAKING CHANGE`, external links, issue references, and other meta-information.
11. Types other than `feat` and `fix` MAY be used in your commit messages.

## Why Use Conventional Commits

* Automatically generating CHANGELOGs.
* Automatically determining a semantic version bump (based on the types of commits landed).
* Communicating the nature of changes to teammates, the public, and other stakeholders.
* Triggering build and publish processes.
* Making it easier for people to contribute to your projects, by allowing them to explore
  a more structured commit history.

## FAQ

### How should I deal with commit messages in the initial development phase?

We recommend that you proceed as if you've an already released product. Typically *somebody*, even if its your fellow software developers, is using your software. They'll want to know what's fixed, what breaks etc.

### What do I do if the commit conforms to more than one of the commit types?

Go back and make multiple commits whenever possible. Part of the benefit of Conventional Commits is its ability to drive us to make more organized commits and PRs.

### Doesn’t this discourage rapid development and fast iteration?

It discourages moving fast in a disorganized way. It helps you be able to move fast long term across multiple projects with varied contributors.

### Might Conventional Commits lead developers to limit the type of commits they make because they'll be thinking in the types provided?

Conventional Commits encourages us to make more of certain types of commits such as fixes. Other than that, the flexibility of Conventional Commits allows your team to come up with their own types and change those types over time.

### How does this relate to SemVer?

`fix` type commits should be translated to `PATCH` releases. `feat` type commits should be translated to `MINOR` releases. Commits with `BREAKING CHANGE` in the commits, regardless of type, should be translated to `MAJOR` releases.

### How should I version my extensions to the Conventional Commits Specification, e.g. `@jameswomack/conventional-commit-spec`?

We recommend using SemVer to release your own extensions to this specification (and
encourage you to make these extensions!)

### What do I do if I accidentally use the wrong commit type?

#### When you used a type that's of the spec but not the correct type, e.g. `fix` instead of `feat`

Prior to merging or releasing the mistake, we recommend using `git rebase -i` to edit the commit history. After release, the cleanup will be different according to what tools and processes you use.

#### When you used a type *not* of the spec, e.g. `feet` instead of `feat`

In a worst case scenario, it's not the end of the world if a commit lands that does not meet the conventional commit specification. It simply means that commit will be missed by tools that are based on the spec.

### Do all my contributors need to use the conventional commit specification?

No! If you use a squash based workflow on Git lead maintainers can cleanup the commit messages as they're merged—adding no workload to casual committers. A common workflow for this is to have your git system automatically squash commits from a pull request and present a form for the lead maintainer to enter the proper git commit message for the merge.

## About

The Conventional Commit specification is inspired by, and based heavily on, the [Angular Commit Guidelines](https://github.com/angular/angular.js/blob/master/CONTRIBUTING.md#commit).

The first draft of this specification has been written in collaboration with some of the
folks contributing to:

* [conventional-changelog](https://github.com/conventional-changelog/conventional-changelog): a
  set of tools for parsing conventional commit messages from git histories.
* [unleash](https://github.com/netflix/unleash): a tool for automating the
  software release and publishing lifecycle.
* [lerna](https://github.com/lerna/lerna): a tool for managing monorepos, which grew out
  of the Babel project.

## Projects Using Conventional Commits

* [yargs](https://github.com/yargs/yargs): everyone's favorite pirate themed command line argument parser.
* [parse-commit-message](https://github.com/olstenlarck/parse-commit-message): Spec compliant parsing utility to get object like `{ header: { type, scope, subject }, body, footer }` from given commit message string.
* [istanbuljs](https://github.com/istanbuljs/istanbuljs): a collection of open-source tools
  and libraries for adding test coverage to your JavaScript tests.
* [standard-version](https://github.com/conventional-changelog/standard-version): Automatic versioning and CHANGELOG management, using GitHub's new squash button and the recommended Conventional Commits workflow.
* [uPortal-home](https://github.com/UW-Madison-DoIT/angularjs-portal) and [uPortal-application-framework](https://github.com/UW-Madison-DoIT/uw-frame): Optional supplemental user interface enhancing [Apereo uPortal](https://www.apereo.org/projects/uportal).

[![Conventional Commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-yellow.svg)](https://conventionalcommits.org)

_want your project on this list?_ [send a pull request](https://github.com/conventional-changelog/conventionalcommits.org/pulls).

## License

[Creative Commons - CC BY 3.0](http://creativecommons.org/licenses/by/3.0/)
