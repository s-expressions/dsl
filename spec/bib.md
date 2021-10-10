# S-expression standard: Bibliography

## Status

Draft

## Abstract

This document defines a S-expression format for bibliographies of
academic papers. It is based on the popular BibTeX format.

## Rationale

### Known entry types

* `article`
* `book`
* `booklet`
* `conference`
* `inbook`
* `incollection`
* `inproceedings`
* `manual`
* `mastersthesis`
* `misc`
* `phdthesis`
* `proceedings`
* `techreport`
* `unpublished`

## Specification

```Lisp
(define-schema bib

  (entry
    `(entry
       (cite ,string)
       (type ,symbol)
       (fields ,@field)))

  (field
    `(,symbol ,@field-value-part))

  (field-value-part
    (or symbol
        string
        (integer 0)
        personal-name))

   (personal-name
     (import standard.s-expressions.org/personal-name)))
```

## Examples

```Lisp
(entry
 (cite "abramowitz+stegun")
 (type book)
 (fields
  (author (personal-name (last-name "Abramowitz") (other-names "Milton")))
  (author (personal-name (last-name "Stegun") (other-names "Irene A.")))
  (title "Handbook of Mathematical Functions with Formulas, Graphs, and Mathematical Tables")
  (publisher "Dover")
  (year 1964)
  (address "New York City")
  (edition "ninth Dover printing, tenth GPO printing")))
```

```Lisp
(entry
 (cite "Haskell-2019")
 (type proceedings)
 (fields
  (acmid "3331545")
  (doi "10.1145/3331545")
  (editor (personal-name (last-name "Eisenberg") (other-names "Richard A.")))
  (isbn "978-1-4503-6813-1")
  (publisher "ACM")
  (title "Proceedings of the 12th International Symposium on Haskell")
  (year 2019)))
```

## Rerefences

* [Citation Style Language 1.0.1 Specification](https://docs.citationstyles.org/en/1.0.1/specification.html). Zelle, Bennett, D’Arcus.
