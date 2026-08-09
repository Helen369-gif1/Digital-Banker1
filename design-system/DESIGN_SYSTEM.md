# SoQuin Design System — Implementation Reference

**Source document:** `design-system/SoQuin_Design_System.pdf`
**Status of source document:** Foundation draft, extracted from existing Figma screens. Not a redesign. Component rules in the source are marked as requiring validation before implementation.
**Purpose of this file:** Translate the PDF into a reference usable during implementation of the existing codebase (`index.html`), and record the approved decisions on how documented tokens apply to this project.
**Revision:** v3 — approved decisions from §11 have been implemented in `index.html`. See §12 for the completed change log.

## How to read this document

- **[TOKEN]** — a value explicitly documented in the PDF as part of the color/type/spacing/radius/effect system.
- **[OBSERVED PATTERN]** — a recurring UI pattern the PDF describes (structure/behavior, not a mandate to unify unrelated elements that merely share a color or radius).
- **[PROJECT NOTE]** — this project's (`index.html`) current implementation status against a token or pattern.
- **[APPROVED]** — a decision that has been ruled on and is authorized for implementation, with the specific scope of that ruling.
- **[PRESERVED]** — an existing value that was reviewed and deliberately kept as-is, either because it serves a distinct visual purpose or because changing it would damage the existing visual hierarchy.

The governing rule for this revision: **bring the implementation into visual alignment with the Design System, not redesign it.** Existing content, layout structure, imagery, functionality, visual hierarchy, and responsive behavior are preserved unless clearly inconsistent with the Design System.

---

## 1. Color tokens

### Primary / brand blues [TOKEN]

| Role | Hex | Documented usage |
|---|---|---|
| Dark Navy | `#06357C` | Deep accent; active stepper icons |
| Primary Blue | `#144E9D` | Primary interactive color; active states; selected borders; stepper fills |
| Vivid Blue | `#0717DE` | Links, highlighted text, secondary interactive accent |
| Mid Blue | `#99C0FB` | Stepper connector lines; soft icon tints |

### Neutral / text [TOKEN]

| Role | Hex | Documented usage |
|---|---|---|
| Heading Text | `#263238` | Page titles and section headings; most-used text color |
| Body Text | `#4A4E53` | Descriptions and secondary labels |
| Muted Text | `#666666` | Placeholder text, input borders, tertiary labels |
| Dark Text Alt | `#1D1B20` / `#191C1F` | Some smaller labels |

### Surfaces / backgrounds [TOKEN]

| Role | Value | Documented usage |
|---|---|---|
| White | `#FFFFFF` | Cards and input fields |
| Frosted White | `#FFFFFF` @ 77% | Glassmorphic card overlays |
| Ice Blue | `#F8FDFF` / `#F8FBFE` | Subtle background tints |
| Light Blue | `#D7EDFD` | Info banners, highlight strips, sidebar active state |
| Pale Blue | `#E9F4FF` | Card borders and selected-row backgrounds |
| Light Lavender | `#F3F4FF` / `#E7E9FE` / `#EBEDFF` | Notification / AI message backgrounds |
| Light Gray | `#F6F5F8` | Page / viewport background |
| Warm Orange Tint | `#FEF0E5` | Warning / caution banner background |

### Color decision — resolved [APPROVED, decision 5]

Ruling: replace an existing color with its documented token when it is an obvious near-miss for the *same visual role*. Do not replace a color that serves a distinct purpose merely because it differs from a token.

**Approved substitutions** (same role, near-miss hex → documented token):

| Current hex | Used for (product UI only) | → Token |
|---|---|---|
| `#0e5fc4` | Primary interactive blue: tile icons, `view-all` link, row icons, row-action button, avatar text, card border | → `#144E9D` (Primary Blue) |
| `#1d2fd6`, `#1d24c9` | Logo mark, Gia-strip border/text, prepared-badge text | → `#0717DE` (Vivid Blue) |
| `#242833` | Text-color usages only: topbar `<h1>`, sidebar-footer name, row-title, transfer amount | → `#263238` (Heading Text) |
| `#525a6c`, `#3a4256` | Base body text, nav-item text | → `#4A4E53` (Body Text) |
| `#7a8296` | Topbar utility icons, subtext, tile subtext, transfer timestamp | → `#666666` (Muted Text) |
| `#fff2df` | `.badge.pending` background | → `#FEF0E5` (Warm Orange Tint) |
| `#8a5a10` | `.badge.pending` text | → `#E76702` (documented warning accent; DS has no dedicated warning *text* token, so this is the nearest documented warning-family color — lower confidence than the others, but same functional role) |

**Preserved — distinct purpose, not replaced:**

| Current hex | Used for | Why preserved |
|---|---|---|
| `#242833` on `.toast` background | Toast/snackbar surface | This is a dark scrim/surface fill, not text. The DS documents no dark surface token — using a "heading text" hex here would be coincidental, not a role match. |
| `#b9cdea` (`.tile` border) | Primary-tile border | Sits over a photographic background image; a paler documented token (e.g. `#E9F4FF`) may not read clearly against that background. Distinct functional purpose (contrast/visibility), not a simple wrong-hex case. |
| `#dde2ea` (`.tile-compact` border) | Secondary-tile border | Same reasoning as above. |

---

## 2. Typography

### Typeface [TOKEN]

| Font | Documented role | Evidence |
|---|---|---|
| Roboto | Primary typeface across the interface | ~95% of text |
| Inter | Secondary / occasional use | ~11 occurrences |

### Weight scale [TOKEN]

| Weight | Documented usage | Frequency |
|---|---|---|
| 500 — Medium | Default for most UI text | 132 |
| 400 — Regular | Supporting descriptions and input values | 43 |
| 700 — Bold | Page titles and emphasis headings | 17 |

### Size scale [TOKEN]

| Size | Documented role | Frequency |
|---|---|---|
| 32px | Page titles | 15 |
| 16px | Primary body, labels, buttons, navigation | 115 |
| 12px | Captions, tags, supporting information | 28 |
| 10px | Micro labels, stepper labels, badge text | 45 |

This is the PDF's originally observed scale (raw frequency data from the source screens). The scale actually implemented for this project's desktop interface is the four-tier system below (current: round 4), which reinterprets that raw data into usable hierarchy levels rather than reproducing it 1:1.

### Adopted desktop typography scale [PROJECT STANDARD — current, round 4]

- **32px — Main headings**
- **20px — Subheadings / important section headings / prominent card headings**
- **16px — DEFAULT AND MINIMUM size for meaningful interface content.** Card content, card titles that aren't a 20px prominent heading, navigation, descriptions, form labels, input text, values/information shown to the user, and any other text that communicates actual information all belong here at minimum. 14px is the exception, never the default for this kind of text.
- **14px — ONLY for genuinely small, secondary, or decorative UI: micro labels, compact status/badge text, and selected button labels where 16px would look disproportionate.** Not every button defaults to 14px — a primary/important action button uses 16px if 14px would make it look too small or under-weighted relative to its role.

10–13px are not used anywhere in the desktop interface for text that communicates information — see the exceptions table at the end of this subsection for the only elements smaller than 14px, and why they don't count as "readable content" in the first place.

This is the standard against which every desktop text element below is classified. See "Desktop typography scale — resolved [round 4]" for the full per-element mapping and rationale.

### Font-size decision — resolved [APPROVED, decision 3]

Ruling (round 1): do not mechanically remap every size to 32/16/12/10. Preserve a size when changing it would damage existing hierarchy. Align only where an existing size is clearly intended to be a standard, documented UI text role.

**Approved alignments** (small delta, unambiguous role match to a documented size):

| Element | Current | → Aligned to | Rationale |
|---|---|---|---|
| `.badge` | 11px | → 10px | DS names "badge text" explicitly as a 10px use case — exact role match |
| `.section-label` | 12.5px | → 12px | Uppercase supporting label = Caption role |
| `.topbar .search` (base/mobile) | 12.5px | → 12px | Supporting chrome text = Caption role |
| `.tile .subtext-tile` (base/mobile) | 11.5px | → 12px | Supporting/caption text under tile title |
| `.tile-compact .title` (base/mobile) | 11.5px | → 12px | Short supporting label, closer to Caption than Micro |
| `.transfer-row .when` | 11.5px | → 12px | Timestamp = Caption role |

### Desktop readability refinement — resolved [APPROVED, round 2, superseded by round 3 below]

Round 2 introduced a 16px floor for main readable text and a 14px allowance for buttons/secondary labels, with 10–12px reserved for "genuinely micro" elements. This has since been replaced by the four-tier desktop scale in round 3 — kept here only as history; see round 3 for the current rule.

### Desktop typography scale — round 3 [superseded by round 4 below]

Round 3 introduced the four-tier scale (32/20/16/14) but treated 14px as a default for most "secondary" text, including several elements that actually communicate meaningful information (tile descriptions, the sidebar name, the search label). Round 4 tightened this: 16px is now the strict floor for anything the user needs to read to understand content, and 14px is reserved only for genuinely small/decorative elements. Kept here as history.

### Desktop typography scale — resolved [APPROVED, round 4 — current]

Ruling: 16px is the default and minimum for any text that communicates actual information — card content, card titles that aren't a 20px prominent heading, navigation, descriptions, values, and form/input text. 14px is an exception for genuinely small, secondary, or decorative UI (micro labels, compact status/badge text, and *selected* button labels where 16px would look disproportionate) — not a default. Button labels may use either 14px or 16px depending on whether the button is a primary/important action.

Mobile typography is unaffected — every desktop-specific value lives in `@media (min-width:761px)` (the same breakpoint used for the desktop/mobile background-image switch); base rules keep their original mobile sizes.

**Classification applied (desktop only, via the 761px media query):**

| Element | Role | Base (mobile, unchanged) | Desktop (≥761px) |
|---|---|---|---|
| `.card h2` | Main heading — the card is the page's primary content | 23px | **32px** |
| `.topbar h1` | Subheading — persistent app-chrome page label | 19px | **20px** |
| `.nav-item` | Meaningful content — navigation | 14px | 16px |
| `.card .subtext` | Meaningful content — description | 13.5px | 16px |
| `.gia-strip .txt` | Meaningful content — informational banner copy | 13.5px | 16px |
| `.row .row-title` | Meaningful content — value (payee + amount) | 13.5px | 16px |
| `.transfer-row .who` | Meaningful content — value (payee name) | 13.5px | 16px |
| `.transfer-row .amt` | Meaningful content — value (amount) | 13.5px | 16px |
| `.sidebar-footer span` | Meaningful content — the signed-in account's name; round 3 wrongly treated this as a decorative chrome label, but it's information the user reads to confirm whose account this is | 13.5px | **16px** *(corrected in round 4)* |
| `.topbar .search` | Meaningful content — "input text" role per round 4's rule; round 3 called it decorative chrome and kept it at 14px, which round 4 overrides since the rule explicitly puts input-adjacent text at 16px minimum | 12px | **16px** *(corrected in round 4)* |
| `.tile .title` | Primary/important button — the four primary tiles (Send/Receive/Scan & Pay/Request) are this page's core actions, so they take 16px rather than the generic 14px button default | 14px | **16px** *(corrected in round 4)* |
| `.tile .subtext-tile` | Meaningful content — describes what each primary action tile does; round 3 kept this at 14px alongside its title, but this is real descriptive card content the user reads before tapping, not a decorative caption | 12px | **16px** *(corrected in round 4)* |
| `.tile-compact .title` | Selected button label kept at 14px — these four secondary tiles (Deposit/Withdraw/Convert/History) are deliberately de-emphasized versus the primary tiles (smaller icon, no description, tighter padding); keeping their label at 14px preserves that intentional two-tier button hierarchy rather than making every button the same weight | 12px | 14px *(kept — see rationale)* |
| `.row-action` | Selected button label kept at 14px — a compact inline "Review" pill button inside a dense list row, visually and functionally secondary to the row's own 16px content it's attached to | 12px | 14px *(kept — see rationale)* |
| `.section-label` | Small/decorative label kept at 14px — an uppercase, letter-spaced eyebrow/kicker heading. Its heading role is carried by the caps+tracking+bold treatment, not by size; enlarging it to 16px (equal to body content) or 20px (a full subheading) would fight that established convention and look disproportionate in this dense card | 12px | 14px *(kept — see rationale)* |
| `.section-label .view-all` | Small label kept at 14px, paired with the above | 12.5px | 14px *(kept)* |
| `.transfer-row .when` | Small/decorative label kept at 14px — a timestamp, classic secondary metadata | 12px | 14px *(kept)* |
| `.badge` | Compact status/badge text — explicitly named as an acceptable 14px case | 10px | 14px *(kept)* |
| `.toast` | Small/decorative label kept at 14px — transient snackbar feedback, not persistent content the user needs to study | 13px | 14px *(kept)* |

**Exceptions — intentionally kept outside the four-tier scale entirely (not "readable content"):**

| Element | Size | Why |
|---|---|---|
| `.avatar-sm`, `.sidebar .logo .mark` | 11px | Icon-equivalent glyphs — fixed-size circular/square containers showing a 2-letter monogram, read as an icon rather than as prose. Forcing these into the 14px (or 16px) floor would overflow their small fixed containers for no readability benefit. |
| `.sidebar .logo` | 16px | Brand label; already sits exactly on the minimum readable-content tier, no change needed. |

**No real form/input elements exist in this prototype** (no `<input>` fields) — `.topbar .search` is the closest analog. Round 4 now treats it as input-adjacent text and sizes it at 16px accordingly, reversing round 3's "decorative chrome" classification.

### Font-weight decision — resolved [APPROVED, decision 4]

Ruling: do not flatten all `600` weights to the documented 400/500/700. Keep 600 where it is visually appropriate (it currently sits between the DS's Medium default and Bold titles as an intentional mid-emphasis weight). Use 400/500/700 for any new or clearly-standardized text style going forward.

**No existing `font-weight: 600` usages are being changed.** These are retained as a project-specific mid-emphasis weight, not part of the DS's documented scale but kept intentionally:

- `.nav-item.active` (active nav emphasis)
- `.badge` (status badge text)
- `.row-action` (button label)
- `.row .row-title`, `.transfer-row .who` (primary list content)
- `.tile-compact .title` (compact tile label)

---

## 3. Spacing

### Spacing scale [TOKEN]

| Value | Frequency | Typical use |
|---|---|---|
| 4px | 57 | Tight inline elements |
| 8px | 190 | Standard compact spacing |
| 10px | 200 | Most-used gap; list items and form rows |
| 12px | 147 | Card internal content spacing |
| 16px | 35 | Section separators and medium gaps |
| 24px | 112 | Major content blocks |
| 32px | 33 | Large section separation |
| 40px | 43 | Top-level section gaps |

10px remains a fully valid, frequently-used documented value — not an exception to "fix."

### Spacing decision — resolved [APPROVED, decision 8]

Ruling: do not globally round off-scale spacing. Preserve component-specific spacing that appears intentional. Align only where a value clearly corresponds to a documented semantic spacing role (small delta, unambiguous fit).

**Approved alignments:**

| Element | Current | → Aligned to | Rationale |
|---|---|---|---|
| `.sidebar` vertical padding | 22px | → 24px | Nearest token (Δ2px); role = section-level padding |
| `.gia-strip` bottom margin | 22px | → 24px | Same reasoning |
| `.topbar` padding | `18px 30px` | → `16px 32px` | Both within Δ2px of documented tokens; topbar padding is generic section-level chrome spacing |
| `.nav-item` vertical padding | 9px | → 8px | Δ1px; matches "standard compact spacing" role |
| `.section` bottom margin | 26px | → 24px | Δ2px; "major content blocks" role |

**Preserved — intentional / structurally ambiguous, not changed:**

| Element | Current | Why preserved |
|---|---|---|
| `.card` padding | `30px 32px 26px` | Asymmetric, load-bearing padding for the page's single main card; no single documented padding pattern maps cleanly onto all three values without a larger, riskier restructure |
| `.content-area` padding | `32px 24px 70px` | 70px bottom padding is a deliberate scroll-clearance value, not a spacing-scale candidate |
| `.row`, `.transfer-row` padding | `12px 2px`, `11px 2px` | Tight list-row spacing; 2px is a hairline alignment value, not a scale candidate; 11px is a borderline case left untouched pending further review |
| `.tile`, `.tile-compact` padding/gaps | various (14px, 13px, 7px, 10px, 8px, 6px) | Dense grid-tile spacing; several values are already on-scale (8, 10, 12); the remainder are small internal offsets tied to the tile's specific layout and are left as project-specific for now |

---

## 4. Border radius

### Radius scale [TOKEN]

| Radius | Frequency | Documented usage |
|---|---|---|
| 12px | 363 | Dominant radius: cards, containers, inputs, modals, buttons |
| 10px | 34 | Secondary containers |
| 8px | 35 | Smaller cards, tags, inner elements |
| 6px | 11 | Compact elements |
| 5px | 10 | Small chips / badges |
| 80–100px | 11 each | Avatars and circular profile images |
| 9999px | 2 | Fully rounded pill / stepper shapes |

### Card radius decision — resolved [APPROVED, decision 1]

Ruling: use 12px as the standard card/container radius. Correct the current 18px `.card` radius to 12px. Do not change unrelated decorative elements just because they have a different radius.

**Approved change:** `.card` border-radius: `18px` → `12px` (this is the only element using 18px in the project).

**Explicitly out of scope for this decision** (different radii, not touched here — not "the 18px card," and not covered by this ruling):
- `.tile` (10px) — already matches the documented "secondary containers" token exactly; no change needed.
- `.tile-compact` (9px), `.row-action` (7px) — off-scale, but were not part of the approved card-radius ruling; left as recorded discrepancies for a future decision.

### Badge radius decision — resolved [APPROVED, decision 2]

Ruling: do not apply one radius to every badge. Use 5–8px for compact tags/badges, and 9999px only where the component is intentionally a pill/full-round shape, chosen by actual structure/role.

**Assessment of the only badge component in this project** (`.badge`, used by `.badge.prepared` / `.badge.pending`):
- Current: `padding: 2px 9px; border-radius: 20px;` on ~11px text — at this height, 20px already exceeds half the element's height, so it already renders as a fully-rounded pill, not a squared-corner tag.
- Structure/role: a small rounded status pill ("Prepared by Gia", "Pending approval") — visually and functionally a pill badge, not a boxy tag.

**Decision:** treat `.badge` as the pill/full-round case → **border-radius: `20px` → `9999px`** (a token correction, not a visual redesign — the shape stays the same since the element is already short enough for 20px to render fully round; 9999px simply makes that intent explicit and robust to future size changes).

No component in the current project matches the "compact 5–8px tag" case (there are no boxy/square-cornered tags today), so that token isn't applied anywhere yet — it remains documented here for future components that fit that structure.

---

## 5. Borders

### Border / stroke tokens [TOKEN]

| Color | Weight | Frequency | Documented usage |
|---|---|---|---|
| `#666666` | 1px | 110 | Default input borders |
| `#144E9D` | 1px | 63 | Active / selected borders |
| `#C8C8C8` | 1px | 38 | Subtle card / divider borders |
| `#FFFFFF` | 1px | 38 | White borders on dark contexts |
| `#E9F4FF` | 1px | 18 | Light blue card borders |
| `#06357C` | 1px | 24 | Dark blue accents |
| `#1E1E1E` | 2px | 33 | Icon strokes |
| `#0717DE` | 1px | 9 | Active links / highlights |
| `#E76702` | 1px | 4 | Warning / orange accents |

### Project note — borders [PROJECT NOTE]

`.card` border color aligns to `#144E9D` per the approved color decision (§1), but its 1.5px weight (vs. the documented 1px) was not part of any approved decision and is left unchanged. `.tile` / `.tile-compact` border colors (`#b9cdea`, `#dde2ea`) are preserved per §1's distinct-purpose reasoning.

---

## 6. Shadows and effects

### Effect tokens [TOKEN]

| Effect | Observed value | Documented usage |
|---|---|---|
| Blue card shadow | `0 4px 4px #0D7BD5 @ 31%` | Primary card shadow; 85 elements |
| Blue glow | `0 0 7px #165EF7 @ 25%` | Ambient glow around focused/elevated elements; 45 occurrences |
| Neutral shadow | `0 4px 4px #000000 @ 25%` | Rare; 1 occurrence |
| Background blur | 19px | Frosted-glass panels; 56 occurrences |
| Heavy background blur | 54px | Outer background elements; 29 occurrences |

### Shadows/glass decision — resolved [APPROVED, decision 6]

Ruling: introduce the documented blue card shadow, blue glow, and glass/blur effects where the DS identifies them as part of the matching pattern, applied only to components whose structure matches that pattern — not indiscriminately.

**Approved additions:**

| Component | Matching pattern | Effect to add |
|---|---|---|
| `.card` | Content Card | Blue card shadow: `box-shadow: 0 4px 4px rgba(13,123,213,0.31)` |
| `.sidebar` | Glass Sidebar | 19px background blur (`backdrop-filter: blur(19px)`) + a translucent blue-tinted fill (Frosted White `rgba(255,255,255,0.77)` as the base, per the documented "glassmorphic card overlay" surface value, since the DS does not give a separate literal hex for the sidebar's "blue gradient tint") |

**Not applied:**
- Blue glow — the DS ties this to focused/elevated *interactive* states. The current static card/sidebar are not documented as using glow, and adding it would mean inventing a new interaction state (e.g. hover/focus glow) that doesn't exist in the project today. Left out per "do not add effects indiscriminately."
- `.topbar` — not documented as a Glass Sidebar-type surface; no blur/tint added.
- Heavy 54px background blur — documented as being for "outer background elements," which in this project's context is the full-page background image itself; the DS gives no basis for applying it to any in-scope UI component.

**Visibility note:** adding a background blur + translucent fill to `.sidebar` is the most visually noticeable change in this revision — today the sidebar is fully transparent over the page background image. This is being called out explicitly ahead of implementation since it changes what the sidebar looks like, even though it brings it in line with the documented Glass Sidebar pattern.

---

## 7. Repeated UI patterns

Unchanged from the source document — documented for reference; see the PDF for full detail. Reproduced here for the patterns relevant to this project's current components:

| Pattern | Core specification | Suggested states |
|---|---|---|
| Content Card | White @ 77% overlay; 12px radius; blue-tinted shadow; 12–24px padding | Default / Selected / Elevated / Disabled |
| Glass Sidebar | 19px background blur; blue gradient tint; icon + navigation item structure | Default / Active / Hover / Disabled |
| Tag / Badge | Small rounded chip; 5–8px radius; 6×4px padding; contextual colored background | Type variants |
| Primary CTA | `#144E9D` fill; white text; 12px radius; 12×24px padding | Default / Hover / Pressed / Disabled |
| Secondary / Ghost | White fill; 1px `#666666` or `#144E9D` border; 12px radius | Default / Hover / Pressed / Disabled |
| Info / AI Banner | Light lavender background; rounded container; sparkle / AI icon | Default / With action |

Patterns with no corresponding component in this project (Stepper, Selection Card, Verification Code, Profile Block, Warning Banner) are omitted here — see the PDF if/when those are built.

---

## 8. Component specifications (post-decision)

| Project component | Pattern | Radius | Color | Effects | Status after this revision |
|---|---|---|---|---|---|
| `.card` | Content Card | 12px *(approved change from 18px)* | Border → `#144E9D` *(approved)* | Blue card shadow *(approved addition)* | To be implemented |
| `.sidebar` | Glass Sidebar | n/a | n/a | 19px blur + frosted tint *(approved addition)* | To be implemented |
| `.tile` | — (informal) | 10px, unchanged (already on-token) | Border `#b9cdea` preserved | none | No change |
| `.tile-compact` | — (informal) | 9px, unchanged (out of scope) | Border `#dde2ea` preserved | none | No change |
| `.gia-strip` | Info / AI Banner | 10px, unchanged (already on-token) | Border/text → `#0717DE` *(approved)* | none | Color only |
| `.badge.prepared` | Tag / Badge | → 9999px *(approved)* | Text → `#0717DE` *(approved)*, bg unchanged (`#f1f1ff` preserved, already lavender-family) | none | Radius + text color |
| `.badge.pending` | Tag / Badge | → 9999px *(approved)* | bg → `#FEF0E5`, text → `#E76702` *(approved)* | none | Radius + color |
| `.row-action` | Secondary/Ghost CTA (informal) | 7px, unchanged (out of scope) | Color/border → `#144E9D` *(approved)* | none | Color only |

---

## 9. Responsive / mobile-desktop guidance

Unchanged from the prior revision — the PDF does not establish a full mobile-vs-desktop token map, so no new responsive rules are introduced here. `index.html`'s existing two breakpoints (760px background swap, 640px tile layout) are preserved as-is; none of the approved decisions in this revision alter responsive behavior.

---

## 10. Known project discrepancies

| # | Discrepancy | Status |
|---|---|---|
| 1 | Font family: Roboto listed after system fonts | Open — not part of the approved decisions in this revision |
| 2 | Off-scale font sizes | Partially resolved — see §2 (some aligned, most preserved) |
| 3 | `font-weight: 600` usage | Resolved — kept intentionally, see §2 |
| 4 | Near-miss color hex values | Resolved — see §1 (some substituted, some preserved) |
| 5 | `.card` border-radius 18px | Resolved — corrected to 12px, see §4 |
| 6 | `.badge` border-radius 20px | Resolved — corrected to 9999px, see §4 |
| 7 | Missing shadow/elevation system | Resolved — blue card shadow + sidebar glass added, see §6 |
| 8 | Off-scale spacing values | Partially resolved — see §3 (some aligned, most preserved) |
| 9 | Background images (full-bleed illustrative imagery) | Closed — kept unchanged per explicit instruction; not a discrepancy to act on |
| 10 | `.proto-bar` (prototype-only chrome) | Out of scope — not product UI |
| 11 | `.tile-compact` (9px) / `.row-action` (7px) radius | Open — off-scale but not covered by the approved card-radius ruling |
| 12 | `.card` border weight (1.5px vs. documented 1px) | Open — not covered by any approved decision |
| 13 | `.tile` / `.tile-compact` border colors (`#b9cdea`, `#dde2ea`) | Open — preserved as possibly-intentional (background contrast), not confirmed either way |
| 14 | `.row`, `.transfer-row` padding (2px, 11px) | Open — borderline, left untouched |

---

## 11. Decisions — resolved

All eight decisions below were reviewed and ruled on. Each is reflected in the corresponding section above.

1. **Card radius:** use 12px as the standard card/container radius; correct `.card` from 18px → 12px only. ✅ Resolved — §4.
2. **Badge radius:** no single radius for all badges; choose 5–8px (compact tag) vs. 9999px (pill) by structure. `.badge` assessed as a pill → 9999px. ✅ Resolved — §4.
3. **Font size:** no mechanical remap to 32/16/12/10; preserve where changing would damage hierarchy; align only clear standard-role cases. ✅ Resolved — §2.
4. **Font weight:** keep existing 600 usages; use 400/500/700 only for new/standardized text. ✅ Resolved — §2.
5. **Color tokens:** replace obvious near-miss colors with the same visual role; preserve colors with a distinct purpose. ✅ Resolved — §1.
6. **Shadows/glass:** add documented blue card shadow and glass/blur effects to matching components only (`.card`, `.sidebar`); no indiscriminate application. ✅ Resolved — §6.
7. **Background images:** keep `desktop_background.png` / `mobile_background.png` unchanged; not replaced with flat surface colors. ✅ Resolved — no action needed, closed.
8. **Spacing:** no global rounding; preserve intentional component spacing; align only clear semantic-role matches; 10px remains valid. ✅ Resolved — §3.

---

## 12. Implementation status — completed

All eight approved decisions (§11) have been applied to `index.html`. No HTML structure, JavaScript, imagery, or background assets were touched — only CSS property values within the existing `<style>` block.

| Area | Applied |
|---|---|
| Radius | `.card` 18px→12px; `.badge` 20px→9999px |
| Color | All 7 approved substitutions applied to product-UI usages only; `.toast` and `.proto-bar` left untouched |
| Typography | 6 approved size alignments applied; all preserved sizes and all `font-weight:600` usages left untouched |
| Card shadow | `box-shadow:0 4px 4px rgba(13,123,213,0.31)` added to `.card` |
| Glassmorphism | `.sidebar` given `background:rgba(255,255,255,0.77)` + `backdrop-filter:blur(19px)` (with `-webkit-` prefix for Safari) |
| Spacing | 5 approved adjustments applied; all other spacing left untouched |

Verified: CSS brace balance (65/65) and JS syntax both check out after the edit; `git diff` confirms only `index.html` changed and every hunk corresponds to an approved item.

**Note:** typography has since gone through three further rounds of refinement (see §2 — rounds 2, 3, and the current round 4). The "6 approved size alignments" line above reflects only this first pass; §2's "round 4" table is the authoritative, current desktop typography state.

---

*This document reflects `design-system/SoQuin_Design_System.pdf` and `index.html` as of implementation on 2026-08-09.*
