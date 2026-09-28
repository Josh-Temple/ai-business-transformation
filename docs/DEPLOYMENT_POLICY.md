# Deployment Policy

Updated: 2026-09-29
Status: Active repository policy

## Purpose

This repository does not deploy automatically from Git pushes or merges.

Deployment is a separate release decision. Work may be committed and merged without changing the public site.

## Default

Default decision: `HOLD`.

Do not deploy only because:
- a commit was created;
- a pull request was merged;
- internal documentation changed;
- research notes were added;
- an intermediate implementation step completed.

## DEPLOY criteria

A task may end with `deployment_decision: DEPLOY` only when all of the following are true:

1. The change materially improves or fixes the public-facing site.
2. The intended task scope is complete enough to publish as one coherent state.
3. No known blocking WIP, broken primary navigation, or obviously incomplete public copy remains in the changed scope.
4. The exact commit to publish is identifiable and is the intended production source.
5. A production deployment can be verified after release.

If any item is uncertain, use `HOLD`.

## HOLD examples

Use `deployment_decision: HOLD` for:
- partial case-study work;
- draft copy;
- research or evidence gathering;
- internal refactors with no publication need;
- multiple changes that should be released together later;
- unresolved verification findings;
- changes where the public benefit is too small to justify a release.

## Manual deployment procedure

When the task decision is `DEPLOY`:

1. Confirm the intended changes are on `main`.
2. Record the exact `main` commit SHA.
3. Trigger one manual production deployment through Vercel.
4. Verify the production deployment reaches `READY`.
5. Open the production URL and verify the primary page and changed user-facing path.
6. Record the release result, including commit SHA and production URL.

Do not re-enable Git automatic deployment as part of an ordinary content or implementation task.

## Task completion record

For tasks that can affect the public site, end with one of:

```
deployment_decision: DEPLOY
deployment_reason: <why this state is ready for public release>
```

or

```
deployment_decision: HOLD
deployment_reason: <why publication should wait>
```

The deployment decision is operational. It does not replace content review, evidence review, or code verification.
