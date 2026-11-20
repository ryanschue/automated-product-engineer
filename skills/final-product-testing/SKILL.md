---
name: final-product-testing
description: Finalize a feature-complete pull request as a release candidate and publish durable repository-hosted walkthrough evidence. Use when asked to get a PR ready to ship, clear conflicts and review feedback, audit happy and unhappy paths, capture a comprehensive screenshot set or GIF, and leave a reusable validation record without merging.
---

# Final Product Testing

Use this skill after implementation is feature-complete. Pair it with `pr-workflow`, `pr-review`, and `manual-ui-qa`; this skill owns the release freeze and evidence contract rather than replacing their branch, review, or exploratory-QA guidance.

## Resolve the delivery target

- Inspect Git, the open pull request, and any stack before editing. Preserve existing ownership and do not create a duplicate implementation.
- If a stack exists, finalize the terminal pull request unless the user names another layer. Verify its exact base and keep earlier layers immutable.
- Never merge or release unless the user explicitly authorizes that action.
- Record the starting head, base, mergeability, checks, unresolved review threads, and automated-review status.

## Reach code freeze

1. Update from the exact requested base with the repository's preferred strategy. Resolve conflicts semantically and preserve both sides' contracts.
2. Review the pull request's remote diff, not only the local working tree.
3. Convert every accepted story into applicable happy-path, boundary, failure, stale-state, accessibility, and responsive checks.
4. Audit authorization, data scope, cache invalidation, optimistic rollback, concurrent actions, empty/loading/error states, keyboard behavior, and cross-surface state consistency.
5. Reproduce each real defect, add the smallest useful regression proof, fix it at the responsible boundary, and rerun focused checks.
6. Resolve actionable review threads with evidence. Batch changes before requesting another automated review and respect the repository's rereview limits.
7. Run required broad local gates only after behavior and design stabilize. Push, then wait for current-head remote checks and the required review result.

Code is frozen only when the worktree is clean, the pull request is mergeable, required gates pass, actionable feedback is resolved, and no known in-scope product defect remains.

## Plan evidence before capture

Create a numbered story/state matrix before opening the browser. Include the applicable set of:

- entry and orientation;
- primary happy path through completion;
- each decision or mutation before, during, and after persistence;
- validation, loading, empty, retry, permission, server failure, stale conflict, and rollback states;
- desktop, compact mobile, and breakpoint-stress layouts;
- long content, narrow widths, scrolling, focus, disabled controls, toasts, and overlap checks.

Prefer deterministic synthetic fixtures or request interception. Never expose production PII, secrets, or private customer data. Do not mutate shared staging data merely to manufacture evidence.

## Capture from the frozen build

- Start from fresh fixture state at the frozen commit and record the exact SHA, environment, viewport, and data mode.
- Use stable viewport sizes and ordered filenames such as `01-entry-desktop.png`.
- Watch browser console, network requests, and relevant server output throughout capture.
- Inspect every image for cropping, overflow, stale counts, duplicate content, overlays, and accidental sensitive data.
- If any product code changes after capture begins, discard the set and recapture from frame 01.
- When the user requests a full walkthrough, capture at least 20 purposeful frames without padding the set with near-duplicates.

## Package repository-hosted evidence

- Follow the repository's evidence convention; when none exists, use `docs/qa/<ticket>/final-walkthrough/`.
- Add a manifest or README mapping every frame to its user story, state, viewport, fixture provenance, and expected result.
- When requested, build one ordered GIF from the reviewed frames with readable text and useful pauses.
- Commit screenshots, GIF, and manifest to the pull-request branch. Embed authenticated repository URLs or repository-relative links in the pull-request body instead of an external hosting service.
- Verify the rendered assets from the pull-request page as an authenticated reviewer. For private repositories, do not treat an unauthenticated `raw.githubusercontent.com` 404 as proof that a committed asset is missing.

## Run the final release audit

Recheck:

- branch, head, base, and terminal-stack position;
- clean worktree and diff integrity;
- mergeability and unresolved conversations;
- local commands and exact results;
- remote CI, preview deployment, and automated-review result on the frozen head;
- rendered screenshot and GIF links;
- absence of PII, secrets, and temporary QA data;
- no merge or release without explicit authorization.

Report the pull-request URL, frozen commit, fixes made, validation, evidence paths, review status, blockers, and next human action.
