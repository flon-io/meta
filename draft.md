
# draft about instructions

* instruction names are nouns, "concurrence", "sequence", "iterator"
* "cursor" is merged into "sequence"

```
concurrence
  a
  b

sequence
  a
  b
  break if x > 1000
  rewind if x > y
  c

sequence blue
  x
  sequence
    a
    b
    break blue if x == 1
    break if x == 2
    c
  y
```

## "break" and "rewind" and "cancel" and "return"

they return to the expression
they accept a "tag", except return

"return" stops at subexecution root
that could be where the counter changes?

_counter is a the root of the execution, each time there is an iteration, subexecution, ... the counter is incremented... Why not? Expressions would use a next_count(node) method.
What if an expression is orphan, should it start a new counter at zero?
Ruote generated ids on the fly...
Should the executed thing keep its own counter? ```sub0: { tree: [ ... ], counter: 0 }```

does "return" set a $(ret) value?

```
iterator [ 1, 2, 3 ]
  a $(e)
  break if x

citerator [ 1, 2, 3 ]
  a $(e)
```

## if

```
sequence if x > y
  a
  b

if x > y [then]
  a
  b
else
  c
  d

if x > y
  sequence # then
    a
    b
  sequence # else
    c
    d

if x > y
  then # alias to sequence
    a
    b
  else # alias to sequence
    c
    d
# this is easier to implement ...
```

await, listen...
add_branch, add_branches (I dislike the names)

on_cancel, on_return (finally), on_timeout
as attribute and as instruction...

```
define sub0
  x
  y

sequence timeout 5h, ontimeout sub0
  a
  b

sequence timeout 5h
  ontimeout sub0
  a
  b

sequence timeout 5h
  ontimeout # sequence
    x
    y
  a
  b
```

## forget vs lose vs flank

* forget: replies to parent expression immediately, is not cancellable (not reachable).
* lose: never replies to the parent expression, is cancellable.
* flank: immediately replies to the parent expression, is cancellable.

Should we thus have, for each 'parent' expression a set of lists "children", "flankers", "losers"?

Is "lost" identical to "flanking"?

