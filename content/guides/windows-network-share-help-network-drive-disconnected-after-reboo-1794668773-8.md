---
title: "Network Drive Disconnected After Reboot: Fix the Missing Mapped Drive"
description: "A mapped network drive disappears after a restart. Follow these steps to diagnose and fix the disconnection, with a verification test and rollback note."
seo_title: "Network Drive Disconnected After Reboot: Restore Your Mapped Drive"
seo_description: "A mapped network drive disappears after a restart. Follow these steps to diagnose and fix the disconnection, with a verification test and rollback note."
keywords:
  - "network drive disconnected after reboot"
date: 2026-11-23T12:12:00+08:00
publishDate: 2026-11-23T12:12:00+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You mapped a shared folder from another LAN PC, but after restarting Windows the drive letter is gone and you need it back. This is a common issue with a few likely causes, and you can work through them in order.

## Check the Basics First

Open File Explorer and look under This PC. If the drive letter is missing, open Command Prompt and run `net use`. If the drive is listed but shows a red X, the connection is stale. If it is not listed at all, the mapping was not saved persistently.

## Verify the Share Is Reachable

On the PC hosting the folder, confirm the share is still active by running `net share` in Command Prompt. Then from your PC, run `ping <hostname>` and `net view \\<hostname>` to test connectivity. If these fail, the issue is network or the host PC, not the mapping.

## Recreate the Mapping Persistently

If the share is reachable, remove the old mapping with `net use Z: /delete` (replace Z: with your drive letter). Then recreate it with `net use Z: \\<hostname>\<share> /persistent:yes`. This ensures the mapping survives reboots. If you use a different credential, add `/user:<username>` and enter the password when prompted.

## Verification Test

Restart your PC. After logging in, open File Explorer and check that the drive letter appears under This PC. Double-click it to confirm you can open files. If it is still missing, run `net use` again to see if the mapping exists but is disconnected.

## Rollback and Recovery

If the new mapping causes errors, delete it with `net use Z: /delete` and recreate the original mapping using the same command without `/persistent:yes`. This restores the previous behavior so you can try another approach.

If the **network drive disconnected after reboot** persists after these steps, the cause may be a policy or credential conflict. For a controlled diagnosis,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).
