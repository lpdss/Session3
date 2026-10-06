---
title: "DESIGN: HireFlow"
status: draft
created: 2026-10-06
updated: 2026-10-06
sources:
  - '{planning_artifacts}/ux-designs/ux-Session3-2026-10-06/.memlog.md'
name: HireFlow
description: Public careers site (Open Roles + Job Application). Closed five-colour, four-space, one-radius token set; hierarchy from weight and colour, not size.
colors:
  surface: '#ffffff'
  ink: '#1a1d21'
  muted: '#6b7280'
  accent: '#2563eb'
  danger: '#dc2626'
typography:
  # One family, two sizes. Sizes reference spacing tokens; no size tokens exist.
  # Line-heights are unitless multipliers (not tokens).
  title:
    fontFamily: 'system-ui, sans-serif'
    fontSize: '{spacing.4}'
    fontWeight: '700'
    lineHeight: '1.25'
  heading:
    fontFamily: 'system-ui, sans-serif'
    fontSize: '{spacing.3}'
    fontWeight: '700'
    lineHeight: '1.5'
  label:
    fontFamily: 'system-ui, sans-serif'
    fontSize: '{spacing.3}'
    fontWeight: '600'
    lineHeight: '1.5'
  body:
    fontFamily: 'system-ui, sans-serif'
    fontSize: '{spacing.3}'
    fontWeight: '400'
    lineHeight: '1.5'
  control:
    # Buttons and single-line inputs. 1.75 x 16px = 28px line box; + 2 x {spacing.2} padding = 44px target.
    fontFamily: 'system-ui, sans-serif'
    fontSize: '{spacing.3}'
    fontWeight: '600'
    lineHeight: '1.75'
rounded:
  DEFAULT: 6px
spacing:
  '1': 4px
  '2': 8px
  '3': 16px
  '4': 32px
components:
  button-primary:
    background: '{colors.accent}'
    foreground: '{colors.surface}'
    radius: '{rounded.DEFAULT}'
    paddingY: '{spacing.2}'
    paddingX: '{spacing.3}'
    typography: '{typography.control}'
  button-secondary:
    background: '{colors.surface}'
    foreground: '{colors.accent}'
    borderColor: '{colors.accent}'
    radius: '{rounded.DEFAULT}'
    paddingY: '{spacing.2}'
    paddingX: '{spacing.3}'
    typography: '{typography.control}'
  link:
    foreground: '{colors.accent}'
    typography: '{typography.body}'
  focus-ring:
    outlineColor: '{colors.accent}'
    outlineOffset: '{spacing.1}'
  search-field:
    background: '{colors.surface}'
    foreground: '{colors.ink}'
    borderColor: '{colors.muted}'
    radius: '{rounded.DEFAULT}'
    paddingY: '{spacing.2}'
    paddingX: '{spacing.3}'
    typography: '{typography.control}'
  text-field:
    background: '{colors.surface}'
    foreground: '{colors.ink}'
    borderColor: '{colors.muted}'
    radius: '{rounded.DEFAULT}'
    paddingY: '{spacing.2}'
    paddingX: '{spacing.3}'
    typography: '{typography.control}'
    labelTypography: '{typography.label}'
    labelGap: '{spacing.1}'
  text-field-error:
    borderColor: '{colors.danger}'
    messageColor: '{colors.danger}'
  text-area:
    background: '{colors.surface}'
    foreground: '{colors.ink}'
    borderColor: '{colors.muted}'
    radius: '{rounded.DEFAULT}'
    padding: '{spacing.2}'
    typography: '{typography.body}'
  field-error:
    foreground: '{colors.danger}'
    typography: '{typography.body}'
    iconGap: '{spacing.2}'
  cv-upload:
    background: '{colors.surface}'
    borderColor: '{colors.muted}'
    borderColorActive: '{colors.accent}'
    borderColorError: '{colors.danger}'
    radius: '{rounded.DEFAULT}'
    padding: '{spacing.3}'
  upload-progress:
    trackBorderColor: '{colors.muted}'
    fill: '{colors.accent}'
    height: '{spacing.2}'
    radius: '{rounded.DEFAULT}'
  job-row:
    background: '{colors.surface}'
    borderColor: '{colors.muted}'
    borderColorHover: '{colors.accent}'
    radius: '{rounded.DEFAULT}'
    padding: '{spacing.3}'
    titleTypography: '{typography.label}'
    titleColor: '{colors.accent}'
    metaColor: '{colors.muted}'
  job-header:
    titleTypography: '{typography.title}'
    titleColor: '{colors.ink}'
    metaColor: '{colors.muted}'
    gap: '{spacing.2}'
  skeleton-row:
    background: '{colors.surface}'
    borderColor: '{colors.muted}'
    radius: '{rounded.DEFAULT}'
    padding: '{spacing.3}'
  error-summary:
    background: '{colors.surface}'
    borderColor: '{colors.danger}'
    ruleWidth: '{spacing.1}'
    headingColor: '{colors.ink}'
    linkColor: '{colors.danger}'
    radius: '{rounded.DEFAULT}'
    padding: '{spacing.3}'
  alert-banner:
    background: '{colors.surface}'
    borderColor: '{colors.danger}'
    ruleWidth: '{spacing.1}'
    iconColor: '{colors.danger}'
    foreground: '{colors.ink}'
    radius: '{rounded.DEFAULT}'
    padding: '{spacing.3}'
  notice:
    background: '{colors.surface}'
    borderColor: '{colors.muted}'
    foreground: '{colors.ink}'
    radius: '{rounded.DEFAULT}'
    padding: '{spacing.3}'
  empty-state:
    headingTypography: '{typography.heading}'
    headingColor: '{colors.ink}'
    bodyColor: '{colors.muted}'
    paddingY: '{spacing.4}'
  confirmation-panel:
    background: '{colors.surface}'
    borderColor: '{colors.accent}'
    ruleWidth: '{spacing.1}'
    iconColor: '{colors.accent}'
    headingTypography: '{typography.heading}'
    radius: '{rounded.DEFAULT}'
    padding: '{spacing.4}'
---

## Brand & Style

HireFlow is a public careers site. A candidate arrives with one question (is there a role for me?) and leaves having either applied or knowing exactly why not. The visual posture is plain and trustworthy: white canvas, near-black text, one blue for "act here", one red for "fix this". No illustration, no gradient, no shadow. The restraint comes from the token set, and the product is better for it. A careers page that looks like a form you can trust gets finished.

**Token override (user choice, 2026-10-06).** This token set replaces the HireFlow style sheet described in the repo `CLAUDE.md` (Inter, `#1D4ED8` primary, `#B91C1C` error, the background, border, tint and hover tokens, and the 28px mobile title). The user was asked and chose their own closed set. Where the two disagree, this file wins for this spec. Recorded in `.memlog.md` as an override.

The set is **closed**: 5 colours, 4 spacing steps, 1 radius, 1 font family. Nothing gets added at build time. Where the set leaves a gap, this file says so (see Do's and Don'ts) rather than filling it.

## Colors

| Token | Hex | Contrast on `{colors.surface}` | Use | Never |
|---|---|---|---|---|
| `{colors.surface}` | `#ffffff` | n/a | Page canvas, cards, inputs, banners, and text on accent | A second "background" tone. There isn't one. |
| `{colors.ink}` | `#1a1d21` | 16.9:1 (computed) | Headings, body, labels, input text | n/a |
| `{colors.muted}` | `#6b7280` | 4.8:1 | Secondary copy, metadata, helper text, **all 1px borders** (inputs, rows, skeletons) | Disabled styling (there is none; locked fields go `readonly`), placeholder-as-label |
| `{colors.accent}` | `#2563eb` | 5.2:1 (surface on accent 5.2:1) | Primary button, links, focus ring, hover borders, upload progress, success marker | Decoration, large fills beyond the primary button |
| `{colors.danger}` | `#dc2626` | 4.8:1 | Error text, error borders, error icons, error-summary and alert-banner rule | Destructive buttons (there are none), large fills |

Pairs checked for non-text and link distinction: accent vs ink 3.3:1 and danger vs ink 3.5:1 (both clear the 3:1 non-text bar; computed, not in the memlog). Inline links are still underlined, so colour is never the only cue.

**No success colour.** Success uses `{colors.accent}` plus a check icon plus the words. Green is not available and is not needed.

## Typography

One family: `system-ui, sans-serif`. Two sizes only, both borrowed from spacing:

| Role | Size | Weight | Line-height | Colour | Where |
|---|---|---|---|---|---|
| `{typography.title}` | `{spacing.4}` (32px) | 700 | 1.25 | ink | One per page: "Open roles" or the job title. The success confirmation heading uses `heading`, so the job title stays the page title. |
| `{typography.heading}` | `{spacing.3}` (16px) | 700 | 1.5 | ink | Section headings (About the role, Apply for this role), empty-state and confirmation headings |
| `{typography.label}` | `{spacing.3}` (16px) | 600 | 1.5 | ink | Form labels, job-row titles (accent), error-summary heading |
| `{typography.body}` | `{spacing.3}` (16px) | 400 | 1.5 | ink or muted | Body copy (ink); metadata, helper text, "(optional)" (muted) |
| `{typography.control}` | `{spacing.3}` (16px) | 600 (buttons) / 400 (inputs) | 1.75 | per component | Buttons and single-line inputs; the taller line box makes the 44px target |

Hierarchy below the title is weight (700 > 600 > 400) and colour (ink > muted). Spacing above a heading (`{spacing.4}`) does the rest. The title stays 32px at every width and wraps; it does not drop to 28px (that size does not exist here).

## Layout & Spacing

| Token | Value | Use |
|---|---|---|
| `{spacing.1}` | 4px | Label-to-field gap, focus-ring offset, error/alert left rule |
| `{spacing.2}` | 8px | Control vertical padding, icon-to-text gap, meta-line gaps, progress-bar height |
| `{spacing.3}` | 16px | Control horizontal padding, row padding, gap between fields' groups, page gutter below 768px |
| `{spacing.4}` | 32px | Between sections, above headings, page gutter at 768px and up, empty-state padding |

**Composed values (not tokens).**

- **Control height = 44px**: `{spacing.2}` + (16px × 1.75 line-height) + `{spacing.2}` = 8 + 28 + 8. Bordered controls (inputs, secondary buttons) add 1px top and bottom, giving 46px. Both exceed the minimum. This is how the 44px minimum target is met on every viewport. There is no separate desktop 40px or touch 48px size.
- **Between fields** = `{spacing.4}` (label + control + message forms one group; groups separated by 32px). `{spacing.3}` is too tight once a two-line error appears. [ASSUMPTION]
- **Content column**: single column, max-width capped by reading measure (about 70 characters of body text) and centred. Expressed in `ch`, not px, because no layout-width token exists. [ASSUMPTION] See Open Questions.
- **Breakpoints** are layout thresholds, not tokens: 768px (gutter change) and a 360px floor. Behaviour lives in EXPERIENCE.md Responsive & Platform.

## Elevation & Depth

None. No shadow token exists and none is used. Separation comes from a 1px `{colors.muted}` border and from `{spacing.4}` whitespace. Overlays and sticky elements are avoided, so nothing needs to float.

## Shapes

One radius, `{rounded.DEFAULT}` (6px), on every bordered box: buttons, inputs, text area, CV upload zone, job rows, skeleton rows, banners, confirmation panel, and the progress track. No pills, no circles except icons. The focus ring follows the element's radius.

## Components

Structural constants used below (sanctioned by the memlog, not tokens): borders are **1px**; the focus ring is **2px** solid `{colors.accent}` at `{spacing.1}` offset. "Rule" means a `{spacing.1}`-wide left border on a banner.

| Component | Anatomy and visual spec | States (visual only) |
|---|---|---|
| Button, primary (`button-primary`) | `{colors.accent}` fill, `{colors.surface}` label in `{typography.control}` 600, `{rounded.DEFAULT}`, padding `{spacing.2}` `{spacing.3}`. Optional leading icon, `{spacing.2}` gap. | Hover: label underlines. Focus: focus ring. Busy: spinner icon + changed label, colours unchanged. Disabled: none. While busy it stays full colour and the label carries the state. |
| Button, secondary (`button-secondary`) | `{colors.surface}` fill, 1px `{colors.accent}` border, `{colors.accent}` label. Same size as primary. Used for "Clear search", "Try again", "Remove". | Hover: label underlines. Focus: focus ring. |
| Link (`link`) | `{colors.accent}` `{typography.body}`. Inline links always underlined. Standalone links (back link, "See open roles") underlined on hover only. | Hover: underline. Focus: focus ring. |
| Focus ring (`focus-ring`) | 2px `{colors.accent}` outline, `{spacing.1}` offset, follows radius. Applies to every focusable element including job rows and the CV upload zone. | `:focus-visible` only. |
| Search field (`search-field`) | Visible label above (`{typography.label}`), leading search icon in `{colors.muted}`, 1px `{colors.muted}` border, full width of the content column. Clear (×) button inside at the right once text is present. | Hover: border to `{colors.accent}`. Focus: focus ring. |
| Text field (`text-field`) | Label (`{typography.label}` ink) + "(optional)" suffix in `{typography.body}` `{colors.muted}`, `{spacing.1}` gap, then 1px `{colors.muted}` input, then optional helper text in muted. | Hover: border to accent. Focus: focus ring. Error: `text-field-error` (1px `{colors.danger}` border + `field-error` below). Locked: `readonly`, visuals unchanged; the submit button's busy label signals the lock. |
| Text area (`text-area`) | As text field; `{typography.body}`, min 6 lines, vertical resize only. Character count below, right-aligned, muted. | As text field. |
| Field error (`field-error`) | Danger icon (16px = `{spacing.3}`) + message in `{colors.danger}` `{typography.body}`, `{spacing.2}` gap, sits `{spacing.1}` below the control. Text, icon and border together, never colour alone. | n/a |
| CV upload (`cv-upload`) | Box with 1px **dashed** `{colors.muted}` border, `{spacing.3}` padding, upload icon, line "Drag your CV here, or" + `button-secondary` "Choose file", helper "PDF or Word (.docx), up to 5 MB" in muted. | Drag-over: border becomes 2px solid `{colors.accent}`. Uploading: filename + `upload-progress` + percent. Uploaded: solid 1px muted border, file icon, filename (ink, 600), size (muted), "Remove" link. Error: 1px solid `{colors.danger}` + `field-error`. |
| Upload progress (`upload-progress`) | Track: 1px `{colors.muted}` border, `{spacing.2}` tall, `{rounded.DEFAULT}`. Fill: `{colors.accent}`. Percent in muted body text beside it. | Indeterminate when size unknown: static full-width fill with "Uploading…" text (no animation under reduced motion). |
| Job row (`job-row`) | Whole-row link. 1px `{colors.muted}` border, `{rounded.DEFAULT}`, `{spacing.3}` padding. Line 1: job title in `{typography.label}` `{colors.accent}`. Line 2: company · location · work type · posted date in `{typography.body}` `{colors.muted}`, separated by " · ". Rows stacked with `{spacing.2}` gap. | Hover: border to `{colors.accent}`, title underlines. Focus: focus ring around the row. |
| Job header (`job-header`) | Back link, then title in `{typography.title}` ink, then company and meta line in muted body, then `button-primary` "Apply now". `{spacing.2}` between lines, `{spacing.4}` below. | n/a |
| Skeleton row (`skeleton-row`) | Same box as `job-row`, 1px `{colors.muted}` border, containing two empty bordered bars (title width about half, meta about a third). No fill (no tint token). | Static. No shimmer. |
| Error summary (`error-summary`) | `{colors.surface}` box, 1px `{colors.danger}` border with `{spacing.1}` left rule, danger icon, heading in `{typography.label}` ink, then a list of links in `{colors.danger}`, one per error, each underlined. | Focusable container (focus ring when focused programmatically). |
| Alert banner (`alert-banner`) | As error summary but for system failures: danger icon, heading (`{typography.label}` ink), one line of body in ink, one `button-secondary` action. | n/a |
| Notice (`notice`) | Neutral info: 1px `{colors.muted}` border, info icon in muted, ink body. Used for slow network and offline-recovered messages. | n/a |
| Empty state (`empty-state`) | Centred in the list area, `{spacing.4}` vertical padding. Heading in `{typography.heading}` ink, one line of body in muted, one action (`button-secondary` or `link`). No illustration. | n/a |
| Confirmation panel (`confirmation-panel`) | Replaces the form. 1px `{colors.accent}` border with `{spacing.1}` left rule, check icon in `{colors.accent}`, heading in `{typography.heading}`, body in ink, ordered "What happens next" list, then a `link`. `{spacing.4}` padding. | n/a |

## Do's and Don'ts

| Do | Don't |
|---|---|
| Use only the 5 colours, 4 spacing steps, 1 radius and 1 family above | Add a token, even "just a light grey". Raise it in Open Questions instead. |
| Build hierarchy with weight (700/600/400) and colour (ink/muted) | Introduce 14, 20, 24 or 28px text |
| Separate with 1px `{colors.muted}` borders and `{spacing.4}` whitespace | Use shadows, tinted backgrounds or a second canvas colour |
| Show hover as an underline or a muted-to-accent border | Darken or lighten the accent on hover (no hover token) |
| Show errors with danger border + danger text + icon together | Rely on red alone, or fill a field red (no error tint) |
| Reach 44px targets through `{spacing.2}` padding + 1.75 line-height | Hard-code 40px, 44px, 48px or 24px as design values |
| Use `{colors.accent}` + check icon + words for success | Introduce green |
| Keep the busy primary button at full colour with a changed label | Grey out the submit button while sending; the label is the state |

**Gaps the closed set leaves (honest list).**

| Gap | Impact | Current handling |
|---|---|---|
| No disabled/opacity value | Locked inputs during submit have no visual cue of their own | Decided 2026-10-06: no opacity. Inputs go `readonly` with unchanged visuals; "Sending your application…" on the button signals the lock. |
| No tint/background token | Skeletons, selected states and error banners can't use a fill | Skeletons are outlined boxes; banners use a `{spacing.1}` left rule; there are no selected states. Skeletons look sparser than usual. |
| No hover token | Buttons have no colour change on hover | Underline on hover. Weaker affordance on the primary button; acceptable. |
| No success colour | Confirmation lacks the usual green cue | Accent + icon + heading copy. |
| No text sizes below 16px | Metadata and helper text are as large as body, so rows and forms are taller | Muted colour and 400 weight de-emphasise; accepted density cost. |
| No layout-width token | Content max-width undefined | `ch` measure [ASSUMPTION]. Open question. |
| Focus-ring width (2px) and border width (1px) | Not tokens | Stated as structural constants per memlog. |

## Open Questions

- Content column max-width: accept a `ch` measure, or define it by composition from spacing?
- Icon set: unspecified. System or a single outline set at 16px (`{spacing.3}`)? [ASSUMPTION: one outline set]
