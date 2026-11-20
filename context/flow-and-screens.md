# Flow and screens

Figma file `FQOv3xhldcOc59KkTe3lq2`. Node IDs are written `10657:4151` (the URL form is `node-id=10657-4151`).
Left = `aside.setup-panel` (steps). Right = `.workspace` panel. "Parent" = the AI step at the top of the list, which finally **settles at the bottom** with italic text.

| # | Screen | Figma | Right panel | Left panel / progress |
|---|---|---|---|---|
| 1 | Search: empty | 10657:4151, button 10785:8965 | Illustration (updated 10673:3461) | Greeting "Hi John!" + search textarea |
| 2 | Searching | 10657:4266 | Skeleton rows | — |
| 3 | Results | 10657:4329 | `.business` cards (hover: shadow + `#698EC4` outline) | — |
| 3b | Create a new profile ("I don't see my business") | 8818:104432 (was 10768:18579) | `main#screen-create`, two columns: **left panel** (696px, white) with description (90px box), location search + live map (opens on the searched city); **right** (#F8F9FA) illustration of a Google search showing a finished Business Profile card ("Johnny's Pizzeria", 4.2 ★, photos) with a dotted arrow, captioned "Tell us a bit about your business. / We’ll handle the rest!". **Create Profile** (disabled until both filled) → screen 4, then the normal flow | No side panel. Back link on later screens = "Back to profile details" → returns here |
| 3c | Google sign-in (new business only) | 10773:18769 | `#gauth`, a full-page Google-style account chooser opened by "Connect Google & Continue" when `cameFrom === 'create'`. Picking a row → toast "Your Google Business Profile has been created" → screens 8–10 (listings) | Back link hidden |
| 4 | Processing | 10657:4415 | AI dot-wave animation | Card flies to top-left; panel shrinks 716→386; steps stack in one by one. Progress **70 (unchanged on purpose)** |
| 5 | Steps completing | 10657:4470 | Animation | Competitor ✓ "Learnt what your competitors are doing." → Brand ✓ "Updated the brand context for your business." → slides in ✓ "Found 9 gaps in your business profile" |
| 6 | Profile form | 10657:4531, 10670:3742 | `#profile-form` with All / AI Corrected / Missing pills, AI reasoning notes, live map | Last working step "Updating your business profile with optimized content" fades; parent → "Business profile is ready for your review. You can make changes, or publish right away!" |
| 7 | Connect GBP modal | 10677:32796 / 32959 | `#connect-modal` (groups + locations, opt-in checkbox) | Toast "Business details updated on google"; **"Back to results" hidden from here on** (also when connecting without the listings opt-in, which stays on the form) |
| 8–10 | Finding publishers → list | 10677:33177 / 33282 | Animation → skeleton → `#publishers` list | Milestone ✓ "We have fixed 9 profile gaps!"; steps "Finding most relevant publishers for your business..." + "updating your brand context ..." → ✓ "Updated the brand context for your business."; parent → "Found the most relevant publishers for your business". Progress **120** |
| 11 | Opt-in modal | 10677:33911 | `#optin-modal` | Toast "Opt-in request submitted for N publisher(s)."; milestone ✓ "Opted in!" |
| 12 | Learning from reviews | — | Animation ("Learning from your reviews...") | Steps "Learning from your reviews" / "Reading your past reviews..." / "Learning your reply pattern..." |
| 13 | Inbox loading | 10677:34560 | `#inbox-loading` skeleton cards | ✓ "Read all your past review replies" |
| 14 | Inbox drafts | 10677:34964 | `#inbox-ready`: writing-style card + 6 review cards with Draft replies (Edit / Send Reply on hover) | ✓ "Learnt your writing style", + ✓ "Generated replies to your unanswered reviews", + ✓ "Updated your brand context"; parent → "Learnt your reply pattern and generated replies for 130 reviews" |
| 14a | Writing-style modal | 10677:35415, 10754:16053; sections 8879:34179 | `#style-modal` with Brand Context / Writing Style tabs; Regenerate → skeleton. Google: 5★…1★ (stars only) + Cross-Rating. Facebook: Facebook Recommends (green tag) + Facebook Doesn't Recommend (grey tag) + Cross-Rating | — |
| 15 | **Send Replies → Replied (temporary)** | pasted design (Reply Status=Replied) | Cards switch to the replied state (1-line review + 1-line italic reply under a divider, ↳ icon, "Read more") | Toast "6 review replies sent"; milestone ✓ "Replied to 6 Reviews / Ensuring no review goes unanswered!". Steps clear. Progress **184**. Cascade (cards replied one by one, heights easing) → ~0.9s beat → scroll to top → replied cards drop away → 15b, with the writing-style card staying in place |
| 15b | Writing style + Automate Replies | 10677:35306 | `#inbox-done`: "Your Reply Writing Style" card (View Detailed Writing Style) + Automate Replies (Positive 5★ 4★ Recommends / Negative 1★ 2★ 3★ Does not Recommend, toggles) + note. Button becomes **Save and Continue** → screen 16 | Unchanged |
| 16 | Creating social proof | 10754:16462 | Animation ("Creating Social Posts") | Steps "Creating Social Proof..." / "Picking your top 6 reviews from your inbox..." / "Getting your posts and website widget ready..." → ✓ "Picked reviews with the strongest praise", ✓ "Created your posts and website widget"; parent → "Turned top Customer Reviews into testimonials". Progress **250** |
| 17–18 | Social posts / all selected | 10754:16531 / 16648 | `#social`: 3×2 posts built from the top reviews (checkbox on hover), accounts list (10 of 11 preselected), "I'll do it later", Share Now split button | Unchanged |
| 19 | Website widget | 10758:17323 | `#widget`: browser frame, 5.0 ★ (120), AI Summary (white, yellow border), 3-card review carousel, HTML code card (Copy / Send as Email) | Toast "N Posts Scheduled." (Share Now only). Progress **316** |
| 20b | Final, new business | 10773:18776 | Same `#screen-final`, `[data-for=new]` head: "Get **your first 100** 5 Star Reviews", star at "Starting out", marks 10 / 50 / 100. Reached from Opt-in (screen 11) on the create path, about 1.2s after the toast | — |
| S1 | Skip-auth: profile form | Lfz2…/8812:16256 | `#connect-later` ("I'll do it later") beside "Connect Google & Continue" | `skipAuth = true`; back link hidden |
| S2 | Skip-auth: listings | Lfz2…/8711:46830 | `#publishers` with "Found 7 Publishers…", `#list-later` shown, `#pub-active` hidden; opt-in works | ◌ "9 Profile fixes drafted." Progress **120** |
| S3 | Skip-auth: inbox | Lfz2…/8812:49960 | `#inbox-recent`: connect banner, 5 read-only cards (hover expands the card with a connect note); `#inbox-continue`. **Connect Google Account** (banner or card) → connect modal without the opt-in checkbox (Facebook result: Connect Facebook) → toast → AI "Learning from your reviews" steps → connected inbox (screen 13 onward) | ◌ "Found 7 Relevant Publishers" (only if listings were skipped; opting in gives ✓ "Opted in!"); steps ✓ "Found 130 reviews on Google", ✓ "Updated your brand context", AI "Brought in your latest Google reviews. Take a look at what your customers are saying." |
| S4 | Skip-auth: posts | Lfz2…/8726:89182 | `#social` with 2 posts at 322px (`.posts__grid--big`) | ◌ "Read your past reviews"; same steps as screen 16. Progress **250** |
| S5 | Skip-auth: final | Lfz2…/8923:152632 | `[data-for=new]` head: "Get **your first 100** 5 Star Reviews" (no rating known without connecting); widget skipped | — |
| 20 | Final | 10758:17527 (cards 10758:17567) | `#screen-final`, no side panel: "Get **75 more 5-star reviews** to reach 4.0 Stars", rating bar (star pops at 1.0, slides with the fill to 3.8), "Go to Dashboard", "Send First Review Request", 3 tool cards; hover reveals each card's description + CTA (Send Quick Review Request / Download QR Code / Preview Feedback Form) | Header link hidden |

## Facebook path (2026-11-18; Figma Lfz2oHviZXGc9NDmp8JEpq)
Search returns **Google listings only**. Facebook is reached only through the **Facebook Page pill** (see below), which sets `picked.platform = 'facebook'`. In that mode:
- **Profile form:** "Connect Facebook & Continue" with the Facebook icon. It opens the **Connect Facebook** modal (`#fb-modal`, Figma 8845:140826): search + two-column Page list, the business first and selected, its other branches, then other Pages (no "Potential match" tags); Connect. No real auth.
- **Connected:** toast "Your Facebook Page is connected" → listings (Active Listings card = Facebook Page; milestone "We have fixed 9 Page gaps! / Your Facebook Page is ready for your customers.") → opt-in → **Facebook inbox** (8848:142623): Facebook icon, **Recommends / Does not Recommend** tags instead of stars (4–5 = Recommends), and **I'll do it later** next to Send Replies (skips to social posts) → replied state → automate replies (8848:143156) → **posts** with the Facebook icon + Recommends tag (8850:155386) → **widget** cards with "Recommended" + Facebook icon (8850:155509) → last step **"To maintain your recommendations, get 50 more on Facebook"** (0/50/100/150/200 count bar, Facebook mark in the marker; Figma 8853:28868).
- **Skipped auth:** not in the prototype. The "Start collecting recommendations" screen is reserved for a future Figma scenario (new Page, no reviews yet).
- Last step on both: request card button "Recommend us", QR card shows the Facebook chip only, tool descriptions mention Facebook.

## Google pill path (2026-11-18; Figma Lfz2oHviZXGc9NDmp8JEpq 8860:178290)
**Google Business Profile** pill on the search screen → Google sign-in (the user's own placeholder account: John Doe · john.doe@gmail.com, letter avatar) → **Connect Google Business Profile** modal (demo business "Third Wave Coffee Jaipur", groups + locations, Opt-in for listings) → toast "Your Google Business Profile is connected" → the search screen steps aside, the left panel shows the chosen profile, AI steps run → profile form with **I'll do it later** + **Publish Changes & Continue** (Google icon). No "Back to results" (there are no results).
- **Publish Changes & Continue** → toast "Business details updated on google" → listings → the connected flow (inbox, posts, widget, final).
- **I'll do it later** → still connected; pending milestone "9 Profile fixes drafted. You can publish them anytime from your dashboard" → listings → the connected flow.

## Facebook pill path (2026-11-18)
**Facebook Page** pill on the search screen → **Connect Facebook** modal straight away (no Facebook login screen; demo business "Third Wave Coffee Jaipur") → toast "Your Facebook Page is connected" → AI steps → form with **I'll do it later** + **Publish Changes & Continue** (Facebook icon), no "Back to results". Publish → toast "Page details updated on Facebook" → listings → the Facebook connected flow (Recommends inbox, posts, widget, "Get 50 more recommendations"). I'll do it later → "9 Page fixes drafted. You can publish them anytime from your dashboard", still connected.

## Read-only inbox · hover (2026-11-19; Figma 8818:89180 / 8818:89672)
On the Google skip-auth inbox, **hovering** a card expands it as an overlay over the card below (nothing moves): hover border + shadow, and a note under the review: Google G + "To view & manage replies, **Connect Google Account**". No action icons (open / copy / reply) on these cards. The link isn't wired yet.

## Copy that the owner set
- "Back to results" (not "Choose another business").
- Basic Details header has no "Added from the business details you've shared" note (removed 2026-11-19).
- Profile form sections: Basic Details → **Category** (Primary/Secondary + Additional Categories, AI notes) → About → Hours → Services → Media → Social Media. Basic Details order: Name/Website → Email, Country, Street, City beside Map → State/Latitude → ZIP/Longitude → Phone/Alt Phone. The opt-in summary uses the same order.
- The AI Corrected reasoning reads like a concise AI layer that researched competitors (e.g. why the About text changed).

## Interactions per screen
- **Results:** click a card → card-flight transition (`list` click handler).
- **Form:** pills switch views; the Missing view lists only empty slots (`markMissing`); lat/lng auto-filled from the map.
- **Inbox (drafts):** Edit toggles inline editing; Send Reply marks one card replied; Send Replies marks all, shows the replied state, then the Automate view; **Save and Continue** (same button, `sendAll.dataset.done`) → `runSocialProof()`.
- **Posts:** clicking a post toggles it; Select All / Clear All; the accounts Select All link appears for partial selections; Share Now is disabled (40% opacity) until ≥1 post and ≥1 account.
- **Widget:** arrows cycle the reviews; Copy → clipboard + toast; Send as Email → `mailto:` draft; Continue → final.
- **Final:** "Go to Dashboard" and the card links are **not wired** (no destination yet).

## Last step · first review request (2026-11-19; Figma 8916:149002)
- **Send First Review Request** opens `#qrr-modal` (Quick Review Request): Add New Contact tab (First Name*, Last Name, Phone, Email), then two options: **New request with template** (Template "🌟 Creative Design" with channel counts, Review Links "All Review Links") or **Add in existing campaign** (Campaign select). Footer: info line, "Send another request" checkbox, **Send Request** (disabled until first name + phone or email + an option).
- Send → "Sending..." (~0.9s) → toast "Review request sent" → modal closes (stays open and resets if "Send another request" is ticked).
- Last step then shows ✓ "You’ve sent your first review request! go to dashboard to see what’s next." (Figma 8919:151199) in place of the link; Go to Dashboard stays the outline (secondary) button. Reset each time the last step is shown.
