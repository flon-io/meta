
# flon quickstart

## prerequisites

* c99 compiler
* some kind of libc
* libev

## method

```
git clone https://github.com/flon-io/flon
cd flon

make provision T=flon0

#
# in a first console

cd flon0

./bin/flon-dispatcher

#
# in a second console

cd flon0

# launch an execution

cat > t.flon
# domain
org.example
# tree
sequence
  trace 'hello $(name)'
  trace 'hello again, $(name)'
# payload
name: Kenneth
<CTRL-D>

bin/flon launch t.flon
  # --> something like "org.example-u0-20150306.0824.mugemijuba"

# inspect the execution

bin/flon scope muge
  # or simply,
bin/flon scope
```

