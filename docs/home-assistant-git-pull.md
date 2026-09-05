# Home Assistant Git Pull deployment

The Home Assistant NUC is the deployment agent. It pulls the public GitHub repository locally; Git is not run on the Windows SMB share.

## Git Pull app settings

Use the official **Git pull** app with these values:

```yaml
repository: git@github.com:RensVerhagen/HomeAssistant.git
git_branch: main
git_command: reset
git_remote: origin
git_prune: false
auto_restart: false
repeat:
  active: true
  interval: 300
deployment_key_protocol: ed25519
```

Paste the dedicated private deploy key generated for this NUC into the app's `deployment_key` field. The matching public key is registered in GitHub as **Home Assistant NUC Git Pull (read-only)**. Do not commit or publish the private key.

Start with `auto_restart: false`. After the first successful pull and configuration check, enable automatic restart if desired. The app's `reset` mode is intentional: `main` is the source of truth and direct edits in `/config` should not be made during normal operation.

## Release flow

1. Create `feature/<description>` locally.
2. Commit and push the feature branch.
3. Open a pull request into `main`.
4. Wait for the required **Home Assistant configuration** check.
5. Squash-merge the pull request.
6. The NUC pulls `main` on its next polling cycle.

## Recovery

For a bad release, use GitHub's **Revert** action on the squash commit. The NUC will pull the resulting revert commit. For system-level recovery, use the existing Home Assistant backup system.