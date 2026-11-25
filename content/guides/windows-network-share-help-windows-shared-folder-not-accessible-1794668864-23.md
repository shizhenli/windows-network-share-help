---
title: "Shared Folder Invisible to Another PC: Check the Share Name and SMB Binding"
description: "When a Windows shared folder is invisible to another LAN PC, verify the share name, SMB binding, and network profile before changing permissions."
seo_title: "Fix: Windows Shared Folder Not Accessible to Another PC"
seo_description: "When a Windows shared folder is invisible to another LAN PC, verify the share name, SMB binding, and network profile before changing permissions."
keywords:
  - "windows shared folder not accessible"
date: 2026-11-25T10:11:45+08:00
publishDate: 2026-11-25T10:11:45+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You shared a folder on one Windows PC, but the other computer cannot see it in File Explorer or reach it by UNC path.

## Confirm the share exists and note its exact name

On the host PC, open Command Prompt and run `net share`. Look for your folder in the list and copy the share name exactly. If the folder is missing, the share was not created or was removed; recreate it before continuing. If the share name contains spaces or unusual characters, test with a simple name like `TestShare` to rule out naming issues.

## Check SMB binding and network profile

Run `Get-SmbServerConfiguration | Select EnableSMB1Protocol, EnableSMB2Protocol` in PowerShell. SMB2 should be True. Next, confirm both PCs are on the same subnet and that the host's network profile is Private, not Public. On the host, go to Settings > Network & Internet > Ethernet (or Wi-Fi) and set the profile to Private. A Public profile blocks discovery and can make the share invisible even when permissions are correct.

## Test by UNC path, not browsing

On the client PC, press Win+R and enter `\\HOST-PC\ShareName` using the exact name from `net share`. If this opens the folder, discovery is the only problem. If it fails with a network path error, the share or SMB service is not reachable. This is the controlled diagnosis step that separates a discovery fault from a permissions fault in a **windows shared folder not accessible** scenario.

## Verification and rollback

Reopen File Explorer on the client and confirm the folder appears under Network. If you changed the share name or network profile during testing, revert those changes and retest the original UNC path. If the share still does not appear,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact error text and the output of `net share`.
