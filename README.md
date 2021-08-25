# unison-read

Provides a `Read a` ability, along with some combinators and handlers, that allows for incrementally consuming some `a`s to produce a result or fail.

## Example

```unison
csv : '{Read Char} [[Text]]
csv = 'let
  cell = '(fromCharList (any '(none [?\n, ?,])))
  cells = '(!cell +: or more '[])
  more = '('(one ?,) *> cells)
  lines = '(!cells +: or moreLines '[])
  moreLines = '('(one ?\n) *> lines)
  !lines

> readText csv "123,123,123\n12,12\n1"
    ⧩
    ReadResult
    (3, 1)
    (Right
        [ ["123", "123", "123"],
        ["12", "12"],
        ["1"] ])
```

## Install

```
.> pull https://github.com/thoradam/unison-read:.releases._v1 .external.read.v1
```
