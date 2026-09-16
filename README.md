# DeepSeek Harness Desktop Builder

This repository periodically builds the Windows x64 desktop installer from the
latest `deepseek-ai/deepseek-harness` `master` revision and publishes it as a
GitHub prerelease.

## How it works

- GitHub Actions runs every six hours or on manual dispatch.
- The upstream commit is used as the immutable release tag (`upstream-<sha>`).
- A revision that already has a release is skipped, so scheduled runs are safe
  to repeat.
- The unsigned installer is uploaded to the GitHub Release for that revision.

## First run

Open **Actions → Build DeepSeek Harness Desktop (Windows) → Run workflow**.
The workflow needs no repository secrets. GitHub's automatically provided
`GITHUB_TOKEN` is used to create the prerelease.

## Important limitations

Builds are unsigned. Windows SmartScreen may show a warning, and this workflow
does not configure electron-updater in the upstream application. A signed
production channel requires a code-signing certificate and a separately
configured update origin.
