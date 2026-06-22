# Contribution 2488: Keep Action up to Date in Docs

**Contribution Number:** 1
**Student:** Siyam Seid
**Issue:** https://github.com/release-plz/release-plz/issues/2488
**Existing PR for this issue:** https://github.com/release-plz/release-plz/pull/2782 (opened by another contributor, mvanhorn)
**Status:** Phase III & IV — Investigation, reproduction, plan, and independent verification of the proposed fix complete. No new PR submitted because the issue is already addressed by an open upstream PR (see Pull Request section).

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

- **Source reviewed for reproduction:** `website/docs/github/security.md` (pinning guidance) and `website/docs/github/update.md` (currently Dependabot-only update guidance) in the local fork clone.
- **Screenshots/logs:** Optional for this docs issue; text evidence from the two docs pages above is sufficient.
- **My findings:** The issue is reproducible as a documentation gap/inconsistency: pinning to a commit SHA is explained in `security.md`, but it is not clearly paired with "keep the pinned action updated automatically." The dedicated update page (`update.md`) only documents Dependabot, even though the issue notes the maintainers use Renovate.
- **Additional finding (key for this contribution):** While preparing to implement the fix, I discovered that another contributor (mvanhorn) had already opened PR #2782, which addresses the same issue by updating the pinned example in `security.md` and adding a tip recommending Renovate or Dependabot. The maintainer (marcoieni) replied questioning whether those tools can actually keep a pinned commit SHA up to date. I redirected my effort to independently verifying that question (see Pull Request section).

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

### Week 1 Progress (Phases I–II)

Selected issue #2488 and reviewed scope.
Reproduced the documentation mismatch across `security.md` and `update.md`.
Mapped affected docs pages and drafted the solution plan with the UMPIRE structure.

### Week 2 Progress (Phase III)

Forked and cloned the repository; created the branch `fix-issue-keep-action-up-to-date-in-docs`.
While starting implementation, found that PR #2782 already implements the `security.md` portion of my plan, so re-doing it would be a duplicate PR (which maintainers close).
Identified that `update.md` (Dependabot-only) is still untouched by #2782 and is the remaining gap, but held off on a competing/overlapping PR while #2782 is in active review for the same issue.

### Week 2 Progress (Phase IV — verification instead of duplicate submission)

The maintainer (marcoieni) asked on PR #2782 whether Renovate/Dependabot can really keep a **pinned commit SHA** current. I independently verified this and confirmed it works, with the key requirement being the trailing `# vX.Y.Z` version comment next to the SHA:

- **Dependabot** has updated SHA-pinned actions and their version comments natively since Oct 2022 — [GitHub Changelog](https://github.blog/changelog/2022-10-31-dependabot-now-updates-comments-in-github-actions-workflows-referencing-action-versions/), [dependabot-core PR #5951](https://github.com/dependabot/dependabot-core/pull/5951).
- **Renovate** does it via the `helpers:pinGitHubActionDigestsToSemver` preset — [Renovate GitHub Actions docs](https://docs.renovatebot.com/modules/manager/github-actions/).
- **Real-world example:** crates.io (already linked in the existing `security.md`) uses Renovate for exactly this pattern.
- **Caveat:** It only works when the `# vX.Y.Z` comment is present and well-formed (known edge cases: Renovate [suffixed tags issue #35789](https://github.com/renovatebot/renovate/issues/35789); Dependabot [won't fix an already-wrong comment, issue #7912](https://github.com/dependabot/dependabot-core/issues/7912)).

### Code Changes

- **Files reviewed/planned:** `website/docs/github/security.md`, `website/docs/github/update.md`
- **Branch:** `fix-issue-keep-action-up-to-date-in-docs` (synced with upstream; no doc edits committed, since the fix was superseded by PR #2782)
- **Outcome decision:** Rather than push a duplicate of PR #2782, my contribution for this cycle was investigating, reproducing, and independently verifying the proposed solution against the maintainer's open question.

---

## Pull Request

**PR Link:** No new PR submitted by me. The issue is already addressed by an existing upstream PR: https://github.com/release-plz/release-plz/pull/2782 (author: mvanhorn).

**Why no new PR:** PR #2782 implements the same `security.md` change I had planned (refresh the pinned example + add a Renovate/Dependabot tip). Opening a second PR for the same scope would be a duplicate, which is poor open-source etiquette and typically gets closed. Out of respect for the active review on #2782, I did not open a competing or overlapping PR.

**My contribution this cycle:** Independent verification of the maintainer's open question on #2782 — whether Renovate/Dependabot can actually keep a pinned commit SHA updated. I confirmed they can (with sourced evidence and the `# vX.Y.Z` comment caveat documented in the Week 2 Phase IV notes above).

**Summary of what I contributed:** Issue selection, reproduction of the docs gap, a UMPIRE solution plan, and a sourced confirmation that the proposed Renovate/Dependabot approach is technically correct.

**Maintainer Feedback / Next steps:** PR #2782 is awaiting maintainer decision. If it stalls, the remaining clean, non-duplicate follow-up would be updating `update.md` to add Renovate alongside Dependabot.

**Status:** Investigation & verification complete; issue addressed by existing PR #2782 (awaiting maintainer review upstream).

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

I would check the issue's linked/related pull requests **before** planning the implementation, so I notice early if another contributor is already working on it. Discovering PR #2782 mid-implementation taught me to scan for existing work first to avoid duplicate effort.

I would also create a short traceability table earlier: issue requirement -> target file -> planned edit.

### Open-Source Etiquette Learned

When an issue already has an active PR, the higher-value move is often to engage with that work (verify it, add evidence, review) rather than open a competing duplicate PR. I practiced this by independently verifying the maintainer's open technical question on #2782.

---

## Resources Used

- Issue: https://github.com/release-plz/release-plz/issues/2488
- Existing PR: https://github.com/release-plz/release-plz/pull/2782
- CONTRIBUTING.md
- `website/docs/github/security.md`
- `website/docs/github/update.md`
- Verification — Dependabot SHA comment support: https://github.blog/changelog/2022-10-31-dependabot-now-updates-comments-in-github-actions-workflows-referencing-action-versions/
- Verification — Renovate GitHub Actions manager: https://docs.renovatebot.com/modules/manager/github-actions/
