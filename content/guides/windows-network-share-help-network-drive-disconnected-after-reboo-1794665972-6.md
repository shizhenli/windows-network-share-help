---
title: "Network Drive Disconnected After Reboot: Restore the Persistent Mapped Drive"
description: "A mapped drive disappears after a restart. Follow these controlled checks to confirm whether the mapping is non-persistent, then restore the expected connection."
seo_title: "Network Drive Disconnected After Reboot: Fix the Persistent Mapping"
seo_description: "A mapped drive disappears after a restart. Follow these controlled checks to confirm whether the mapping is non-persistent, then restore the expected connection."
keywords:
  - "network drive disconnected after reboot"
date: 2026-11-21T16:51:11+08:00
publishDate: 2026-11-21T16:51:11+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You restart your Windows PC, open File Explorer, and the mapped drive to the shared folder is gone, even though it worked before the reboot.

## Confirm the mapping is actually missing
Open Command Prompt and run `net use`. If the drive letter is absent, the mapping was not restored. If it shows a status like Disconnected or Unavailable, the mapping exists but the connection failed. Note the exact result before changing anything.

## Check whether the mapping was saved as persistent
In the same Command Prompt, run `net use Z:` (replace Z with your drive letter). If Windows reports that the network connection does not exist, the mapping was created without persistence. Reconnect it with `net use Z: \\ServerName\ShareName /persistent:yes`. The `/persistent:yes` switch tells Windows to recreate it at every sign-in.

## Rule out a credential or policy reset
If `net use` lists the drive as Disconnected, run `net use Z: /delete`, then reconnect with the persistent switch and sign in again. If it still drops after reboot, check whether a logon script or Group Policy is removing mappings at startup. A quick test is to map the drive manually, reboot, and run `net use` again. If the manual mapping survives, a script or policy is the cause.

## Verification test
Reboot once more and run `net use` before opening File Explorer. A persistent mapping should appear as OK or Reconnected. Then open the drive and confirm you can list files.

## Rollback note
If the persistent mapping causes errors, remove it with `net use Z: /delete` and recreate it without the persistent switch. This restores the previous behavior without leaving a broken entry.

If the mapped drive still shows as **network drive disconnected after reboot**,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact `net use` output.
