
# messages

The messages are mostly "orders", "do execute", "do task", "do receive".

There are messages whose point is to convey an event. "failed", "launched", "terminated".

Event messages are logged in the msgs.log. Event messages are transmitted to subscribers as well.

## execute

"execute" filenames are prefixed with "exe_".

```js
{
  point: "execute",
  exid: "xxx", // execution id
  nid: "xxx", // node id
  tree: [ "task", { "_0": "stamp" }, [] ],
  payload: { color: "blue" }
}
```

## task

"task" filenames are prefixed with "tsk_".

```js
{
  point: "task",
  exid: "xxx",
  nid: "yyy",
  tree: [ "task", { "_0": "stamp" }, [] ],
  payload: { color: "blue" }
}
```

## return

Return files are written by tasker implementations. They contain the raw payload of the tasker's reply. The dispatcher turns that ret_ file into a regular receive "rcv_" file.

The dispatcher determines the nid (and exid) of the return by its filename.

```js
{
  // ... payload ...
}
```

## receive

"receive" filenames are prefixed with "rcv_".

```js
{
  point: "receive",
  exid: "xxx",
  nid: "yyy",
  payload: { color: "red" }
}
```

## schedule

"schedule" filenames are prefixed with "sch_".

```js
{
  point: "schedule",
  at: "20141128.103239", // seconds (not below)
  //cron: "* * * * *", // minutes (not seconds)
  exid: "xxx",
  nid: "yyy", // identify scheduler
  msg: { point: "receive", exid: "aaa", nid: "bbb", ... }
    // identify scheduled
}
```

## launched

"evt_"

TODO

## terminated

TODO

## failed

TODO

