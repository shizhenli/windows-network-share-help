---
title: "Windows Shared Folder Not Accessible: When the Other PC Can't See the Share"
description: "The other PC cannot see your Windows shared folder in Explorer or by UNC path. Follow these checks to diagnose and restore visibility."
seo_title: "Windows Shared Folder Not Accessible: Fix Invisible Share"
seo_description: "The other PC cannot see your Windows shared folder in Explorer or by UNC path. Follow these checks to diagnose and restore visibility."
keywords:
  - "windows shared folder not accessible"
date: 2026-11-16T09:11:25+08:00
publishDate: 2026-11-16T09:11:25+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

Your Windows shared folder is invisible to another LAN PC, and you are stuck before completing a controlled diagnosis. Let's fix that.

## Confirm the Share Exists Locally

On the sharing PC, open Command Prompt and run `net share`. Look for your folder name in the list. If it is missing, the share was never created or was removed. Recreate it via right-click > Properties > Sharing > Advanced Sharing. If it appears, note the exact share name and path.

## Check Network Discovery and Firewall

On both PCs, ensure Network Discovery is on: Control Panel > Network and Sharing Center > Advanced sharing settings. Turn on network discovery and file and printer sharing. Then check Windows Defender Firewall > Allow an app through firewall and confirm File and Printer Sharing is ticked for Private networks. If the network profile is Public, switch it to Private.

## Test by UNC Path, Not Browse

On the other PC, press Win+R and type `\\<sharing-PC-IP>\<sharename>`. If this opens the folder, the share works and the issue is browsing only. If you get error 0x80070035, the name is not resolving; use the IP address directly. If you get access denied, permissions are the problem, not visibility.

## Verify and Roll Back

After any change, repeat the UNC test from the other PC. If the folder opens, create a shortcut for future use. If a change makes things worse, reverse it immediately: re-enable the previous firewall rule or set the network profile back. Keep a note of original settings before editing.

If the share remains invisible after these checks, the cause may be a deeper SMB or policy issue.

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) for a guided diagnosis of your **windows shared folder not accessible** problem.
