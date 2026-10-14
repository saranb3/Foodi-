# Foodi MVP PRD

Oct 12, 2026 · @Mighty

**Status:** v2, updated Oct 14 after the design was locked. This version matches the current mockups and is the spec for building in Claude Code.

## Problem

People find restaurants on TikTok and Google Maps, but they rate them somewhere else, so the two never connect. A spot gets saved as a screenshot, a TikTok bookmark or a Maps star. Months later you show up and can't remember why you saved it or what to order.

Beli covers rating, but it has real friction for heavy users:

- It forces comparisons across unrelated places, like a sandwich spot against fine dining
- Some features are locked behind referring friends
- Food recommendations are janky and sometimes send you to a news article
- The map reloads every time you zoom in or out
- The feed isn't something people check regularly

## Target user and positioning

**Positioning:** Save restaurants from TikTok and Maps, and remember exactly what to order when you get there.

**First users:** UIUC students in Champaign who already save food spots on Google Maps or TikTok and eat out often. The model user is a friend who saves everything on Google Maps and rarely records what they ordered.

**What we are not:** a discovery feed. TikTok and Google Maps keep discovery; Foodi is where those finds land and where rating happens.

## Design principles

Each principle answers a specific Beli frustration, so every feature can be checked against one.

| Principle | Beli frustration it answers | Build cost |
|---|---|---|
| You only rate the thing you ate (dishes, never cross-category places) | Forced sandwich vs fine dining comparisons | Core of v1 |
| Logging a meal takes under 30 seconds, even from home the next day | Unintuitive rating flow | Core of v1 |
| The map feels instant, no reload on zoom | Map reloads on every zoom | Core of v1 |
| Find what you're in the mood for in a tap or two (cuisine, occasion and vibe filters that stack) | No interactive cuisine filtering | Small, v1 |
| No feature is ever locked behind referrals | Referral-gated features | None, a promise |

## MVP scope

The MVP is one loop that is useful to a single user on day one: search or save a place, go, rate dishes, and know what to order next time.

Rating is the step that powers everything else, which is why it gets the most design attention.

| Feature | What it does | Done when |
|---|---|---|
| **Map home** | Your saved and been spots as cuisine emoji pins on a full-screen map. Tapping a pin opens a preview card with a photo, stars, status and the dish people get. Nearby pins cluster into a "+5" bubble. | Pins load once, zooming never reloads, and a tap shows the card |
| **Filters** | Cuisine, Occasion and Vibe chips that stack, each opening a scrolling row of options, plus an All / To try / Been toggle | Picking Thai and Date night shows only matching pins |
| **Search** | Search bar listing matching nearby restaurants from Google Places, each with stars, status, the top dish and a one-tap save | Typing "ramen" lists ramen spots, and tapping one opens its page |
| **Save a place** | Save from search or a restaurant page as Want to try, and record where it came from (TikTok, Maps, search) | The spot shows on the map and in the list with its source |
| **List tab** | Want to try and Been tabs with counts, sort by nearest or top rated, and the same filters as the map | Been rows show your pick and its verdict |
| **Restaurant page** | Photo header with name, stars and rating count; Want to try and Been toggles; hours and directions; swipeable What to order dish cards with verdicts and % would reorder; your note | You can tell what to order in 3 seconds |
| **Dish stories** | Tap a dish card to see people's photos full screen, in order Vibes, #1, #2 and so on, up to 5 photos per dish. The menu is a separate viewer. | Tapping goes photo to photo, then dish to dish |
| **Log a meal** | The + button suggests where you ate, then you add photos from that visit, pick dishes, rate each one and add an optional note | Done from home the next day in under 30 seconds |
| **Next-morning nudge** | One notification after a likely visit: "How was Kizuna Ramen?" | Tapping it opens the log sheet with that spot picked |
| **Share card** | After saving, a "My order at …" card sized for Instagram stories | One tap opens the share sheet |

## How ratings work

- **Dishes get a verdict:** Skip, Mid, Solid or Elite. The same four words are the rating input when logging. "% would reorder" is the share of a dish's ratings that are Solid or Elite.
- **Restaurants get stars,** computed from dish ratings. Proposed mapping: Elite 5, Solid 4, Mid 2.5, Skip 1, averaged across all dish ratings at that place. A place shows stars once it has 3 or more ratings, and "New" before that.
- **Why two layers:** people pick where to eat by cuisine hunch ("I want Japanese"), so stars help choose a place, and verdicts tell you what to order once you're there. Users only ever do one thing, rate what they ate, and never compare a taco truck to fine dining.
- **Dish duplicates:** when logging, show dishes already entered at that restaurant first, so "Pad Thai" and "pad thai w/ shrimp" don't split the ranking.

## Logging after the meal

Most people rate when they get home, not at the table. So Foodi doesn't need live location. The + sheet ranks likely spots using:

- photos you took near a restaurant (location and time)
- what you did in the app (opened a page, tapped Directions)
- your want to try list

One nudge the next morning catches the rest. Photo access is the main technical risk (see open questions).

**Empty restaurant pages:** most search results will have no Foodi ratings at first. Show "No dishes rated yet. Been here? Rate what you ordered." so an empty page becomes a prompt to contribute.

**Seeding:** before inviting testers, log dishes at 30 to 50 Champaign restaurants with two or three friends, and tag each place's occasion and vibe, so early searches land on pages with real dishes.

**Platform:** mobile app built with React Native and Expo. Friends test through Expo Go, so no App Store release is needed for v1.

## Design

The mockups are on the Foodi Screens canvas, page "full app flow (current)", linked as a clickable prototype. Visual rules live in the Foodi design system:

- a smooth rounded sans for names, and Figtree for text
- violet means you can act, and ink means selected
- Elite / Solid / Mid / Skip verdict pills
- emoji only on map pins

**Design v1 is locked.** New design ideas go to the backlog instead of reworking finished screens.

## Out of scope for v1

| Feature | Why not now | When |
|---|---|---|
| In-app feed, friends and follows | Empty network problem. The share card is the growth loop instead. | Later |
| Dish leaderboards ("best birria in Champaign") | Unintuitive. People pick by cuisine, not by dish. | Not planned |
| Dish search | Ranking dishes across restaurants needs many ratings | v1.5 |
| Import Google Maps saved lists | Needs a feasibility check on the export format | v1.5 |
| Automatic TikTok and Maps link parsing | Picking the place manually works for testing | v1.5 |
| Live or background location | Battery and privacy cost. Photos and in-app signals cover most visits. | Not planned |
| Notifications beyond the one nudge | One well-timed nudge is enough to test the idea | Later |
| Reservations (OpenTable) | Not core to remembering what to order | Later |
| Recommendations and ML ("people like you loved X") | Needs many overlapping ratings (cold start) | Once ratings are dense |

## Success metrics

The MVP works if friends keep using it after the novelty wears off and open it before ordering. These are proposed first-month targets, to adjust after launch.

| Metric | Proposed target (first month) | What it proves |
|---|---|---|
| Testers who log 5+ dishes | 10 people | Logging is easy enough to become a habit |
| Testers who open a restaurant page before ordering at least once | 3 people | The restaurant page delivers real value |
| Logs started from the + suggestions or the nudge | 50%+ | Logging from home works |
| Median time to log a meal | Under 30 seconds | The core promise holds |
| Searches that land on a page with at least one rated dish | 50%+ | Seeding covers what people actually look up |
| Places saved per tester | 10+ | Foodi is replacing screenshots and Maps stars |
| Share cards posted | 5+ | The growth loop has a pulse |

## Data model and tech approach

Store every rating as a `(user, dish, verdict, time)` record from day one. That is exactly the data collaborative filtering needs later, so the ML phase needs no migration.

| Table | Key fields |
|---|---|
| `users` | id, name, created_at |
| `places` | id, google_place_id, name, lat, lng, cuisine, occasion_tags, vibe_tags, price |
| `saves` | user_id, place_id, status (want_to_try / been), source (tiktok / maps / search), saved_at |
| `dishes` | id, place_id, name |
| `ratings` | id, user_id, dish_id, verdict (skip / mid / solid / elite), note, created_at |
| `photos` | id, rating_id, url, taken_at, lat, lng, is_vibe |
| `place_scores` (computed) | place_id, stars, rating_count, and per dish: verdict mix and % would reorder |

**Stack (proposed):**

- Expo (React Native) for the app
- Supabase for the Postgres database, logins and photo storage
- Google Places API for search and cuisine
- react-native-maps with clustering
- expo-media-library for photo time and location
- expo-notifications for the nudge

## Build order

- [ ] Set up Expo and Supabase, and seed 10 Champaign spots
- [ ] Thin slice: map pins → restaurant page → log one dish with a verdict
- [ ] Spike: read photo time and location on iOS (decides how the + suggestions work)
- [ ] Save, the List tab and filters
- [ ] Search with Google Places
- [ ] Photos in logging, then dish stories
- [ ] Next-morning nudge and share card
- [ ] Seed 30 to 50 spots and invite testers

## Open questions

- Can Expo read photo location and time reliably on iOS, and will people grant photo access? If not, the + sheet falls back to app activity and the want to try list.
- Is the verdict to stars mapping right (Elite 5, Solid 4, Mid 2.5, Skip 1)?
- Should stars be relative to cuisine, so a great taco truck can be 5 stars?
- Who tags occasion and vibe: me during seeding, users with one optional tap, or both?
- Do stars alone help people choose, or do they need "people get the spicy miso" next to them?
- Without referrals or a feed, is the share card enough to spread past the first friend group?

**Research to run alongside the build:** interview the friend who saves everything on Google Maps, ask 5 to 8 friends about their last new restaurant visit, and watch 2 or 3 friends log a meal in the prototype to see where they hesitate.
