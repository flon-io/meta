
# ret

## in use

```
  sequence
    3 > 3
    # now "ret" is false (or 0 ?)
    4 < 5
    # now "ret" is true
    if
      4 < 5
      trace "hello"
    # "hello" just got traced
```

"ret" is usually read by the next instruction to get executed. Well, in the case above, it's read by the "if" receiving the answer from ```4 < 5```.

## ret as rcv.payload.ret

An instruction sets its return value as the field "ret".

* + tasker may set it easily (like an instruction would do)
* + easily read
* - it stays as the flow goes on

## ret as vars.ret

An instruction sets its as the "local" variable "ret".

* + it's hidden from the taskers
* + easily read

## ret as rcv.ret

An instruction sets its return as the "ret" entry in the return (parent.receive()) message.

* + it's hidden from the taskers
* - there must be a function to read the "ret" (not just lookup_var() or lookup_field())

## notes

Each time an instruction returns "v" (over) it should set "ret", even setting it to nothing or "null".

It could be reset each time an instruction gets executed.

## truth values

0 and false are false, right?

