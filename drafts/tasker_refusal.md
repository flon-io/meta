
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

## execution vs tasking

Execution is "workflow", tasking is "resource allocation". Sometimes they are intertwined, some other times they are kept separate.

As an idealist idiot looking for some elegant design, I'd love them to be kept separate, orthogonal. But there are many organizations out there and many ways of thinking. I can carve a tool right, it will somehow fit my hand, but there are other hands out there, that could possibly wield my tool to greater effect.

Execution is carried out by the executor. Tasking is carried out by the task\[mast\]er.

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

the imperative points:

* *completed*, the default, task has been completed
* *failed*, tasker tried but failed somehow
* *refused*, tasker has not touched the task, it refused it
* *uncompleted*, tasker did some work, but could not complete, more work is expected

the informative points:

* started
* suspended
* allocated
* offered

Upon receiving an 'informative' point, the executor simply flags the `task` node with a `task_status`.

```
  task_status:
  [
    { tasker: zozo, taskee: toto, point: started, ctime: 1234 },
    { tasker: zozo, taskee: toto, point: suspended, ... }
  ]
```

OR, should that go not in the `execution.nodes.0_0-1` but in some `tsk.0_0-1.log` file?
Does the execution need to access that information? Do some of the execution logic require that information? Sometimes that logic goes into the execution, sometimes it goes into the tasking...

log file:
* plus: no need to read the whole execution to get at the status
* plus: previous assignments are there, event if the node is dead
* zero: one log file per node?

task status array in node:
* plus: easily accessible from the executor
* minus: gone when the node is gone

All these worries for task history... Is task history confined to its execution?

## taskee, misc

Could it be something like `task.taskee` or `task._taskee_`?
Does the task comprises headers? Should the taskee go into those headers?
The tasker only sees the payload.

Should we have a `flon.json` option that says "dump the whole task, not just the payload"?

The task\[master\].rad has access to the whole task. It should have access to some "headers"...

