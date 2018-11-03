---
title: Conventionele Commits 1.0.0-beta.2
language: nl-NL
---

# Conventionele Commits 1.0.0-beta.2

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

### Commit bericht met omschrijving en breaking change in de body
```
feat: allow provided config object to extend other configs

BREAKING CHANGE: `extends` key in config file is now used for extending other config files
```

### Commit bericht zonder body
```
docs: correct spelling of CHANGELOG
```

### Commit bericht met scope
```
feat(lang): added polish language
```

### Commit bericht voor een herstel met gebruik van een (optioneel) issue-nummer.
```
fix: minor typos in code

see the issue for details on the typos fixed

fixes issue #12
```

## Introductie

Het is mijn ervaring in software ontwikkeling, dat bugs meestal geïntroduceerd
worden op de grenzen tussen applicaties. Unit testen werkt geweldig voor het
testen van de interacties waar een open-source beheerder van op de hoogte is,
maar werkt slecht voor het vangen van alle interessante, vaak onverwachte,
manieren waarop een gemeenschap een bibliotheek gebruikt.

Iedereen die een upgrade heeft uitgevoerd naar een nieuwe patch versie van een
afhankelijkheid en door de applicatie geconfronteerd werd met een gestage stroom
van 500 errors, weet hoe belangrijk een leesbare commit-historie (en
[idealiter een goed onderhouden CHANGELOG](http://keepachangelog.com/en/0.3.0/))
is voor het daaruitvolgende forensische proces.

De Conventionele Commits specificatie stelt voor om een gestandaardiseerde,
lichtgewicht conventie te introduceren op commit berichten. Deze conventie
sluit aan op [SemVer](http://semver.org) en vraagt software software
ontwikkelaars om features, fixes en breaking changes in commit berichten te
omschrijven.

Met het introduceren van deze conventie, creeëren we een gedeelde taal die het
makkelijker maakt om issues over projectgrenzen heen te debuggen.

## Conventionele Commits specificatie

De sleutelwoorden "MOET" ("MUST"), "MOET NIET" ("MUST NOT"), "VEREIST"
("REQUIRED"), "SHALL" ("ZAL"), "ZAL NIET" ("SHALL NOT"), "SHOULD"
("ZOU MOETEN"), "SHOULD NOT" ("ZOU NIET MOETEN"), "RECOMMENDED" ("AANBEVOLEN"),
"MAG" ("MAY") en OPTIONEEL ("OPTIONAL") in dit document dienen geïnterpreteerd
te worden zoals omschreven in [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

1. Commits MOETEN voorafgegaan worden door een type prefix, welke bestaat uit
  een zelfstandig naamwoord, bijvoorbeeld `feat` of `fix`, gevolgd door een
  dubbele punt en een spatie.
2. Het type `feat` MOET worden gebruikt wanneer een commit een nieuwe feature
  toevoegt aande applicatie of bibliotheek.
3. Het type `fix` MOET gebruikt worden wanneer een commit een bug fix betreft
  voor de applicatie.
4. Een optionele scope MAG worden toegevoegd na een type. Een scope is een
  zinsnede die een sectie van de codebase omschrijft en is omsloten door
  haakjes, bijvoorbeeld `fix(parser):`
5. Een omschrijving MOET direct volgen op de type/scope prefix.
  De omschrijving is een korte omschrijving van de codewijzigingen,
  bijvoorbeeld _fix: array parsing issue when multiple spaces were contained in
  string._
6. Een langere commit body MAG worden aangeleverd na de korte omschrijving,
  waarmee aanvullende contextuele informatie over de codewijzigingen wordt
  verschaft. De body MOET op een lege regel na de omschrijving beginnen.
7.  Een footer MAG worden aangeleverd een lege regel na de body (of na de
  omschrijving als er geen body is). The footer ZOU aanvullende issue-
  verwijzingen MOETEN bevatten over de codewijzigingen (zoals de issues die
  er mee worden verholpen, bijvoorbeeld "Fixes \#13").
8. Breaking changes MOETEN aangegeven worden aan het alleerste begin van de
  footer of de body sectie van een commit. Een breaking change MOET bestaan uit
  de tekst `BREAKING CHANGE` in hoofdletters, gevolgd door een dubbele punt en
  een spatie.
9. Een omschrijving MOET worden gegeven na de `BREAKING CHANGE: ` en
  omschrijven wat veranderd is aan de API, bijvoorbeeld: _BREAKING CHANGE:
  environment variables now take precedence over config files._
10. De footer MOET alleen `BREAKING CHANGE`, externe links, issueverwijzingen
  en andere meta-informatie bevatten.
11. Types anders dan `feat` en `fix`  MOGEN worden gebruikt in uw commit-
  berichten.

## Waarom Conventional Commits gebruiken

* Automatisch genereren van CHANGELOGs
* Automatisch bepalen van een semantic version bump (gebaseerd op de type
  commits)
* Communiceren van de aard van de veranderingen naar teamgenoten, het publiek
  en andere stakeholders.
* Starten van build en publish processen.
* Het makkelijker maken voor mensen om bij te dragen aan uw projecten, doordat
  ze in staat zijn de commithistorie in een meer gestructureerde manier door te
  nemen.

## FAQ

### Hoe moet ik omgaan met commitberichten in de initiële ontwikkelfase?

We raden u om te werken alsof u al een gereleased product heeft. Doorgaans
gebruikt *iemand*. al zijn het uw collega ontwikkelaars, uw software. Ze zullen
willen weten wat er verbeterd is, wat niet meer werkt, etc.

### Wat doe ik als de commit van toepassing is op meer dan een van de commit
types?

Ga terug en maak meerdere commits waar mogelijk. Een deel van het nut van
Conventional Commits is zijn mogelijkheid om ons aan te sporen om  meer
georganizeerde commits en PRs te maken.

### Ontmoedigt dit niet snel ontwikkelen en snelle iteraties?

Het ontmoedigt snel handelen op een ongeorganiseerde manier.Het helpt u om op
de lange termijn snel te handelen over meerdere projecten met verschillende
bijdragers.

### Kan Conventional Commits developers er toe leiden om het aantal type commits
te beperken, omdat ze zullen denken in de aangeboden types?

Conventional Commits moedigt ons aan om meer van bepaalde soorten commits, zoals
fixes, te maken. Daarnaast stelt de flexibiliteit van Conventional Commits
uw team in staat om met eigen types te komen en die typen in de loop van de tijd
te veranderen.

### Hoe verhoudt zich dit tot SemVer?

`fix` type commits zouden vertaald moeten worden naar `PATCH` releases. `feat`
type commits zouden vertaald moeten worden naar `MINOR` releases. Commits met
`BREAKING CHANGE` in de commits, ongeacht het type, zouden vertaald moeten
worden naar `MAJOR` releases.

### Hoe zou ik mijn extenties van de Conventional Commits Specification moeten
versioneren, bijvoorbeeld `@jameswomack/conventional-commit-spec`?

We raden aan om SemVer te gebruiken om releases van uw eigen extensie op deze
specificatie uit te brengen (en we moedigen u aan deze extensies te maken!).

### Wat doe ik als ik per ongeluk het verkeerde commit type gebruik?

#### Wanneer u een type heeft gebruikt dat onderdeel is van de specificatie maar niet het correcte type, bijvoorbeeld `fix` in plaats van `feat`

Voordat u de fout merget of releaset, raden we aan om `get rebase -i` te
gebruiken om de commithistorie te bewerken. Na release zal het opruimen anders
zijn, afhankelijkheid van de tools en processen die u gebruikt.

#### Wanneer u een type heeft gebruikt dat *niet* onderdeel is van de specificatie, bijvoorbeeld `feet` in plaats van `feat`

In het ergste geval is het niet het einde van de wereld als een commit niet
voldoet aan de conventional commit specificatie. Het betekent simpelweg dat
de commit gemist wordt door tools die zijn gebaseerd op de specificatie.

### Moeten al mijn bijdragers de conventional commits specificatie gebruiken?

Nee! Als u een squash-gebaseerde workflow hanteert op Git, dan kunnen lead
maintainers de commitberichten opruimen terwijl ze die mergen — zonder extra
werkdruk voor personen die af en toe een commit leveren. Een veel voorkomende
workflow hiervoor is om uw git systeem automatisch commits te laten squashen
uit een pull request en een formulier te presenteren aan de lead maintainer
waarmee het juiste commitbericht kan worden ingegeven voor de merge.

## Over de specificatie

De Conventional Commit specificatie is geïnspireerd door, en sterk gebaseerd op,
de [Angular Commit Guidelines](https://github.com/angular/angular.js/blob/master/CONTRIBUTING.md#commit).

De eerste versie van deze specificatie is geschreven in samenwerking met enkele
van de personen die bijdragen aan:

* [conventional-changelog](https://github.com/conventional-changelog/conventional-changelog):
  een set van tools voor het parsen van conventional commit berichten uit git
  histories.
* [unleash](https://github.com/netflix/unleash): een tool voor het automatiseren
  van de software release en publicatie lifecycle.
* [lerna](https://github.com/lerna/lerna): een tool voor het beheren van
  monorepos, onstaan uit het Babel project.

## Projecten die Conventional Commits gebruiken

* [yargs](https://github.com/yargs/yargs): iedereens favoriete piratenthema
  command line argument parser.
* [parse-commit-message](https://github.com/olstenlarck/parse-commit-message):
  Spec compliant parsing utility om een object zoals `{ header: { type, scope, subject }, body, footer }` uit de gegeven commitbericht string te krijgen.
* [istanbuljs](https://github.com/istanbuljs/istanbuljs): een collectie van
  open source tools en bibliotheken voor het toevoegen van test coverage aan uw
  JavaScript tests.
* [standard-version](https://github.com/conventional-changelog/standard-version):
  Automatisch versioneren en CHANGELOG-beheer, maakt gebruik van GitHubs nieuwe
  squash-knop en de aanbevolen Conventional Commits workflow
* [uPortal-home](https://github.com/UW-Madison-DoIT/angularjs-portal) en [uPortal-application-framework](https://github.com/UW-Madison-DoIT/uw-frame):
  Optionele aanvullende user interface voor het verbeteren van [Apereo uPortal](https://www.apereo.org/projects/uportal).

[![Conventional Commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-yellow.svg)](https://conventionalcommits.org)

_Wilt u uw project op deze lijst?_ [Stuur een pull request](https://github.com/conventional-changelog/conventionalcommits.org/pulls).

## Licentie

[Creative Commons - CC BY 3.0](http://creativecommons.org/licenses/by/3.0/)
