
# trees

Trees are Abstract Syntax Trees.

The structure of a tree is:
```js
[
  head,  // string or tree
  {},    // attributes
  12,    // line number
  []     // children (array of trees)
]
```

For example, the radial expression `task Alan value: (1 + 2)` will get parsed and translated to:
```js
[ 'task',
  { _0: 'Alan',
    value: [
      [ 'val', { _0: 1 }, 1, [] ],
      { _0: '+', _1: 2 },
      1,
      [] ] }
  1,
  [] ]
```

