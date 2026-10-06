---
title: "EXPERIENCE: HireFlow"
status: draft
created: 2026-10-06
updated: 2026-10-06
sources:
  - '{planning_artifacts}/ux-designs/ux-Session3-2026-10-06/.memlog.md'
name: HireFlow
---

# HireFlow: Experience Spine

## Foundation

| Item | Decision |
|---|---|
| Product | Public, consumer-facing careers site. Stakes: consumer. |
| Form factor | Responsive web, **desktop-first**; must work down to 360px wide. |
| UI system | None yet. No component library; components below are built to `DESIGN.md`. |
| Visual reference | `DESIGN.md` (closed token set; overrides the repo `CLAUDE.md` style sheet by user choice). |
| Accessibility floor | WCAG 2.2 AA. |
| Theme | Light only. No dark-mode tokens exist. [ASSUMPTION] |
| Mocks | None yet (fast path). These tables are the build spec. |

## Information Architecture

| Surface | URL [ASSUMPTION] | Reached from | Purpose |
|---|---|---|---|
| Open Roles | `/roles` (`?q=` holds the search) | Site entry, back link, "See open roles" links | Find a role: searchable list with empty states |
| Job Application | `/roles/{role-id}` | Job row on Open Roles, shared link | Read the role, then apply on the same page |
| Application sent (state, not a page) | same URL | Successful submit | Confirmation replaces the form in place |

Job Application is one page, single column, in this order: back link → `job-header` (title, company, meta, "Apply now") → role description sections → "Apply for this role" form. "Apply now" is an in-page link that moves focus to the form heading. [ASSUMPTION: single column at all widths; no side-by-side form]

Role description sections [ASSUMPTION]: About the role · What you'll do · What you'll bring · Nice to have · About {company}.

## Voice and Tone

Warm and professional. Talk to one person. Say what happened, what's safe, what to do next.

| Do | Don't |
|---|---|
| "We couldn't send your application. Your answers and CV are still here." | "Error 500: Submission failed." |
| "That email doesn't look quite right." | "Invalid input." |
| "Thanks, Priya. Your application is in." | "Your submission has been received successfully." |
| "We're not hiring right now." | "No records found." |
| Contractions, plain verbs, one idea per sentence | Exclamation marks, emoji, jokes in error states, "Oops!" |
| Name the field and the fix in every error | Blame the user ("You entered…wrong") |

### Microcopy: Open Roles

| Slot | Copy |
|---|---|
| Page title | Open roles |
| Intro (muted) | Find a role where you can do your best work. [ASSUMPTION] |
| Search label | Search roles |
| Search hint (muted) | Try a job title, team or location |
| Result count, unfiltered | {n} open roles · 1 open role |
| Result count, filtered | {n} roles match "{q}" · 1 role matches "{q}" |
| Slow network notice | Still loading. Thanks for bearing with us. |
| No results heading | No roles match "{q}" |
| No results body | Try a different word or check the spelling. New roles are added often. |
| No results action | Clear search |
| Zero roles heading | We're not hiring right now |
| Zero roles body | There are no open roles at the moment, but that changes. Please check back soon. |
| Load error heading | We couldn't load the roles |
| Load error body | Check your connection and try again. |
| Load error action | Try again |
| Search request failed (list already shown) | Search isn't working right now. Showing all roles instead. · action: Try again [ASSUMPTION] |

### Microcopy: Job detail

| Slot | Copy |
|---|---|
| Back link | All open roles |
| Primary action | Apply now |
| Load error heading / body / action | We couldn't load this role · Check your connection and try again. · Try again |
| Role closed heading | This role has closed |
| Role closed body | {company} has stopped taking applications for {role title}. Have a look at what's open now. |
| Not found heading | We can't find that role |
| Not found body | It may have been filled, or the link may be out of date. |
| Closed / not found action | See open roles |

### Microcopy: Apply form

| Slot | Copy |
|---|---|
| Form heading | Apply for this role |
| Intro (muted) | It takes about 5 minutes. Fields marked (optional) can be left blank. [ASSUMPTION] |
| Labels | Full name · Email · Phone (optional) · CV · Cover note (optional) |
| Email hint | We'll only use this to contact you about this role. [ASSUMPTION] |
| Phone hint | Include your country code if you're outside {company country}. [ASSUMPTION] |
| CV zone | Drag your CV here, or **Choose file** · hint: PDF or Word (.docx), up to 5 MB |
| Cover note hint | A few lines on why this role interests you. Up to 3,000 characters. [ASSUMPTION: limit] |
| Submit | Send application |
| Submit, busy | Sending your application… |

### Microcopy: field errors (exact)

| Field | Trigger | Copy |
|---|---|---|
| Full name | Empty | Please enter your full name. |
| Email | Empty | Please enter your email address. |
| Email | Not a valid address | That email doesn't look quite right. Check for a typo, like name@example.com. |
| Phone | Provided but bad format (allowed: digits, spaces, `+ ( ) -`; 7–15 digits) [ASSUMPTION: rule] | That phone number doesn't look right. Use digits and spaces, with + at the start for a country code. |
| CV | Missing | Please add your CV as a PDF or Word (.docx) file. |
| CV | Wrong type | We can only accept PDF or Word (.docx) files. "{filename}" is a .{ext} file. |
| CV | Over 5 MB | "{filename}" is {size} MB. The limit is 5 MB. Try saving a smaller PDF. |
| CV | Upload failed | We couldn't upload "{filename}". Check your connection and try again. (action: Try again) |
| CV | Submit pressed while still uploading | Your CV is still uploading. Send again once it's finished. |
| Cover note | Over limit [ASSUMPTION] | Your cover note is {n} characters over the 3,000 limit. |
| Error summary heading | Submit with errors | {n} things need fixing before we can send your application · 1 thing needs fixing before we can send your application |

### Microcopy: submit outcomes (exact)

| Outcome | Heading | Body | Action |
|---|---|---|---|
| Success | Thanks, {first name}. Your application is in. | We've emailed a confirmation to {email}. | Browse other open roles |
| Success, "What happens next" list | n/a | 1. You'll get a confirmation email in the next few minutes. 2. The {company} hiring team reads every application. 3. You'll hear back either way, usually within {response window}. [ASSUMPTION: window comes from role data] | n/a |
| Server error | We couldn't send your application | Something went wrong on our side. Your answers and CV are still here, so nothing is lost. | Try again |
| Offline | You're offline | Your answers are still here. Reconnect and press Try again. | Try again |
| Timeout | This is taking longer than it should | We're not sure your application went through. Press Try again. If it already arrived, we'll let you know rather than send it twice. | Try again |
| Duplicate | You've already applied for this role | We already have your application for {role title}, sent on {date}. There's no need to send it again. | Browse other open roles |
| Role closed mid-form | This role closed while you were applying | We're sorry. {company} stopped taking applications for {role title} before we could send yours. Your cover note is still below if you want to copy it. | See open roles |

## Component Patterns

Behavioral. Visual specs live in `DESIGN.md.Components`; names match.

| Component | Use | Behavioral rules |
|---|---|---|
| Button, primary (`button-primary`) | "Apply now", "Send application" | One per view region. Native `<button>` (or `<a>` for "Apply now"). While busy: `aria-disabled="true"`, label swaps, clicks ignored. |
| Button, secondary (`button-secondary`) | Clear search, Try again, Choose file | Native button. Never the only way to recover; Enter/Space work. |
| Link (`link`) | Back link, "See open roles", inline links, error-summary items | Real `<a href>`. Error-summary links move focus to the field, not just scroll. |
| Focus ring (`focus-ring`) | All focusables | `:focus-visible`. Never removed; never hidden behind other elements. |
| Search field (`search-field`) | Open Roles | `type="search"`, visible label. Filters on input after 300ms debounce [ASSUMPTION]. Enter runs immediately. Esc or the × clears and returns focus to the field. Query mirrored to `?q=` (replaceState, no history spam) [ASSUMPTION]. Matches title, team, location [ASSUMPTION]. |
| Text field (`text-field`) | Name, email, phone | Native input with `autocomplete` (`name`, `email`, `tel`) and `type` (`email`, `tel`). Validation timing per State Patterns. |
| Text area (`text-area`) | Cover note | Count updates live, announced politely only at 90% and over limit. Does not block typing past the limit; validates instead. |
| Field error (`field-error`) | Under any invalid field | Linked via `aria-describedby`; field gets `aria-invalid="true"`. Removed as soon as the field is valid. |
| CV upload (`cv-upload`) | CV | Accepts drag-and-drop or "Choose file" (native `<input type="file" accept=".pdf,.docx">`). Type and size checked client-side before upload. Uploads immediately on selection [ASSUMPTION: async upload, submit references the uploaded file]. One file only; a new file replaces the old one. |
| Upload progress (`upload-progress`) | CV, while uploading | `role="progressbar"` with `aria-valuenow`. Cancel = "Remove". |
| Job row (`job-row`) | Open Roles list | Entire row is one link to the role; one tab stop per row. Content: title, company · location · work type · posted date [ASSUMPTION: fields]. |
| Job header (`job-header`) | Job Application | Title is the page `<h1>`. "Apply now" jumps to and focuses the form heading. |
| Skeleton row (`skeleton-row`) | Open Roles loading | 5 rows [ASSUMPTION]. `aria-hidden`; container gets `aria-busy="true"`. |
| Error summary (`error-summary`) | Top of the apply form on failed submit | `tabindex="-1"`, receives focus on submit-with-errors. Lists errors in form order. Updates as errors are fixed; disappears when none remain. |
| Alert banner (`alert-banner`) | Server error, offline, timeout, list/role load error | Placed directly above the submit button for submit failures [ASSUMPTION], or in the list/content area for load failures. `role="alert"`. One at a time. |
| Notice (`notice`) | Slow network, back online | `role="status"`. Non-blocking. |
| Empty state (`empty-state`) | No results, zero roles, closed/not found role | Replaces the list or content area. Heading is a real heading. |
| Confirmation panel (`confirmation-panel`) | After successful submit | Replaces the form (not the role description). Heading gets `tabindex="-1"` and focus. |

## State Patterns

### Open Roles

| State | Trigger | Treatment | Focus / announcement |
|---|---|---|---|
| Initial loading | First visit, no data yet | Title, intro and search field render immediately; search is usable. List area shows 5 `skeleton-row`s. No count. | List `aria-busy="true"`. Nothing announced. |
| Slow network | Still loading after 3s [ASSUMPTION] | Skeletons stay; `notice` above them: "Still loading. Thanks for bearing with us." | `role="status"` announces once. |
| Load timeout | No response after 15s [ASSUMPTION] | Becomes Load error. | As Load error. |
| Load error | Request fails or times out | Skeletons replaced by `alert-banner`: "We couldn't load the roles" / "Check your connection and try again." + "Try again". Search field hidden or disabled. [ASSUMPTION: hidden] | `role="alert"`. Focus stays where it was. |
| Retrying | "Try again" pressed | Back to Initial loading. | Focus moves to the list region heading [ASSUMPTION: visually hidden "Roles" heading]. |
| Populated | Data loaded, ≥1 role | Count line ("{n} open roles") then `job-row` list, newest first [ASSUMPTION]. All roles on one page up to 50; beyond that, numbered pagination [ASSUMPTION]. | Count in an `aria-live="polite"` region (not announced on first load). |
| Search typing | Input changes | Debounce 300ms. During debounce the current list stays; no spinner. | Nothing announced mid-typing. |
| Search applied | Debounce elapses or Enter | List filters; count line becomes "{n} roles match "{q}"". | Count region announces the new count. |
| Search pending (server search, slow) | Result takes over 300ms [ASSUMPTION] | Previous results stay, `aria-busy` on list; no skeleton flash. | None until results land. |
| Search request failed | Search call errors, list was shown | Inline `notice` under the field: "Search isn't working right now. Showing all roles instead." + "Try again". | `role="status"`. |
| No results | Query matches nothing | `empty-state`: "No roles match "{q}"" / "Try a different word or check the spelling. New roles are added often." + `button-secondary` "Clear search". Query echoed exactly as typed. | Count region announces "No roles match "{q}"". "Clear search" empties the field, restores full list, moves focus to the search field. |
| Zero roles at all | Loaded, total = 0 | Search field hidden. `empty-state`: "We're not hiring right now" / "There are no open roles at the moment, but that changes. Please check back soon." No action button. | Announced via count region. |
| Deep link with `?q=` | URL carries a query | Field pre-filled, filtered result shown after load. | Normal. |

### Job Application: job detail

| State | Trigger | Treatment | Focus / announcement |
|---|---|---|---|
| Loading | Direct visit or row click | Back link renders. Title and meta show as outlined `skeleton-row` bars; body as 3 bars. Form not rendered yet. | `aria-busy` on main. |
| Slow network | Over 3s | `notice`: "Still loading. Thanks for bearing with us." | `role="status"`. |
| Loaded | Role open | `job-header`, description sections, then the form (Pristine). | Focus starts at top of page (normal navigation). Page `<title>`: "{role title} at {company} · HireFlow" [ASSUMPTION]. |
| Load error | Request fails | `alert-banner`: "We couldn't load this role" + "Try again". | `role="alert"`. |
| Role closed | Role exists, not accepting | Title and company shown; description hidden; `empty-state` "This role has closed" + "See open roles". No form. | Normal page load; heading readable first. |
| Not found | Unknown id | `empty-state` "We can't find that role" + "See open roles". | Page `<title>` reflects "Role not found". |

### Job Application: apply form

**Validation timing.** A field is checked (1) on blur, but only after the user has typed in it at least once; (2) after its first error appears, on every input, so the error clears the moment it's fixed; (3) on submit, every field at once. Tabbing through an untouched field never raises an error.

| State | Trigger | Treatment | Focus / announcement |
|---|---|---|---|
| Pristine | Form renders | All fields empty, no errors. Optional fields labelled "(optional)"; required ones not starred [ASSUMPTION]. Submit enabled. | n/a |
| Field focus | Focus enters a field | `focus-ring` on the control. Hint text stays visible. | Label + hint read via `aria-describedby`. |
| Field hover | Pointer over field | Border `{colors.muted}` → `{colors.accent}`. | n/a |
| Inline error | Blur after edit, or live after first error | `text-field-error`: `{colors.danger}` border, `field-error` (icon + exact copy) below. | `aria-invalid="true"`, message added to `aria-describedby`. Not announced on blur (user is moving on); read when the field is focused again. |
| Error fixed | Live check passes | Error and danger border removed immediately. No "success" tick. | Nothing announced. |
| Submit with errors | "Send application" pressed, ≥1 invalid | No request sent. Every invalid field shows its error. `error-summary` appears at the top of the form listing each error as a link. | Focus moves to the summary. Its heading is read ("2 things need fixing…"). Each link focuses its field. |
| Submitting | Valid submit | Button label "Sending your application…" with spinner, `aria-disabled`, stays full colour. All inputs and the CV "Remove" locked (`readonly`, visuals unchanged; no opacity). Further clicks and Enter ignored (double-submit blocked client-side; server also de-duplicates by idempotency key [ASSUMPTION]). | `aria-live="polite"` status region announces "Sending your application". Focus stays on the button. |
| Success | 2xx | Form replaced by `confirmation-panel`: "Thanks, {first name}. Your application is in." + email confirmation line + "What happens next" list + "Browse other open roles". Role description stays above. | Focus moves to the confirmation heading. Page `<title>` prefixed "Application sent ·". |
| Server error | 5xx or unknown failure | Form unlocked, **every value and the uploaded CV preserved**. `alert-banner` above the submit button: "We couldn't send your application" / "Something went wrong on our side. Your answers and CV are still here, so nothing is lost." + "Try again" (resubmits the same data). | `role="alert"`. Focus moves to the banner heading. |
| Offline | `navigator.onLine` false at submit, or network failure | No request sent (or treated as failed). Data preserved. `alert-banner`: "You're offline" / "Your answers are still here. Reconnect and press Try again." When the connection returns, the banner changes to `notice` "You're back online." Nothing auto-submits. [ASSUMPTION] | `role="alert"`, then `role="status"` on reconnect. |
| Timeout | No response after 30s [ASSUMPTION] | Data preserved. `alert-banner`: "This is taking longer than it should" + body about safe retry + "Try again". Retry uses the same idempotency key, so a late success shows Duplicate/Success, never two applications. | `role="alert"`. Focus to banner. |
| Duplicate | Server says this email already applied to this role | Form replaced by `notice`-style panel: "You've already applied for this role" / "…sent on {date}. There's no need to send it again." + "Browse other open roles". | Focus to heading. |
| Role closed mid-form | Server says role closed at submit | Form fields locked; cover note left selectable for copying. `alert-banner`: "This role closed while you were applying" + "See open roles". Not retryable. [ASSUMPTION: detected only at submit; no polling] | `role="alert"`. Focus to banner. |
| Session / CSRF expired [ASSUMPTION] | Server rejects token | Treated as Server error; retry refreshes the token silently. | As Server error. |

### CV upload

| State | Trigger | Treatment | Focus / announcement |
|---|---|---|---|
| Empty | Pristine | Dashed muted box: "Drag your CV here, or Choose file" + hint. | "Choose file" button is the tab stop. |
| Dragging over | File dragged over the zone (or the page) | Border becomes 2px solid `{colors.accent}`; text "Drop your CV to upload". | Pointer-only state; keyboard path is "Choose file". |
| Rejected before upload | Wrong type or over 5 MB | No upload starts. `{colors.danger}` border + exact error (wrong type / over 5 MB). Zone stays ready for another file. | Error announced via `role="alert"` on the zone message (user just acted). |
| Uploading | Valid file chosen | Filename, `upload-progress` with percent, "Remove" (cancels). | `role="progressbar"`; "Uploading {filename}" announced once; "Uploaded" announced at completion. |
| Uploaded | Upload completes | Solid border, file icon, filename (600), size (muted), "Remove". | "Remove" is a tab stop; label "Remove {filename}". After remove, focus returns to "Choose file". |
| Upload failed | Network/server error during upload | Danger border + "We couldn't upload "{filename}". Check your connection and try again." + "Try again" (re-uploads the same file) and "Choose a different file". | `role="alert"`. |
| Missing on submit | Submit with no file | Danger border + "Please add your CV as a PDF or Word (.docx) file." Listed in `error-summary`. | Summary link focuses "Choose file". |
| Still uploading on submit | Submit while uploading | Not sent. CV error "Your CV is still uploading. Send again once it's finished." Listed in `error-summary`. | As Submit with errors. |

## Interaction Primitives

- **Pointer + keyboard parity.** Every action works with Tab, Shift+Tab, Enter, Space. Drag-and-drop always has the "Choose file" equivalent.
- **Search:** type to filter (300ms debounce), Enter to apply now, Esc to clear. [ASSUMPTION: debounce and Esc]
- **Hover** is decoration only: underline, or border muted → accent. Nothing is revealed only on hover.
- **Focus moves only on purpose:** after submit-with-errors (summary), submit failure (banner), success (confirmation heading), "Apply now" (form heading), "Clear search" (search field), "Remove" CV ("Choose file").
- **No modals, toasts, infinite scroll or auto-advancing content.** Feedback is inline where the user is looking. [ASSUMPTION]
- **Nothing is lost.** Field values persist through every failure. Values are also kept in `sessionStorage` so an accidental reload keeps typed text (not the CV file). [ASSUMPTION] Navigating away from a dirty form shows the browser's native "Leave site?" prompt. [ASSUMPTION]
- **Motion:** spinner on busy button and progress fill only. No page transitions.

## Accessibility Floor

Behavioral. Contrast lives in `DESIGN.md.Colors` (all text pairs ≥ 4.5:1, borders ≥ 3:1).

| Area | Rule |
|---|---|
| Standard | WCAG 2.2 AA on every surface and state. |
| Labels | Every input has a visible `<label>`; no placeholder-as-label. "(optional)" is part of the label text. Required fields carry `aria-required="true"`. |
| Errors | Invalid fields get `aria-invalid="true"` and the error id in `aria-describedby` (with the hint). Errors use icon + text + border, never colour alone. |
| Error summary | Focused on failed submit; heading states the count; each item is a link to its field. |
| Live regions | Search result count: `aria-live="polite"`, announces after debounce. Submit status: polite region announces "Sending your application". Failures: `role="alert"`. Slow/offline-recovered notices: `role="status"`. |
| Focus management | As listed in Interaction Primitives. Focus is never dropped to `<body>`; replaced content always hands focus to its new heading. |
| Keyboard paths | Open Roles: skip link → search → rows (one stop each) → pagination. Job Application: skip link → back link → "Apply now" → description links → form fields in visual order → submit. No keyboard traps. |
| Focus visibility | 2px `{colors.accent}` ring at `{spacing.1}` offset, never obscured (no sticky headers) (2.4.11). |
| Target size | 44px minimum for all controls (composed: `{spacing.2}` padding + 1.75 line-height). Exceeds 2.5.8. |
| Headings & landmarks | One `<h1>` per page; sections `<h2>`. `<main>`, `<nav>` for back link, `<form>` with accessible name "Apply for {role title}". |
| Reduced motion | `prefers-reduced-motion`: no spinner rotation (static icon + label), progress bar jumps instead of animating, no smooth scroll on "Apply now". |
| Zoom & reflow | Works at 400% zoom / 320 CSS px without horizontal scroll (1.4.10), which also covers the 360px floor. |
| Autocomplete | `name`, `email`, `tel` tokens set (1.3.5). |
| Timing | No session timeout that discards typed data (2.2.1, 3.3.7 redundant entry: nothing re-asked after errors). |
| Language | `lang` set; file sizes read as "5 megabytes" via text, not abbreviations alone [ASSUMPTION]. |

## Responsive & Platform

Desktop-first. One column at every width; only gutters and wrapping change.

| Width | Behavior |
|---|---|
| ≥ 1024px | Content column centred, max ~70ch [ASSUMPTION], page gutter `{spacing.4}`. Job row meta on one line. |
| 768–1023px | Same layout; column fills to gutters. Gutter `{spacing.4}`. |
| 480–767px | Gutter `{spacing.3}`. Job row meta wraps; " · " separators stay with the following item. Buttons full width inside forms [ASSUMPTION]. |
| 360–479px (floor) | Gutter `{spacing.3}`. Title stays 32px (`{typography.title}`) and wraps ("Senior .NET / Engineer"). CV zone text stacks: "Drag your CV here, or" above "Choose file"; drag hint hidden on touch-only devices [ASSUMPTION]. Error summary and banners full width. Long filenames truncate in the middle with full name in `title` and accessible name. |
| < 360px | Not designed for, but must not scroll horizontally (reflow rule above). |
| Touch | Same 44px targets. No hover-dependent behaviour. Native file picker. |

## Key Flows

### Flow 1: Priya applies on her lunch break [ASSUMPTION: protagonist from memlog placeholder]

Priya, a backend developer, on her laptop during a lunch break, applying to Senior .NET Engineer at Northgate Labs.

1. Priya opens `/roles`. Skeleton rows show briefly, then "24 open roles". [ASSUMPTION: count]
2. She types ".net" in Search roles. After she pauses, the list narrows and the count announces "3 roles match ".net"".
3. She clicks "Senior .NET Engineer · Northgate Labs". The role loads; she reads What you'll do and What you'll bring.
4. She presses "Apply now"; focus lands on "Apply for this role".
5. Browser autofill fills Full name and Email. She types her phone without a country code; on blur, nothing complains (format is valid).
6. She drags `priya-cv.pdf` onto the CV zone. The border turns accent, progress runs, then "priya-cv.pdf · 412 KB · Remove".
7. She writes three lines in Cover note and presses "Send application".
8. The button reads "Sending your application…"; fields lock.
9. **Climax:** The form gives way to "Thanks, Priya. Your application is in." Focus is on that heading. Below it, "What happens next" tells her a confirmation email is on its way and she'll hear back either way. She closes the laptop with ten minutes of lunch left.

### Flow 2: Server error, nothing lost [ASSUMPTION]

1. Priya completes steps 1–7 of Flow 1.
2. The server returns an error. The button returns to "Send application"; fields unlock.
3. An alert banner appears above the button, focused: "We couldn't send your application. Something went wrong on our side. Your answers and CV are still here, so nothing is lost."
4. She checks: name, email, phone, cover note and "priya-cv.pdf" are all still there.
5. She presses "Try again". The same data (same idempotency key) is sent.
6. **Climax:** The confirmation appears exactly as in Flow 1. She never retyped a word.

Failure branch: the retry times out → "This is taking longer than it should" banner; a later retry that the server already accepted returns the confirmation rather than a second application.

### Flow 3: Fixing errors on submit [ASSUMPTION]

1. Priya, in a hurry, types "priya@gmail" and attaches `cv.pages`.
2. The CV is rejected at once: "We can only accept PDF or Word (.docx) files. "cv.pages" is a .pages file."
3. She presses "Send application" anyway. Focus jumps to the summary: "2 things need fixing before we can send your application", with links to Email and CV.
4. She follows the Email link, adds ".com"; the error clears as she types, and the summary drops to 1 item.
5. She follows the CV link, chooses `cv.pdf`; it uploads; the summary disappears.
6. **Climax:** She sends, and lands on the confirmation.

### Flow 4: No match, then nothing at all [ASSUMPTION]

1. On Open Roles, Priya searches "rust". Result: "No roles match "rust"" with "Clear search".
2. She presses "Clear search"; focus returns to the field and the full list is back.
3. **Climax:** She types ".net" instead and finds the Northgate role (continues as Flow 1, step 3).
4. Alternative: when the site has no roles at all, she sees "We're not hiring right now" and no search box, so she isn't invited to search an empty list.

## Open Questions

- Response window for "What happens next" (per role, per company, or omitted?).
- Is search client-side over all roles or server-side? Affects the Search pending and Search request failed states.
- Does the duplicate check key on email + role only? What date do we show?
- Should the closed-role check also run on page focus/return, not only at submit?
- Phone validation rule (7–15 digits) and the cover note limit (3,000) need product confirmation.