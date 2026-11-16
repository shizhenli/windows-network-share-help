---
title: "Shared Folder Invisible to Another PC: Check the Share Name and Network Path"
description: "Step-by-step fix when a Windows shared folder is invisible to another PC on the LAN. Check share name, UNC path, and network discovery to restore access."
seo_title: "Windows Network Share Not Showing: Fix Invisible Shared Folder"
seo_description: "Step-by-step fix when a Windows shared folder is invisible to another PC on the LAN. Check share name, UNC path, and network discovery to restore access."
keywords:
  - "windows network share not showing"
date: 2026-11-16T11:11:30+08:00
publishDate: 2026-11-16T11:11:30+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You shared a folder on one Windows PC, but the other computer cannot see it in File Explorer or by UNC path. This is a common **windows network share not showing** problem, and it usually comes down to a mismatch between what you shared and how the other PC is looking for it.

## Confirm the share exists and note its exact name

On the PC that hosts the folder, open Command Prompt and run:

`net share`

Look for your folder in the list. If it is missing, the folder was not actually shared—re-share it and set permissions for the other user. If it appears, note the exact share name. Windows often appends a suffix if the name was already used, so "Reports" may actually be shared as "Reports2".

## Test the UNC path directly

On the other PC, press Win+R and type the full path using the host name or IP address:

`\\HOSTPC\ShareName`

If this opens the folder, the share is fine and only network discovery is failing. If you get "Windows cannot access" or a network path error, the name or path is wrong, or SMB is blocked. Try the IP address instead of the host name to rule out name resolution.

## Check network profile and discovery

On both PCs, confirm the network profile is Private, not Public. In Settings > Network & Internet, turn on network discovery and file and printer sharing. A Public profile silently blocks browsing even when the share itself is healthy.

## Verification test

Return to the other PC and open File Explorer > Network. The host PC should appear within a minute. Double-click it and confirm your shared folder is listed. Then open it and create a test text file to confirm write access.

## Rollback note

If changes make things worse, set the network profile back to its previous state and re-enable any discovery settings you turned off. If the share still will not appear,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact error text and the output of `net share`.
