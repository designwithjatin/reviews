# context/: project memory

This folder holds everything a new coding agent needs to pick up the work without the chat history. **Keep it current:** see the update table in [`../AGENTS.md`](../AGENTS.md#0-keep-context-up-to-date-mandatory).

| File | What's in it | Read when |
|---|---|---|
| [onboarding.md](onboarding.md) | First-hour guide: setup, preview server, how to work with the owner, test recipes | **First**, always |
| [architecture.md](architecture.md) | Files, page structure, JS state and helpers, CSS layout, assets | Before editing code |
| [flow-and-screens.md](flow-and-screens.md) | Every screen in order: Figma node, copy, step labels, progress, behaviour | Before touching any screen |
| [tasks.md](tasks.md) | Ongoing, on hold, open questions, done, rejected | Start of every session |
| [decisions.md](decisions.md) | Dated log of design and behaviour decisions and Figma deviations | When unsure why something is the way it is |
| [gotchas.md](gotchas.md) | Traps that have already bitten us, and how to avoid them | Before debugging or testing |
| [changelog.md](changelog.md) | One line per commit | After committing |

**Rules of thumb for these docs**
- Write for an agent with zero context. Use plain language and concrete names (IDs, functions, Figma nodes).
- Prefer editing an existing entry over adding a duplicate. Date entries as `YYYY-MM-DD`.
- Don't paste large code here. Point to the function or selector instead.
