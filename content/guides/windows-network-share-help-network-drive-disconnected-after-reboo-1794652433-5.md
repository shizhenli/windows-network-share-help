---
title: "Mapped Drive Disappears After Reboot: Restore the Persistent Connection"
description: "A mapped drive disappears after a restart. Follow these exact checks to interpret why the connection is not restored, verify the fix, and recover safely."
seo_title: "Network Drive Disconnected After Reboot: Fix the Mapped Drive That Won't Stay"
seo_description: "A mapped drive disappears after a restart. Follow these exact checks to interpret why the connection is not restored, verify the fix, and recover safely."
keywords:
  - "network drive disconnected after reboot"
date: 2026-11-15T19:17:45+08:00
publishDate: 2026-11-15T19:17:45+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You restart your PC, open File Explorer, and the mapped drive to the other LAN PC is gone, leaving you unsure whether the share or the mapping failed. This is the **network drive disconnected after reboot** step, and it needs a controlled diagnosis before you change anything.

## Check the mapping and its persistence

Open Command Prompt and run `net use`. If the drive letter is missing entirely, the mapping was not saved for this logon session. If it appears with a status like Unavailable or Disconnected, the mapping exists but the connection failed. That distinction matters: a missing entry points to persistence, while an unavailable entry points to connectivity or credentials.

## Check whether the share is reachable

Run `ping <remote-PC-name>` and then `net view \\<remote-PC-name>`. A successful ping but failed view means name resolution works and SMB is the problem. If ping fails, fix name resolution or the remote PC's network state first; remapping will not help.

## Check stored credentials

Open Credential Manager and look under Windows Credentials for the remote PC. A stale or wrong entry can cause the reconnect to fail silently. Remove only the entry for that host, then run `net use Z: \\<remote-PC-name>\<share> /persistent:yes` and enter the correct credentials when prompted.

## Verification test

Sign out and sign back in, then run `net use` again. The drive should show as Available with no reconnect error. Open the drive and create a small test file, then confirm it appears on the remote PC. If the drive returns but the file does not, the problem is share permissions, not persistence.

## Rollback note

If a change makes things worse, delete the mapping with `net use Z: /delete`, restore any credential you removed, and reconnect manually. Keep a note of the working command before experimenting. If the drive still vanishes after these checks,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact `net use` output.
