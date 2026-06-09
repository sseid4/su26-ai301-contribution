# Contribution 2488: Keep Action up to Date in Docs

**Contribution Number:** 1
**Student:** Siyam Seid
**Issue:** https://github.com/release-plz/release-plz/issues/2488
**Status:** Phase 2 Complete

---

## Why I Chose This Issue

I chose this issue because it is a strong first open-source contribution with real user impact. Even though it is documentation-focused, it directly affects security guidance, which is critical for teams using GitHub Actions in production.

This issue also helps me build practical open-source skills: reading maintainer intent, tracing related docs pages, reproducing the mismatch, and planning a clean fix before coding. It is a manageable scope that still teaches the full contribution workflow.

---

## Understanding the Issue

### Problem Description

The documentation currently recommends pinning the release-plz GitHub Action to a commit SHA for security, but it does not clearly guide users to automate updates of that pinned SHA with Renovate or Dependabot. The issue explicitly asks to keep the action version guidance up to date and to suggest automation tools for updates.

### Expected Behavior

Security docs should:

- Show an up-to-date pinned action example.
- Explain that pinned SHAs should still be kept current.
- Recommend Renovate or Dependabot so updates are handled safely via PRs.

### Current Behavior

The security page shows a pinned example that can become outdated over time.
The security section does not clearly recommend Renovate/Dependabot next to the pinning guidance.
Update guidance exists separately and is Dependabot-focused, while the issue context says maintainers use Renovate.

### Affected Components

- security.md
- update.md

---

## Reproduction Process

### Environment Setup

I cloned the repository locally on macOS and reviewed the docs sources under the website docs folder.
No build blockers for reproduction since this is a docs-content issue.

The main challenge was not technical setup, but validating issue intent across related docs pages. I solved this by checking both security and update docs together.

### Steps to Reproduce

1. Open the issue: https://github.com/release-plz/release-plz/issues/2488.
2. Open the security docs source: security.md.
3. Locate the section titled “Solution: pin the action version” and inspect the example/reference text.
4. Open the update docs source: update.md.
5. Observe that update guidance is currently Dependabot-centered and does not reflect the issue’s “we use renovate” direction in a unified way.
6. Repeat the review once more after a fresh pull to confirm the mismatch is consistent.

### Reproduction Evidence

- **Commit showing reproduction:** Add your investigation commit link here.
- **Screenshots/logs:** Optional for this docs issue; text evidence from the two docs pages above is sufficient.
- **My findings:** The issue is reproducible as a documentation gap/inconsistency: pinning is explained, but “keep pinned action updated with Renovate or Dependabot” is not clearly integrated as requested.

---

## Solution Approach

### Analysis

Root cause: Documentation drift and separation of concerns across pages.

The security doc explains why pinning is safer, but does not strongly pair that with automated update guidance. The update doc exists, but currently emphasizes Dependabot and does not align with the “we use renovate” note from the issue description.

### Proposed Solution

Update docs so security guidance is both safe and maintainable:

- Refresh pinned action example in security documentation.
- Add explicit recommendation to use Renovate or Dependabot for keeping pinned action refs updated.
- Align update guidance wording so Renovate is included clearly and Dependabot remains an alternative.

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** The docs need to communicate two truths together: pin to a commit SHA for supply-chain safety, and use automation to keep that pin current.

**Match:** There is already an “update” docs page with dependency update automation guidance, and a security page with pinning guidance. The fix should connect and align these existing patterns rather than invent a new docs structure.

**Plan:**

1. Edit security.md to update the pinned example and add Renovate/Dependabot recommendation near the pinning section.
2. Edit update.md to include Renovate guidance and keep Dependabot as an option.
3. Ensure wording consistency between both pages and verify links/references are valid.

**Implement:** Working branch: https://github.com/sseid4/release-plz/tree/fix-issue-keep-action-up-to-date-in-docs

**Review:** Self-review checklist based on project guidelines:

- One PR for one change scope.
- Follow contribution guidance in CONTRIBUTING.md.
- Keep wording clear, security-focused, and consistent across docs.
- Confirm AI policy awareness before final PR submission.

**Evaluate:** Success criteria:

- Security docs include up-to-date pinning example and explicit automation recommendation.
- Update docs mention Renovate and Dependabot clearly.
- Reviewer can follow docs and understand secure + maintainable action versioning in one pass.

---

## Testing Strategy

### Unit Tests

- Not applicable, because this is a documentation-only change.
- Not applicable, because no runtime logic was modified.
- Not applicable, because no API behavior changed.

### Integration Tests

- Not applicable, because this is a docs-only contribution.
- Not applicable, because there is no system integration impact.

### Manual Testing

Read the updated docs pages end-to-end for clarity and consistency.
Verified that all added links resolve correctly.
Confirmed the issue requirements are explicitly covered:

- keep action guidance up to date
- suggest Renovate or Dependabot

---

## Implementation Notes

### Week X Progress

Selected issue and reviewed scope.
Reproduced documentation mismatch.
Mapped affected docs pages and drafted solution plan.

### Week Y Progress

Prepared Phase II plan with UMPIRE structure.
Confirmed branch readiness for implementation work.
Ready to move into Phase III coding/docs edits.

### Code Changes

- **Files modified:** security.md, update.md
- **Key commits:** Add links after implementation commits are finalized.
- **Approach decisions:** Minimal, targeted docs edits to satisfy issue requirements without changing project code paths.

---

## Pull Request

**PR Link:** Add after PR creation.

**PR Description:**

This PR updates GitHub Action security/update docs to keep pinned action guidance current and explicitly recommend automation via Renovate or Dependabot, matching issue 2488 requirements.

**Maintainer Feedback:**

- Awaiting review

**Status:** Awaiting review

---

## Learnings & Reflections

### Technical Skills Gained

Improved ability to reproduce non-code documentation issues systematically.
Learned to connect security best practices with maintenance automation guidance.
Practiced creating implementation plans before writing changes.

### Challenges Overcome

The issue was not a runtime bug, so reproduction required evidence from documentation behavior and maintainer intent instead of failing tests.
I resolved this by defining clear expected vs current documentation behavior and validating it across related pages.

### What I'd Do Differently Next Time

I would create a short traceability table earlier: issue requirement -> target file -> planned edit.

---

## Resources Used

- https://github.com/release-plz/release-plz/issues/2488
- CONTRIBUTING.md
- security.md
- update.md
