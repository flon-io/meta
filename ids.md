
# ids

* domain: `acme.main` or `acme.ch.main`
* exid: execution id
* nid: node id

## symbols

```ruby
/^[a-z0-9_]+$/
```

NB: no uppercases.

## domain

A tree of names, read from left to right. Domains are used to allow/reject executions and taskings. For example a feu might be set to only allow "acme.ch.sales" prefixed executions / taskings.

Symbol dot symbol.

## feu

Flon execution group id dot flon execution unit id.

```ruby
"{feg-id}.{feu-id}"

# for example:
"group.unit0"
"g0.u0"
"u0"
```
The feg-id should be optional.

Symbol dot symbol.

## tid

Time id.

```ruby
"{yyyyMMdd}.{hhmm}.{NNNNN}"

# for example:
"20141015.0955.tekunekogo"
```

## exid

```ruby
"{domain}-{feu}-{tid}"

# for example:
"acme.ch.main-g0.u0-20141015.0955.tekunekogo"
```
(Eventually prefix with flon execution unit id?)

## nid

```ruby
"{treeid}-{counter}"

# for example:
"0_1-f"
```

`counter` is in hexadecimal.

Eventually: make a trailing `-0` optional.

## treeid

Where to locate the node in the execution tree. Elements are separated by underscores. Elements are in hexadecimal.

```ruby
#for example:
"0"
"0_1a"
"0_1a_4"
```

## exnid (or enid)

Exid + nid.

```ruby
"{exid}-{nid}"

# for example:
"acme.ch.main-g0.u0-20141015.0955.tekuneko-0_1a-f"
"acme.ch.main-g0.u0-20141015.0955.tekuneko-0_2"
```

