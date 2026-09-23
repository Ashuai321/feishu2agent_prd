---
name: yuanbo-calendar-workflows
description: Route Yuanbo calendar requests to the smallest relevant workflow for itinerary images, travel-email review, event editing, or Skill maintenance without duplicating onboarding or calendar defaults.
---

# Yuanbo Calendar Workflows

Use this Skill only when the request is an itinerary image, a travel-email/reservation review, a calendar read/write, or Skill creation/update/validation/packaging.

Load only the one relevant reference:
- Itinerary image or photo: read references/pic-to-event.md.
- Travel email or reservation scan: read references/review-travel-email-events.md.
- Calendar search, availability, create, update, cancel, recurrence, color, or invitation response: read references/calendar-event-editing.md.
- Skill creation, update, validation, improvement, or packaging: read references/skill-creator.md.

For every calendar request, `references/calendar-event-editing.md` is authoritative for calendar routing
and event colors. Never use the connector's default calendar. An explicitly named `Perfect710` is the
only allowed use of that calendar; family cues 小奇/小果/诺诺 route to `Family`; work-related requests
must ask the user to choose `Bo Bozway` or `Bo YW`; all other or unclear requests default to `Bo Bozway`.
For create/modify colors, uncertain time is pink with highest priority; with definite time, online or no
modality/location is green, and offline or an actual location is purple. The preview and write must use
the same resolved live-palette color.

For create, update, delete, or cancel proposals, classify the direct confirmation reply as follows: after
normalizing surrounding whitespace, case, and punctuation, `执行`, `开始`, `接受`, `确认`, `行`, `行的`, `好`, `好的`,
`可以`, `yes`, `ok`, `同意`, `确认创建`, `确认修改`, `确认删除`, or `确认取消` (including a direct phrase such as
`好的，执行`) confirms the immediately preceding proposal. Explicit refusal wins over any positive token:
`不执行`, `不开始`, `不接受`, `不确认`, `不行`, `不行的`, `不好`, `不好的`, `不可以`, `no`, and the corresponding
`不确认创建/修改/删除/取消` forms reject it and must not call a write tool. A reply with changed fields,
no pending proposal, or neither clear polarity is not confirmation and requires a new question or proposal.

Use yuanbo-calendar-onboarding only when its existing trigger requires missing durable defaults; do not restate or replace that Skill. Existing Yuanbo Memory, the connected Google Calendar account, and the target agent's original instructions remain authoritative for calendar identity, timezone, defaults, and persistence. Do not import another agent's account names, calendar IDs, mailbox, timezone, or defaults. If a required app or dependency is not attached, explain the exact gap and stop rather than substituting another account or writing directly.

Shared safeguards:
- Keep discovery and proposals read-only.
- Ask only for missing or ambiguous fields; never invent event details.
- Before every calendar mutation or invitation response (create, update, delete/cancel, recurrence change, or guest response), identify and read the exact target, check relevant conflicts, show the complete change or deletion scope, and get explicit confirmation.
- Treat the user's original request as a request to prepare a proposal, never as confirmation to write. Only an explicit confirmation that matches the immediately preceding proposal may authorize the mutation.
- For deletion/cancellation, confirm the exact event, calendar, local time/timezone, and whether the request applies to one occurrence or the entire recurring series before calling the delete/cancel action.
- If any candidate, field, time, calendar, or scope changes, discard the prior confirmation and present a new proposal.
- Preserve existing event fields unless the user explicitly requests a change.
- Return direct event links after successful writes when the calendar action provides them.
- Read only the relevant reference for the current request; do not load all references.
