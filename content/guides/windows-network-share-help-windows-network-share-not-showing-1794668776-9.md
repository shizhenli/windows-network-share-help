---
title: "Windows Network Share Not Showing: When the Other PC Can't See the Folder"
description: "The other PC cannot see your shared folder in Explorer or by UNC path. Follow these checks to restore visibility without guessing."
seo_title: "Windows Network Share Not Showing: Fix Invisible Shared Folder"
seo_description: "The other PC cannot see your shared folder in Explorer or by UNC path. Follow these checks to restore visibility without guessing."
keywords:
  - "windows network share not showing"
date: 2026-11-24T08:11:49+08:00
publishDate: 2026-11-24T08:11:49+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You shared a folder on one Windows PC, but the other computer on the same LAN cannot see it in Explorer or by typing the UNC path.

## Confirm the share exists on the host
On the PC that owns the folder, open Command Prompt and run `net share`. You should see your folder name and its path. If it is missing, the share was never created or was removed. Recreate it through Folder Properties > Sharing. If it appears, note the exact share name, including spaces.

## Test the UNC path directly
On the second PC, press Win+R and type `\\HOSTNAME\ShareName` using the host's computer name. If you get an error like 0x80070035, name resolution is failing. Try `\\IPAddress\ShareName` instead. If the IP works but the name does not, the problem is name resolution, not the share itself. If both fail, continue below.

## Check network profile and discovery
On the host, open Settings > Network & Internet > Ethernet (or Wi-Fi). The profile must be Private, not Public. On Public, Windows blocks discovery and sharing. Also open Control Panel > Network and Sharing Center > Advanced sharing settings and turn on network discovery and file and printer sharing for the Private profile. This is the most common reason a **windows network share not showing** appears to the other PC.

## Verify with a direct connection test
On the second PC, run `ping HOSTNAME` and `ping IPAddress`. If the IP responds but the name does not, use the IP in the UNC path as a workaround while you fix name resolution. If neither responds, the two PCs are not on the same reachable network segment.

## Rollback note
If you changed the network profile or discovery settings and the share becomes visible but other trusted connections break, set the profile back to its previous state and test again.

If these checks do not restore visibility,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact error code and the results of each test.
