---
title: "Shared Folder Invisible to Another PC: Fix the Missing Share"
description: "Troubleshoot why a shared folder is invisible to another PC on your LAN. Step-by-step checks for network discovery, sharing settings, and firewall rules to restore access."
seo_title: "Windows Shared Folder Not Accessible: Fix Invisible Share"
seo_description: "Troubleshoot why a shared folder is invisible to another PC on your LAN. Step-by-step checks for network discovery, sharing settings, and firewall rules to restore access."
keywords:
  - "windows shared folder not accessible"
date: 2026-11-21T16:51:11+08:00
publishDate: 2026-11-21T16:51:11+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You've shared a folder on one Windows PC, but the other computer on your LAN can't see it in File Explorer or reach it by UNC path—this guide fixes that specific visibility failure.

## Confirm the share exists on the host
On the PC hosting the folder, open Command Prompt and run `net share`. Look for your folder name in the list. If it's missing, the share was never created or was removed. Re-create it via right-click > Properties > Sharing > Advanced Sharing. If it's listed, note the exact share name—spaces and special characters can break UNC paths.

## Check network discovery and sharing settings
On both PCs, go to Control Panel > Network and Sharing Center > Advanced sharing settings. Under Private, ensure Network discovery and File and printer sharing are turned on. If they're off, the other PC won't see the share in Explorer's Network view. After enabling, restart both PCs or run `ipconfig /flushdns` to refresh discovery.

## Verify firewall rules
On the host, open Windows Defender Firewall > Allow an app or feature through Windows Defender Firewall. Confirm File and Printer Sharing is checked for Private networks. If it's unchecked, the share is blocked even though it exists. Check the box and click OK.

## Test with a direct UNC path
On the other PC, press Win+R and type `\\HOST-PC\ShareName` (replace with actual names). If it opens, the share is reachable and the issue is only Explorer's Network browsing—try mapping the drive manually. If you get an error, the problem is connectivity or permissions, not visibility.

## Rollback note
If changes to sharing settings or firewall rules cause other network problems, revert them by re-opening Advanced sharing settings and restoring the previous toggles. Document what you changed so you can undo it.

If the share remains invisible after these checks, the cause may be deeper—such as SMB version mismatch or service failure—and you may need **windows shared folder not accessible** diagnostics. For a guided review,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).
