---
title: "Windows Network Share Not Showing: Confirm the Share Is Published Before Changing Permissions"
description: "When another PC cannot see your shared folder in Explorer or by UNC path, verify the share is actually published, test local access, and isolate the cause before changing permissions."
seo_title: "Windows Network Share Not Showing? Check Share Publishing First"
seo_description: "When another PC cannot see your shared folder in Explorer or by UNC path, verify the share is actually published, test local access, and isolate the cause before changing permissions."
keywords:
  - "windows network share not showing"
date: 2026-11-15T19:17:45+08:00
publishDate: 2026-11-15T19:17:45+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You shared a folder on one Windows PC, but the other computer cannot see it in File Explorer or by typing the UNC path, and you want to fix the **windows network share not showing** issue without guessing.

## Confirm the share exists on the hosting PC
On the PC that owns the folder, open Command Prompt and run `net share`. Look for the share name in the list. If it is missing, the folder was never published as a share. If it appears with a trailing `$`, it is hidden and will not show in Explorer, though a direct UNC path can still reach it.

## Test the share locally
From the same PC, press Win+R and enter `\\localhost\ShareName`, replacing ShareName with the exact name from `net share`. If this opens, the share is published and the problem is network-side. If it fails, remove and recreate the share from the folder's Properties > Sharing tab, then retest.

## Verify name resolution and reachability from the other PC
On the second PC, run `ping HostName` using the hosting PC's computer name. A reply confirms name resolution. A failure means use the IP address instead, or check that both PCs are on the same network profile. Then run `net view \\HostName` to list published shares. If the share appears here but not in Explorer, the issue is Explorer discovery, not the share itself.

## Verification test
Open Run on the second PC and enter `\\HostName\ShareName`. Successful access confirms the share is reachable and the earlier invisibility was a discovery or browsing delay.

## Rollback note
If you changed sharing or permission settings during diagnosis, record the original values first. To revert, reopen the folder's Sharing tab and restore the previous share name and permissions, or run `net share ShareName /delete` to remove a test share you created.

If these checks do not isolate the cause,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).
