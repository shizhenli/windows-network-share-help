---
title: "Shared Folder Invisible to Another PC: Is the Share Actually Published?"
description: "Fix a shared folder that is invisible to another LAN PC by checking share publication, permissions, and network discovery, then verify with a UNC test."
seo_title: "Windows Network Share Not Showing: Verify the Share Is Published"
seo_description: "Fix a shared folder that is invisible to another LAN PC by checking share publication, permissions, and network discovery, then verify with a UNC test."
keywords:
  - "windows network share not showing"
date: 2026-11-18T12:15:02+08:00
publishDate: 2026-11-18T12:15:02+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

**windows network share not showing**. You shared a folder on one Windows PC, but the other computer cannot see it in Explorer or by UNC path, and you want to restore visibility without guessing.

## Confirm the share exists on the host
On the PC that owns the folder, open Command Prompt and run `net share`. Look for the exact share name. If it is missing, the folder was not actually shared; re-share it from Properties > Sharing. If it appears with a trailing `$`, it is hidden and will not show in browsing—use the explicit UNC path instead.

## Check share permissions and NTFS
Run `net share <name>` to see the path and remark. Then open the folder's Properties > Sharing > Advanced Sharing > Permissions. Confirm the other PC's user account or a group containing it has at least Read. Also check Security tab permissions for the same account. An empty or restrictive list here makes the share effectively invisible.

## Verify network profile and discovery
On both PCs, confirm the active network profile is Private, not Public. Public profiles block discovery and can make the share appear absent. Turn on network discovery and file and printer sharing for the Private profile. If discovery remains unreliable, the UNC path is still the authoritative test.

## Verification test
From the other PC, press Win+R and enter `\\HOSTNAME\SHARENAME` using the host's actual name. If it opens, the share is published and only browsing is failing. If it fails, note the error: "cannot find" points to name resolution or firewall; "access denied" points to permissions.

## Rollback note
If you changed permissions or the network profile and access worsens, revert the last change before continuing. Record the original permission entries so you can restore them.

If the share remains invisible after these checks,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact UNC error and the output of `net share`.
