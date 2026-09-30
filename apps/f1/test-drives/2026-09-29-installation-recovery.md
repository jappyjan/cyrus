# Test Drive: Cyrus installation recovery

**Date:** 2026-09-29
**Goal:** Verify restored Claude installation through the actual Cyrus pipeline.
**Test Repo:** `/tmp/cyrus-recovery-f1-20260929`

## Verification Results

- PASS: fresh repository scaffolded and F1 server started at port 3600.
- PASS: `f1 ping`, issue creation (`issue-1`, DEF-1), session creation (`session-1`).
- PASS: repository routing elicitation handled with a selection prompt.
- PASS: native Claude started, assigned session `f9769ea6-53eb-4f00-9b78-20b865069800`, and produced actual assistant output.
- PASS: `view-session --limit 10 --offset 0` exposed six coherent timestamped activities, including a final response `CYRUS_RECOVERY_OK`.
- PASS: Claude emitted a success result; AgentSessionManager logged successful completion.
- PASS: test session stopped and the F1 server shut down gracefully.

## Final Retrospective

The restored locked dependency graph includes the Apple Silicon binary and successfully runs Claude through EdgeWorker. The CLI test issue retained its `active` transport status after receiving a response, so completion evidence is the real success result and response activity rather than that transport status. Routing initially required explicit repository selection because the scaffold has no matching label. The test repository has no remote, so GitService's local-branch fallback warning was expected. No production issue was used for this smoke test.
