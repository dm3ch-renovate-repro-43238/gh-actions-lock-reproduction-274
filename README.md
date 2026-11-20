# gh-actions-lock IP allow list reproduction

Reproduces [github/gh-actions-lock#274](https://github.com/github/gh-actions-lock/issues/274)
and validates the fix in [github/gh-actions-lock#275](https://github.com/github/gh-actions-lock/pull/275).

The `verify` workflow runs on GitHub-hosted runners with the `GITHUB_TOKEN` of an
organization-owned repository. It checks out an immutable public commit whose `actions.lock`
records `aquasecurity/setup-trivy`, shows whether GitHub refuses the token for that
organization's IP allow list, then runs `gh actions-lock --verify` with the released
`v0.4.1` and with the fix, one after the other on the same runner.

Whether a runner is refused depends on the current allow list of the organization and on
the runner's IP address, so the job runs three times.
