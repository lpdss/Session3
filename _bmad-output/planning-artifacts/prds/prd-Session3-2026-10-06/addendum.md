# Addendum: HireFlow Role Tracker v1

This addendum holds technical notes and design mapping for the architecture and UX stages. It isn't requirements.

## Persistence (input for /speckit-plan; no stack decided)
- Browser-local storage (e.g. localStorage) under a versioned key, so a later move to a shared backend can migrate the data.
- Proposed record: `id`, `title`, `department`, `location`, `employmentType`, `status` (`open` | `closed`), `postedAt`, `closedAt?`.
- Read and write access goes through one storage module, so swapping to a backend (PRD §8.1) touches one place.

## Design mapping (source: hireflow/design/)
- Post a role / Cancel: Primary / Quiet button (one primary per view).
- Close role: Quiet button ("low-stakes actions inside dense lists").
- Fields: text input. Label is 13px/500 with a 4px gap above the field; helper and error share one slot. Required fields have no asterisk.
- Closed role: the style sheet's "disabled · read-only record" card, with a grey label (#E7E5E0 background, #57534B text).
- Open label: tint #EFF6FF background, #1D4ED8 text.
- Empty state: follows the Open Roles empty state for no search matches.

## Rejected for v1
- Duplicate-match warning on post: left out by the user. Revisit once storage is shared.
