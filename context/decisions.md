# Decisions log

Newest first. Each entry: **date · decision**, why, and who decided (owner = Jatin; agent = a judgment call flagged to the owner).

## Process
- **2026-10-16 · Ask before every push** (owner). Several pushes went out unasked; from now on every push needs a yes.
- **2026-10-16 · Agent docs live in the repo** (owner): `AGENTS.md`, `CLAUDE.md` → `AGENTS.md`, `context/`. Agents must keep `context/` current. `.vercelignore` keeps them off the public site (agent).
- **~2026-10-06 · One file only** (owner): all work in `index.html`, no `-v2` copies; experiments on branches.
- **~2026-10-03 · Personal repo + Vercel** (owner): `designwithjatin/reviews` on `main`, auto-deployed. The team repo `groupone-design` isn't used (no merge rights).
- **Build from Figma data, not screenshots** (owner, 2026-10-16).

## Left panel milestones
- **2026-10-17 · Milestone: only the check is animated** (owner). The block still fades in from -8px as before; inside it the green check grows gently from 0.7 (`EASE_OUT_SOFT`) and draws its tick (inline SVG, `M.pop` / `M.draw`). Everything else tried that day was reverted at the owner's request: a ripple ring and strong pop ("sudden, not polished"), blur-in text ("don't like blur at all"), a 12px slide-in and a clip-wipe for the text, a 200ms lead-in, and delaying the progress fill until the check landed. Text timing and the 600ms progress fill are back to the original.

## Final screen
- **2026-10-16 · Star travels from 1.0 with the bar** (owner): it pops in at the left, then slides to 3.8 on the same curve as the fill. Implemented with the `translate` + `scale` properties so the pop can't distort the slide (see gotchas).
- **2026-10-16 · Highlight behind the text** (owner): the yellow bar sits about 3.5px above to 5.5px below the baseline (Figma: 28px down a 46px line).
- **2026-10-16 · Long business names in the Feedback Form card start right of the John Doe chip and ellipsize** (agent).
- **2026-10-16 · QR chip labelled "Google"** (agent; Figma says "Facebook" next to a Google icon). Awaiting confirmation.

- **2026-10-16 · Tool-card CTAs: Figma icons and copy** (owner; Figma 10774:19150), on both final variants. **Shown only on hover/focus** (owner reversed the brief always-visible version the same day). The per-card descriptions stay the agent-written ones, because Figma still repeats the Quick Review Request text on all three.

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
- **2026-10-16 · Name from the search, category from the description** (agent).
- **2026-10-16 · City/state/PIN/coordinates from a real address lookup, not the search** (owner: "city state you can get from the map results itself"). Uses OpenStreetMap Nominatim (Google's geocoder needs an API key). The typed street is kept, the locality and city are appended if missing, and it falls back to heuristics if the lookup finds nothing.
- **2026-10-16 · New profiles have no website** (owner).
- **2026-10-16 · Google sign-in replaces the Connect GBP modal for new businesses** (owner; Figma 10773:18769). Rebuilt in HTML (the Figma frame is a screenshot). The footer says "SocialPilot's" Privacy Policy (the Figma screenshot said "Claude's") (agent). The account row shows **the business name, the profile's email and a letter avatar** (owner, replacing the owner's own name/email from Figma). "Use another account" also just continues (agent).
- **2026-10-16 · New businesses skip reviews/posts/widget: Opt-in → "Get your first 100 5 Star Reviews"** (owner: "this would be the step after listings"; the Opt-in trigger is the agent's reading).
- **2026-10-16 · Toast after sign-in: "Your Google Business Profile has been created"** (agent).
- **2026-10-16 · Back link on this path reads "Back to profile details" and returns to the create screen with inputs kept** (agent).
- **2026-10-16 · No way back from the create screen to the results** (agent; Figma has none). Flagged to the owner.

## Skip-auth path (2026-11-16, owner; Figma file Lfz2oHviZXGc9NDmp8JEpq)
- **"I'll do it later" on the profile form skips Google sign-in**; the main button reads "Connect Google & Continue".
- **Listings don't need auth**: opt-in works from the business details (owner).
- **Then an inbox of 5 recent reviews, read-only, with a Connect Google banner → Continue → posts → final** (owner).
- **Counts follow the prototype, not the Figma placeholders** (agent): "9 Profile fixes drafted" (Figma says 6; the steps say "Found 9 gaps"), "Found 7 Publishers / 7 Relevant Publishers" (Figma says 7 in one frame and 9 in another; there are 7 publishers). The drafted subtext stays "once you connect your business profile" everywhere (the Figma inbox frame says "later in the product").
- **Opting in on this path shows ✓ "Opted in!"**; only skipping the listings shows the pending "Found 7 Relevant Publishers" (agent).
- **Posts on this path: the 2 best of the 5 recent reviews**; Share Now and I'll do it later both go straight to the final screen (no widget) (owner: "the last step").
- **Not wired yet**: the inbox's "Connect Google Account" link and the card's open/reply actions (copy works). "View all 130 reviews" was removed (owner, 2026-11-16). The listings' "I'll do it later" goes to the inbox (agent reading).

## Google pill path
- **2026-11-19 · Social posts are all selected by default** (owner). "N Posts Selected", Share Now enabled on arrival; users untick what they don't want.
- **2026-11-19 · Create-profile screen is two columns** (owner; Figma 8818:104432). Form moves into a 696px left panel; the right side shows what they'll get — a Google Business Profile in search — with the caption "Tell us a bit about your business. We’ll handle the rest!". The illustration is static (Figma's "Johnny's Pizzeria"); photos are downscaled JPEGs.
- **2026-11-19 · First review request is sent from the last step** (PM feedback via owner; Figma 8916:149002). "Send First Review Request" opens the Quick Review Request modal (New Contact; "New request with template" or "Add in existing campaign"). Send Request → toast "Review request sent" → the link becomes a green-tick line "You’ve sent your first review request! go to dashboard to see what’s next." (Figma 8919:151199); **Go to Dashboard stays secondary (outline)** — it's the only action left (owner). Trial version — owner will iterate. "Add in existing campaign" body (one Campaign select) and the other two tabs being inert are agent choices; Figma doesn't show them.
- **2026-11-19 · Writing style split by platform** (owner, Figma 8879:34179). Google: 5-Star … 1-Star sections with stars only (no Facebook tags) + Cross-Rating. Facebook: Recommends + Doesn't Recommend + Cross-Rating.
- **2026-11-18 · Skipping the drafts still offers Automate Replies** (owner). Inbox "I'll do it later" → pending milestone → the review cards drop away → Writing Style + Automate Replies → **Save and Continue** → social posts. Automation is about future reviews, so it applies even when today's drafts aren't sent.
- **2026-11-18 · Connected users (Google or Facebook) who click the inbox "I'll do it later"** get a pending milestone in the sidebar, in the skip-auth style (Figma 8818:89951): **"Read your past reviews · We’ve drafted replies to your reviews"** (owner; the skip-auth path keeps "We’re ready to draft your review replies"). The progress bar moves on from where the inbox left it.
- **2026-11-18 · Listings "I'll do it later" shows on every path** (owner), next to Get Listed in All. Connected users: pending milestone "Found 7 Relevant Publishers", then learning from reviews → the inbox (create-profile path → its final screen). Skipped auth: unchanged (recent reviews).
- **2026-11-18 · Inbox "I'll do it later" shows for every connected user** (owner), not just the pill starts and Facebook. It skips to social posts. Supersedes the entry below.
- **2026-11-18 · Inbox "I'll do it later" shows on both pill starts** (Google and Facebook), as well as for any Facebook result (owner). Search-result Google path keeps Send Replies only.
- **2026-11-18 · Facebook pill mirrors the Google pill** (owner): Connect Facebook modal → AI steps → Publish Changes & Continue → the Facebook connected flow. No separate sign-in screen before the modal (agent; the Google pill has one because Figma shows it).
- **2026-11-18 · Google pill = sign in → pick the profile → AI steps → form with "Publish Changes & Continue"** (owner; Figma 8860:178290).
- **2026-11-18 · Sign-in shows a placeholder user (John Doe, letter avatar)**, not the business, because the business isn't known yet. Figma shows the owner's own name; never a real person (agent).
- **2026-11-18 · No "Back to results" on this path** (agent; Figma shows it, but there are no results to go back to).
- **2026-11-18 · "I'll do it later" on this path keeps the user connected**: fixes stay drafted, listings and the rest of the connected flow continue (agent reading).
- **2026-11-18 · Facebook inbox: "I'll do it later" sits 16px left of Send Replies** (owner reported the spacing).

## Facebook result path
- **2026-11-18 · Overlay reply editor on the Google inbox too** (owner; Figma 8882:73241). Same as Facebook, but the toolbar has **no image or GIF buttons** (emoji, then the pills). Inline edit is gone. Google cards get the same hover actions (open on Google, copy, reply).
- **2026-11-18 · Edit reply = overlay editor** (owner; Figma 8882:71943 / 8882:71969). On the **Facebook** inbox, **Edit** or the card's **reply icon** expands the card as an overlay over the cards below (nothing moves): the review, a divider, the editable reply, a toolbar (emoji, image, GIF, Templates, Rewrite, Shorten, Expand, Grammar, Tone) and a blue **Send** button. Send marks that card replied; clicking outside, Escape or the reply icon again closes it and keeps the edit. Cards also get hover actions (open, copy, reply). The owner will add a Google case in Figma; the Google inbox keeps inline edit until then.
- **2026-11-18 · Toolbar copy "Grammar"** (agent; Figma says "Grammer"). Rewrite / Shorten / Expand change the text with simple demo rules; Grammar and Tone show a toast; Templates, emoji, image and GIF do nothing yet (agent).
- **2026-11-18 · Facebook flow checked against Figma "Start with FB Auth" (8860:192375) and aligned** (owner asked for a full comparison):
  - Pill paths show a **form skeleton** (~1.4s) between the AI steps and the form (8860:200044).
  - Listings: **"Found 7 Publishers…"**, Active Listings label **"Facebook"** (8860:194680).
  - Writing-style modal: **"Facebook Recommends"** (Recommends tag), **"Facebook Doesn't Recommend"** (Does not Recommend tag, grey like the inbox), then Cross-Rating Behavioral Patterns; no star sections (8879:34179, supersedes 8860:196213 on 2026-11-19).
  - **Send Replies sending state**: dots in the button and "I'll do it later" dimmed for ~0.9s before the replied cascade (8860:196341). Applies to every path.
  - Last step: tools are the **same as Google** ("Leave a review", "Send First Review Request", both QR chips); the QR **Facebook chip shows "Recommends"** on every final screen (Tools component); the goal marker uses the **reviews icon** (8871:60281). Supersedes the Facebook-specific tool copy.
  - Not changed, flagged to the owner: Figma shows "Back to results" on the pill form (no results exist on that path); Figma's left-panel milestone copy is the Google one ("easier to find in Google"); avatars and "John Doe" names are placeholders.
- **2026-11-18 · Facebook pill opens SocialPilot's Connect Facebook modal directly** (owner: "we don't even need the connector"). A Facebook-style permission dialog was tried the same day and removed.
- **2026-11-18 · Search returns Google listings only; Facebook is reached only through the Facebook Page pill** (owner: "we don't get FB search results"). Search status reads "Searching your business on Google …". Each result is a distinct listing (the old Google + Facebook twin of the main listing is now a branch).
- **2026-11-18 · Facebook skipped-auth last step ("Start collecting recommendations") removed from the prototype** (owner). It'll come back in Figma for a new scenario: a new Facebook Page with no reviews yet. Supersedes the skipped-auth entries below.
- **2026-11-18 · Facebook connected last step heading = "To maintain your recommendations, get **50 more** on Facebook"** (owner). Highlight on "50 more". Updated in the prototype and in Figma 8853:28868 / 8868:221566.
- **2026-11-19 · No "Potential match" tags in the Connect Facebook modal** (owner). Supersedes the tags in the entry below.
- **2026-11-18 · Connect Facebook = a modal like the GBP picker** (owner; Figma 8845:140826): "Connect Facebook" tab, search, two-column list of Pages, the picked business first and selected, its other branches tagged **Potential match**, then other Pages the account manages; Connect only (no opt-in checkbox). Replaces the Facebook-style login stand-in.
- **2026-11-18 · Facebook widget card follows Figma 8850:155586** (owner flagged it): name and time on one line, "Recommended" row below, 20px Facebook mark, 16px padding. Avatars stay letters, like the Google widget (agent; Figma uses a stock photo).
- **2026-11-18 · A Facebook result runs a Facebook version of the flow** (owner). Connect Facebook instead of Google; inbox/posts/widget show Recommends instead of stars (Figma 8848:142623, 8848:143156, 8850:155386, 8850:155509).
- **2026-11-18 · Last step, connected: "Get 50 more recommendations on Facebook"** with a count bar (owner; Figma 8853:28868). The recommend % line was removed (owner).
- **2026-11-18 · Last step, skipped auth: "Start collecting recommendations", Go to Dashboard only, no connect nudge** (owner; Figma 8854:32265). The reminder to connect belongs in the dashboard ("Finish setup") and feature-level prompts.
- **2026-11-18 · Review requests can be sent without auth** (owner): the review link comes from the search result (Google place ID / Facebook Page). Suggested guardrails: verified account email as reply-to, a send cap before connecting (agent).
- **2026-11-18 · (superseded the same day by the Connect Facebook modal) Facebook login stand-in.** The Facebook connected path keeps the widget (owner sent the widget frame).
- **2026-11-18 · Facebook "I'll do it later" in the inbox skips to social posts** (agent reading).

## Connect GBP
- **2026-11-19 · Read-only inbox: hover expands the card as an overlay with the connect note; no action icons** (owner; Figma 8818:89180). Supersedes the 2026-11-18 click-reply version.
- **2026-11-18 · Read-only inbox reply → connect note under the card** (owner; Figma 8818:89672).
- **2026-11-17 · Skip-auth inbox banner note "To See and Reply to 130 more Reviews" = regular, black (`--txt-primary`), 14px** (owner; Figma had 12px semibold grey).
- **2026-11-17 · Listings groups have no outer border or padding** (owner; Figma Lfz2oHviZXGc9NDmp8JEpq 8711:46871): just the group label row, then the white rounded list 4px below. Applies to every listings screen.
- **2026-11-16 · Listings AI animation cycles exactly two phrases: "Finding relevant listing publishers" → "Updating brand context"** (owner). Applies to both connect paths and the skip-auth path, via `listingPhrases()`. The category / city phrases were dropped.
- **2026-10-16 · No form flash after Connect / Google sign-in** (owner). `coverForListings()` swaps the form for the AI animation behind the modal or sign-in page, which then closes straight onto the listings step. The toast shows there.
- **2026-10-16 · No "Back to results" after connecting GBP** (owner). Applies to both connect paths. The hide doesn't depend on the fade finishing, so a cancelled fade can't bring the link back.

## Reviews inbox
- **2026-11-16 · Brand Context tab = 2 inputs + Save** (owner; Figma FHSl3IYwrNTDd0auwgks6q 7422:121796). It replaces the read-only summary (Business, Short Description, Description, Categories, Amenities). The footer note is hidden, as in Figma (opacity 0). Save writes to `#form-email` / `#about-desc` and keeps the modal open (agent).
- **2026-10-16 · Connected transition from replied cards to Automate Replies** (owner: "feels stuck… no transition"). Replaces a flat 1.8s wait + whole-panel crossfade. The shared writing-style card is the anchor that doesn't move. `markReplied()` is now async and eases card height.
- **2026-10-16 · Automate Replies step restored** (owner: "missed one step after replied reviews"). Flow: Send Replies → temporary Replied state (~1.8s) → Writing Style + Automate Replies (10677:35306) → Save and Continue → Creating Social Posts. This supersedes the earlier same-day call to skip it.
- **2026-10-16 · Replied: review and reply 1 line each** (owner). "Read more" appears only when something is truncated and expands both (agent).
- **2026-10-16 · ↳ reply icon** drawn by hand (agent; awaiting the real Figma icon).
- **2026-10-15 · Regenerate Writing Style shows a skeleton loader**: headings, stars and tag stay; bullets and pattern become grey bars (owner).

## Profile & search (earlier)
- **2026-10-21 · Coworking Space category; whole-word category matching** (owner reported "co working space" labelled Beauty Salon) (agent fix).
- **2026-10-21 · Submit icon button in the search box** (owner: "for better usability"; Figma 10785:8965 / 9079). It's disabled until there's non-space text. The left magnifier is no longer a button (agent).
- **Progress bar doesn't move during the first step** (owner).
- **Parent task moves down and shows the finished message** in every phase (owner).
- **The last working step is "Updating your business profile with optimized content"** (owner).
- **AI Corrected tab shows concise, realistic competitor-based reasoning** (owner).
- **Missing filter lists every empty field incl. services, media, social; lat/lng auto-filled from the map** (owner). The "Added from the business details you've shared" header note was later removed everywhere (owner, 2026-11-19).
- **Search works from any keyword and any city** (owner).
- **"Back to results"** replaces "Choose another business" (owner).
- **Transition: left panel shrinks, card flies to top-left, steps stack one by one, slow and natural** (owner; an alternative was rejected).
- **Skip-auth final shows "Get your first 100 5 Star Reviews"**, not "75 more to reach 4.0": without a connection we don’t know their rating (Surbhi).
