# MIDI-FX API

This code is only for representing the schema of a node

```js
const input0 = {
  name: "Note",
  types: { channelMessages: "*" },
  callback: (message, messageType) => {
    if (messageType === "note") {
      message.channel += 1;
      output(0, message);
    }
  }
}

const output0 = {
  name: "Shifted",
  types: ["notes", "cc"],
}

export const inputs = [
  input0,
  input1,
]

export const outputs = [
  output0,
]

```

## Instantiation

I realized we can't directly use a module, because we want to create many instances of the same node.

In web MIDI FX, instantiation was done through Svelte components. 

In Python it can be achieved using classes. But we can also use a functional programming style:

```python
from api import create_input, create_output

def transpose_node:

	state = {
		"transpose": 0	
	}
	
	output = create_output("out", "note message type")
	
	def handler(message):
		transposed_message = message.note += transpose
		output(transposed_message)
	
	return {
		"state" = state,
		"inputs" = [create_input("in", "note message type", handler)]
		"outputs" = [output]
	}
```

Here, calling `transpose_node` creates a new node. If we want to use any shared state between all transpose nodes, it would be stored outside this function.

`create_output(name, type)` creates an object of class `Output`. This class has a `__call__` method defined, which allows for the `output(new_message)` syntax, while also allowing `output.name`, `output.type` , etc. I find this cleaner than `emit(output, new_message)`.

### State

The current implementation of state shown above is how state works in the web version - it is just a special name, and any data in it gets stored in preset files. But the idea of state seems connected to the [state connections](./state-connections.md) idea. Maybe we can have an `input_state` and `output_state`, and some mechanism to get notified when state changes. 
