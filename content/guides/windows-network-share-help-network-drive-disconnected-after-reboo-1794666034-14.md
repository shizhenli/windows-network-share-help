---
title: "Mapped Drive Vanishes After Reboot? A Step-by-Step Diagnosis"
description: "Fix a mapped drive that disappears after restart on Windows. Follow targeted checks to diagnose why the network drive disconnected after reboot and restore the persistent connection."
seo_title: "Network Drive Disconnected After Reboot: Diagnose and Restore"
seo_description: "Fix a mapped drive that disappears after restart on Windows. Follow targeted checks to diagnose why the network drive disconnected after reboot and restore the persistent connection."
keywords:
  - "network drive disconnected after reboot"
date: 2026-11-21T16:54:10+08:00
publishDate: 2026-11-21T16:54:10+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You restart your Windows PC, open File Explorer, and the mapped drive to the shared folder on the other LAN PC is gone—this is the classic case of a **network drive disconnected after reboot**.

## Check the Drive's Reconnect Setting

Open File Explorer, right-click the missing mapped drive, and choose Properties. If the drive is absent from This PC, open Command Prompt and run `net use`. Look at the output: if the drive letter shows `Unavailable` or is missing entirely, the mapping is not reconnecting. In the Properties dialog, confirm that Reconnect at sign-in is checked. If it is unchecked, Windows treats the mapping as temporary and removes it after each restart. Check it and click OK.

## Verify the Network Is Ready Before Logon

A mapped drive can fail to reconnect if the network stack is not ready when Windows processes the mapping. Press Win+R, type `gpedit.msc`, and navigate to Computer Configuration > Administrative Templates > System > Logon. Enable Always wait for the network at computer startup and logon. This delays logon until the network is available, giving the mapping time to succeed.

## Test with a Manual Reconnect

Run `net use Z: \\PC-NAME\Share /persistent:yes`, replacing Z and the share path with your values. If this succeeds, the share and credentials are fine; the problem is the automatic reconnect timing. If it fails, note the exact error code—it points to credentials or connectivity.

## Verification

Restart the PC and open This PC. The drive should appear with a status of Connected. If it still does not, run `net use` again and compare the status.

## Rollback Note

If a change makes logon slow or breaks other mappings, reverse the Group Policy setting and re-enable Reconnect at sign-in only.

Still stuck?

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).
