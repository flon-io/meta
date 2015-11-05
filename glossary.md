
# glossary


### composition

definition
program? routine? model? formulation? description?
enumeration? (musical) score? composition?

### execution

The carrying out of a definition.

### flon-tasker
### flon-dispatcher
### flon-executor
### flon-listener

### tasking

Handing a task (workitem) to a service/action/actor external to flon.

### tasker

A piece of code that receives a task (workitem) from flon-tasker (taskmaster) and carries it out himself, or hands it somewhere else and gives back the result once available.

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

