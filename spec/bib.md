# BibTeX as S-expressions

## Known entry types

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

## People's names

```Lisp
(person
 (last-name "John")
 (other-names "P. Q. Public"))

(person
 (last-name "von Neumann")
 (other-names "John")
 (sort-key "von Neumann"))

(person
 (last-name "von Ettingshausen")
 (other-names "Andreas" "Freiherr")
 (sort-key "Ettingshausen"))

(person
 (full-name "鮑岳橋")
 (sort-key "Yueqiao"))
```

`(person ...) `can be used inside `(author ...)` and `(editor ...)` to
give a person's name in a way that makes it easy to separate the first
and last name for indexing and different styles of display.

## Examples

```Lisp
(entry
 (cite "abramowitz+stegun")
 (type book)
 (field
  (author (person (last-name "Abramowitz") (other-names "Milton")))
  (author (person (last-name "Stegun") (other-names "Irene A.")))
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
  (editor (person (last-name "Eisenberg") (other-names "Richard A.")))
  (isbn "978-1-4503-6813-1")
  (publisher "ACM")
  (title "Proceedings of the 12th International Symposium on Haskell")
  (year 2019)))
```

## Rerefences

* [Falsehoods Programmers Believe About Names](https://www.kalzumeus.com/2010/06/17/falsehoods-programmers-believe-about-names/)
