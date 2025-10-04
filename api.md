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
