
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
```

No need for a payload.

## taskee, misc

Could it be something like `task.taskee` or `task._taskee_`?
Does the task comprises headers? Should the taskee go into those headers?
The tasker only sees the payload.

Should we have a `flon.json` option that says "dump the whole task, not just the payload" ?

The task\[master\].rad has access to the whole task. It should have access to some "headers"...

