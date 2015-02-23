
# tasker

A tasker is a piece of code that receives a task as JSON through its STDIN. It them emits it back, potentially updated, via its STDOUT.

A tasker resides in a directory with its name under `usr/local/tsk/{domain}`.

Where domain is either `any`, for taskers available to any domain or a fully or incompletely expanded domain name. For example, one might have `usr/local/tsk/com.acme.accounting/` and `usr/local/tsk/com.acme/` paths. Taskers under `tsk/com.acme/` are available to all the `com.acme` executions, while `com.acme.accounting/` is only for ACME accounting executions.

## flon.json

A tasker is reachable through its `flon.json`, a small configuration file read by `flon-tasker` when working on handing the task to the "real" tasker.

```
in: all
run: "ruby thattasker.rb -e $(exid) -x $(pl.xyz)"
out: xxx
```

