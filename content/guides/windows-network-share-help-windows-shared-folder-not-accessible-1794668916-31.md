---
title: "Shared Folder Not Visible on Another PC: Fix the Missing Share in File Explorer"
description: "Step-by-step fix when a Windows shared folder is not accessible and remains invisible to another LAN PC in File Explorer or by UNC path. Verify with a direct test and recover safely."
seo_title: "Windows Shared Folder Not Accessible: Fix Invisible Share to Another PC"
seo_description: "Step-by-step fix when a Windows shared folder is not accessible and remains invisible to another LAN PC in File Explorer or by UNC path. Verify with a direct test and recover safely."
keywords:
  - "windows shared folder not accessible"
date: 2026-11-26T10:10:06+08:00
publishDate: 2026-11-26T10:10:06+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You shared a folder on your Windows PC, but the other computer on the same LAN cannot see it in File Explorer or reach it by UNC path.

## Confirm the share exists on the host
On the sharing PC, open Command Prompt and run `net share`. Look for your folder name in the list. If it is missing, the share was never created or was removed. Recreate it via right-click the folder > Properties > Sharing > Advanced Sharing. If it appears, note the exact share name and move on.

## Check network visibility and firewall
On the sharing PC, ensure the active network profile is Private, not Public. Then open Windows Defender Firewall > Allow an app or feature > confirm File and Printer Sharing is enabled for Private. A Public profile or blocked rule commonly makes the share invisible.

## Test by UNC path, not browsing
On the other PC, press Win+R and enter `\\HOSTNAME\SHARENAME` using the exact share name. Interpret the result: if it opens, browsing is the problem, not the share. If you get error 0x80070035, name resolution or SMB is failing. If access is denied, permissions are the issue. This isolates the failure before changing settings.

## Verify from the host side
On the sharing PC, run `net view \\localhost` to confirm the share is advertised locally. Then check Share permissions and NTFS permissions both grant at least Read to the account the other PC uses.

## Rollback note
If a change makes things worse, revert the firewall rule or network profile first, then recheck `net share`. Keep a note of the original share name and permissions so you can restore them.

If the share still does not appear after these checks, this is a **windows shared folder not accessible** case that needs deeper SMB diagnosis.

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).
