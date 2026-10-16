# Onboarding: how a new agent gets productive here

## 1. What this is
A **static** prototype (no build, no framework, no backend): `index.html` (markup + all JS), `styles.css`, `assets/`. It mimics the SocialPilot Reviews AI onboarding from Figma file `FQOv3xhldcOc59KkTe3lq2`. All data (search results, reviews, accounts) is generated or hard-coded in `index.html`.

## 2. Who you're working with
- **Jatin Solanki**, product designer, not a developer. You run every git and terminal step. Explain outcomes in plain words, not commands.
- He gives direction as **Figma links** (`node-id=10758-17567` → node `10758:17567`), pasted Figma HTML, or screenshots with notes.
- **Ask before every `git push`.** Commit locally, ask, and push only on a yes.
- He likes: natural, unhurried motion; exact Figma fidelity; realistic AI copy; short status updates.

## 3. Read first
1. `../AGENTS.md`: rules, design tokens, and the owner's component direction.
2. `tasks.md`: what's in flight and what's parked.
3. `flow-and-screens.md`: the screen you're about to touch.
4. `gotchas.md`: before you test anything.

## 4. Tools you'll use
- **Figma MCP:** `get_design_context` (fileKey `FQOv3xhldcOc59KkTe3lq2`, nodeId with `:`), `get_metadata`, and `get_screenshot` (for comparison only). Big nodes overflow the tool output and get saved to a file, so extract them with `jq -r '.[0].text' <file>` and fetch child nodes separately.
- **Asset URLs** from Figma expire after 7 days. `curl -L -o assets/<name>.svg <url>`, then reference `assets/<name>.svg`.
- **Design system doc:** `~/Downloads/Skills/Design System.md`. **Animation guidance:** `~/Downloads/Skills/animate-skill-main/SKILL.md`. **Original AI animation:** `~/Downloads/AI - Animation/AI-Onboarding Animation.html` (ported into `#processing`).

## 5. Local preview
- Launch config **`ai-onboarding-reviews`** → `http://localhost:4202`. It runs `~/Library/Caches/ai-onboarding-reviews-preview/serve_nocache.py`, which serves `…/site/`.
- macOS blocks the server from reading `~/Downloads`, so **sync after every edit**:
  ```
  rsync -a --delete --exclude .git --exclude .gitignore "/Users/jatinsolanki/Downloads/AI Onboarding Reviews/" ~/Library/Caches/ai-onboarding-reviews-preview/site/
  ```
- Bump `styles.css?v=N` in `index.html` when CSS changes (browsers cache hard).
- The desktop app stops this server from time to time. Restart it with `preview_start` (name `ai-onboarding-reviews`).
- Don't put server files in the session scratchpad: it gets wiped.

## 6. Testing recipe
- Set the viewport to **1440×800** (`resize_window`), and reset to "desktop" when done.
- All top-level `const`/`function` names in the inline script are page globals, so you can drive the flow from `javascript_tool`:
  - Search: `document.getElementById('query').value = 'Third Wave Coffee Jaipur cafe'; document.getElementById('search-form').requestSubmit();`, then wait about 3s and click `.business[data-index]`.
  - Skip waits: run an interval that calls `.finish()` on every non-`CSSAnimation` in `document.getAnimations()`.
  - **Reproduce real phase order.** Jumping straight to `runReviews()` / `runSocialProof()` without the preceding `showSteps()` leaves stale steps on the left and makes the step animation look broken (see `gotchas.md`).
- Check `read_console_messages` (errors only) after every run.
- To test an animation precisely, **pause the animations and step `currentTime`**, reading `getBoundingClientRect()` at each step. The preview pane sometimes stops rendering frames, so real-time sampling isn't reliable.

## 7. Shipping
1. Sync, test, check the console.
2. Update `context/` (tasks, decisions, flow, architecture, changelog as relevant).
3. `git add -A && git commit` (author is already set in the repo config, plus the harness's co-author trailer).
4. **Ask** "Push this to main?" Push only on yes. Vercel deploys `main` in about a minute.
