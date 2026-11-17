---
title: "Network Drive Disconnected After Reboot: Diagnose the Persistence Failure"
description: "A mapped drive disappears after a restart. Follow these checks to diagnose why the network drive disconnected after reboot and restore the persistent connection."
seo_title: "Network Drive Disconnected After Reboot: Fix Mapped Drive Persistence"
seo_description: "A mapped drive disappears after a restart. Follow these checks to diagnose why the network drive disconnected after reboot and restore the persistent connection."
keywords:
  - "network drive disconnected after reboot"
date: 2026-11-17T10:11:29+08:00
publishDate: 2026-11-17T10:11:29+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You mapped a shared folder from another LAN PC, and after restarting Windows the drive letter is gone from File Explorer.

## Check the mapped drive's persistence setting

Open Command Prompt and run `net use`. Look at the entry for the missing drive. If it shows no status or is absent, the mapping was not saved as persistent. Recreate it with `net use Z: \\PC-NAME\Share /persistent:yes`, replacing Z and the path with your values. If `net use` lists the drive but File Explorer does not, the issue is display or session-related, not the mapping itself.

## Confirm the remote share is reachable at boot

Run `ping PC-NAME` and then `net view \\PC-NAME`. If ping fails, the host is offline or name resolution is failing; the drive cannot reconnect. If ping succeeds but `net view` fails, SMB or firewall on the host is blocking access. A successful `net view` listing the share means the host side is fine and the problem is local persistence.

## Verification test

Recreate the mapping with persistence enabled, restart the PC, and run `net use` again. The drive should appear with a status of OK before you open File Explorer. If it still vanishes, check whether a logon script or Group Policy is removing mappings at startup.

## Rollback note

If a new mapping causes conflicts, remove it with `net use Z: /delete` and restore your previous configuration. Keep a note of the original path before changing anything.

If the **network drive disconnected after reboot** persists after these checks, the cause is likely a policy or credential conflict that needs closer inspection.

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with your `net use` output and event log details.
