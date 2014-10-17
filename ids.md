
# ids

* domain: `acme.main` or `acme.ch.main`
* exid: execution id
* nid: node id

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

## treeid

Where to locate the node in the execution tree. Elements are separated by dots. Elements are in hexadecimal.

```ruby
#for example:
"0"
"0.1a"
```

## exnid

Exid + nid.

```ruby
"{exid}-{nid}"

# for example:
"acme.ch.main-20141015.0955.tekuneko-0.1a-f"
```

