# Flow and screens

Figma file `FQOv3xhldcOc59KkTe3lq2`. Node IDs are written `10657:4151` (the URL form is `node-id=10657-4151`).
Left = `aside.setup-panel` (steps). Right = `.workspace` panel. "Parent" = the AI step at the top of the list, which finally **settles at the bottom** with italic text.

| # | Screen | Figma | Right panel | Left panel / progress |
|---|---|---|---|---|
| 1 | Search: empty | 10657:4151, button 10785:8965 | Illustration (updated 10673:3461) | Greeting "Hi John!" + search textarea |
| 2 | Searching | 10657:4266 | Skeleton rows | — |
| 3 | Results | 10657:4329 | `.business` cards (hover: shadow + `#698EC4` outline) | — |
| 3b | Create a new profile ("I don't see my business") | 10768:18579 | `main#screen-create`, full width: description textarea, location search + live map (opens on the searched city). **Create Profile** (disabled until both filled) → screen 4, then the normal flow | No side panel. Back link on later screens = "Back to profile details" → returns here |
| 3c | Google sign-in (new business only) | 10773:18769 | `#gauth`, a full-page Google-style account chooser opened by "Connect Google & Publish" when `cameFrom === 'create'`. Picking a row → toast "Your Google Business Profile has been created" → screens 8–10 (listings) | Back link hidden |
| 4 | Processing | 10657:4415 | AI dot-wave animation | Card flies to top-left; panel shrinks 716→386; steps stack in one by one. Progress **70 (unchanged on purpose)** |
| 5 | Steps completing | 10657:4470 | Animation | Competitor ✓ "Learnt what your competitors are doing." → Brand ✓ "Updated the brand context for your business." → slides in ✓ "Found 9 gaps in your business profile" |
| 6 | Profile form | 10657:4531, 10670:3742 | `#profile-form` with All / AI Corrected / Missing pills, AI reasoning notes, live map | Last working step "Updating your business profile with optimized content" fades; parent → "Business profile is ready for your review. You can make changes, or publish right away!" |
| 7 | Connect GBP modal | 10677:32796 / 32959 | `#connect-modal` (groups + locations, opt-in checkbox) | Toast "Business details updated on google"; **"Back to results" hidden from here on** (also when connecting without the listings opt-in, which stays on the form) |
| 8–10 | Finding publishers → list | 10677:33177 / 33282 | Animation → skeleton → `#publishers` list | Milestone ✓ "We have fixed 9 profile gaps!"; steps "Finding most relevant publishers for your business..." + "updating your brand context ..." → ✓ "Updated the brand context for your business."; parent → "Found the most relevant publishers for your business". Progress **120** |
| 11 | Opt-in modal | 10677:33911 | `#optin-modal` | Toast "Opt-in request submitted for N publisher(s)."; milestone ✓ "Opted in!" |
| 12 | Learning from reviews | — | Animation ("Learning from your reviews...") | Steps "Learning from your reviews" / "Reading your past reviews..." / "Learning your reply pattern..." |
| 13 | Inbox loading | 10677:34560 | `#inbox-loading` skeleton cards | ✓ "Read all your past review replies" |
| 14 | Inbox drafts | 10677:34964 | `#inbox-ready`: writing-style card + 6 review cards with Draft replies (Edit / Send Reply on hover) | ✓ "Learnt your writing style", + ✓ "Generated replies to your unanswered reviews", + ✓ "Updated your brand context"; parent → "Learnt your reply pattern and generated replies for 130 reviews" |
| 14a | Writing-style modal | 10677:35415, 10754:16053 | `#style-modal` with Brand Context / Writing Style tabs; Regenerate → skeleton | — |
| 15 | **Send Replies → Replied (temporary)** | pasted design (Reply Status=Replied) | Cards switch to the replied state (1-line review + 1-line italic reply under a divider, ↳ icon, "Read more") | Toast "6 review replies sent"; milestone ✓ "Replied to 6 Reviews / Ensuring no review goes unanswered!". Steps clear. Progress **184**. Cascade (cards replied one by one, heights easing) → ~0.9s beat → scroll to top → replied cards drop away → 15b, with the writing-style card staying in place |
| 15b | Writing style + Automate Replies | 10677:35306 | `#inbox-done`: "Your Reply Writing Style" card (View Detailed Writing Style) + Automate Replies (Positive 5★ 4★ Recommends / Negative 1★ 2★ 3★ Does not Recommend, toggles) + note. Button becomes **Save and Continue** → screen 16 | Unchanged |
| 16 | Creating social proof | 10754:16462 | Animation ("Creating Social Posts") | Steps "Creating Social Proof..." / "Picking your top 6 reviews from your inbox..." / "Getting your posts and website widget ready..." → ✓ "Picked reviews with the strongest praise", ✓ "Created your posts and website widget"; parent → "Turned top Customer Reviews into testimonials". Progress **250** |
| 17–18 | Social posts / all selected | 10754:16531 / 16648 | `#social`: 3×2 posts built from the top reviews (checkbox on hover), accounts list (10 of 11 preselected), "I'll do it later", Share Now split button | Unchanged |
| 19 | Website widget | 10758:17323 | `#widget`: browser frame, 5.0 ★ (120), AI Summary (white, yellow border), 3-card review carousel, HTML code card (Copy / Send as Email) | Toast "N Posts Scheduled." (Share Now only). Progress **316** |
| 20b | Final, new business | 10773:18776 | Same `#screen-final`, `[data-for=new]` head: "Get **your first 100** 5 Star Reviews", star at "Starting out", marks 10 / 50 / 100. Reached from Opt-in (screen 11) on the create path, about 1.2s after the toast | — |
| 20 | Final | 10758:17527 (cards 10758:17567) | `#screen-final`, no side panel: "Get **75 more 5-star reviews** to reach 4.0 Stars", rating bar (star pops at 1.0, slides with the fill to 3.8), "Go to Dashboard", "Send First Review Request", 3 tool cards; hover reveals each card's description + CTA (Send Quick Review Request / Download QR Code / Preview Feedback Form) | Header link hidden |

## Copy that the owner set
- "Back to results" (not "Choose another business").
- The Missing view must not say "Added from the business details you've shared" on empty fields.
- The AI Corrected reasoning reads like a concise AI layer that researched competitors (e.g. why the About text changed).

## Interactions per screen
- **Results:** click a card → card-flight transition (`list` click handler).
- **Form:** pills switch views; the Missing view lists only empty slots (`markMissing`); lat/lng auto-filled from the map.
- **Inbox (drafts):** Edit toggles inline editing; Send Reply marks one card replied; Send Replies marks all, shows the replied state, then the Automate view; **Save and Continue** (same button, `sendAll.dataset.done`) → `runSocialProof()`.
- **Posts:** clicking a post toggles it; Select All / Clear All; the accounts Select All link appears for partial selections; Share Now is disabled (40% opacity) until ≥1 post and ≥1 account.
- **Widget:** arrows cycle the reviews; Copy → clipboard + toast; Send as Email → `mailto:` draft; Continue → final.
- **Final:** "Go to Dashboard" and the card links are **not wired** (no destination yet).
