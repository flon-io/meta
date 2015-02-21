
# draft about tasker refusal

A tasker may refuse a task.

## steps

1. Executor hands task to taskmaster via dispatcher
2. Taskmaster runs tsk/{domain}/task\[mast\]er.rad if present, that script may set `_taskee_`
3. Taskmaster finds tasker pointed at by `_taskee_` or `task.tree.1._0`
4. Taskmaster forks tasker
5. Tasker hands back task to dispatcher
6. Vanilla case, dispatcher hands back task to executor. Refusal case, dispatcher hands back task to taskmaster, back to 2.

## refusal and payload

One could imagine that refusing would return

```
{ point: refused, reason: xyz, payload: { ... } }
```

Instead of only the payload.

Or even

```
{ point: refused, reason: xyz }
  # or
{ point: refused, reason: { msg: xyz } }
```

No need for a payload.

## states and points

### states

* created
* offered (to 1 res, to many res)
* allocated (to a single resource)
* started
* suspended
* failed
* completed

### points

```
{ point: failed, error: { msg: xyz } }
  # or
{ point: failed, reason: xyz }
```

* *completed*, the default, task has been completed
* *failed*, tasker tried but failed somehow
* *refused*, tasker has not touched the task, it refused it
* *uncompleted*, tasker did some work, but could not complete, more work is expected

Upon receiving an 'informative' point, the executor simply flags the `task` node with a `task_status`.

```
  task_status:
  [
    { tasker: zozo, taskee: toto, point: started, ctime: 1234 },
    { tasker: zozo, taskee: toto, point: suspended, ... }
  ]
```

OR, should that go not in the `execution.nodes.0_0-1` but in some `tsk.0_0-1.log` file?

* started, informative
* suspended, informative
* allocated, informative
* offered, informative

## taskee, misc

Could it be something like `task.taskee` or `task._taskee_`?
Does the task comprises headers? Should the taskee go into those headers?
The tasker only sees the payload.

Should we have a `flon.json` option that says "dump the whole task, not just the payload"?

The task\[master\].rad has access to the whole task. It should have access to some "headers"...

