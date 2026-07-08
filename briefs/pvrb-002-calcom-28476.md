# PVRB-002: Cal.com PR #28476

## Purpose
This brief organizes possible review focus areas for a public pull request.

It is not an official review and is not affiliated with the target project.

## PR
Repository: calcom/cal.com

PR: #28476

PR URL: https://github.com/calcom/cal.com/pull/28476

PR Type: Bug fix / Email / Booking flow

## PR Summary
This PR appears to address time format fallback behavior across booking-related email flows.

The review focus is whether fallback behavior stays consistent across attendee, organizer, reschedule, cancel, seated booking, workflow email, and template rendering paths.

## Must-Review Changes
- Fallback behavior for attendee and organizer `timeFormat`.
- Consistency across reschedule, cancel, seated booking, and workflow emails.
- Type boundary around `TimeFormat`.
- Logic differences between template class implementations and React component implementations.
- Possible side effects on fields near `timeFormat`, such as recurring event count.

## Potentially Missed Risks
- Reviewers may want to check whether attendee and organizer emails use the same fallback rule.
- Reviewers may want to check whether all email paths are covered.
- Reviewers may want to check whether invalid or missing `TimeFormat` values are handled consistently.
- Reviewers may want to compare class-based templates and React components for logic drift.
- Reviewers may want to check adjacent email fields for unintended side effects.

## Impact Areas
- Booking confirmation emails.
- Reschedule and cancel emails.
- Seated booking emails.
- Workflow-triggered emails.
- Email template rendering consistency.
- User trust in displayed booking time.

## Test Focus
- Attendee and organizer emails with missing `timeFormat`.
- Reschedule and cancel flows.
- Seated booking emails.
- Workflow email rendering.
- Invalid or undefined `TimeFormat` values.
- Regression checks for recurring event count and adjacent email fields.

## Docs / README Update Needed
Probably no, unless user-facing time format behavior is documented.

If fallback behavior is part of expected product behavior, internal documentation or test documentation may be useful.

## Questions for Reviewer
- Are all email rendering paths using the same fallback rule?
- Are class-based templates and React components aligned?
- What is the expected behavior when `timeFormat` is missing or invalid?
- Are seated booking and workflow email cases covered by tests?
- Did changes near `timeFormat` affect recurring event count or adjacent fields?

## Existing Review Coverage
Existing AI review bot overlap appears meaningful.

The unique value of this brief depends on whether it stays shorter, more focused, and better at cross-path consistency risks.

## Noise Check
Medium.

The brief is relevant, but some points may overlap with existing AI review comments or obvious review concerns.

## Decision
Published Candidate
