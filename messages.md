
# messages

The messages are mostly "orders", "do execute", "do invoke", "do receive".

## execute

```js
{
  exid: "xxx", // execution id
  nid: "xxx", // node id
  execute: [ "invoke", { "_0": "stamp" }, [] ],
  payload: { color: "blue" }
}
```

### launch

There is no `nid`. The `exid` is given upwards.

```js
{
  exid: "xxx", // execution id
  execute: [ "invoke", { "_0": "stamp" }, [] ],
  payload: { color: "blue" }
}
```

## invoke

```js
{
  exid: "xxx",
  nid: "yyy",
  invoke: [ "invoke", { "_0": "stamp" }, [] ],
  payload: { color: "blue" }
}
```

## receive

```js
{
  exid: "xxx",
  nid: "yyy",
  receive: 1,
  payload: { color: "red" }
}
```

