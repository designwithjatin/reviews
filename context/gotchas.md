# Gotchas (things that already bit us)

## Styling
- **Class-name collisions.** `.social` already styles the social-link rows in the profile form (`display:flex; align-items:center`). The social-posts panel is therefore `.share-panel`. Before adding a new class, grep `styles.css` for it.
- **Cache.** Browsers keep the old `styles.css`. Bump `?v=N` in `index.html` on every CSS change, and use the no-cache preview server.
- **Inline highlight backgrounds** position relative to the span's content box (~34px for 24px text), not the 46px line box. Measure against the baseline.

## Animation
- **`scale` vs `transform`.** The individual `scale`/`translate` properties compose with `transform`, and `scale` is applied *outside* `transform`, so scaling a `transform: translateX()` scales the distance too. To pop and slide one element, slide with `translate` and pop with `scale`.
- **Two animations on the same property:** the later one wins, even in its backwards-fill delay phase. Don't animate one property from two places.
- **Phases chain on `done()` / `hold()`**, which run on the animation clock. If the tab or preview pane stops producing frames, the whole flow pauses (expected).

## Testing in the preview pane
- The pane **sometimes stops rendering frames**: animations freeze at `currentTime` 0 and timers throttle to 1s. Real-time sampling then lies. Instead, pause the animations and step `currentTime`, or force `.finish()`.
- **Screenshots can lag a frame** behind the DOM (e.g. a button looked disabled but wasn't). Confirm state with `javascript_tool`.
- **Shortcuts corrupt the left steps.** Calling `runReviews()` or `runSocialProof()` without the preceding phase's `showSteps()` leaves old steps in the list, and `settleParent` then moves the wrong row. The owner once saw this in the shared pane and thought the animation was broken. Reproduce the real phase sequence, and remember the owner can see the pane.
- The `ai-onboarding-reviews` server gets stopped by the app; restart it with `preview_start`.

## Maps
- The preview pane doesn't render Google Maps embeds (all map iframes are blank there, including the old profile-form map). They work on the live site. Don't chase it as a bug.

## Figma
- Large nodes exceed the MCP output limit, so the result is saved to a file: `jq -r '.[0].text' file`, or fetch child nodes.
- Asset URLs expire after 7 days, so download them locally.
- Figma often has placeholder data (repeated copy, celebrity names, a mislabelled chip). Choose sensibly, then flag and log the choice.

## Search
- A query without a category keyword (e.g. "Third Wave") gets "Local Business" (`parseQuery` fallback). Known, parked.
