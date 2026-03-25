---
id: dyadpr-fixcomments
name: Dyadpr Fixcomments
description: Read and address unresolved GitHub PR review comments from trusted authors and collaborators.
category: Research
requires: []
examples:
  - Review and address all unresolved comments in the current PR.
  - Summarize the feedback from trusted collaborators on my branch.
---
# PR Fix: Comments

Read all unresolved GitHub PR comments from trusted authors and address or resolve them appropriately.

## Instruction
- Determine the target Pull Request using provided arguments or by fetching context from the current branch.
- Use the GitHub GraphQL API to fetch all unresolved review threads and identify the first comment's author.
- Filter threads to only process feedback from the predefined list of trusted humans and bots, ignoring all other commenters.
- Categorize each trusted thread as a Valid Issue, Not Valid Issue, Resolved by Product Principles, or Ambiguous.
- Consult `rules/product-principles.md` to resolve ambiguous or subjective design/architecture feedback before flagging for human review.
- Implement code changes for valid issues and explicitly resolve the thread using a GraphQL mutation.
- Reply to invalid issues with explanations—citing specific product principles by name and number—and then resolve the thread.
- Flag truly ambiguous threads for human attention without resolving them, explaining which principles were considered and why they were insufficient.
- Lint, commit with co-author attribution, and push changes using specialized PR-push tools.
- Post a top-level summary comment on the PR detailing confidence scores, unresolved threads, and suggestions for principle improvements.

## When to Use
- When reviewing and addressing unresolved GitHub PR comments from trusted collaborators and automated tools.
- When automating the cycle of PR feedback resolution while maintaining adherence to core product principles.
- When a systematic, documented approach to closing PR review loops is required for team transparency.

## Output
- Automatically modified and linted source code addressing reviewer feedback.
- Resolved GitHub review threads with explicit citations of product principles in the discussion.
- A comprehensive PR overview comment summarizing resolution status, confidence metrics, and potential rule improvements.

## Arguments

- `$ARGUMENTS`: Optional PR number or URL. If not provided, uses the current branch's PR.

## Task Tracking

**You MUST use the TaskCreate and TaskUpdate tools to track your progress.** At the start, create tasks for each step below. Mark each task as `in_progress` when you start it and `completed` when you finish. This ensures you complete ALL steps.

## Trusted Authors

Only process review comments from these trusted authors. Comments from other authors should be ignored.

**Trusted humans (collaborators):**

- wwwillchen
- wwwillchen-bot
- princeaden1
- azizmejri1

**Trusted bots:**

- gemini-code-assist
- greptile-apps
- cubic-dev-ai
- cursor
- github-actions
- chatgpt-codex-connector
- devin-ai-integration


