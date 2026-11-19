---
name: make-music-in-tracker
description: Write, edit, arrange and mix songs in EditLab Tracker on the person's Mac. Use when the person wants Claude to make or change music in EditLab Tracker, such as a beat, a song, drums, a bassline, chords, an arrangement, a mix, or a song they split from a recording.
---

# Making music in EditLab Tracker

EditLab Tracker is a music app for the Mac. A song is a set of patterns (rows of notes on channels) played in an order. When Tracker's Claude connector is on, you can read the song that's open and change it with Tracker's tools.

The person is the author. You write and edit, and they decide. Every change you make is one step in Tracker's Edit > Undo, labelled with what you did, and they can change anything by hand.

## Only when asked

Use Tracker's tools only when the person wants music made or changed in Tracker. Don't open, play, change or save anything they didn't ask for.

If Tracker's tools aren't available, say that this works in EditLab Tracker, a Mac app that's free to download from the Mac App Store, with the Claude desktop app. To connect them, they choose Help > Use EditLab Tracker with Claude… in Tracker. Then help with what they asked in another way, and don't bring it up again unless they do.

## How a session goes

1. **Start with `tracker_status`.** It says which song is open, its tempo and size, whether it's playing, what Undo would take back, and which style names the lay, complete and generate commands accept. To work on another song, open it with `open_song` and its full path. If the open song has unsaved changes, offer to save it first. For Tracker's own advice on a topic, such as working with a split song, read `tracker_guide`.
2. **Before each new change, call `what_changed`.** Build on the person's own edits, never over them.
3. **Read before you write.** On a big song, read the overview first with `read_song`, then only the patterns and channels you'll touch.
4. **Change in small, named steps.** Each call to `edit_notes`, `arrange`, `mix`, `effects`, `change_pitch`, `run_commands`, `add_sound` or `fix_sound` is one undo step. Give it a short, plain label, like "kick on every beat" or "took the hats out of the intro". The person sees it in Tracker as "Undo Claude: <label>".
5. **Check before you say it's ready.** Run `check` on the steps you changed. It finds clipping, clicks and dropouts, hears the key and tuning, and measures the low, mid and high bands. Fix what it finds, then check again.
6. **You can't hear the song.** Use `play` on the part you changed, then ask the person how it sounds. Their ears decide.
7. **Save only when asked.** Before a big change, like a remix or replacing the song, offer Save As first (`open_save` as a new song) so their version stays as it was.
8. **Exporting a file** opens Tracker's Export window with `open_export`, and the person picks where the file goes. Exporting needs Tracker Pro. Check the whole song first: on a long song, each check covers what it can and says where to carry on.

## Writing music that sounds finished

- **Start from their brief:** style, tempo, key, length and mood. If they give you little, choose for them and say what you chose.
- **Build in sections:** intro, verse, chorus, build, drop, bridge, outro, whatever the style needs. Use one pattern per section and set the play order with `arrange`. Vary each repeat, so the second chorus isn't a copy of the first.
- **Give every part a job:** drums keep time, bass holds the root, chords give the harmony, the lead carries the melody, and texture fills the gaps. Keep kick and bass from fighting, either with different rhythms or with EQ.
- **Choose each sound on purpose.** Search Tracker's built-in sounds with `find_sounds`, add them with `add_sound`, and look at `list_sounds` for each one's peak, tuning and any silence before it starts. Use `fix_sound` to trim silence, tune, normalize, fade or loop a sound.
- **Think about how each sound should come through in the mix, and put every part through some effects.** With `mix`, set each channel's level, pan and EQ, plus its reverb, echo, filter and flange sends. With `run_commands` and addEffect, add drive, compression, chorus, phaser, gate and the rest where they help, then use `effects` to set each effect's knobs, switch it off, reorder the chain or remove it, on a channel or on the master. Call `effects` with no changes first to see the chain and each knob's range. Check before and after a mix change to see which bands moved.
- **Make it play like a person:** vary volumes, accent the strong beats, add ghost notes and fills, and change something every few bars.
- **Earn the big moments:** strip back before a drop, build with risers and drum fills, and land the drop with everything at once.
- **Use the lay and complete commands as starting points, not answers.** After `layDrums`, `layBass`, `layChords`, `layArp`, `layIdea` or `complete`, edit the notes so the part belongs to this song. These commands work on the pattern on screen, so call `select` first.
- **Never use `generate` to replace the person's song unless they ask for new songs.** Tracker asks them before it replaces anything.

## Editing a song someone already made

- **Keep the song's own sound.** Change only what was asked.
- **Tuning and key:** `change_pitch` moves a channel or a sound by any amount, down to fractions of a semitone. Keep the speed (the default) for a split vocal or a loop, so it stays in time with the song. Run `check` afterwards to hear the key and tuning.
- **A song split from a recording** has its vocal, bass, guitar, piano and drums on channels of their own, and the rest as loops. Read the overview first, and keep each part's character.
- **Taking changes back:** to undo one of your own changes, use `take_back` with its label. It keeps any cells the person changed since. If they've edited after you, ask before using `undo` across their steps.

## Examples

**"Make a two-minute lo-fi beat at 85 BPM with a mellow piano."**
Check the status and set the tempo and title. Build an intro, a verse loop and a variation as separate patterns, with dusty drums, a round bass and soft piano chords. Give the piano reverb and a little echo, keep the drums dry and warm, then check, play and ask how it sounds.

**"The chorus sounds muddy. Clean it up without changing the notes."**
Read the chorus and check its bands. Use `mix` to cut low-mids on the pads and chords, keep the bass centred and pan the doubled parts apart. Check again to show what moved, then play the chorus and ask.

**"Take the drums out of the intro and add a build before the drop."**
Call `what_changed` first. Clear the intro's drum channels, then add a pattern with a snare roll that speeds up and a riser before the drop. Put it in the order, then check and play from just before the drop.

**"Undo what you just did to the hats."**
Use `take_back` with that change's label, and tell the person if any of their own edits were kept.
