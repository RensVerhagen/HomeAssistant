# Contributing to this Home Assistant configuration

This is a public, personal Home Assistant configuration. Please keep all credentials, tokens, private keys, and identifying values out of Git. Use `!secret` references and update `secrets_dummy.yaml` only with harmless placeholders when a new secret key is needed.

## Branch workflow

- `main` is the production branch pulled by Home Assistant.
- Create work on a `feature/<short-description>` branch.
- Open a pull request into `main`.
- Wait for the **Home Assistant configuration** check to pass.
- Squash-merge the pull request.
- The Home Assistant Git pull app polls `main` and deploys the merged commit.

Do not edit tracked files directly on the Home Assistant host except during an emergency. If an emergency edit is unavoidable, copy it back into a feature branch immediately so Git remains authoritative.

## Local setup

The managed working copy is `C:\Workspace\HomeAssistant`. Git operations and all normal editing should happen there, not on the SMB share.

## Rollback

Revert the problematic squash commit on GitHub. The revert commit will be picked up by Home Assistant as the next production version. For an urgent recovery, use the Home Assistant backup system as the system-level recovery path.