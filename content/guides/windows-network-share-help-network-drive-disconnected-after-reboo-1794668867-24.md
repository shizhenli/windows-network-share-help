---
title: "Network Drive Disconnected After Reboot: Fix the Lost Mapping"
description: "A mapped drive disappears after a restart. Follow these checks to diagnose the lost connection and restore the expected mapping."
seo_title: "Network Drive Disconnected After Reboot: Restore the Mapping"
seo_description: "A mapped drive disappears after a restart. Follow these checks to diagnose the lost connection and restore the expected mapping."
keywords:
  - "network drive disconnected after reboot"
date: 2026-11-25T11:11:49+08:00
publishDate: 2026-11-25T11:11:49+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You mapped a shared folder from another LAN PC, but after restarting Windows the drive letter is gone from File Explorer.

## Check the Mapping Persistence Setting

Open Command Prompt and run `net use`. If the drive is listed but marked unavailable, the mapping exists but the connection failed. If it is absent entirely, Windows did not save it. Next, open File Explorer, right-click the mapped drive if present, and choose Disconnect, then remap it with Reconnect at sign-in checked. If the option is greyed out, the mapping was created without persistence.

## Confirm the Share Is Reachable at Boot

Run `ping <remote-PC-name>` and then `net view \\<remote-PC-name>`. A successful ping but failed net view points to SMB or credential timing, not the network. If the remote PC boots slower than yours, the mapping can fail before the share is online. This is a common cause of a **network drive disconnected after reboot**.

## Verification Test

Restart both PCs, wait two minutes after the remote PC finishes booting, then sign in locally. Open File Explorer and double-click the mapped drive. If it opens without a prompt, the fix holds. If it still fails, run `net use Z: \\<remote-PC>\<share> /persistent:yes` and repeat the restart test.

## Rollback Note

If remapping causes errors, run `net use Z: /delete` to remove the broken entry, then recreate it manually. Keep a note of the original share path so you can restore it.

If the drive still vanishes,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with your `net use` output and the remote PC name.
