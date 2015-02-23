
# taskmaster

## terms

* tasker: the piece of code that handles a task
* taskmaster: usually flon-tasker, forking the tasker and handing it the task
* tasked: the designation (string) pointing to a tasker, as seen in the flon execution
* taskee: another designation (string) pointing to a tasker, as determined by the taskmaster

## mission

The taskmaster is forked by the dispatcher.

The taskmaster is expected to hand the task to the `tasked` (the name/string as found in the execution, `task xyz`).

If there is a `taskee` field, it's used in lieu of the `tasked` field (tree.1._0).

## taskmaster.rad

If the taskmaster is given a task for a domain with a taskmaster.rad, it interprets it to determine the `taskee`.

If there is no `taskee`, the task goes to the `tasked`.

One level of indirection.

No need to fork, just interpret taskmaster.rad transiently. The answer can be interpreted immediately.

## taskmaster.pl / taskmaster.json

Need to fork, and reply to the dispatcher. The dispatcher then hands the answer to a new fork of flon-tasker.

## tasker.rad

Tasker.rad indicates a tasker implemented in .rad. No need to fork, it is executed transiently immediately.

Could the tasker.rad and taskmaster.rad handling mechanisms be shared?

And if the mecha were the same? It's somehow duplicating a bit of the dispatching mecha? Well, the dispatcher simply forks a flon-tasker, nothing more... Well, it may fork flon-executor as well...

## misc

How does the taskermaster.rad lookup fall through the domain tree?

The impl steps could be a) tasker.rad b) taskmaster.rad

