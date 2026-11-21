---
title: "Shared Folder Invisible to Another PC: Fix the Windows Network Share Not Showing"
description: "Troubleshoot a Windows shared folder that is invisible to another LAN PC. Follow these steps to diagnose and restore visibility, with a verification test and rollback note."
seo_title: "Windows Network Share Not Showing: Fix Invisible Shared Folder"
seo_description: "Troubleshoot a Windows shared folder that is invisible to another LAN PC. Follow these steps to diagnose and restore visibility, with a verification test and rollback note."
keywords:
  - "windows network share not showing"
date: 2026-11-21T16:54:10+08:00
publishDate: 2026-11-21T16:54:10+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You've shared a folder on your Windows PC, but the other computer on your LAN cannot see it in File Explorer or by UNC path, leaving you stuck at the shared folder is invisible to the other pc step.

## Check Network Discovery and Sharing Settings

On the sharing PC, open Control Panel > Network and Sharing Center > Advanced sharing settings. Under the current profile, ensure Network discovery is on and File and printer sharing is on. If either is off, turn it on and save changes. Result interpretation: if network discovery was off, the share won't appear in Explorer's Network view, but a direct UNC path might still work.

## Verify the Share Exists and Permissions

On the sharing PC, run `net share` in Command Prompt. You should see the share name and path. If missing, recreate the share. Then check the folder's Properties > Sharing > Advanced Sharing > Permissions to confirm the other PC's user account has access. Result interpretation: if `net share` lists the share but the other PC still can't see it, the issue is likely network or firewall related.

## Test Direct UNC Access

On the other PC, press Win+R and type `\\SharingPCName\ShareName` (replace with actual names). If it opens, the share is visible but not discoverable; if it errors, note the exact message. This is your verification test.

## Check Firewall and Services

On the sharing PC, ensure File and Printer Sharing is allowed through Windows Firewall. Also confirm the Function Discovery Provider Host and Function Discovery Resource Publication services are running. If you changed firewall settings, you can roll back by restoring the previous rules.

If the share remains invisible,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) for a controlled diagnosis. This **windows network share not showing** issue often stems from discovery settings or firewall blocks.
