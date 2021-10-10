# S-expression standard: Low-level constants

## Status

Draft

## Abstract

This document defines a S-expression schema to represent constant
values extracted from code written in low-level programming languages.
Values can be strings, integers (signed or unsigned), or real numbers.
Additionally, information about the size and offset of record fields
can be encoded. Input and outputs suitable for a "groveler" (a program
to retrieve such values) are specified.

## Rationale

## Specification

### Groveler input language

```
(pkg-config-path <string>)
(pkg-config <string>)
(include <angle-bracket-header>)
(include "string-header")
(error <string>)
(warning <string>)

(when <expression>
  <body>...)

(type-signedness <type>)
(type-size <type>)
(type-slot <type> <slot>)
(constant <constant> signed|unsigned|string)
(call-constant <function> <constant> signed|unsigned|string)
(constant-ifdef <constant> signed|unsigned|string)
(call-constant-ifdef <function> <constant> signed|unsigned|string)
```

### Groveler output language

```
(constant <constant> <value>)
(call-constant <function> <constant> <value>)
(type-signedness <type> <signedness>)
(type-size <type> <size>)
(slot-size <type> <slot> <size>)
(slot-offset <type> <slot> <size>)
```

## Examples

### GTK

Input:

```
(constant GTK_STYLE_PROPERTY_BACKGROUND_COLOR string)
(constant GTK_STYLE_CLASS_DIM_LABEL string)
(constant GTK_WINDOW_TOPLEVEL unsigned)
```

Output:

```Lisp
(constant GTK_STYLE_PROPERTY_BACKGROUND_COLOR "background-color")
(constant GTK_STYLE_CLASS_DIM_LABEL "dim-label")
(constant GTK_WINDOW_TOPLEVEL 0)
```

### Conditionals and function calls

Input:

```Lisp
(include <errno.h>)
(include <string.h>)
(constant-ifdef EACCES signed)
(call-constant-ifdef strerror EACCES string)
```

Output when found:

```
(constant EACCES 13)
(call-constant strerror EACCES "Permission denied")
```

Output when missing:

```
(constant EACCES undefined)
(call-constant strerror EACCES undefined)
```
