
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

It's easy for "iterator", "citerator" to keep their own counters
Should the "sub definitions" keep their own counters? ```sub0: { tree: [ ... ], counter: 0 }``` (definition)
Warning: each time the "sub definition" gets applied, the counter might get reset...
The "execution" could hold the counter (not a root variable)... -0 then -1. better.

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

```
if x > y and z < u
  a

if sub0
  a

if sub0 and x > 3
  a

if sub0 > 3
  a

if
  and
    sub0
    $(ret) > 3
  a
```

"and" executes until false (returns false) else returns true
"or" excutes until true (return true) else returns false
"sequence" executes all in sequence
"cand" executes all concurrently and returns true if all returned true
"cor" executes all concurrently and returns true if at least one returned true

That begs for a $(ret) field. How did ruote do that?
ruote had a __result__ field.

## cond

```
#(cond ((> 3 3) 'greater)
#      ((< 3 3) 'less)
#      (else 'equal))
cond
  $(x) > 3
  a
  $(x) > 1
  b
  else
  c
```

Well...

## more instructions

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

```
sequence
  flanking
    a
  b

sequence
  forget
    a
  b

sequence
  lose
    a
  b
```

| exp    | replies     | cancellable |
|--------|-------------|-------------|
| forget | immediately | no          |
| lose   | never       | yes         |
| flank  | immediately | yes         |
| ???    | never       | no          |

```
sequence
  sequence reply: immediately cancellable: no
    a
  b
```

becomes

| exp    | child ? | cancellable |
|--------|---------|-------------|
| forget | no      | no          |
| lose   | yes     | yes         |
| flank  | no      | yes         |
| ???    | yes     | no          |

```
sequence
  sequence child: no cancellable: no
    a
  b
```

By default, goes into the "children" array...

"children", "flanking"
"children", "estranged", "disowned"
"children" vs "bastards"

* "children", you wait for them, you cancel them
* "bastards", you cancel them
* what are they when you don't cancel them? forgotten, they don't get listed

