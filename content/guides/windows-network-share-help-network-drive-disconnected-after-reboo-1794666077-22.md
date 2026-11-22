---
title: "Network Drive Disconnected After Reboot: Diagnose the Persistent Connection"
description: "A mapped drive disappears after a restart. Follow these checks to diagnose the persistent connection and restore the expected outcome: network drive disconnected after reboot."
seo_title: "Network Drive Disconnected After Reboot: Fix the Persistent Connection"
seo_description: "A mapped drive disappears after a restart. Follow these checks to diagnose the persistent connection and restore the expected outcome: network drive disconnected after reboot."
keywords:
  - "network drive disconnected after reboot"
date: 2026-11-22T10:11:56+08:00
publishDate: 2026-11-22T10:11:56+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You mapped a shared folder on another LAN PC, but after restarting Windows the drive letter is gone and you are stuck before completing a controlled diagnosis.

## Check the drive mapping and reconnect state
Open File Explorer and look under This PC. If the drive letter is missing, open Command Prompt and run `net use`. A line showing the remote path with status `Unavailable` means the mapping exists but the connection failed at logon. If no line appears, the mapping was not saved persistently. Run `net use Z: \\PC-NAME\ShareName /persistent:yes` using your actual drive letter and share path, then restart once to test.

## Check credential storage
If `net use` shows the mapping but it stays unavailable, stored credentials may be stale. Open Credential Manager, select Windows Credentials, and remove any entry for the remote PC. Reconnect the drive and enter the correct username and password when prompted. A successful reconnect without an error means stored credentials were the cause.

## Verification test
After making one change, restart the PC and open File Explorer. Double-click the mapped drive and open a file. If the drive letter is present and the folder opens, the persistent connection is restored. If it still disappears, note whether `net use` reports `Unavailable` or shows nothing; that result tells you whether the problem is connection timing or mapping persistence.

## Rollback and recovery
Before changing registry settings or logon scripts, record the current drive letter and share path. If a change makes things worse, run `net use Z: /delete` and remap the drive manually. This returns you to a known working state while you investigate further. If the **network drive disconnected after reboot** persists after these checks,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact `net use` output and your Windows version.
