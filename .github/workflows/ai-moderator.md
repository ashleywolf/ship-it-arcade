---
description: "AI-powered content moderation for issues and comments"
on:
  issues:
    types: [opened, edited]
  issue_comment:
    types: [created, edited]
permissions:
  contents: read
safe-outputs:
  add-comment:
  add-labels:
  create-issue:
  update-issue:
---

# AI Moderator Workflow

## Description

Automatically moderate issues and issue comments to maintain a healthy, welcoming community. This workflow monitors new issues and issue comments for content that violates project guidelines.

## Triggers

- `issues: [opened, edited]`
- `issue_comment: [created, edited]`

## Detection Categories

### Spam
Detect self-promotion, cryptocurrency scams, unrelated commercial links, SEO spam, and repetitive unsolicited content.

### Toxicity
Detect personal attacks, harassment, hate speech, bullying, threats, slurs, and deliberately hostile or intimidating language.

### Off-topic
Detect content that is clearly unrelated to the project scope, purpose, or technical domain.

### Guideline Violations
Detect any content that violates the project's CODE_OF_CONDUCT.md or CONTRIBUTING.md guidelines.

## Steps

1. **Read project guidelines** — Read `CODE_OF_CONDUCT.md` and `CONTRIBUTING.md` from the repository root to understand the community standards and contribution expectations.

2. **Fetch content** — Retrieve the full text of the new or edited issue or issue comment that triggered the workflow.

3. **Evaluate content** — Analyze the content against all four detection categories (spam, toxicity, off-topic, guideline violations). Consider context, intent, and severity.

4. **Apply labels** — Based on the evaluation, apply exactly one of the following labels to the issue:
   - `moderation/approved` — Content is appropriate and follows all guidelines
   - `moderation/flagged` — Content needs human review (borderline cases)
   - `moderation/spam` — Content is spam or self-promotion
   - `moderation/toxic` — Content contains toxic, harmful, or harassing language

5. **Comment on flagged content** — If the content is flagged, spam, or toxic, add a comment to the issue explaining:
   - Which category the content was flagged under
   - A brief, respectful explanation of why it was flagged
   - A reference to the relevant section of CODE_OF_CONDUCT.md or CONTRIBUTING.md
   - A note that a human maintainer will review the decision

6. **Create summary report** — Create or update a summary issue titled `[AI Moderator Report]` that tracks all moderation actions taken, including:
   - Issue/comment number and link
   - Detection category
   - Action taken (label applied)
   - Timestamp
