---
title: "Network Drive Disconnected After Reboot: Restore the Persistent Mapping"
description: "Fix a mapped drive that disappears after a Windows restart. Check persistent mapping, credential conflicts, and run a verification test to restore the connection."
seo_title: "Network Drive Disconnected After Reboot: Fix the Persistent Mapping"
seo_description: "Fix a mapped drive that disappears after a Windows restart. Check persistent mapping, credential conflicts, and run a verification test to restore the connection."
keywords:
  - "network drive disconnected after reboot"
date: 2026-11-16T10:11:27+08:00
publishDate: 2026-11-16T10:11:27+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You mapped a shared folder from another LAN PC, but after restarting Windows the drive letter is missing and you are stuck before you can diagnose it properly.

## Check whether the mapping is set to persist

Open Command Prompt and run `net use`. Look at the entry for the missing drive. If it is absent, the mapping was not saved for this logon session. If it appears with a status like Unavailable or Disconnected, the mapping exists but the connection is failing. In either case, remove the stale entry with `net use Z: /delete` (replace Z: with your drive letter), then recreate it with `net use Z: \\ServerName\ShareName /persistent:yes`. Using the server name rather than its IP address avoids failures when the address changes.

## Check for conflicting stored credentials

Open Credential Manager and review Windows Credentials. A saved credential for the server that no longer matches its current account can silently break reconnection at logon. Remove the old entry, then reconnect and enter the correct credentials when prompted.

## Verification test

Restart the PC and sign in. Run `net use` again and confirm the drive shows as Available, then open it in File Explorer and create a small test file. If the drive returns but the file operation fails, the share permissions, not the mapping, need attention.

## Rollback and recovery

If a change makes things worse, delete the mapping and recreate it with the original settings. Keep a note of the exact `net use` command that worked so you can restore it quickly. If the **network drive disconnected after reboot** persists after these checks, the cause is likely policy or logon timing rather than the mapping itself.

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with your `net use` output and Credential Manager details for a targeted diagnosis.
