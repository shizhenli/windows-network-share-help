---
title: "Shared Folder Invisible to Another PC: Fix Windows Network Share Not Showing"
description: "Step-by-step fix when a shared folder is invisible to another PC on your LAN. Check discovery, permissions, and UNC access to restore the share."
seo_title: "Windows Network Share Not Showing: Shared Folder Invisible to Another PC"
seo_description: "Step-by-step fix when a shared folder is invisible to another PC on your LAN. Check discovery, permissions, and UNC access to restore the share."
keywords:
  - "windows network share not showing"
date: 2026-11-14T19:58:38+08:00
publishDate: 2026-11-14T19:58:38+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You shared a folder on one Windows PC, but the other computer cannot see it in File Explorer or by UNC path, and you want to restore visibility before changing anything else.

## Confirm the share exists and is reachable
On the host PC, open Command Prompt and run `net share`. You should see your folder name listed with its path. If it is missing, the share was not created or was removed. Next, run `ping <host-ip>` from the other PC. A reply means basic network reachability is fine; a timeout means you have a network or firewall issue, not a sharing issue.

## Check network discovery and firewall
On both PCs, go to Settings > Network & Internet > Sharing options and turn on network discovery and file and printer sharing for the current profile. Then, on the host, open Windows Defender Firewall > Allow an app through firewall and confirm File and Printer Sharing is checked for Private networks. If the other PC still cannot see the share, temporarily set the host network profile to Private.

## Test direct UNC access
On the other PC, press Win+R and type `\\<host-ip>\<share-name>` (for example, `\\192.168.1.10\Docs`). Press Enter. If credentials are requested, enter the host username and password. If the folder opens, the share is working but discovery is failing. If you get error 0x80070035, the name resolution or firewall is still blocking SMB.

## Verification test
From the other PC, run `net view \\<host-ip>` in Command Prompt. A list of shares confirms SMB access. Then open File Explorer and navigate to Network; the host should appear within a minute. If it does not, restart the Function Discovery Resource Publication service on the host.

## Rollback note
If changes make things worse, revert the firewall rule and network profile to their previous state. Record original settings before editing.

If the share remains invisible after these checks,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) for a guided diagnosis of your **windows network share not showing** issue.
