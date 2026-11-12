# Podglance

A small, fast macOS app for browsing Kubernetes clusters on AWS EKS: namespaces, pods,
deployments and Helm releases, with live logs, Helm history and rollback.

This repository only holds the **releases**. The source code is at
[ace53thntu/podglance](https://github.com/ace53thntu/podglance).

## Install

**One line in Terminal** (recommended; macOS doesn't block an app installed this way):

```shell
curl -fsSL https://github.com/ace53thntu/podglance-releases/releases/latest/download/install.sh | sh
```

It downloads the latest release and checks its SHA-256 checksum, app identity, version and code
signature before installing. Podglance goes into `/Applications`, or `~/Applications` if
`/Applications` isn't writable.

**Or with the disk image:** download
[Podglance-darwin-arm64.dmg](https://github.com/ace53thntu/podglance-releases/releases/latest/download/Podglance-darwin-arm64.dmg),
open it and drag Podglance into Applications. Podglance isn't notarized by Apple yet, so the first
time macOS refuses to open it. Go to **System Settings → Privacy & Security** and click
**Open Anyway**.

### Requirements

- A Mac with Apple Silicon (M1 or later), macOS 11 Big Sur or newer.
- `kubectl`, plus `aws-iam-authenticator` or the AWS CLI for EKS sign-in.
- `helm` for Helm releases, and `aws-azure-login` if your company signs in to AWS through Azure AD.

Settings → Tools shows which of these are missing and how to install each one.

## Updates

From 1.0.1 on, Podglance updates itself:

- It checks for a new version every 2 hours and downloads it in the background.
- Before installing, it checks the download's signature and checksum. An update not signed with
  Podglance's key is refused.
- The new version installs when you click **Relaunch to Update Podglance**, or when you quit.
- Turn this off, or check right away, in **Settings → Updates**.

**Upgrading from 1.0.0:** install 1.0.1 once by hand with one of the methods above, because 1.0.0
has no updater.

## What's in a release

| File | What it is |
|---|---|
| `Podglance-<version>-darwin-arm64.dmg` | Disk image for that version |
| `Podglance-darwin-arm64.dmg` | The same disk image under a name that never changes (always the latest) |
| `Podglance-<version>-darwin-arm64.zip` | The app that the in-app updater downloads |
| `podglance-update.json` | Update feed: version, file, size, SHA-256 and signature |
| `install.sh` | The one-line installer |

The changes in each version are in its [release notes](https://github.com/ace53thntu/podglance-releases/releases).

## Getting started

1. Open Podglance. It reads every kubeconfig file in `~/.kube`. You can pick another folder, or
   add single files, in **Settings → Kubeconfig files**.
2. Click a cluster in the left bar. If it needs a sign-in, Podglance runs it for you.
3. Browse namespaces, pods, deployments and Helm releases. Logs follow new lines live and can open
   in their own window.

Podglance only reads from your clusters. The only actions that change anything are a Helm
rollback and the fixes for releases stuck in `pending-install` / `pending-upgrade`, and each one
asks you to confirm first.

## Uninstall

Quit Podglance, then delete `Podglance.app` from Applications. To also remove its settings, delete
`~/Library/Application Support/Podglance`. Your kubeconfig files are never changed.

## Licence

Podglance is open source under the [MIT licence](https://github.com/ace53thntu/podglance/blob/main/LICENSE).
Licences of the libraries it uses are in the app under **Settings → About → Open-source licences**.
Kubernetes is a registered trademark of The Linux Foundation. Podglance isn't affiliated with or
endorsed by it, AWS or Microsoft.
