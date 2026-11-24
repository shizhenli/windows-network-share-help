---
title: "Shared Folder Invisible to Another PC: Confirm the Share Is Actually Published"
description: "When the other PC cannot see your shared folder in Explorer or by UNC path, verify the share is published and reachable before changing anything else."
seo_title: "Windows Network Share Not Showing: Verify the Share Is Published"
seo_description: "When the other PC cannot see your shared folder in Explorer or by UNC path, verify the share is published and reachable before changing anything else."
keywords:
  - "windows network share not showing"
date: 2026-11-24T12:14:12+08:00
publishDate: 2026-11-24T12:14:12+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You shared a folder on your Windows PC, but the other computer on the LAN still cannot see it in Explorer or reach it by UNC path.

## Check the share exists and is visible

On the hosting PC, open Command Prompt and run:

```
net share
```

Look for your folder name in the list. If it is missing, the folder was never shared, or the share was removed. Re-create it from the folder's Properties > Sharing tab. If it appears with a trailing `$` (for example `Docs$`), it is a hidden share and will never appear in the other PC's browse list; connect by typing the full UNC path instead.

Next, confirm the share permissions and NTFS permissions both allow the other PC's account. A share can be published but still reject access silently in Explorer.

## Test reachability from the other PC

On the other computer, open Command Prompt and run:

```
net view \\HOSTNAME
```

Replace HOSTNAME with the hosting PC's name. If this lists your share, the share is published and the problem is Explorer's browse list or cached credentials. If it returns error 53 or 6118, the network path is not reachable: check that both PCs are on the same network profile (Private), that network discovery is on, and that File and Printer Sharing is allowed in Windows Defender Firewall.

Then test the direct path:

```
net use \\HOSTNAME\ShareName
```

A successful mapping confirms the share works and only discovery is broken. This is the most common cause of a **windows network share not showing** in Explorer.

## Recovery note

If you changed firewall or discovery settings and the share still fails, revert those changes before continuing, then retest with the direct UNC path to avoid stacking fixes.

If the direct path also fails,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact error code from `net view`.
