
# tasker

A tasker is a piece of code that receives a task as JSON through its STDIN. It then emits it back, potentially updated, via its STDOUT.

A tasker resides in a directory with its name under `usr/local/tsk/{domain}`.

Where domain is either `any`, for taskers available to any domain or a fully or incompletely expanded domain name. For example, one might have `usr/local/tsk/com.acme.accounting/` and `usr/local/tsk/com.acme/` paths. Taskers under `tsk/com.acme/` are available to all the `com.acme` executions, while `com.acme.accounting/` is only for ACME accounting executions.


## flon.json

A tasker is reachable through its `flon.json`, a small configuration file read by `flon-tasker` when working on handing the task to the "real" tasker.

```
in: all
run: "ruby thattasker.rb -e $(exid) -x $(pl.xyz)"
out: xxx
```

### run

### in

### out


## responses

by default, a tasker responds with the task payload, potentially modified. The default "point" is "completed".

There are other potential answers. The schema for a not-"completed" response is:

```
{
  point: string,   # mandatory
  reason: string,  # optional
  taskee: toto,    # optional
  payload: {...},  # optional
}
```

### point

#### active points

May be set to "completed" (default), "uncompleted", "refused", "failed".

On "completed", the execution resumes.

On "uncompleted", the taskmaster is given the task again, it thus determines a new taskee and hands it the task. The "payload" is expected to be set (with potential modifications), this new, modified payload is handed to the \[new\] taskee. If a new taskee cannot be determined, the taskmaster responds with "failed".

On "refused", the taskmaster has to determine a new taskee, like for "uncompleted", but the payload is not expected. The new taskee will receive a copy of the original, refused, task. If a new taskee cannot be determined, the taskmaster responds with "failed".

On "failed", the execution is notified and does what it can (error handling, etc...)

#### informative points

* started
* suspended
* allocated
* offered

TODO

### reason

### taskee

### payload

