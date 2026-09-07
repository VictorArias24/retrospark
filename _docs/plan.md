# Weekly Feedback and Discussion Tool — MVP

## Product goal

Help teams turn weekly **Start, Stop, Continue** feedback into prioritized discussions, documented decisions, and actionable follow-ups.

## Roles

### Project manager

- Signs in through a passwordless email link.
- Creates and manages multiple projects.
- Invites members by email.
- Customizes the weekly feedback template.
- Reviews and edits generated discussion topics.
- Receives the private weekly feedback summary.
- May act as the meeting facilitator.

### Team member

- Does not need an account.
- Uses one private link per project.
- Submits feedback under their name by default.
- May choose to remain anonymous.
- Can edit feedback until the weekly deadline.
- Receives three votes for prioritizing discussion topics.

### Facilitator

- Runs the discussion using the prioritized agenda.
- Marks topics as discussed, skipped, or deferred.
- Records notes, decisions, and action items.
- Uploads meeting recordings or transcripts.
- Reviews and approves system-generated suggestions.

## Phase 1: Weekly feedback

The default template asks:

1. What should we **start** doing?
2. What should we **stop** doing?
3. What should we **continue** doing?

Managers can customize these questions before the next round opens. Feedback can address project practices and team interactions, but the MVP will not include a separate performance-review system.

## Phase 2: Automatic weekly cycle

1. The manager receives a reminder one day before the round opens.
2. The manager may update the feedback template.
3. The round opens automatically on Monday.
4. Members receive the project link and an email reminder.
5. Members submit or edit their feedback.
6. The round closes Friday at 5 p.m.
7. The manager receives a concise private summary.

Before the deadline, the manager can see who has submitted but cannot read the responses.

## Phase 3: Topic clustering

After the round closes, the system:

- Groups related feedback into discussion-topic clusters.
- Creates a short title and description for each cluster.
- Preserves the anonymity of anonymous contributors.
- Shows the clusters to the manager for review.
- Allows the manager to edit, merge, split, remove, or add topics.
- Publishes the approved topics for team voting.

## Phase 4: Voting

Each team member receives exactly three votes.

- Multiple votes may be assigned to the same topic.
- All three votes may be assigned to one topic.
- Members may change their votes until voting closes.
- Topics are ranked by total votes.
- The ranked topics become the meeting agenda.

## Phase 5: Facilitated discussion

The facilitator works through the prioritized agenda and marks every topic as:

- Discussed
- Skipped
- Deferred

During the meeting, the facilitator can manually record:

- Notes
- Decisions
- Action items

Each action item can include a description, owner, and optional due date.

## Phase 6: Meeting upload and processing

After the meeting, the facilitator can upload:

- Audio
- Video
- Transcript files

The system:

1. Validates whether a usable transcript is available.
2. Generates a transcript from audio or video when necessary.
3. Associates transcript sections with discussion topics when possible.
4. Suggests:
   - Meeting notes
   - Decisions
   - Action items
   - Topic statuses
5. Requires the facilitator to review and approve suggestions before saving them as final.

Uploaded recordings and transcripts remain private to the project manager and facilitator in the MVP.

## Manager dashboard

The dashboard includes:

- Managed projects
- Member invitations
- Feedback-template editor
- Current round and deadline
- Submission participation
- Weekly feedback summary
- Topic-cluster review
- Voting progress
- Prioritized meeting agenda
- Meeting notes, decisions, and action items
- Previous weekly rounds

## MVP boundaries

Not included in the first version:

- Member accounts
- Individual member links
- Slack, Teams, Jira, or calendar integrations
- Performance ratings
- Dedicated peer-review workflows
- Live audio or video recording
- Automatic assignment of action-item owners
- Automated reminders for overdue actions
- Advanced trend analytics across multiple weeks
- Team access to raw feedback or the manager's private summary
- Fully automatic publication of AI-generated content

## MVP success criteria

The MVP succeeds when a manager can:

1. Create a project and invite members.
2. Run an automatic weekly feedback round.
3. Receive a useful private summary.
4. Turn feedback into editable discussion topics.
5. Let members prioritize topics using three votes each.
6. Facilitate and track the resulting discussion.
7. Upload a meeting recording or transcript.
8. Review and approve suggested notes, decisions, and action items.
