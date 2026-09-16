# DeepSeek Harness Desktop Builder

This repository periodically builds the Windows x64 desktop installer from the
latest `dsh-v*` release tag from `deepseek-ai/deepseek-harness` and publishes
it as a GitHub prerelease.

## How it works

- GitHub Actions runs every six hours or on manual dispatch.
- The newest upstream `dsh-v*` tag is checked out and used as the release
  identity (`upstream-dsh-v...`).
- A tag that already has a release is skipped, so scheduled runs are safe
  to repeat.
- The unsigned installer is uploaded to the GitHub Release for that revision.
- The same updater files are mirrored to GitHub Pages under
  `_/harness/desktop/stable/win-x64/` for the experimental in-app update
  channel.
- The workflow applies a temporary compatibility patch for an upstream stale
  `fs-ext` smoke check; the upstream runtime has already migrated away from
  that dependency.

## First run

Open **Actions → Build DeepSeek Harness Desktop (Windows) → Run workflow**.
The workflow needs no repository secrets. GitHub's automatically provided
`GITHUB_TOKEN` is used to create the prerelease.

## Important limitations

Builds are unsigned. Windows SmartScreen may show a warning, and the
GitHub-Pages updater channel is experimental because electron-updater may reject
unsigned packages. A signed production channel requires a code-signing
certificate.
