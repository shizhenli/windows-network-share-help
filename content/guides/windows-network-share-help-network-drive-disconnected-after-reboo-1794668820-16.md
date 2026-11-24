---
title: "Network Drive Disconnected After Reboot: Diagnose the Persistent Mapping Failure"
description: "A mapped network drive disappears after a restart. Diagnose the persistent connection failure with exact checks, a verification test, and a rollback note."
seo_title: "Network Drive Disconnected After Reboot: Fix the Persistent Mapping"
seo_description: "A mapped network drive disappears after a restart. Diagnose the persistent connection failure with exact checks, a verification test, and a rollback note."
keywords:
  - "network drive disconnected after reboot"
date: 2026-11-24T11:12:00+08:00
publishDate: 2026-11-24T11:12:00+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You mapped a shared folder from another LAN PC, but after restarting Windows the drive letter is gone and you are stuck before you can complete a controlled diagnosis.

## Confirm the mapping is actually persistent

Open Command Prompt and run `net use`. If the drive is listed with a status of Unavailable or Disconnected, the mapping exists but cannot reconnect. If it is absent entirely, the mapping was created without persistence. In that case, remove it with `net use Z: /delete` and recreate it using `net use Z: \\PC-NAME\Share /persistent:yes`, replacing Z: and the share path with your values. Reboot and check `net use` again. A listed drive with no error means persistence is fixed; an Unavailable entry means the problem is reconnection, not persistence.

## Check credential and network timing

If the entry returns as Unavailable, open Credential Manager and confirm a Windows credential exists for the remote PC name. Delete stale entries for that host, then reconnect and enter the password when prompted. Next, verify the remote PC is reachable before Windows tries to map the drive: ping the host name, then the IP address. A host name that fails while the IP succeeds points to name resolution at boot. This is a common cause of a **network drive disconnected after reboot** and is fixed by using the IP in the mapping or correcting name resolution.

## Verification test

Run `net use Z: /delete`, recreate the mapping with `/persistent:yes`, reboot, and immediately run `net use`. The drive should show as OK with no reconnect prompt. Open it in File Explorer and create a test folder to confirm write access.

## Rollback note

If the new mapping fails, delete it and restore your previous mapping command. Keep a note of the original share path so you can revert without losing access. For guided diagnosis,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).
