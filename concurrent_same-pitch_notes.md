# Multiple concurrent notes of the same pitch in the same channel

MIDI channels don't support concurrent same-pitch notes.
Going from a system that supports same-pitch note concurrency to a single MIDI channel requires special handling to avoid problems.
When two same-pitch notes are played the second note could be either ignored or the active note could be stopped before the second starts (voice stealing).
The later is is commonly implemented by synths, thus, adding a note off message before the second note could be omitted.
When two concurrent same-pitch notes stop, the first note-off message will stop the sounding note entirely. In order to avoid this, active same-pitch notes need to be tracked and a note-off message should be passed to the MIDI channel only for the last active note stops, i.e. note-off messages should be filtered out if there are remaining active notes of the same pitch.

## Examples

```
note 1 : |---|
note 2 :   |---|
output : |-|-| |
```

Two same-pitch notes passed to a MIDI channel without handling note-off messages.
The note gets retriggered on the second note-on and it stops early on the first note-off, followed by a useless note-off.


```
note 1 :   |--| |---------|
note 2 : |--------|
output : |-|--| |-|       |
                  ↑
```
The final useless note-off can cause an early stop of a new note.
