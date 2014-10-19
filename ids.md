
# ids

* domain: `acme.main` or `acme.ch.main`
* exid: execution id
* nid: node id

## domain

A tree of names, read from left to right. Domains are used to allow/reject executions and invocations. For example a feu might be set to only allow "acme.ch.sales" prefixed executions/invocations.

## exid

```ruby
"{domain}-{yyyyMMdd}.{hhmm}.{NNNNN}"

# for example:
"acme.ch.main-20141015.0955.tekuneko"
```
(Eventually prefix with flon execution unit id?)

## nid

```ruby
"{treeid}-{counter}"

# for example:
"0.1-f"
```

`counter` is in hexadecimal.

Eventually: make a trailing `-0` optional.

## treeid

Where to locate the node in the execution tree. Elements are separated by dots. Elements are in hexadecimal.

```ruby
#for example:
"0"
"0.1a"
```

## exnid (or enid)

Exid + nid.

```ruby
"{exid}-{nid}"

# for example:
"acme.ch.main-20141015.0955.tekuneko-0.1a-f"
"acme.ch.main-20141015.0955.tekuneko-0.2"
```

