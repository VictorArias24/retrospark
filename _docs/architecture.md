# Architecture

## Stack

- **Application:** Django monolith with server-rendered templates and HTMX.
- **Database:** PostgreSQL.
- **Background work:** Celery with Redis, running in a separate worker process.
- **Runtime:** Docker Compose with Django web, Celery worker, Celery scheduler, PostgreSQL, and Redis services.
- **Email:** Resend.
- **AI:** OpenAI Whisper for transcription, plus OpenAI language models for clustering, summaries, and draft meeting suggestions.

This is deliberately one application and one codebase. A separate frontend or API service is not part of the MVP.

## Application boundaries

The Django web process owns rendered pages, HTMX actions, authentication, authorization, validation, and all synchronous business operations.

Celery workers own round opening and closing, reminders, summaries, feedback clustering, and AI draft generation. Tasks must be idempotent so retries cannot duplicate emails, votes, or generated records.

Recordings are not retained. The Django process validates an upload's filename metadata, extension, MIME type, size, and actual content, writes it only to an OS-managed temporary file when required by the OpenAI Whisper client, and deletes it after transcription whether processing succeeds or fails. The resulting transcript may be persisted as private project data.

## Identity and access

- Managers authenticate with short-lived, single-use passwordless email links.
- Each invited member has a revocable, high-entropy project link whose secret is stored only as a hash.
- Managers, members, and facilitators are authorized server-side for every resource read and mutation; no role or identity is accepted from request data.
- Anonymous feedback is separated from attribution before manager-facing clustering, summaries, and AI prompts whenever attribution could be revealed.
- Raw feedback, private manager summaries, and transcripts are never exposed to members in the MVP. Recordings are discarded immediately after transcription.

## Core workflow data

The application models projects, member invitations, feedback templates, weekly rounds, feedback submissions, topic clusters, vote allocations, agenda topic state, meeting notes, decisions, action items, and processing/audit metadata.

Template changes apply to the next round. The weekly lifecycle opens and closes automatically. The manager sees submission participation before close, but not feedback content. Topic clusters require manager review before publication. Voting closes before the agenda is finalized.

Vote allocation is enforced transactionally in the database: a member may allocate exactly three votes per round, may place multiple votes on one topic, and may revise allocations before voting closes.

## AI and media processing

OpenAI language-model calls for clustering, summaries, and draft generation run only from background workers. AI output is always a draft: facilitators must approve suggested notes, decisions, action items, and topic statuses before those records become final.

Audio and video uploads are transcribed by OpenAI Whisper during the upload flow and discarded immediately afterward. A usable provided transcript is preferred; otherwise Whisper generates one, then background processing associates transcript sections to discussion topics when possible.

This synchronous transcription flow deliberately avoids a media-storage service. If real recordings exceed web-request or provider limits, add private transient object staging with automatic expiry and immediate deletion after processing; do not add durable recording retention.

## Security and operations

- Validate external input at the request boundary using Django forms, model validation, or explicit schemas; reject unknown or invalid data.
- Use Django ORM queries and database transactions for data access and workflow invariants.
- Return generic user-facing errors and use structured logs that exclude feedback text, transcript content, email addresses, magic-link secrets, session data, and API credentials.
- Inject OpenAI, Resend, database, and Redis credentials through environment variables; never commit secret values.
- Treat uploads and AI output as untrusted; do not execute uploaded content and do not make AI suggestions final without human review.
- Retain project data indefinitely in the MVP, except recordings, which are deleted immediately after transcription. No other automated deletion policy is included.

## Verification priorities

Test passwordless-link expiry and one-time use, member-link revocation, cross-project authorization denial, weekly lifecycle timing, anonymous-feedback visibility, transactional vote limits, facilitator-only meeting access, upload validation, recording deletion on successful and failed Whisper calls, task retry idempotency, and mandatory approval of AI suggestions.
