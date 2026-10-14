# Foodi design (design.md)

_Design v1, locked Oct 14, 2026. Source of truth: the Foodi design system and the "full app flow (current)" page on the Foodi Screens canvas. Build screens from these tokens only._

Save restaurants from TikTok and Maps, and remember exactly what to order when you get there.

Foodi is smooth, friendly and modern: white pages, a smooth geometric sans (Sora) for names, a soft friendly sans (Figtree) for everything else, and one violet for anything you can tap. Personality comes from type, photos and copy, not from decoration. It deliberately avoids the editorial serif look of Beli. Values are starting points; check them on a real phone.

## Principles

- **One system, every screen.** Map, search, list, the restaurant page, dish stories and logging all use the same two fonts, the same colors and the same components. If a screen looks like it came from another app, it's wrong.
- **The dish is the hook.** Every card, row and result says what people order ("People get the spicy miso").
- **Photos over decoration.** Restaurants and dishes show photos (striped placeholders in mockups). No emoji tiles or pastel blobs standing in for food.
- **Each color has one job.** See Color. When a color starts doing two jobs, people stop being able to read it.
- **Sentence case everywhere.** "Want to try", "How was it?", "Your spots". Never all lowercase, never all caps (except tiny map labels).
- **Fast first, depth optional.** One tap saves a spot. Logging a meal is pick the place, add photos, rate each dish, save. Notes are optional.

## Color

| Token | Its one job |
|---|---|
| `ink` | Text, and every selected state (chips, toggles, the selected pin ring) |
| `violet` | Things you tap to act (primary buttons, the + button, links), plus the Elite verdict |
| `lilac` + `violet-ink` | Soft selection: picked cuisine, the Solid verdict, the New badge |
| `star` / `star-on-photo` | The star glyph next to a restaurant score. Nothing else is yellow |
| `open` | The word "Open". Closed is `text-secondary`, never red |
| `note` + `note-ink` | Your own note on a restaurant page |
| `surface-muted`, `line`, `border` | Fields, tracks, hairlines, outlines |
| `text-secondary` | Meta lines, counts, sources |
| `text-tertiary` | Inactive icons only (fails as text) |
| `scrim` | Dark gradient under white type on photos |
| `map-*` | The map's land, roads, parks, water and labels |

Rules:
- Selected is ink, action is violet. A selected chip is never violet; a primary button is never black.
- Yellow never carries text; it fails contrast.
- Status is always a word, never color alone.

## Ratings

Two layers, on purpose:
- **Restaurants get stars**, computed from their dish ratings: "4.7 (35)". Fewer than 3 ratings shows a lilac **New** badge instead.
- **Dishes get verdicts**: **Elite, Solid, Mid, Skip**, plus "% would reorder". The same four words are the rating input when logging.

| Verdict | Pill |
|---|---|
| Elite | `violet` background, white text |
| Solid | `lilac` background, `violet-ink` text |
| Mid | `surface-muted` background, ink-ish text |
| Skip | `surface-muted` background, `text-secondary` text |

## Typography

Two Google Fonts families, matched to the Zesty reference:
- **Sora** (`display`, weights 700 and 800) for names and big moments only: the score, restaurant and dish names, screen and section titles.
- **Figtree** (`sans`) for everything else: buttons, chips, meta, body, quotes and notes.

If you're unsure, it's Figtree. Sora is a headline face, so it never appears in buttons, chips, meta lines or paragraphs. No italics anywhere; quotes are Figtree 600 inside quote marks. (Tried and rejected: Fraunces, too editorial and Beli-like; Archivo Expanded, too stretched.)

## Emoji

Emoji appear in one place: **map pins**, where the cuisine emoji in a white circle tells you what a spot is at a glance with no text (text pins crowd fast).

Everywhere else uses line icons or words: to try is a bookmark, been is a fork and knife, sources are written out ("Saved from TikTok · 3d ago"), and all three filters (cuisine, occasion, vibe) are the same text pills. If an emoji ever sits before text, leave a clear gap before the first letter.

## Iconography

Outline icons with round caps and joins: 24px in the tab bar (1.75 stroke, 2.25 when active), 18 to 20px in buttons, 14 to 16px in chips. Core set:
- bookmark = want to try
- fork and knife = been
- map, list, profile = tabs
- search, locate, share, back, close

## Components and screens

### Map home
- Full-bleed muted map (`map-*`) with spaced uppercase neighborhood labels.
- **Pins**: white circle with a cuisine emoji and a small badge, violet with a bookmark for to try or ink with a fork and knife for been. The selected pin grows and gets an ink ring. Dense areas cluster into a "+5" pill.
- **Top**: a white search pill ("Craving something?") with a locate button, then a segmented scope control: All / To try / Been.
- **Bottom**:
  - a preview card for the tapped pin (photo, `row-title` name, To try / Been tag, score line, "People get the …")
  - three filter chips: Cuisine / Occasion / Vibe
  - the open filter's options as one sideways-scrolling row of pills, starting with Any (picked = ink, others white)
  - the tab bar, with the violet + button beside it

### Search
- Back button and a `surface-muted` search field.
- Chips: Spots / Dishes / Under $15.
- Each row:
  - photo thumbnail
  - name in `row-title` with the matched part heavier
  - score, cuisine, distance and status
  - "People get the …"
  - an outline bookmark button that fills ink when saved

### List tab
- `screen-title` "Your spots" with a Nearest / Top rated sort button.
- Want to try / Been segmented control with counts.
- The same Cuisine / Occasion / Vibe chips as the map.
- Rows:
  - photo, name in `row-title`, score line and two tag pills
  - want to try rows: "People get the …" and where it was saved from
  - been rows: "Your pick: …" with its verdict pill and how many visits

### Restaurant page
- **Hero**: photo with a dark scrim, occasion and vibe tags, `hero-name`, the big `score` with a star bar and rating count, then price and cuisine.
- **Actions**: Want to try and Been toggles (ink when on), then open hours and Directions.
- **What to order**: swipeable dish cards. Each has:
  - story bars across the top, one per photo
  - a white panel with rank, the dish name in `card-title`, the verdict pill and "% would reorder"
  - Tapping a card opens dish stories.
- **Note** card in `note`, a Good to know list (hours, call, menu), and a sticky violet "Rate what you ate" button.

### Dish stories
- Full-screen photos with progress bars and the dish name.
- Tap right for the next photo, left for the previous. Order: Vibes, then dishes by rank, at most 5 photos each.
- Each photo shows the dish verdict, "% would reorder", a `quote` from the person who posted it, and how they rated it. A pill row at the bottom jumps between dishes.
- The menu is a separate zoomable viewer, never a story.

### Logging a meal
1. Next-morning nudge.
2. "How was it?" sheet: recent spots suggested from photos and app activity.
3. Add your photos (pre-selected from that visit).
4. What did you get: dish chips, then a verdict for each.
5. Saved, with a share card for Instagram stories.

## Accessibility

- Text at least 4.5:1. `text-tertiary`, `map-label` and `star` are not text colors.
- Tap targets at least 44px.
- Pins carry the place name, cuisine and status in their label.
- Segmented controls and verdict pickers are radio groups.
- Never color alone: Open, Closed and every verdict are words.

## Building it (Expo)

Load Sora and Figtree with `expo-font` (both on Google Fonts, via `@expo-google-fonts`), export these tokens from one `theme.ts`, and build screens from tokens only. Use a native map with a custom style matching `map-*`. Build order: Map home, Restaurant page, Log a meal, then List, Search and Dish stories.


## Tokens

### Color

| Token | Value | Use |
|---|---|---|
| `bg` | `#FFFFFF` | Every screen and sheet. Foodi is white first. |
| `surface-muted` | `#F3F2F5` | Search field, segmented control track, close buttons, empty states, tag pills and the Mid / Skip verdict pills. |
| `line` | `#EEECF1` | Hairlines between list rows and around quiet cards. |
| `border` | `#D9D6DE` | 1.5px outline on unselected chips, toggles and the save button. |
| `ink` | `#1A1820` | All primary text, plus every selected state: selected chips, the active segment's count, a pressed Want to try or Been toggle, the selected map pin ring. |
| `text-secondary` | `#6E6B76` | Meta lines, counts, sources, "Closed" and helper copy. About 5.2:1 on white. |
| `text-tertiary` | `#8E8A95` | Inactive tab bar icons and decorative strokes only. About 3.4:1, so never body text. |
| `violet` | `#5A3DE0` | The one action color: primary buttons (Rate what you ate, Continue, Save), the + button, links, the to try pin badge, and the Elite verdict. If it is violet you can tap it, or it is Elite. |
| `violet-pressed` | `#4528C4` | Pressed state of violet; link hover. |
| `lilac` | `#ECE7FF` | Soft accents: the Solid verdict and the New badge. |
| `violet-ink` | `#3B23B0` | Text on lilac (Solid, New). About 8:1 on lilac. |
| `star` | `#E8B400` | The star glyph next to a restaurant score on white. Glyph only, never text. |
| `star-on-photo` | `#FFD84D` | The star bar on the restaurant hero, over the dark photo scrim. |
| `open` | `#1E8A4C` | The word "Open" and nothing else. Closed is text-secondary, not red. |
| `note` | `#FFF6D6` | Background of your own note on a restaurant page ("Spicy miso, extra spicy"). |
| `note-ink` | `#7A6A2E` | Meta text on the note card. |
| `scrim` | `rgba(14, 10, 30, 0.85)` | Bottom of the photo gradient on the restaurant hero and in dish stories, so white type reads on any photo. |
| `map-land` | `#F4F2EE` | Map base. |
| `map-road` | `#FFFFFF` | Map roads. |
| `map-park` | `#E1E9DA` | Parks and quads. |
| `map-water` | `#DCE5EE` | Water. |
| `map-label` | `#9A96A0` | Spaced uppercase neighborhood labels on the map. Decorative wayfinding, not content. |

### Type

- `display`: "Sora", system-ui, sans-serif
- `sans`: "Figtree", system-ui, -apple-system, sans-serif

| Style | Family | Size / line height | Weight | Use |
|---|---|---|---|---|
| `score` | display | 52px / 48px, tracking -1px | 700 | The restaurant score on its hero. The biggest thing on the page after the photo. |
| `hero-name` | display | 36px / 40px, tracking -0.5px | 800 | Restaurant name on its page, over the photo. |
| `screen-title` | display | 28px / 32px, tracking -0.3px | 800 | Top of a tab or a step in a flow (How was it?, Add your photos). |
| `section-title` | display | 22px / 28px, tracking -0.2px | 800 | Section headings on a restaurant page. |
| `card-title` | display | 18px / 23px | 800 | Dish names on dish cards; smaller section headings. |
| `row-title` | display | 17px / 22px | 800 | Restaurant names in list rows, search results and the map preview card. |
| `quote` | sans | 22px / 29px | 600 | What someone said about a dish, in dish stories, in quote marks. |
| `note` | sans | 18px / 25px | 600 | Your own note on a restaurant page. |
| `button` | sans | 17px / 22px | 600 | Full-width primary buttons. |
| `body` | sans | 15px / 21px | 400 | Paragraphs, subtitles under screen titles, inputs. |
| `body-strong` | sans | 15px / 21px | 600 | Toggles, tabs, list labels. |
| `chip` | sans | 14px / 18px | 600 | Filter chips, scope toggle, sort button. |
| `meta` | sans | 13px / 18px | 400 | The line under a name: score, status, cuisine, distance, source. |
| `badge` | sans | 12px / 16px | 700 | Verdict pills, counts, the New badge. |

### Spacing

| Token | Value | Use |
|---|---|---|
| `space-1` | `4px` | Gap between bars in a story progress row; tight icon gaps. |
| `space-2` | `8px` | Gaps between chips and pills. |
| `space-3` | `12px` | Gutter for floating controls over the map; gap between dish cards. |
| `space-4` | `16px` | Screen gutter on list and search screens; card padding. |
| `space-5` | `20px` | Screen gutter on the restaurant page and in flows. |
| `space-6` | `24px` | Space between sections. |

### Radius

| Token | Value | Use |
|---|---|---|
| `radius-thumb` | `14px` | Photo thumbnails in rows, photo grid tiles, small buttons. |
| `radius-panel` | `16px` | The white info panel inside a dish card; the note card. |
| `radius-card` | `20px` | Map preview card, empty states. |
| `radius-feature` | `24px` | Dish cards in What to order. |
| `radius-sheet` | `28px` | Top corners of bottom sheets. |
| `radius-pill` | `999px` | Every button, chip, toggle, badge, search field and the tab bar. |

### Shadow

| Token | Value | Use |
|---|---|---|
| `shadow-float` | `0 1px 2px rgba(26, 24, 32, 0.06), 0 4px 14px rgba(26, 24, 32, 0.08)` | Controls floating over the map; the selected segment in a segmented control. |
| `shadow-raised` | `0 8px 24px rgba(26, 24, 32, 0.12)` | Tab bar and the map preview card. |
| `shadow-cta` | `0 10px 24px rgba(90, 61, 224, 0.32)` | The violet + button only. |
