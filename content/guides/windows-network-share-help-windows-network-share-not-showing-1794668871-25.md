---
title: "Windows Network Share Not Showing: Fix the Invisible Share Before You Change Permissions"
description: "Shared folder invisible to another PC? Follow these checks to confirm the share exists, test the UNC path, and restore visibility without guessing."
seo_title: "Windows Network Share Not Showing? Fix the Invisible Share First"
seo_description: "Shared folder invisible to another PC? Follow these checks to confirm the share exists, test the UNC path, and restore visibility without guessing."
keywords:
  - "windows network share not showing"
date: 2026-11-25T12:11:52+08:00
publishDate: 2026-11-25T12:11:52+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You shared a folder on one Windows PC, but the other computer cannot see it in File Explorer or by UNC path.

## Confirm the share exists on the host
On the PC that owns the folder, open Command Prompt and run `net share`. You should see the share name and its path. If it is missing, the folder was not actually shared. Re-create the share and note the exact name. If it appears, write down the name and path; you will use them next.

## Test the UNC path from the other PC
On the second PC, press Win+R and enter `\\HOSTNAME\ShareName` using the host's computer name, not a mapped drive. Interpret the result:
- A credential prompt or access-denied error means the share is reachable and the problem is permission or authentication, not visibility.
- "Windows cannot access" or a network path error means name resolution or SMB connectivity is failing.
- The folder opens but appears empty means the share is visible and the issue is content or offline files.

## Check network profile and discovery
On both PCs, confirm the active network profile is Private, not Public. Public profiles block network discovery. Also confirm both PCs are on the same subnet. If the UNC path works but browsing does not, discovery is the failing layer, not the share itself. This is a common reason for a **windows network share not showing** in Explorer's Network view.

## Verification test
From the second PC, run `net view \\HOSTNAME` in Command Prompt. If the share name appears, visibility is restored at the SMB level. Then open the UNC path again in Explorer.

## Rollback note
If you changed firewall rules or network profiles during testing, record the original settings first. To recover, set the profile back to its previous state and re-enable any disabled discovery services before retesting.

If the share still does not appear after these checks,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).
