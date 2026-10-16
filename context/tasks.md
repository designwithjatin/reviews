# Tasks

Update this file whenever a task starts, finishes, is parked or is dropped. Date format `YYYY-MM-DD`.

## Ongoing
- _(none)_. The flow is built end to end through the final screen (as of 2026-10-16).

## Open questions (waiting on the owner)
| Since | Question | Context |
|---|---|---|
| 2026-10-16 | Should the left QR-code chip say "Google" (built) or "Facebook" (as in Figma)? | Figma shows the Google icon labelled "Facebook", which looks like a slip. |
| 2026-10-16 | Real copy for the **QR Code** and **Feedback Form** card descriptions and links | Figma reuses the Quick Review Request text on all three cards, so placeholder copy was written. |
| 2026-10-16 | Exact **reply (↳) icon** from Figma | A hand-drawn SVG (`assets/reply.svg`) is used until the owner shares the node. |

## On hold / backlog
| Since | Task | Notes |
|---|---|---|
| 2026-10-15 | Search with no category word (e.g. "Third Wave") gets the category **"Local Business"** | `parseQuery` falls back when no `CATEGORIES` regex matches. Possible fixes: infer from known brand names, or default to the most common category. The owner hasn't asked for a fix yet. |
| 2026-10-15 | Wire **Go to Dashboard**, **Send First Review Request** and the tool-card links | No destinations defined in Figma. |
| 2026-10-15 | Reviews and the widget AI summary are always café-themed | Fine for the café demo. Would need per-category content for other business types. |

## Done (recent first)
- 2026-10-16: Restored the Writing Style + Automate Replies step (10677:35306) after the temporary replied state; Save and Continue → social posts.
- 2026-10-16: Agent docs: `AGENTS.md`, `CLAUDE.md`, `context/`, `.vercelignore`.
- 2026-10-16: Rating star pops in at 1.0 and travels with the bar fill; heading highlight moved behind the text baseline.
- 2026-10-16: Replied state: review and reply truncated to 1 line each, "Read more" only when cut off, ↳ icon.
- 2026-10-16: Send Replies → temporary Replied state (the auto-skip past Automate Replies was reversed the same day; see above).
- 2026-10-16: AI Summary card: removed the gradient (plain white).
- 2026-10-16: Share Now disabled = 40% opacity on the whole split button.
- 2026-10-16: Final-screen tool cards rebuilt in HTML/CSS (no screenshots).
- 2026-10-15: Social Posts, select-all state, Website Widget and Final screens built and wired.
- 2026-10-15: Reviews inbox (loading, drafts), writing-style modal with regenerate skeleton.
- Earlier: Connect GBP, publishers, opt-in; Missing filter, auto lat/lng, live map; AI reasoning notes; keyword- and any-city search; card-flight transition; profile form.

## Rejected (don't redo)
| Date | Idea | Why |
|---|---|---|
| ~2026-10-05 | `index-v2.html` "easier" business-select transition | The owner preferred the original transition. One-file rule since then. |
| ~2026-10-05 | Alternative copy options for "Choose another business" (first rounds) | Settled on "Back to results". |
| 2026-10-16 | PNG screenshots of the final-screen card illustrations | The owner asked for real HTML/CSS. |
| 2026-10-16 | Gradient background on the AI Summary card | Figma 10758:17434 is plain white. |
| 2026-10-16 | 2-line clamp for replied reviews | The owner wants 1 line for both review and reply. |
| 2026-10-16 | Pale-blue (`#C5DBFA`) disabled Share Now | Replaced by 40% opacity of the brand button. |
