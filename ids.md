
# ids

* domain: `acme.main` or `acme.ch.main`
* exid: execution id
* nid: node id

## exid

```ruby
"{domain}_{yyyyMMdd}.{hhmm}.{NNNNN}"

# for example:
"acme.ch.main_20141015.0955.tekuneko"
```
(Eventually prefix with flon execution unit id?)

## nid

```ruby
"{exid}_{treeid}__{counter}"

# for example:
"acme.ch.main_20141015.0955.tekuneko_0_1__f"
```

