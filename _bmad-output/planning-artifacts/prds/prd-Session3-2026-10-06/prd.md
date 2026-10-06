---
title: "PRD: HireFlow Role Tracker (v1 prototype)"
status: draft
created: 2026-10-06
updated: 2026-10-06
---

# PRD: HireFlow Role Tracker (v1 prototype)

## 1. Summary

An in-house recruiting team of about five recruiters tracks roughly 30 open roles in a shared spreadsheet. Two things keep going wrong: the same role gets entered twice, and roles are never closed once they're filled or cancelled, so nobody can tell which roles are actually live.

v1 is a **single-user prototype in the browser**. It proves the core flow: a recruiter posts a role, sees it in a list, and closes it when it's done. There are two screens, data is stored in the browser, and there is no backend.

**What v1 does not solve, stated plainly:** because data stays in one browser, recruiters cannot see each other's roles. **v1 therefore does not fix duplicate entry across the team**, and it only partly addresses stale roles, because closing still depends on someone remembering to do it. These are the problems the client actually has. v1 exists to validate the flow and the UI before investing in a shared backend (see §8).

## 2. Goals and success criteria

| ID | Goal | Measured by |
|---|---|---|
| G1 | Posting a role is fast and hard to get wrong | A recruiter can post a role and see it in the list within **30 seconds** (AC1) |
| G2 | The list is a trustworthy record of what's live | Open and closed roles are clearly told apart at a glance; nothing disappears on reload (AC3, AC4) |
| G3 | The prototype shows whether the flow is worth building out | The client reviews it and decides whether to go ahead with a shared multi-user version |

**Counter-metric:** if recruiters still keep the spreadsheet alongside the prototype during review, the prototype hasn't earned trust. Ask about this in the review session.

## 3. Users

**Primary:** an in-house recruiter. They post roles that hiring managers ask for and need to know which ones are still open. They aren't technical and work mostly on a laptop, sometimes on a phone.

In v1 there is one user per browser. No roles or permissions.

## 4. Scope

**In:** two screens.
1. **Post a role**: a form with four required fields.
2. **Roles list**: every posted role, open and closed, with a way to close an open role. It includes an empty state.

**Non-goals (explicitly excluded from v1):**
- Candidate applications (including the HireFlow public Open Roles and Job Application pages)
- Authentication
- Search and filtering
- Editing a posted role
- File upload
- Email notification
- Multi-user or multi-tenant behaviour
- Warning about duplicates when posting a role (considered and left out of v1)

## 5. Functional requirements

### Feature A: Post a role

- **FR-1** The roles list has one primary action, **Post a role**, which opens the post-a-role screen.
- **FR-2** The form collects four fields, all required:
  - **Title**: free text
  - **Department**: free text
  - **Location**: free text (for example "Hybrid, London" or "Remote (UK)")
  - **Employment type**: chosen from a fixed list `[ASSUMPTION: Full-time, Part-time, Contract, Temporary, Internship]`
- **FR-3** A field counts as invalid if it's empty or contains only whitespace. Text fields are trimmed before saving. `[ASSUMPTION: Title, Department and Location are capped at 100 characters]`
- **FR-4** Submitting is blocked until all four fields are valid (AC2). Validation follows the existing HireFlow pattern:
  - Errors appear after the first submit attempt, then update as the user types.
  - Each invalid field shows the error border and an imperative message in the helper slot, such as "Enter a job title." or "Choose an employment type."
  - A summary alert above the form reads "A few things need fixing before you can post this role."
  - Focus moves to the first invalid field.
- **FR-5** A successful submit:
  - saves the role with status **Open** and the date it was posted;
  - returns the recruiter to the roles list with the new role at the top;
  - confirms the post with a short message `[ASSUMPTION: an inline confirmation such as "Senior .NET Engineer is now live." that screen readers announce]`.
- **FR-6** The post screen has a quiet **Cancel** action that goes back to the list without saving.

### Feature B: Roles list

- **FR-7** The list shows every posted role, newest first `[ASSUMPTION: closed roles stay in their date order rather than moving to the bottom]`.
- **FR-8** Each role shows:
  - title;
  - department, location and employment type on one line separated by middle dots;
  - a status label (**Open** or **Closed**);
  - for open roles, the posted date ("Posted 3 days ago");
  - for closed roles, the closed date ("Closed on 6 Oct").
- **FR-9** A header count shows how many roles are open, for example "4 open roles".
- **FR-10** Each open role has a quiet **Close role** action. Closing:
  - sets the status to **Closed** and records the closed date;
  - keeps the role in the list (AC4).
  `[ASSUMPTION: closing can't be undone in v1, there's no confirmation dialog, and there's no reopen]`
- **FR-11** Closed roles are visibly different from open ones using the style sheet's read-only card treatment: muted background, muted text, and a grey **Closed** label. They have no close action. Colour is never the only signal, because the "Closed" text label is always shown.
- **FR-12** **Empty state.** Before any role exists, the list shows:
  - a headline;
  - one line of warm, plain-language copy;
  - the **Post a role** action. `[ASSUMPTION copy: "No roles posted yet" / "Post your first role and it'll show up here, so everyone knows what's live."]`

### Feature C: Persistence

- **FR-13** Roles are saved in the browser. A posted or closed role survives a page reload and closing and reopening the browser (AC3).
- **FR-14** If browser storage isn't available or is full, the app says so in plain language and doesn't report a post as successful. A role is never silently lost.

## 6. Non-functional requirements

- **NFR-1 Design system.** The UI uses only HireFlow tokens and components: button, text input, card, and the inline status label. Font is Inter, spacing follows the 8px grid, and there are no gradients or heavy shadows. See §7 for gaps.
- **NFR-2 Accessibility.**
  - Meets WCAG 2.1 AA.
  - Every field has a visible label.
  - Errors are linked to their fields and announced to screen readers.
  - The full flow works with the keyboard alone.
  - Focus shows the 2px offset ring in primary blue.
- **NFR-3 Responsive.** The layout is mobile-first and works from 360px wide. The page title drops from 32px to 28px below 480px. Controls are 48px tall on touch screens.
- **NFR-4 Performance.** With 100 roles saved, the list renders and a post completes without a noticeable delay.
- **NFR-5 Tone.** Copy is warm and professional, not corporate-stiff.

## 7. Design gaps (flagged under the design standing instruction)

The HireFlow design references don't cover everything v1 needs. Each gap below needs a decision before UX or build work starts:

| Gap | Need | Proposal |
|---|---|---|
| No select/dropdown component | Employment type (FR-2) | `[ASSUMPTION]` A native select styled with the text-input tokens. This counts as a new component, so it needs approval through spec/plan. The alternative is a free-text field, which gives messier data. |
| No closed or inactive role state | FR-11 | Reuse the style sheet's existing "read-only record" card and grey inactive label (the "Withdrawn" precedent) |
| No "no roles yet" empty state | FR-12 | Follow the layout of the Open Roles empty state for no search matches; the copy is new |
| No department field in the designs | FR-2, FR-8 | Text input; shown on the card's metadata line |

The Open Roles page is candidate-facing. This list is a recruiter view, so it borrows the card layout but has no Apply button and no skill tags.

## 8. Known limitations and next steps

1. **Single browser, single user.** Recruiters can't see each other's roles, so duplicates across the team still happen. **First follow-up:** shared storage so all recruiters see one list.
2. **Nothing prompts a recruiter to close a role.** Stale roles still depend on memory. Possible follow-up: a reminder when a role has been open longer than N days.
3. **No duplicate check.** Once the list is shared, a "possible match" warning on post becomes worth building.
4. **No edit and no reopen.** A mistake means closing the role and posting it again.

## 9. Acceptance criteria

| AC | Criterion | Covered by |
|---|---|---|
| AC1 | A recruiter can post a role and see it in the list within 30 seconds | FR-1, FR-5 |
| AC2 | Title, department, location and employment type are required; submitting is blocked until they're valid | FR-2 to FR-4 |
| AC3 | A posted role is saved and survives a page reload | FR-13 |
| AC4 | Closing a role keeps it in the list, clearly marked as closed | FR-10, FR-11 |
| AC5 | The list shows a clear empty state before any role exists | FR-12 |

## 10. Open questions

| # | Question | Blocks |
|---|---|---|
| Q1 | Approve a select component for employment type, or use free text? | UX / build |
| Q2 | Confirm the employment type values | Build |
| Q3 | Should closing ask for confirmation, given it can't be undone? | UX |
| Q4 | Approve the empty-state and confirmation copy | UX |
| Q5 | Fill in `.specify/memory/constitution.md` before running `/speckit-specify` (it's still the template) | Spec Kit cycle |
