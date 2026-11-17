---
title: "Shared Folder Not Visible on the Other PC: Check These Three Things First"
description: "The other PC can't see your shared folder in Explorer or by UNC path. Work through three quick checks to find why the share is hidden and restore access."
seo_title: "Windows Network Share Not Showing: Fix Invisible Share on LAN"
seo_description: "The other PC can't see your shared folder in Explorer or by UNC path. Work through three quick checks to find why the share is hidden and restore access."
keywords:
  - "windows network share not showing"
date: 2026-11-17T11:11:28+08:00
publishDate: 2026-11-17T11:11:28+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You shared a folder on one Windows PC, but the other computer on the same LAN cannot see it in Explorer or open it by UNC path.

## Check the share actually exists

On the hosting PC, open Command Prompt and run `net share`. Look for your folder name in the list. If it is missing, the folder was never shared or the share was removed. Re-create it from the folder's Properties > Sharing tab. If it appears with a `$` at the end, it is hidden by design and will not show in Explorer; connect using `\\PC-NAME\ShareName$` instead.

## Confirm the other PC can reach the host

On the other PC, run `ping PC-NAME`. A reply confirms name resolution and basic connectivity. A failure means the PCs are on different networks or the name is wrong; try `ping` with the host's IP address. If the IP works but the name does not, the problem is name resolution, not sharing.

## Test the share directly by UNC path

Press Win+R on the other PC and enter `\\PC-NAME\ShareName`. If it opens, the share is fine and only network discovery is failing, which is common and does not block access. If you get an error, note the exact message: access denied points to permissions, while a network path error points to connectivity or the firewall.

## Verification

After any change, repeat the Win+R UNC test. Success means the folder opens and files are listed. Then check that it appears under Network in Explorer.

## Rollback note

If a change makes things worse, reverse it: re-enable the previous sharing setting, restore the original permission entries, or turn the firewall rule back on. Keep a note of what you changed so you can undo it cleanly.

If the share is still a **windows network share not showing** after these checks,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact error message and the results of each test.
