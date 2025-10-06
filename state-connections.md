# State connections

Connections between nodes that send MIDI data are event-based. The receiving node runs a callback, when the sending node outputs a message.

But for some situations, state-based connections can be better suited. These are not tied to events, but are more like values that can be read by the receiving node. In addition, there would be a way for the receiving node to know that the state has been updated. 

A popular example of a pure state-based node system is Blender's shader nodes.

A popular example of a pure event-based node system is any DAW that allows connecting VST plugins in a node based fashion.

## Use cases

### Tempo-synced delay

This setup would involve three nodes:

1. A MIDI clock-pulse to BPM converter. This would receive the MIDI clock messages, and output a BPM "state", computed based on the clock pulses.
2. A BPM to beat duration converter. This would accept a BPM state, and convert it to a duration state (whole note, half note, dotted note, etc.) chosen by the user.
3. A delay node, which accepts MIDI messages, and outputs them after a delayed time. The delay duration can be accepted as a state input from the BPM to duration node.

### Pitch-bend range

The pitch-bend range can be adjusted using a sequence of messages. Instead of having every node that works with pitch bend keep track of the pitch bend range state internally, it can be exposed via a dedicated node (or a Hardware Mapping) as a state that receiving nodes can read from.

If the pitch-bend range comes straight from the input Hardware Mapping, then it can be forwarded to the output Hardware Mapping, where it gets converted into MIDI messages again. Such a pattern abstracts away odd characteristics of the device/MIDI spec, and gives all the nodes a simpler environment to work in. For example, we could let the Hardware mapping handle all RPN messages and convert them to states. And all CC messages would be treated as pure CC messages inside MIDI FX. A possible downside, is that the conversion to/from state will increase the latency of these state-based messages. 

### Launchpad matrix dimensions

The state can also be used to pass static data (which does not change over time) that isn't a MIDI message. For example, it can be used by nodes that work with launchpad controllers to know the dimensions of the launchpad matrix (rows and columns) as this context can be helpful for their functionality.

## Some notes

### State connections are one-to-many and not many-to-one

A state input can only receive one state output. If it received multiple, it would not know which state to read from.

But a state output can send its state to multiple state inputs.

## Open questions

1. Should we set in stone, the types of state connections that can exist?
2. If so, how should we decide what types of states should be available? I imagine they would need to be very general. Like a "2D array of numbers" instead of a "grid of button colors".
3. If not, how do we coordinate the possible kinds of states that people can create?
4. What should the [API](./api.md) look like? 

