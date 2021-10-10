# S-expression standard: Personal name

## Status

Draft

## Abstract

This document defines a S-expression format for representing people's
names. It aims to allow customary splitting and rearrangement for most
names of European descent, while signaling that names which don't
adhere to these customs should stay intact. Fully customizable sorting
and collation is provided for all names.

## Rationale

```Lisp
(personal-name
 (last-name "John")
 (other-names "P. Q. Public"))

(personal-name
 (last-name "von Neumann")
 (other-names "John")
 (sort-key "von Neumann"))

(personal-name
 (last-name "von Ettingshausen")
 (other-names "Andreas" "Freiherr")
 (sort-key "Ettingshausen"))

(personal-name
 (full-name "鮑岳橋")
 (sort-key "Yueqiao"))
```

## Rerefences

* [Falsehoods Programmers Believe About Names](https://www.kalzumeus.com/2010/06/17/falsehoods-programmers-believe-about-names/). Patrick McKenzie. 2010-06-17.

* [Against Structured Names And Telephone Numbers](https://docs.google.com/document/d/1Of_rL8gMtHcfPaE5DfZ1xahrOtOaxFEHiQkcxvvR3lY/edit). John Cowan. 2009-04-22.

* [BibTeX sorting and name prefixes](https://texfaq.org/FAQ-bibprefixsort)

* BibTeX and sorting names with `von' prefixes. [[Google Groups](https://groups.google.com/g/comp.text.tex/c/pQCPH3fwGSE)]

* [Names (texhelp)](https://nwalsh.com/tex/texhelp/bibtx-23.html). Norman Walsh.
