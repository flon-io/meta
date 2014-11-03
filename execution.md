
# execution

## serialization

```js
{
  //trees: {
  //  original:
  //    [ "sequence", {}, [
  //      [ "invoke", { "_0": "stamp" }, [] ]
  //    ] ],
  //  "0_0-0": [ "invoke", { "_0": "stamp2" }, [] ]
  //},
  nodes: {
    "0-0": { tree: [ ... ] },
    "0_0-0": {}
  },
  errors: {
  }
  // timers? watches?
}
```
### nodes

```js
{
  nid: "0_0",
  t: "invoke",
  c: "20141103.072803.123", // created
  m: "20141103.072804.654",  // modified
  p: null // no parent
  // ...
}
```

#### `p` (parent)

When pointing to `null`, it means the node is a root.
Else p contains the nid of its parent.

