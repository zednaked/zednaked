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

**[ZGT](https://github.com/zednaked/zgt-bin)** — A real terminal inside the
Godot editor's bottom panel. A C++ GDExtension that runs your shell on a
pseudoterminal and draws the character grid itself, so it behaves the same on
X11 and Wayland with no window embedding. Tabs, mouse forwarding, scrollback
search, truecolor — enough to run `nvim`, `htop` or `lazygit` without leaving
the editor.

**[godot-web-build-budget](https://github.com/zednaked/godot-web-build-budget)** —
How a production web build went from 119 MB to 37 MB. What was actually in the
`.pck`, why lossless import inflates art that was already compressed, and the
measurement that contradicted the obvious fix: VRAM compression made the build
54% larger where lossy cut it 74%.

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

**Nirbija** — a plugin host and mixer for Linux, in the spirit of AUM: channels,
plugins in the strip, loop, record, session. No timeline. 45k lines of C++20 and
Qt6 hosting LV2, CLAP and VST3 in the same slot over JACK or PipeWire, with
native plugin editors embedded, MIDI routing and Lua scripting. 30 test binaries
under AddressSanitizer and ThreadSanitizer, because real-time audio does not
forgive a data race. → [nirbija site](https://zednaked.github.io/nirbija-site/)

**[Ganja-TUI](https://github.com/zednaked/Ganja-TUI)** — Plant growth simulation
in the terminal, in Rust. 35 strains with real genetics, seven growth stages, and
stress that follows the plant all the way to harvest.

### Games

Seven titles on [itch.io/zedcave](https://zedcave.itch.io), three playable in
the browser — a cyberpunk text MMO with an authoritative Cloudflare Workers
backend, a tactical FPS, an RTS, a match-3.

---

Curitiba, Brazil · remote, any timezone · Godot · GDScript · C++ · Qt · Rust · Linux
