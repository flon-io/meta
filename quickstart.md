
# flon quickstart

## prerequisites

* c99 compiler
* some kind of libc
* libev (~> 4.11)

## method

steps here:

* clone flon
* provision an instance of flon (tree of binaries and data)
* implement a tasker
* run the dispatcher (the heart of the flon engine)
* launch an execution
* inspect that execution, now hopefully completed

```
git clone https://github.com/flon-io/flon
cd flon

make provision T=flon0
  # that creates a flon instance under flon0/
```

Implementing a tasker:
```
mkdir flon0/usr/local/tsk/any/greeter/

cat > flon0/usr/local/tsk/any/greeter/flon.json
ontask: { cmd: 'ruby greeter.rb' }
<CTRL-D>

cat > flon0/usr/local/tsk/any/greeter/greeter.rb
require 'json'
task = JSON.parse(STDIN.read)
task['greetings'] = "greetings to #{task['name']}"
task.delete('name')
STDOUT.puts(JSON.dump(task))
<CTRL-D>
```
This is a very simple tasker, it does a simple trick with the task and replies immediately.

This tasker is placed under the domain "any", which means that executions from any domain may use it. To restrict its use to the "org.example" domain (and its subdomains), you would have to place it under a directory named "org.example" at the same level as "any".

In a first console:
```
cd flon0

./bin/flon-dispatcher
```

In a second console:
```
cd flon0

# launch an execution

cat > t.flon
# domain
org.example.greetings
# tree
sequence
  task greeter
# payload
name: Kenneth
<CTRL-D>

bin/flon launch t.flon
  # --> something like "org.example.greetings-u0-20150306.0824.mugemijuba"

# inspect the execution

bin/flon scope muge
  # or simply,
bin/flon scope
  #
  # the last msg should contain `greetings: "greetings to Kenneth"`
```

