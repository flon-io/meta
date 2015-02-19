
# draft about tasker refusal

A tasker may refuse a task.

## steps

1. Executor hands task to taskmaster via dispatcher
2. Taskmaster runs tsk/{domain}/task\[mast\]er.rad if present, that script may set `_taskee_`
3. Taskmaster finds tasker pointed at by `_taskee_` or `task.tree.1._0`
4. Taskmaster forks tasker
5. Tasker hands back task to dispatcher
6. Vanilla case, dispatcher hands back task to executor. Refusal case, dispatcher hands back task to taskmaster, back to 2.

