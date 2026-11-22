---
title: "Shared Folder Invisible on LAN: Check These Before Rebuilding the Share"
description: "The shared folder is invisible to the other PC. Run these targeted checks on discovery, firewall, and share permissions before rebuilding the share."
seo_title: "Windows Shared Folder Not Accessible: Fix Invisible Share on LAN"
seo_description: "The shared folder is invisible to the other PC. Run these targeted checks on discovery, firewall, and share permissions before rebuilding the share."
keywords:
  - "windows shared folder not accessible"
date: 2026-11-22T09:11:47+08:00
publishDate: 2026-11-22T09:11:47+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You shared a folder on your Windows PC, but the other computer on the same LAN cannot see it in Explorer or reach it by UNC path.

## Confirm the share exists and is reachable locally

On the host PC, open Command Prompt and run `net share`. The folder name should appear with its local path. If it is missing, the share was removed or never created; recreate it before continuing. Next, run `ping <host-ip>` from the other PC. A reply means basic IP connectivity is fine, so the problem is in discovery or permissions, not the network cable.

## Check network discovery and the firewall

On the host, open Settings > Network & Internet > Sharing options and turn on network discovery and file and printer sharing for the current profile. Then open Windows Defender Firewall > Allow an app through firewall and confirm File and Printer Sharing is ticked for Private networks. If the other PC still cannot see the share, test the UNC path directly: press Win+R on the client, type `\\<host-ip>\<sharename>`, and press Enter. An access-denied message points to permissions; a path-not-found message points to the share name or firewall.

## Verify share permissions

Right-click the folder, choose Properties > Sharing > Advanced Sharing > Permissions, and confirm the other PC's user account has at least Read access. Check the Security tab as well, because NTFS permissions can override share permissions.

## Verification test

From the client PC, run `net view \\<host-ip>` in Command Prompt. The share name should be listed. Then open it by UNC path and create a small test file, which confirms write access if granted.

## Rollback note

If a change makes things worse, reverse the last firewall or permission edit and retest with the UNC path before trying another fix.

If the share remains invisible after these checks, this is a **windows shared folder not accessible** case that needs a closer look at SMB services and event logs.

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) and include the exact error text you see.
