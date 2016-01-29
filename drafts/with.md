
# with

```
  sequence
    set x { name: john, age: 33 }
    with f:x
      echo "$(name): $(age) years old"
    echo $(x.name)
```

or

```
  sequence
    set x { name: john, age: 33 }
    sequence payload: f:x
      echo "$(name): $(age) years old"
    echo $(x.name)
```

