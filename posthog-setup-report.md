# PostHog post-wizard report

The wizard has completed a PostHog integration for DevEvent, a Next.js 16 App Router application. PostHog is initialized via `instrumentation-client.ts` (the recommended pattern for Next.js 15.3+), with a reverse proxy configured in `next.config.ts` to route analytics requests through `/ingest` to avoid ad blockers. Three client-side events are captured in user interaction handlers: one when users click the "Explore Events" button, one when users click on any event card (with event slug, location, and date as properties), and one when users click navigation links (with link label and href). Exception autocapture and session replay are enabled by default via `capture_exceptions: true` in the PostHog init.

| Event Name | Description | File |
|---|---|---|
| `explore_events_clicked` | User clicked the 'Explore Events' button on the homepage. | `components/ExploreBtn.tsx` |
| `event_card_clicked` | User clicked on an event card to view event details. Properties: `event_slug`, `event_location`, `event_date`. | `components/EventCard.tsx` |
| `nav_link_clicked` | User clicked a navigation link in the top navbar. Properties: `link_label`, `link_href`. | `components/Navbar.tsx` |

## Next steps

We've built some insights and a dashboard for you to keep an eye on user behavior, based on the events we just instrumented:

- [Analytics basics (wizard) — Dashboard](https://us.posthog.com/project/525930/dashboard/1897017)
- [Explore Events button clicks (wizard)](https://us.posthog.com/project/525930/insights/nZeOU3e8) — Daily trend of homepage "Explore Events" button clicks
- [Event card clicks by event (wizard)](https://us.posthog.com/project/525930/insights/2bZjow9a) — Most clicked events, broken down by event slug
- [Navbar link clicks by destination (wizard)](https://us.posthog.com/project/525930/insights/bmXCWq2S) — Navigation activity broken down by link label
- [Event discovery funnel (wizard)](https://us.posthog.com/project/525930/insights/Ynu8nFRW) — Conversion from "Explore Events" click to event card click
- [PostHog setup notebook](https://us.posthog.com/project/525930/notebooks/fA3XpZZZ) — In-app copy of this report

## Verify before merging

- [ ] Run a full production build (the wizard only verified the files it touched) and fix any lint or type errors introduced by the generated code.
- [ ] Run the test suite — call sites that were rewritten or instrumented may need updated mocks or fixtures.
- [ ] Add `NEXT_PUBLIC_POSTHOG_PROJECT_TOKEN` and `NEXT_PUBLIC_POSTHOG_HOST` to `.env.example` and any onboarding scripts so collaborators know what to set.
- [ ] Wire source-map upload (`posthog-cli sourcemap` or your bundler's upload step) into CI so production stack traces de-minify.

### Agent skill

We've left an agent skill folder in your project. You can use this context for further agent development when using Claude Code. This will help ensure the model provides the most up-to-date approaches for integrating PostHog.
