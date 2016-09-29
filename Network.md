
# Network
 
The `Network` object represents an FBP network. It can be generated by reading an FBP
file or it can be generated programatically.
 
Once generated, a representation of every FBP Process is created as well
as a representation of the network connections

## Network Connections.

Imagine a very simple network with process P with inports I,J and outport O, process R with outport O
and process S with inport I.

We won't worry about the components at the moment.

```fbp
 R.O -> P.I
 P.O -> S.I
 'foo' -> P.J
```

This will translate to a JSON representation of:

```json
 {
  "R": {
    "out": { "O": { "process": "P", "port": "I", "capacity": 20 } },
    "in" :{}
  },
  "P": {
    "out": { "O": { "process": "S", "port": "I", "capacity": 20 } },
    "in": { "I": [ { "process": "R", "port": "O" } ], 
            "J": [ { "data": "foo" } ] }
  },
  "S": {
    "out": {},
    "in": { "I": [ { "process": "P", "port": "O" } ] }
  }
 }
 ```