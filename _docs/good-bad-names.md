---
layout: docs
title: Good and Bad Names
date: 2015-08-28 10:54:30
permalink: /docs/good-bad-names/
---

One of the most popular use cases is finding whether or not a name string
corresponds to a current and valid scientific name.  And most users want just
one "correct" answer.  Currently [Global Names Index/Resolver][gnr] contains
about 23 million name strings coming from many sources. To figure out which of
these name strings we should return to users we started a Google Summer of Code
project in 2015 and @wencanluo tried to classify them into "good" and
"bad" ones.

This document is a compilation of thoughts by Paddy, @dimus and @wencan about
what would be considered "good" and "bad" name.

What is name-string?
--------------------

A name-string is a collection of characters, spaces, and punctuation that
makes up a name: "Homo sapiens Linnaeus 1758" and "H. sapiens L." are two name
strings representing the same name.

What are ranks?
---------------

| Ranks - in the hierarchy of taxa | Example            |
|----------------------------------|--------------------|
|Kingdom                           | Metazoa or Plantae |
|Division or Phyla                 | Vertebrata         |
|Class                             | Mammalia           |
|Order                             | Primate            |
|Family                            | Hominidae          |
|Genus                             | Homo               |
|Species                           | Homo sapiens       |

What is a good name?
--------------------

Most people will NOT know what they mean by "good".  They probably expect that
there is a correct name, and do not want to use a name that is wrong. There is
in fact no single correct name, because one element of applying a name to a
taxon (a related group of organisms) is subjective. There is usually broad,
frequently unanimous, consensus, but there will always be a minority who think
that they should use different names for the same thing.

What was considered the right name also changes over time.

I understand that our task is only to find out which name should be considered
"good" today.  That makes things easier.

So, it is wiser to think about "good" and "bad" names, and then to identify
factors that help to distinguish the better names from the less good names.

For a name to be "good" three factors need to be considered:

* Does the name-string represent a scientific name
* Does the name comply with a relevant code of nomenclature
* Is the name being used now by one or more taxonomists to refer to a taxon
  (a group of organisms with a common taxonomic history)


What are we trying to establish?
--------------------------------

Is this a scientific name, is it nomenclaturally correct, and is endorsed by a
taxonomist

Ideally, a good name is one that is nomenclaturally good (complies with a code)
and also is deemed to be the best name for a taxon (taxonomically endorsed)
according to one or more good taxonomists.

The long term vision
--------------------

In the long term, we would expect that GN is dynamically connected to other
on-line specialist sources that keep GN informed as to whether the name is
scientific, and whether it is taxonomically endorsed. One parts of those
resources are available, and sometimes not freely and openly; such that the
infrastructural service that we dream of, cannot be created today. Because
of this, we need to find some way to estimate the likelihood of a
name being good.


What makes a name "scientific"?
-------------------------------

Scientific names are latinized.  Alternative names are common names (also
referred to as vernacular or colloquial or familiar or informal - such as cat,
dog, crow, maple); there are surrogates for names (being name-strings that may
refer to a culture, or some term by which an organism is widely known in, for
example, research settings).

Names have ranks, that indicate where in the hierarchy of classification they
belong: Kingdom, Phylum, Class, Order, Family, Genus, Species) - see the
vocabulary document as these are just the most common ranks.  The most numerous
names are those for species (there are about 2.3 million species, and most will
have had more than one name).  A species name is distinctive. It is made of two
parts, a genus and a species part (Homo sapiens, Drosophila melanogaster).
These are binomial names.  Not all latinized binomial names that have a capital
letter at the front are organisms: ‘Anorexia nervosa is an eating disorder, and
Habeas corpus is a legal term’).

Most other names are uninomial: the Hominidae is the family that includes
Homo - us.

But, you will find trinomials and polynomials, when an author wants to
indicate, as an example, which subgenus a species belongs in: Drosophila
(Sophophora) melanogaster tells us that the author places the species
‘melanogaster’ in the subgenus Sophophora.

Namestrings and names
---------------------

A name-string is the collection of characters, spaces, and punctuation that can
be used for the name.  There can be very many name-strings for the same name -
as seen below.  In addition there are abbreviations, mis-spellings, and who
knows what.  In trying to match name-strings together, we try to identify the
‘canonical’ version, being just the latinised words without annotations,
abbreviations, or names or authors or dates. Dima’s parser seeks to do this.


The following illustrates a variety of name-strings (not all!) that are used
for the same scientific name, a subspecies called Carex scirpoidea convoluta.
Names may also be mis-spelled or annotated in various ways.

```
Carex scirpoidea convoluta
Carex scirpoidea var. convoluta
Carex scirpoidea subsp. convoluta
Carex scirpoidea var. convoluta Kuk.
Carex scirpoidea convoluta Gardner
Carex scirpoidea convoluta Kükenth.
Carex scirpoidea var. convoluta Kük.
Carex scirpoidea var. convoluta Kükenth.
Carex scirpoidea var. convoluta Kükenthal
Carex scirpoidea Michx. var. convoluta Kük.
Carex scirpoidea ssp. convoluta (Kük.) Dunlop
Carex scirpoidea Michx. var. convoluta Kükenth.
Carex scirpoidea subsp. convoluta (Kük.) Dunlop
Carex scirpoidea ssp. convoluta (Kukenth.) Dunlop
Carex scirpoidea Michaux var. convoluta Kükenthal
Carex scirpoidea subsp. convoluta (Kük.) D.A.Dunlop
Carex scirpoidea subsp. convoluta (Kük.) D.A. Dunlop
Carex scirpoidea Michx. ssp. convoluta (Kük.) Dunlop
Carex scirpoidea subsp. convoluta (Kuk.) D. A. Dunlop
Carex scirpoidea Michx. subsp. convoluta (Kük.) Dunlop
Carex scirpoidea Michx. ssp. convoluta (Kükenth.) Dunlop
Carex scirpoidea subsp. convoluta (Kükenthal) D.A. Dunlop
Carex scirpoidea Michx. subsp. convoluta (Kük.) D.A.Dunlop
Carex scirpoidea Michx. subsp. convoluta (Kük.) D.A. Dunlop
Carex scirpoidea subsp. convoluta (Kükenthal 1909) D.A. Dunlop 1998
```
Where do we find information about whether a name is nomenclaturally correct,
next ...


Names which are good **nomenclaturally**
----------------------------------------

Theses are names that comply with relevant code(s) of nomenclature.
This category is more or less the same as we call ‘scientific names’. Code compliancy usually stops at the level of Family.

### Codes of nomenclature

The codes of nomenclature provide a set of rules as to how names of organisms
should be formed.  There are a number of codes, but most follow the same basic
rules

* Names should be formed of latinized names
* Names should be introduced (published) in a scientific document. The part of the document that includes the introduction of a name (or a change that complies with a code) is referred to as a nomenclatural act.
* Names of species have two words, the first, the genus, is capitalized; and they are usually presented in Italics
* There has to be a single specimen placed in a Museum or similar place that is an example and the ultimate reference of the species to which the name is used.
* In addition, the first species described in a genus is the type species for that genus, and the first genus described in a Family is the type for the family.
* If a name is used, the same name cannot be used for another kind of organism (but see homonyms and ambiregnal issues below)
* If two or more groups come up with different names for the same species, the first one to apply a name has priority

Different codes of nomenclature apply to:

* Animals (International Code of Zoological Nomenclature, or ICZN also referred to as the zoological code),
* Plants (The International Code of Nomenclature of Algae, Plants and Fungi - ICN or ICNAFP, the ‘botanical code’
* For bacteria, viruses, cultivated plants, and more
* The ‘Biocode’ an effort to create a unified framework for all of these ‘typological codes’ - i.e. ones that require a type specimen.
* Finally, there is the ‘Phylocode’ which is not typological, and is used to refer to clades of life.

In our case, the majority of names will be those that relate to the Botanical
and Zoological codes.

Nomenclatural criteria are 'objective' because scientific names are created in
a published nomenclatural act.

The names follow a standard format: Homo sapiens Linnaeus 1758, but may be
represented by variations on this theme - see the Carex example above.

The name may not be considered the appropriate name for a taxon.  Even if these
names are considered 'wrong' now -- they still represent a nomenclatural act
which really happened and therefore "good" nomenclaturally.

Code compliant names may be:

* Currently accepted names, i.e. a taxonomist says that this is the best name for a taxon.
* Valid synonyms of any sort -- homotypic synonyms (old combinations), heterotypic synonyms (two names for what was found be one species) - see below
* They may be annotated to, for example, to distinguish different taxon concepts (sensu, sec. ... "Stenometope laevissimus sec. Eschmeyer 2004" or "nec  Stenometope laevissimus sensu Patterson, 2001"). This is used to tell someone that the taxon I am talking about is as defined or used by Eschmeyer, but it is not the same as what Patterson meant when he used that name.
* Other annotations may refer to names described after the fact (ex ... like "Osmundaria obtusiloba (Mertens ex C. Agardh) R.E. Norris" which means Agardh added a name to an item, but did not describe it in a way that complies with a code;  later Mertens described it in proper compliance with the code, and later Norris created a new combination)
* Homonyms

Such names **do not include**:

* Misspellings except inasmuch as permitted or enforced by the codes, as they may require changes to names after publication
* Chresonyms (names containing authors who had nothing to do with the corresponding nomenclatural act ... like "Monochamus galloprovincialis De Fluiter, 1950"). Typically a chresonym is used to indicate the use of a name by a particular author.  In such a case, it should have a colon -- Homo sapiens:Mozzherin, 2015; but many taxonomic sources will include chresonyms among synonymies, and not distinguish the two.
* A name not properly described or published

Who keeps track of nomenclaturally correct names?
-------------------------------------------------

A subset of particularly diligent taxonomists will keep track of all of the
Code compliant names in their area of interest - Bill Eschmeyer, for example,
is the principal source for fish names.  There have been a major number of
books that have sought to keep track of nomenclaturally compliant names - Airey
Neave’s Nomenclator Zoologicus, Sherborne’s Index Animalium, or the Index
Nominum Genericorum (for plant genera).

Taxonomically authoritative sources, such as the World Spider Catalog are good
sources of nomenclatural information. There is no complete list of such
sources.

This responsibility is now passing to ‘registries’, one line environments that
keep track of new names. Examples are Index Fungorum, ZooBank, and
International Plant Name Index (IPNI).  Increasingly, these will replace
publications as the places where names officially appear.

The Global Name Usage Bank, based at Bishop Museum in Hawaii, was set up to
manage nomenclatural acts, and is the basis of ZooBank.

Ideally, GN could find code-compliant names by calling on services from
registries. Nice idea, BUT

* Even a good nomenclator is not complete
* Many taxonomic areas are not covered by nomenclators of any sort
* Digital nomenclators may not provide web services
* Some nomenclators do not freely release their information.

Can we be certain if a name is code-compliant?
----------------------------------------------

Yes, when a name occurs in a nomenclator, or in registry, or in an exemplary
taxonomic source -  you should trust that source. BUT, many (most) code
compliant names will not have made their way to on-line sources, so in the
digital age, you must exercise caution.

Special problem of ambiregnal taxa
----------------------------------

The jurisdiction of the codes assume that all organisms fall comfortably into
plants, animals, bacteria and so on. This is not the case. Some single-celled
protists are considered to be animals by some researchers, and the zoological
code has been applied to them.  But other researchers think of them as plants,
and have treated their nomenclature as those of plants.  In the case of the
cyanobacteria or blue green algae, they have been subject to both the botanical
and bacterial codes.

As the codes are independent of each other, the ‘correct’ name in one code may
be different to the correct name under another code. That is, there are two
objectively correct names for the taxon.

Special problems of chresonyms
------------------------------

Chresonyms are not things that many people are familiar with, but are a major
problem. A chresonym is a reference to the use of a name.  For example, a
review might state

```
Xysticus cristatus (Clerck, 1757) Koch, 1843
  Araneus cristatus Clerck, 1757
  Xysticus promiscuus O. Pickard-Cambridge, 1876
  Xysticus cristatus Levy, 1976
  Xysticus cristatus Levy 1985
  Xysticus cristatus: Azarkina & Logunov, 2001
  Xysticus caspicus Azarkina & Logunov, 2001
```

The indentation suggests the names following the first entry are synonyms.  The
list may even have the term ‘synonym’. While the first name is the basionym,
first use of cristatus for a spider, the second is the author’s view that
promiscuus, named as a  different species refers to the same organism (i.e. is
a heterotypic synonym), but the other four entries are chresonyms. The author
of the list is trying to say, I think Xysticus cristatus (Clerck, 1757) is the
same species as the thing described by Levy in 1976 and 1985, and by Azarkina
and Logunov under the name Xysticus cristatus, and also the organisms described
by Azarkina & Logunov under the name Xysticus caspicus.

Chresonyms are NOT code-compliant, because the person referred to is not the
author of the scientific name, rather they are users of the name. The
formulation of the name-string of a chresonym can be indistinguishable from a
code-compliant name.  In some cases, a reference is indicated by a colon, and
that is helpful.

How can you tell if a name string that parses to a canonical form is a code-compliant scientific name (i.e. is good) or is a chresonym (is bad).

* It is possible that a name string with the same genus and species but different authors are homonyms.  The number of species level homonyms are very low, and most have been compiled by Tony Rees (see IRMNG).
* If there is a colon in the name before author, then it is a chresonym
* Xysticus caspicus sensu Azarkina & Logunov, 2001 and Xysticus caspicus sec Azarkina & Logunov, 2001 are other ways that references to names may be written out
* If the genus name and species names match perfectly, but there are different authors and / or dates (that can’t be explained by a typographic error or different transliterations), then the later dated name will be the chresonym.

Special problems of Homonyms
----------------------------

Homonyms are names that are spelled in exactly the same way, but point to
different taxa. Homonyms may occur because a later taxonomist may not be aware
that the name has already been used. When this is discovered, the later homonym
has to be changed. Another source of homonyms is that the codes are
independent, so a name might have been used for an animal, but a botanist is
still free to use the same name for a plant

A major source of  names is IRMNG. It is compiled by Tony Rees. He believes he
has compiled over 95% of all generic names, and therefore knows most homonyms.
Perhaps 15% of generic names are homonyms, but the number of special names that
are homonyms is around a hundred or so.  Names currently accepted by
taxonomists (subjective) Taxonomists publish their views about the species, and
the most appropriate name for them in papers and books - some of which may take
many years to be published.  For each species, they will use the name that they
think is nomenclaturally correct, and based on their concept of the species,
decide which of the names that have ever been applied to this group, is the
best one.

The scientific names used by taxonomists to refer to species and other taxa are
fewer than all of the code compliant names. Such names are subjective because
they represent an opinion of taxonomists, and different taxonomists may slice
and dice the process of evolution (see heterotypic synonymy below).

The scientific names for taxa is a 'perfect' subset of names from the first
group. It can only be formed from nomenclaturally valid names.


Which names are "good" taxonomically?
-------------------------------------

What all taxonomists must do is to use the single nomenclaturally valid name
for the group that contains the type material.

### Taxonomic subjectivity &rarr; judgement

Different taxonomists may differ in their views.  This is because some are
lumpers and some are splitters, and when a taxonomist casts a ‘wider net’ to
draw in a larger sample or set, they may find that one name in the broader set
has priority over the name that is widely used for the narrower set preferred
by splitters.  Also names may change because taxonomy is a dynamic discipline
and closely linked to evolutionary studies. As relationships are revealed, taxa
may move from one place to another in a classification, and names have to
change so that the earliest name for the genus applies.

They will list names that have been used for a taxon, but are no longer the
right name, as ‘synonyms’.  Typically, there will be list with the correct name
(in their view) being listed without comment or stated to be the senior
synonym, and with incorrect names, sometimes prefaced with the word ‘synonyms’
listed below.


### Homotypic synonyms

Synonyms may be homotypic or heterotypic.  A homotypic synonym is ‘objective’
and comes from the priority rule in the codes of nomenclature.  If I describe a
new species of Paramecium (let us say Paramecium irelandicum), but someone
later shows that the type material has a feature that is distinctive for and
unique to an adjacent genus, Frontonia, then the name will be changed to
Frontonia irelandica.  We have simply moved the species into a different genus,
and with that act, we must, according to the codes, change the generic vehicle
to reflect the genus that contains the earliest described type species.  As
Paramecium and Frontonia must have had different types, when we create  a new
combination, at lkeast one name has changed.  The original name is the
basionym.  In cases where the genus has been changed, taxonomists may or not
include the authors of the names. When this change is referred to, some pedants
may well include the name of the author of the basionym in parentheses, and the
name of the author of the combination at the end.  Paramecium irelandicum Me,
2014 Frontonia irelandica (Me, 2014) Her, 2015 or Frontonia irelandica (Me) Her


### Heterotypic synonyms

When a taxonomist revises a taxon, they consider all of the nomenclatural and
taxonomic acts that have created species names, identified new species, and so
on.  Sometimes, they find that one later author (Patterson) has described as a
new species (Volvox irelandicum) something that has already been described by
Linnaeus (Volvox globator).  Perhaps Patterson is a splitter and the reviewer
is a lumper, or perhaps Patterson described an unusual form of Volvox
globator, or a special stage in the life history, or perhaps Patterson just
hadn’t read all of the literature.  The reviewer will conclude that Volvox
irelandicum is a synonym of Volvox globator. As Patterson, to be code
compliant, had to place a type in a Museum, the two names are ‘heterotypic
synonyms’, and the rule of priority demands that the first created name takes
precedence.

How do we get information from taxonomists
------------------------------------------

Taxonomists publish their views in scientific papers and books.

Some have on-line web-sites that carry information about species, one of the
best of which is FishBase.  Many who have web sites do not have any services to
allow machine-to-machine dialogue. For many other taxa, there are no on-line
sources.

The largest compilation of taxonomies is the Catalogue of Life.  It however
collects data on each taxonomic area from a ‘Global Species Database’ (GSD),
which means that the diversity of taxonomic opinion is not represented, and
some GSDs may be very slow in responding to requests for updates.  As a result,
CoL is not consistent in quality.

For the moment, we should accept the assumption, if the name is in Catalogue of
Life, it is taxonomically endorsed.

But, if a name is not in catalogue of life does not mean that is is NOT
taxonomically endorsed.

If a name is not in Catalogue of Life, but is in another taxonomic source,
then it is taxonomically endorsed.

Some compilations are less good and some more good.

Global Names collects lists and classifications, and we know where all names in
GNI come from.  That is, Global Names can indicate if it thinks a source is
taxonomically reliable and therefore is a source of ‘Good’ names.

[gnr]: http://resolver.globalnames.org