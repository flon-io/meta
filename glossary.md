
# glossary


### composition

definition
program? routine? model? formulation? description?
enumeration? (musical) score? composition?

### dispatcher

The dispatcher is the core flon program. It watches for incoming files and forks flon-executor processes to deal with them.

It also keeps track of schedules and triggers them at their appointed times.

See [flon-dispatcher](#flon-dispatcher)

### execution

The carrying out of a definition.

### flon-tasker

The executable forked by the [dispatcher](#dispatcher) when it has to deal with a task. The tasker

### flon-dispatcher

The executable implementing the [dispatcher](#dispatcher).

### flon-executor

The executable forked by the [dispatcher](#dispatcher) when an execution starts or starts again. An execution starts when the dispatcher receives an execution message, while it restarts when a task reply comes or a schedule is triggered by the dispatcher.

### flon-listener

The executable implementing the [listener](#listener).

### listener

The listener is the web interface to Flon. It listens for incoming execution requests via POSTS and eventual external tasker replies via POST as well.

It also lets external systems query the flon execution unit the listener belongs to.

See [flon-listener](#flon-listener).

### schedule

An "at" or a "cron" schedule. Messages kept for delayed execution (at) or for repeated execution with a given frequency (cron).

Schedules are managed and triggered by the [dispatcher](#dispatcher).

### task

Sometimes called a "workitem". A piece of information handed by flon to an external tasker. Usually flon expects an answer after the task has been performed in some way.

### tasking

Handing a task (workitem) to a service/action/actor external to flon.

### tasker

A piece of code that receives a task (workitem) from flon-tasker (taskmaster) and carries it out himself, or hands it somewhere else and gives back the result once available.

See also [flon-tasker](#flon-tasker).

### taskmaster

The flon-tasker binary/executable. Receives task from the dispatcher, looks up taskers, forks them, hand them the tasks.

### taskbox

A "worklist" of tasks offered/allocated/started/suspended for "users".

### tasklog

For a given execution, the list of msgs related to tasks. Mostly a filtered version of the msgs.log of the execution.

### node

A piece of flon execution.

### flon execution unit (feu)

A pair listener + dispatcher and their executors and taskers.

### flon execution group (feg)

A group of flon execution units, known to each other.

