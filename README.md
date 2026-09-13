# distribution

SpexCode's atlas — the skill that reads a repository into a spec tree, draws its architecture diagrams and hands
over one browsable page — packaged in the format of each host that installs agent add-ons. Nothing here is part of
SpexCode itself: SpexCode's own skills and hooks live in `.spec/spexcode/.plugins/`, and these folders are what other
products load. Every package runs SpexCode through `npx`, so a user installs nothing and configures nothing.

| Folder | Host | What the host gets | Install it |
| --- | --- | --- | --- |
| `claude-code/atlas` | Claude Code | a plugin with the `atlas` skill | `claude plugin marketplace add shuxueshuxue/spexcode-plugins` then `claude plugin install atlas@spexcode` |
| `codex/plugins/atlas` | Codex | a plugin with the `atlas` skill | `codex plugin marketplace add shuxueshuxue/spexcode-plugins` then `codex plugin add atlas@spexcode` |
| `zcode/atlas` | ZCode | a plugin with the `atlas` skill, plus `atlas.dwf.ts`: the whole job as one dynamic workflow | list the folder in `plugins.dirs` |
| `gugu/spexcode-atlas` | gugu | a tab extension: the spec tree with each node's diagram drawn in the tab, and a button that starts an agent on the atlas | Settings → Extensions → Install, pick the folder |
| `penguin/use-spexcode` | PenguinHarness | a library plugin with the `atlas` skill | upload `skills/atlas` as a zip, or copy it into an agent's `agent_state/skills/` |

**This directory IS a marketplace root, and it is installed from a mirror.** Claude Code and Codex both resolve a
plugin out of a marketplace and neither installs a bare plugin directory, so the two manifests that name the same
plugins sit here — `.claude-plugin/marketplace.json` and `.agents/plugins/marketplace.json` — and one directory
serves both. A plugin manifest that VALIDATES is not a plugin that installs: `claude plugin validate` passes on a
bare plugin folder that `claude plugin marketplace add` then refuses.

Both hosts clone the WHOLE repository a marketplace names, and the `owner/repo` form reads the manifest only at the
repository ROOT — a subdirectory cannot be addressed. Pointing adopters here would cost them 33M and 1605 files for
a skill that is four, so this directory is mirrored to
[`shuxueshuxue/spexcode-plugins`](https://github.com/shuxueshuxue/spexcode-plugins) (1.2M, 23 files), which holds
nothing else. `.github/workflows/distribution-sync.yml` keeps the two equal and runs only when this directory
changes; it regenerates first and fails if what is committed differs from what the generator writes. Edit here,
never there.

**Generated or written by hand.** `npm run build:distribution` writes every manifest, every `SKILL.md`, the gugu tab's
prompt and its copies of archify (`archify.js`, `focus.js`, `diagram.css`) from their sources: the atlas preset in
`.spec/spexcode/.plugins/skills/atlas/`, the root version, and `packages/archify`. `npm run lint` fails while any of
them is stale. The rest was written by hand and the generator never touches it: `zcode/atlas/skills/atlas/atlas.dwf.ts`,
the gugu tab's `index.html`, `app.js`, `atlas-model.js` and `style.css`, and PenguinHarness's `icon.svg`.
