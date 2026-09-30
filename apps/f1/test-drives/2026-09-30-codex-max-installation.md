# Test Drive: Cyrus upstream update and Codex max reasoning

**Date:** 2026-09-30
**Commit:** 7d83b3ec, with local @openai/codex dependency updated to 0.159.0
**Behavior:** Codex subscription inference with gpt-6.1-sol at max reasoning through EdgeWorker.
**Test repo:** /tmp/cyrus-codex-upgrade-20260930

## Results

- Original bundled CLI 0.144.4 reproduced the exact unsupported-model HTTP 400; installed CLI 0.159.0 completed the same inference with the same account.
- Updated original upstream Cyrus from 0.2.69 to 0.2.73; full workspace build passed.
- Codex runner suite: 12 files, 69 tests passed.
- Cyrus-only CODEX_HOME config resolves gpt-6.1-sol / max; general Codex config remains medium.
- F1 launched with Node, matching the production daemon runtime, port 3600, CYRUS_DEFAULT_RUNNER=codex, CODEX_MODEL=gpt-6.1-sol, CODEX_HOME=/Users/jappy/.cyrus/codex-home.
- Created issue-1 / DEF-1 with explicit [repo=f1-test/primary-repo] routing; started session-1.
- Timeline contained timestamped routing, codex/gpt-6.1-sol model selection, and final response CYRUS_CODEX_MAX_OK. Real inference completed without the unsupported-model error.
- Session stopped and temporary F1 server shut down after verification.
- Production /version returned 0.2.73 and /status returned idle after restart. Configuration and persisted session state backed up; shutdown logged successful state save.

## Limitations

The first F1 attempt launched under Bun failed during Codex app-server launch; the Node runtime used by production completed successfully. Test repository has no origin; local-branch fallback was expected. No production ticket was used or resumed by this smoke test. Upstream dependency audit still reports six advisories (four moderate, two high); the prior version had 24. No unrelated security remediation was performed.
