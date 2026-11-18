---
title: "Network Drive Disconnected After Reboot: Diagnose the Lost Mapping"
description: "A mapped drive disappears after a restart. Follow these checks to diagnose why the network drive disconnected after reboot and restore the persistent mapping."
seo_title: "Network Drive Disconnected After Reboot: Fix the Lost Mapping"
seo_description: "A mapped drive disappears after a restart. Follow these checks to diagnose why the network drive disconnected after reboot and restore the persistent mapping."
keywords:
  - "network drive disconnected after reboot"
date: 2026-11-18T11:29:49+08:00
publishDate: 2026-11-18T11:29:49+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You mapped a shared folder on another LAN PC, but after restarting Windows the drive letter is gone, and you want to restore the expected connection.

## Confirm the share is reachable before touching the mapping

Open Command Prompt and run `ping <remote-PC-name>`. A reply means name resolution and basic connectivity are fine; a timeout means the remote PC is off, asleep, or on a different network, and the mapping cannot survive. Next run `net view \\<remote-PC-name>` and confirm the shared folder name appears. If it does not, the problem is on the sharing PC, not the mapped drive.

## Check whether the mapping is persistent

In File Explorer, right-click the missing drive and choose Disconnect if it still appears, then reconnect it with Reconnect at sign-in ticked. Alternatively, in Command Prompt run `net use Z: \\<remote-PC-name>\<share> /persistent:yes`. Then run `net use` and read the output: a line for the drive with no status note means it is stored; a line marked Unavailable means Windows kept the entry but could not reach the share at logon.

## Verification test

Restart the PC and run `net use` again before opening File Explorer. If the drive is listed and accessible, the mapping is persistent. If it is missing, the logon is running before the network is ready.

## Recovery note

If a change makes things worse, disconnect the drive with `net use Z: /delete` and remap it manually; this returns you to the previous working state. For a controlled diagnosis of why the **network drive disconnected after reboot**,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).
