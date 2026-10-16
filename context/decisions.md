# Decisions log

Newest first. Each entry: **date · decision**, why, and who decided (owner = Jatin; agent = a judgment call flagged to the owner).

## Process
- **2026-10-16 · Ask before every push** (owner). Several pushes went out unasked; from now on every push needs a yes.
- **2026-10-16 · Agent docs live in the repo** (owner): `AGENTS.md`, `CLAUDE.md` → `AGENTS.md`, `context/`. Agents must keep `context/` current. `.vercelignore` keeps them off the public site (agent).
- **~2026-10-06 · One file only** (owner): all work in `index.html`, no `-v2` copies; experiments on branches.
- **~2026-10-03 · Personal repo + Vercel** (owner): `designwithjatin/reviews` on `main`, auto-deployed. The team repo `groupone-design` isn't used (no merge rights).
- **Build from Figma data, not screenshots** (owner, 2026-10-16).

## Final screen
- **2026-10-16 · Star travels from 1.0 with the bar** (owner): it pops in at the left, then slides to 3.8 on the same curve as the fill. Implemented with the `translate` + `scale` properties so the pop can't distort the slide (see gotchas).
- **2026-10-16 · Highlight behind the text** (owner): the yellow bar sits about 3.5px above to 5.5px below the baseline (Figma: 28px down a 46px line).
- **2026-10-16 · Long business names in the Feedback Form card start right of the John Doe chip and ellipsize** (agent).
- **2026-10-16 · QR chip labelled "Google"** (agent; Figma says "Facebook" next to a Google icon). Awaiting confirmation.

## Widget
- **2026-10-16 · AI Summary has no gradient** (owner; Figma 10758:17434).
- **2026-10-15 · AI summary text names the picked business** (agent).
- **2026-10-15 · Send as Email opens a `mailto:` draft; Copy writes to the clipboard and shows a toast** (agent).

## Social posts
- **2026-10-16 · Disabled Share Now = 40% opacity on the whole split button, brand blue** (owner).
- **2026-10-15 · Checkboxes only on hover or when selected** (owner).
- **2026-10-15 · Posts show six different real reviews** instead of one repeated placeholder image (agent).
- **2026-10-15 · Accounts named after the picked business** instead of Figma placeholders (Tony Stark etc.); 10 of 11 preselected (Bluesky off) to match "10 Accounts selected." (agent).
- **2026-10-15 · Share Now disabled until ≥1 post and ≥1 account** (agent; Figma shows it always enabled).
- **2026-10-15 · "I'll do it later" skips to the widget without the toast** (agent).

## Create a new profile
- **2026-10-16 · "I don't see my business" opens a create screen, then the same flow until publishers and beyond** (owner; Figma 10768:18579).
- **2026-10-16 · Create Profile disabled (40%) until both fields are filled** (agent; Figma shows it enabled).
- **2026-10-16 · Name from the search, category from the description, address/city from the location; the form map pins the typed street** (agent).
- **2026-10-16 · Back link on this path reads "Back to profile details" and returns to the create screen with inputs kept** (agent).
- **2026-10-16 · No way back from the create screen to the results** (agent; Figma has none). Flagged to the owner.

## Connect GBP
- **2026-10-16 · No "Back to results" after connecting GBP** (owner). Applies to both connect paths. The hide doesn't depend on the fade finishing, so a cancelled fade can't bring the link back.

## Reviews inbox
- **2026-10-16 · Connected transition from replied cards to Automate Replies** (owner: "feels stuck… no transition"). Replaces a flat 1.8s wait + whole-panel crossfade. The shared writing-style card is the anchor that doesn't move. `markReplied()` is now async and eases card height.
- **2026-10-16 · Automate Replies step restored** (owner: "missed one step after replied reviews"). Flow: Send Replies → temporary Replied state (~1.8s) → Writing Style + Automate Replies (10677:35306) → Save and Continue → Creating Social Posts. This supersedes the earlier same-day call to skip it.
- **2026-10-16 · Replied: review and reply 1 line each** (owner). "Read more" appears only when something is truncated and expands both (agent).
- **2026-10-16 · ↳ reply icon** drawn by hand (agent; awaiting the real Figma icon).
- **2026-10-15 · Regenerate Writing Style shows a skeleton loader**: headings, stars and tag stay; bullets and pattern become grey bars (owner).

## Profile & search (earlier)
- **Progress bar doesn't move during the first step** (owner).
- **Parent task moves down and shows the finished message** in every phase (owner).
- **The last working step is "Updating your business profile with optimized content"** (owner).
- **AI Corrected tab shows concise, realistic competitor-based reasoning** (owner).
- **Missing filter lists every empty field incl. services, media, social; lat/lng auto-filled from the map; no "Added from the business details you've shared" on empty fields** (owner).
- **Search works from any keyword and any city** (owner).
- **"Back to results"** replaces "Choose another business" (owner).
- **Transition: left panel shrinks, card flies to top-left, steps stack one by one, slow and natural** (owner; an alternative was rejected).
