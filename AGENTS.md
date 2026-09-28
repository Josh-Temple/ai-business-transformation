# AGENTS.md

## Deployment rule

Git/Vercel automatic deployment is intentionally disabled for this repository.

For every task that changes public-facing site content or behavior:

1. Complete and verify the task first.
2. Treat deployment as a separate final decision.
3. Default to `HOLD`.
4. Use `DEPLOY` only when the repository state is coherent and materially worth publishing.
5. Never deploy merely because a commit or merge occurred.
6. When `DEPLOY` is justified, deploy the exact intended `main` commit manually and verify production afterward.

Read `docs/DEPLOYMENT_POLICY.md` for the full decision criteria and release procedure.
