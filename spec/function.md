# S-expression standard: Function signature

## Status

Draft

## Abstract

This document defines an S-expression representation of function
signatures. The signature is general enough to covers the function,
procedure, and method calls in many existing programming languages.
Argument names and types, as well as return types, can be given.

## Rationale

## Specification

```Lisp
(define-schema function

  (function
    `((signature (,symbol ,@symbol)
                 (returns ,type))
      (fragment ,string)
      (source ,any)
      (kind ,kind)))

  (kind
    (choice 'procedure))

  (type
    symbol))
```

## Examples

```Lisp
((signature (cons a d)
            (returns pair))
 (fragment "cons")
 (source (srfi 1))
 (kind procedure))

((signature (list object ...)
            (returns list))
 (fragment "list")
 (source (srfi 1))
 (kind procedure))
```

## Rerefences

[Common Lisp HyperSpec, section 3.4 Lambda Lists](http://www.lispworks.com/documentation/HyperSpec/Body/03_d.htm)
