
# the "call" instruction

```
define sub
  trace a
call sub a, b

# => args: { _0: a, _1: b }
```

```
define sub g
  trace a
call sub a, b

# => payload.args: { _0: a, _1: b } and
#    payload.g: a

# OR

# => payload.args: { _1: b } /* remaining args */ and
#    payload.g: a
```

```
define sub g0 v.g1
  trace a
call sub a, b

# => payload.args: {} /* remaining args */ and
#    payload.g0: a
#    vars.g1: b
```

```
define sub g0 g1
  trace a
call sub g1: a, g0: b

# => payload.args: {} /* remaining args */ and
#    payload.g0: b
#    payload.g0: a
```

Following "invoke"'s lead:

```
define sub
  trace a
call sub g1: a, g0: b

# => vars.args: { _0: sub, g1: a, g0: b }
```

or directly

```
define sub
  trace a
call sub g1: a, g0: b

# => vars: { _0: sub, g1: a, g0: b }
```

`vcall` vs `fcall` vs `call`?

