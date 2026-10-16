# AGENTS.md: SocialPilot Reviews · AI Onboarding prototype

A clickable HTML prototype of the **SocialPilot Reviews AI onboarding**. The flow goes: find your business → AI fixes your Google profile → publishers → reviews inbox → social posts → website widget → next rating milestone.

- **Owner:** Jatin Solanki, product designer at group.one / SocialPilot. He is not a developer. Explain things in plain language and run all git and terminal work for him.
- **Design source:** Figma file `FQOv3xhldcOc59KkTe3lq2` ("AI Onboarding - Reviews").
- **Live:** GitHub `designwithjatin/reviews` → Vercel auto-deploys `main`.

> **Start here:** read [`context/README.md`](context/README.md), then [`context/onboarding.md`](context/onboarding.md).
> Everything you need to pick up the work is in `context/`.

---

## 0. Keep `context/` up to date (mandatory)

The `context/` folder is the project's memory. Any agent that changes the project **must update it in the same piece of work**, before reporting done:

| When you… | Update |
|---|---|
| Start, finish, park or drop a task | `context/tasks.md` (move it between Ongoing / On hold / Done / Rejected) |
| Make or are told a design or behaviour decision, or deviate from Figma | `context/decisions.md` (dated entry) **and** the matching rule in this file if it's a standing direction |
| Add or change a screen, a step label, copy, or flow order | `context/flow-and-screens.md` |
| Add or change files, helpers, CSS sections, IDs or state | `context/architecture.md` |
| Hit a bug or trap worth warning the next agent about | `context/gotchas.md` |
| Commit | `context/changelog.md` (one line per commit) |

If the owner gives a new standing instruction in chat ("always…", "never…", "moving forward…"), add it to this file **and** log it in `context/decisions.md`. Never let the docs fall behind the code.

---

## 1. Working rules (from the owner)

1. **One version only.** All work goes into `index.html` + `styles.css` + `assets/`. **Never** create copies like `index-v2.html`. Experiments go on a git branch (Vercel gives branches a preview link) and the branch is deleted if rejected.
2. **Ask before every push.** Commit locally, then ask "Push this to main?" and push only on a clear yes. Each yes covers one push. Pushing to `main` deploys to Vercel, so the production link changes.
3. **Run git for him.** Commit author is `Jatin Solanki <jatin.solanki@group.one>` (set in this repo's local config). End commit messages with the trailer the harness provides (e.g. `Co-Authored-By: Claude …`). Short, plain commit subjects.
4. **Verify before saying done.** Sync to the local preview, test at **1440×800**, check the console, and compare against Figma. Say what you checked and what you couldn't check.
5. **Build from Figma data, not screenshots.** Use the Figma MCP `get_design_context` for exact values. Don't ship PNG screenshots of designs as UI: rebuild illustrations in HTML/CSS/SVG. Screenshots are only for visual comparison.
6. **Figma asset URLs expire (7 days).** Download icons into `assets/` with `curl -L` and reference them locally.
7. **Follow Figma exactly, but flag deviations.** If Figma has placeholder data or an apparent mistake, make the sensible choice, tell the owner, and log it in `context/decisions.md`.
8. **Behavioural guidelines:** think before coding and state assumptions, keep things simple, make surgical changes, and don't refactor what isn't broken. If you notice unrelated dead code, mention it rather than deleting it.

---

## 2. Design system

Source: `~/Downloads/Skills/Design System.md` (SocialPilot tokens). The tokens are mirrored as CSS variables at the top of `styles.css`, so **always use the variables** rather than raw hex.

- **Font:** Source Sans Pro (loaded as Source Sans 3 from Google Fonts) → `var(--font)`. Type scale: `--header-md` 16/20, `--body-sm` 14/18, `--body-xs` 12/16. Code uses Spline Sans Mono.
- **Brand:** `--brand-primary #0F67EA` (hover `#004FD2`, active `#0037BA`), subtle `#ECF3FD`, disabled `#C5DBFA`. Brand secondary / highlight yellow `#FFCB00`.
- **Text:** primary `#18181A`, secondary `#5F6166`, tertiary `#777A80`, disabled `#C8C8C8`.
- **Surfaces:** page `#F8F9FA`, card `#FFFFFF`, recessed `#F5F5F5`, input `#F2F5F5`.
- **Borders:** `#D8D8D8`, `#F2F2F2`; input active `#89B9FF`; hover `#698EC4`.
- **Radii:** 2 (buttons, inputs), 4, 8 (cards, panels), 48/80 (pills, avatars).
- **Spacing:** 4 / 8 / 16 / 24 / 32 / 40.
- **Shadow:** `--shadow-bottom-sm` `0 2px 8px rgba(0,0,0,.12)`.
- **Success toast:** green border `#5CB85C`, bg `#EDFFEE`.

## 3. Motion direction

From the animate skill (`~/Downloads/Skills/animate-skill-main/SKILL.md`) and the owner's feedback:

- **Easing by purpose:** entrances ease-out (`EASE_OUT`), on-screen moves ease-in-out (`EASE_IN_OUT`), exits ease-in and shorter (`EASE_IN`). Use a small overshoot (`EASE_OUT_BACK`) for checks and pops.
- **Feel natural, not fast.** The owner asked twice to slow transitions down. Phases **overlap** so nothing comes to a dead stop.
- **Reasoning steps arrive one below the other**, about 400–800ms apart. They never appear all at once.
- **Parent (AI) task:** when a phase finishes, the parent step **moves all the way down to the bottom** of the list, then its label changes to the finished message (in italics). Every phase does this.
- **Never flash the previous screen when a modal closes.** If closing a modal or overlay leads to a new step, swap the screen behind it first (see `coverForListings()`), so it closes straight onto the next step. Show the toast there.
- Respect `prefers-reduced-motion` (the `motion(ms)` helper returns 0).
- Use the WAAPI helpers (`fade`, `done`, `hold`) and the run-id cancellation pattern. See `context/architecture.md`.

## 4. Component and screen direction (owner's decisions so far)

**Search and results**
- Results are generated from **any keyword** typed (name, city, category parsed from the text), in **any city**, not just Jaipur.
- The result card has a simple hover state: white bg, `--shadow-bottom-sm`, 1px `#698EC4` outline, radius 8.
- The back link copy is **"Back to results"**. It's **hidden once GBP is connected**, with or without the listings opt-in, and never comes back in later steps.

**"I don't see my business" → Create a new profile** (Figma 10768:18579)
- A full-width screen (no side panel) with "Tell us what your business does" and "Where is it located?" (search + "Pin your location" live map).
- **Create Profile** stays at 40% opacity until both are filled. It then joins the **same flow** as a found business: reasoning steps → location details form → Connect GBP → listing publishers → and on.
- The new business is built from the inputs: the name from the search and the category from the description.
- **City, state, PIN and coordinates come from the address lookup** (OpenStreetMap Nominatim), the way a map search would, not from the search query. The typed street is kept as written, with the locality and city added if missing. The form's map pins the exact coordinates.
- **New profiles have no website**: the Website field stays empty.
- **Connect = Google sign-in, not the GBP picker** (Figma 10773:18769). "Connect Google & Publish" opens a full-page Google "Choose an account" screen. It's a stand-in only: no real auth, nothing is typed or sent, and either row continues. **The account shown is the business's own**: the business name, the profile's email, and a letter avatar (never a real person's name or photo). Then: toast "Your Google Business Profile has been created" → the listings (publishers) screen.
- **After the listings → "Get your first 100 5 Star Reviews"** final screen (Figma 10773:18776). The star stays at "Starting out", with marks at 10 / 50 / 100. New businesses have no reviews, so the reviews inbox, posts and widget are skipped. The back link reads **"Back to profile details"** and returns to the filled-in create screen.

**Business-select transition**
- The left panel shrinks, and the selected business card flies to the top of the left panel. Then reasoning starts, with steps stacking one by one.
- The transition is slow and natural. An alternative "easier" transition (index-v2) was **rejected**.

**Profile steps and form**
- During the first step **don't move the progress bar** (the user has only just found their business).
- The last working step is "Updating your business profile with optimized content". Completed steps slide down, showing one more step done.
- The parent task ends as "Business profile is ready for your review. You can make changes, or publish right away!"
- **AI Corrected** tab: Claude acts as the AI layer. It shows concise, realistic reasoning for each fix (based on competitor research), e.g. for the About section.
- **AI notes** also show while scrolling the All Fields tab.
- **Missing** filter: shows only unfilled fields, including Services, Media and Social media.
- **Auto-fill:** latitude and longitude come from the map location. Don't say "Added from the business details you've shared" on fields that need user input.
- The map is a live Google map embed.

**Reviews inbox**
- Order: skeleton loading → AI drafts → **Send Replies**.
- On **Send Replies**, every card switches to the **Replied** state, then hands over to the **Writing Style + Automate Replies** view (Figma 10677:35306). The button becomes **Save and Continue**, which leads to "Creating Social Posts".
- **Transition between the two must feel connected, never a stall** (owner):
  1. Cards turn replied one by one, top to bottom (~140ms apart), with heights easing as they shrink.
  2. A short beat (~0.9s).
  3. Scroll back to the top if needed, then the replied cards fade and drop away in turn.
  4. The Writing Style card stays put (it's in both views), and Automate Replies + the note rise into the freed space.
- **Replied card:**
  - The header is unchanged.
  - The review text is **1 line** with an ellipsis, plus "Read more".
  - Below a `#F2F2F2` divider: ↳ icon and the reply in italic secondary text, **also 1 line**.
  - "Read more" shows only when something is cut off, and it expands both lines.
- **Writing-style modal:** opens from "View Detailed Writing Style".
  - It has Brand Context and Writing Style tabs (yellow `#FFCB00` active indicator).
  - **Regenerate** shows a **skeleton loader**: headings, stars and tags stay, while bullets and the pattern become grey bars.

**Social posts**
- Post checkboxes are **hidden until hover**, and stay visible once selected. The selected border is `#89B9FF`.
- Select All / "N Posts Selected" + **Clear All**. A partial selection shows a minus checkbox.
- The accounts list is named after the picked business, with a partial state of "N Accounts selected." + "Select All".
- **Share Now (split button) disabled state = whole split button at 40% opacity**, in brand blue (not pale blue). It's disabled until ≥1 post and ≥1 account are selected.

**Website widget**
- The **AI Summary card has no gradient**: plain white with a `#FFCB00` border.
- Includes a browser-frame preview, a review carousel, an HTML code card with Copy and Send as Email, and a "N Posts Scheduled." toast.

**Final screen**
- No side panel, and the header shows the logo only.
- **Heading highlight:** the "75 more 5-star reviews" yellow bar (30% `#FFCB00`, 9px) sits **behind the bottom of the letters**, from about 3.5px above the baseline to 5.5px below it. It isn't an underline below the text.
- **Rating bar animation (the owner likes it):** the star **pops in at 1.0**, then **travels to 3.8 together with the bar's fill** on the same curve, so it stays on the end of the bar.
- **Tool cards** (Quick Review Request, QR Code, Feedback Form) are built in **HTML/CSS, not screenshots**. On hover they reveal a description and a link.

## 5. Local preview

- Launch config **`ai-onboarding-reviews`** (port **4202**), defined in `~/.claude/launch.json`.
- It serves a **synced copy**, because macOS blocks servers from reading `~/Downloads`. After every edit, sync:
  ```
  rsync -a --delete --exclude .git --exclude .gitignore ./ ~/Library/Caches/ai-onboarding-reviews-preview/site/
  ```
- **Bump `styles.css?v=N`** in `index.html` whenever CSS changes (cache-buster).
- Details and test recipes: `context/onboarding.md`.
