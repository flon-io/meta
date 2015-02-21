
# map, filter, fold

## map, for-each

```
sequence
  [ 1, 2, 3 ]
  map
    * $(ret) 3
  # ret -> [ 3, 6, 9 ] ?
```

```
sequence
  [ 1, 2, 3 ]
  map *
    # ~~> * 1 2 3
```

```
  map [array_or_object] [as fname_or_vname]
    [sequence]
# or
  map [array_or_object] [as fname_or_vname] [callable]

[ 1, 2, 3]
map as i
  + $(i) 7
#
map [ 1, 2, 3 ] as i
  + $(i) 7
```

```
  1 * 2 * 3
#
# gets rewritten as
#
  * 1 2 3
#
# as
#
  *
    1
    2
    3
```

