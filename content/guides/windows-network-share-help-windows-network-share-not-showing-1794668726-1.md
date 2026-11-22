---
title: "Windows Network Share Not Showing: When the Other PC Can't See the Shared Folder"
description: "The other PC can't see your shared folder in Explorer or by UNC path. Follow these checks to diagnose why the Windows network share is not showing and restore visibility."
seo_title: "Windows Network Share Not Showing? Fix Invisible Shared Folder"
seo_description: "The other PC can't see your shared folder in Explorer or by UNC path. Follow these checks to diagnose why the Windows network share is not showing and restore visibility."
keywords:
  - "windows network share not showing"
date: 2026-11-22T11:12:02+08:00
publishDate: 2026-11-22T11:12:02+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You've shared a folder on one Windows PC, but the other computer on the same LAN can't see it in Explorer or reach it by UNC path.

## Confirm the share exists on the host
On the PC hosting the folder, open Command Prompt and run `net share`. Look for your folder name in the list. If it's missing, the folder isn't actually shared. Re-share it via Properties > Sharing. If it appears with a trailing `$`, it's hidden and won't show in browsing—use the explicit UNC path instead.

## Check network profile and discovery
On both PCs, go to Settings > Network & Internet > Ethernet (or Wi-Fi). Confirm the profile is Private, not Public. Public profile blocks discovery and sharing by default. Then open Control Panel > Network and Sharing Center > Advanced sharing settings and ensure network discovery and file and printer sharing are on for the Private profile.

## Test by UNC path, not browsing
On the other PC, press Win+R and type `\\HOST-PC\FolderName` (replace with the host's name and share name). If this opens the folder, the share works and only browsing/discovery is broken—often a firewall or discovery service issue. If it fails with a specific error, note the error code; it tells you whether it's name resolution, permissions, or connectivity.

## Verify with a ping and SMB port test
Ping the host by name. If it fails but the IP works, name resolution is the problem. Then run `Test-NetConnection HOST-PC -Port 445` in PowerShell. A failed TCP test means SMB traffic is blocked—check Windows Firewall on the host for File and Printer Sharing rules.

## Rollback note
If you changed firewall or sharing settings and access worsens, revert the last change before continuing. Keep a note of original settings.

If the **windows network share not showing** persists after these checks,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with your exact error code and `net share` output.
