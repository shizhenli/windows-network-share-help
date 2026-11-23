---
title: "SMB Direct Test: When Windows Share Is Invisible or Asks for Credentials"
description: "Fix a Windows shared folder that is invisible to another LAN PC by testing SMB directly. Step-by-step checks, result interpretation, and verification."
seo_title: "SMB Direct Test: Windows Share Invisible or Credentials Prompt"
seo_description: "Fix a Windows shared folder that is invisible to another LAN PC by testing SMB directly. Step-by-step checks, result interpretation, and verification."
keywords:
  - "Windows Share Not Showing or Asking for Credentials: Test SMB Directly"
date: 2026-11-23T09:11:42+08:00
publishDate: 2026-11-23T09:11:42+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You've shared a folder on one Windows PC, but the other computer can't see it in Explorer or reach it by UNC path, and you want to stop guessing and test SMB directly.

## Confirm the share exists on the host
On the PC sharing the folder, open Command Prompt and run `net share`. You should see the share name and its path. If it's missing, the folder was never shared or the share was removed. Also run `net share <ShareName>` to confirm the path. If the path is wrong, fix the share before testing from the other PC.

## Test SMB from the other PC
On the second PC, open Command Prompt and run `net use \\<HostIP>\<ShareName>` using the host's IPv4 address, not its name. Interpret the result:
- System error 53: the host isn't reachable or SMB isn't listening. Check the host's firewall and that File and Printer Sharing is enabled.
- System error 5: SMB is reachable but access is denied. The account lacks share or NTFS permission.
- System error 67: the share name is wrong or missing.
- A credential prompt: SMB is working; the problem is authentication, not visibility.

This is the core of **Windows Share Not Showing or Asking for Credentials: Test SMB Directly** — separate reachability from permission.

## Verify the fix
After correcting the identified layer, rerun the same `net use` command. Success means no error and the drive maps. Then open `\\<HostIP>\<ShareName>` in Explorer to confirm the folder appears.

## Rollback note
If a change makes things worse, run `net use * /delete` on the client to clear test connections, then re-enable the previous firewall rule or share permission. If SMB still fails after these checks,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).
