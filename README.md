## Thiago Gonçalves

I build games in Godot at production scale, and I write C++ for the parts an
engine leaves to you.

For the past year I've been the sole front-end engineer on a catalogue of 20+
commercial Godot titles shipped to the browser: one shared runtime replicated
across 17 projects, 12 locales including Arabic RTL, and web builds held under a
hard byte budget. That work is under contract and lives in a private org — what
follows is the part I can show.

**Available for contract and consulting work.** Web builds that outgrew their
byte budget, localization that has to survive a dozen languages, and
GDExtension work when the editor won't do what you need.

**zednaked@gmail.com** · [LinkedIn](https://www.linkedin.com/in/thiago-g/)

### Godot

**[ZGT](https://github.com/zednaked/zgt)** — A real terminal inside the
Godot editor's bottom panel. A C++ GDExtension that runs your shell on a
pseudoterminal and draws the character grid itself, so it behaves the same on
X11 and Wayland with no window embedding. Tabs, mouse forwarding, scrollback
search, truecolor — enough to run `nvim`, `htop` or `lazygit` without leaving
the editor.

**[godot-web-build-budget](https://github.com/zednaked/godot-web-build-budget)** —
Three production web builds, the same default every time, and every one 48%
lighter or more with no assets deleted. The first went from 119 MB to 37 MB; on
the third, the largest file in the pack was a 7.1 MB JSON that nothing reads at
runtime. What was actually in the `.pck`, why lossless import inflates art
that was already compressed, and the measurement that contradicted the obvious
fix: VRAM compression made the build 54% larger where lossy cut it 74%. The
later editions add what the export ships that nobody chose (`all_resources`
sweeps in work files and test scenes, a filter problem rather than a cleanup
one) and where the floor is: the engine alone is 8.9 MB over brotli, confirmed
by an unrelated Godot game at 9.6 MB. Below that you are optimising the engine,
not your game. The editor shows none of these numbers, so the measurement became
[godot-proposals#15505](https://github.com/godotengine/godot-proposals/issues/15505),
triaged by the Godot team under `topic:editor` and `topic:import`.

**[godot-i18n-that-holds-up](https://github.com/zednaked/godot-i18n-that-holds-up)** —
Shipping a Godot 4 game in 12 locales. 3,673 source and translation pairs
measured: the usual advice to reserve 30% runs backwards, because paragraphs sit
at a p95 of 1.30x while buttons hit 2.00x with a worst case of 3.67x, and the
whole tail is in the short strings that make up the UI. Counting with `.length`
inflates Hindi by 60% and Nepali by 76% and reports exactly 0% growth for Arabic
and German, so the check you would write to catch the bug passes clean. Two
zero-dependency tools: one measures expansion from the reader's CSV, one gates
a build in CI.

**[godot-canvas-shaders](https://github.com/zednaked/godot-canvas-shaders)** —
Nine `canvas_item` shaders lifted out of shipped games and documented for reuse.
GL Compatibility, so they survive HTML5 export and low-end mobile. No addon, no
dependencies, MIT.

**[mcpgodot](https://github.com/zednaked/mcpgodot)** — MCP server for Godot 4.
Scene operations an agent can actually drive, with the token cost of reading a
scene tree cut down to something workable.

**[godot-claude-tools](https://github.com/zednaked/godot-claude-tools)** —
Summarises Godot scenes and scripts before an agent reads them. A `.tscn` that
costs 40k tokens raw costs a fraction of that summarised.

**[SpineViewer](https://github.com/zednaked/SpineViewer)** — Inspect Spine
skeletons, skins and animation names outside the runtime, before wiring them
into a scene.

### Systems

**Nirbija** — a Linux mixer that is also an instrument, in the spirit of AUM.
45k lines of C++20 and Qt6. It hosts LV2, CLAP and VST3 in the same slot over
JACK or PipeWire with the plugins' own editors embedded — and it ships with a
drone synth on just intonation, a sixteen-pad sampler, a looper, a step
sequencer, an arpeggiator and a Lua MIDI plugin, so a session does not start
empty. Bluetooth LE MIDI is handled directly, because PipeWire advertises the
port and never delivers the events. 30 test binaries under AddressSanitizer and
ThreadSanitizer, because real-time audio does not forgive a data race.
→ [source](https://github.com/zednaked/Nirbija) · [site](https://zednaked.github.io/nirbija-site/)

![Nirbija](https://raw.githubusercontent.com/zednaked/Nirbija/master/docs/nirbija.png)

**[Ganja-TUI](https://github.com/zednaked/Ganja-TUI)** — Plant growth simulation
in the terminal, in Rust. 35 strains with real genetics, seven growth stages, and
stress that follows the plant all the way to harvest. The grow was ported to pure
QML as **[Ganja](https://github.com/zednaked/omarchy-ganja)**, a plant that lives
in the Omarchy bar.

**[Omahold](https://github.com/zednaked/omahold)** — A miniature dwarf fortress
that lives in the Omarchy shell. 48×30 cells across 8 z-levels, seven dwarves with
hunger, mood and trades, digging and brewing and strange moods, caravans, goblin
ambushes, floods and magma. 250k of deterministic simulation in plain JavaScript
behind a QML surface — no binary, no network, one tick costing a fraction of a
millisecond on a 2014 MacBook, and the world keeps ticking while the panel is
closed. English and Portuguese.

Both passed review in the Omarchy plugin marketplace and install with
`omarchy plugin add` — [zed.omahold](https://omarchy.org/plugins/zed.omahold) ·
[zed.ganja](https://omarchy.org/plugins/zed.ganja).

**[omarchy-zero](https://github.com/zednaked/omarchy-zero)** — The Omarchy shell
on a plain Arch install, without the official installer. Measured layer by layer
on a 2018 laptop: the shell costs 149 packages over base, and the file manager
alone costs 174. The installer runs as a dry run first, marks the 124 pending
migrations done the way Omarchy's own finalizer does, and puts a guard in front of
the 16 commands that would rewrite the machine. It builds on
**[omarchy-guest](https://github.com/zednaked/omarchy-guest)**, which runs the same
shell on top of an existing Hyprland setup and checks every upstream ref against
a written contract before it lands.

### Games

On [itch.io/zedcave](https://zedcave.itch.io), and the two worth your time are
playable in the browser:

**Ciberteia** — a cyberpunk text MMO in Godot exported to the web, with an
authoritative backend on Cloudflare Workers. Server owns the world state, the
client reconciles; the interesting part is what happens to a session when the
connection does not cooperate.

**Rinha** — a real-time strategy game in the StarCraft lineage, also in the
browser. Selection, orders and unit counts are where an RTS spends its frame
budget, and where a 2D engine starts telling you what it actually costs.

---

**Hire me for it:** a fixed-scope audit of your Godot web build, from **USD 1,200**,
3 business days, no access to your source needed.
[What you get](https://github.com/zednaked/godot-web-build-budget#if-your-build-has-the-same-problem)
· zednaked@gmail.com

Curitiba, Brazil · remote, any timezone · Godot · GDScript · C++ · Qt · Rust · Linux
