
# messages

The messages are mostly "orders", "do execute", "do invoke", "do receive".

## execute

"execute" filenames are prefixed with "exe_".

```js
{
  exid: "xxx", // execution id
  nid: "xxx", // node id
  execute: [ "invoke", { "_0": "stamp" }, [] ],
  payload: { color: "blue" }
}
```

## invoke

"invoke" filenames are prefixed with "inv_".

```js
{
  exid: "xxx",
  nid: "yyy",
  invoke: [ "invoke", { "_0": "stamp" }, [] ],
  payload: { color: "blue" }
}
```

## receive

"receive" filenames are prefixed with "rcv_". Except when they come from invocations, in which case they are prefixed with "ret_" (return).

```js
{
  exid: "xxx",
  nid: "yyy",
  receive: 1,
  payload: { color: "red" }
}
```

