# Architecture

## Files
```
AI Onboarding Reviews/
├── index.html      # all markup + one inline <script> with every behaviour (~2.3k lines)
├── styles.css      # tokens (:root) + one section per screen (~1.9k lines)
├── assets/         # icons/images downloaded from Figma (svg/png), referenced as assets/<name>
├── AGENTS.md       # rules + design/component direction (CLAUDE.md just imports it)
├── context/        # project memory (this folder)
└── .gitignore      # .DS_Store, index-v2.html
```
Hosting: GitHub `designwithjatin/reviews` (`main`) → Vercel (Hobby, framework "Other", no build). `.vercelignore` keeps the agent docs out of the public deploy.

## Page structure (`index.html`)
| Region | Element | Notes |
|---|---|---|
| Header | `header.header` | Logo + "I'll Explore Later Myself" link (`exploreLater`, hidden on the final screen) |
| Screens 1–3 | `main#screen-search` | Left greeting + `#search-form`; right panel states: illustration → searching skeleton → results `.business[data-index]` |
| Screens 4+ | `main#screen-processing` | `aside.setup-panel` (back link, selected business, `.progress`, `#milestones`, `ol#steps`) + `.workspace` |
| Workspace panels (one visible at a time) | `#processing` (AI dot-wave animation), `#profile-form`, `#publishers`, `#inbox` (`#inbox-loading` / `#inbox-ready` / `#inbox-done`), `#social`, `#widget` | Swapped with `swapPanel(from, to)` |
| Final | `main#screen-final` | Heading + `.goal` rating bar + CTAs + `.tools` cards (HTML illustrations) |
| Overlays | `#connect-modal`, `#optin-modal`, `#style-modal`, `#toast` | `openModal` / `closeModal`, `showToast` |

`#inbox-done` is the Writing Style + Automate Replies view shown after the temporary replied state (Figma 10677:35306).

## Script layout (in order)
1. **Search:** `CITIES`, `CATEGORIES`, `parseQuery(q)`, `buildResults(q)` (deterministic: same query → same results), `resultRow`.
2. **Business pick → processing:** `T` timings, easings `EASE_IN/OUT/IN_OUT/OUT_BACK`, `fade()`, `done()`, `fillSelected(b)` (sets `picked`, fills the form), `resetTransition()`, the card-flight click handler.
3. **Steps → profile form:** `T2`, `hold()`, `motion()`, `finishStep()`, `completeSteps()`, `settleParent()`, `resetProcessingScreen()`.
4. **Connect → publishers → opt-in:** `T3`, `PUBLISHERS`, `GROUPS`, modal and toast helpers, `stepHTML`, `showSteps()`, `addMilestone()`, `swapPanel()`, connect/locations rendering, the opt-in handler.
5. **Reviews:** `REVIEWS` (6 café reviews with drafted replies), `reviewHTML`, `runReviews(id)`.
6. **Social proof:** `runSocialProof()`, which runs the steps, settles the parent, then shows `#social`.
7. **Social posts / widget / final:** `renderPosts`, `syncPosts`, `renderAccounts`, `syncAccounts`, `syncShare`, `renderWidget`, `runWidget(scheduled)`, copy/email, `#widget-continue` → final screen (rating bar animation lives here).
8. **Writing-style modal:** `STYLE`, `styleHTML(loading)`, `skelLines`, `brandHTML`, `showTab`, regenerate.
9. **Reviews interactions:** `markReplied(card, delay)`, the review list click handler (`more` / `edit` / `send`), the `sendAll` handler: 1st click marks all replied, waits about 1.8s, swaps `#inbox-ready` → `#inbox-done` and relabels the button "Save and Continue" (`dataset.done`); 2nd click → `runSocialProof()`.
10. **Form interactions:** pills (All / AI Corrected / Missing), map embed, `markMissing()`.
11. **`processing`:** IIFE that ports the AI animation (`start`, `stop`, `setPhrases`).

## Core patterns (reuse these)
- **Animations = WAAPI.** `fade(el, from, to, ms, {from, to, delay, easing})` uses `fill: both`. `done(anims)` resolves `true`, or `false` if cancelled. `hold(ms)` is a timer that runs on the animation clock (so it pauses with the tab).
- **Cancellation:** `resetTransition()` bumps `run` and cancels non-CSS animations. Every async phase captures `id = run` and checks `live()` after each `await`, bailing if stale.
- **Left panel:** `showSteps([{ai, icon, label}])` replaces the list. `finishStep(step, label)` swaps to a ✓. `settleParent(aiStep, others, text)` moves the AI step to the bottom and sets the final italic text. `addMilestone(title, sub)` pins a ✓ block above.
- **Progress bar widths:** 70 (start) → 120 (publishers) → 184 (replied) → 250 (social) → 316 (widget). Set `progressBar.style.width` and animate from the previous value.
- `motion(ms)` → 0 under reduced motion.

## CSS layout (`styles.css`)
`:root` tokens → base → header → search screens → **Screen 4 processing** → **Screens 5–6 form** → publishers/modals/toast → **inbox / reviews** (`.review-card`, `.is-replied`) → writing-style modal → **Screens 18–19 social** (`.share-panel`, `.post`, `.account`, `.split-btn`) → **Screen 20 widget** (`.browser`, `.wgt__*`, `.code-card`) → **Screen 21 final** (`.final`, `.goal`, `.tools`, `.phone`, card illustrations).
Shared buttons: `.btn-primary`, `.btn-solid`, `.btn-outline`, `.link-btn`, `.link-underline`, `.icon-btn`, `.check` (custom checkbox with `checkbox-on/off/mixed.svg`).

## Data notes
- `picked` = the selected business `{name, category, noun, address, city, state, zip, lat, lng}`. Final-screen cards and accounts read `picked.name`.
- Reviews and the widget summary are café-flavoured regardless of category (prototype simplification).
