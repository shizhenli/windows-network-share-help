---
title: "Shared Folder Invisible to Another PC: Diagnose the Missing Share"
description: "Shared folder invisible to another PC? Diagnose SMB discovery, firewall, and share permissions step by step to restore access on your LAN."
seo_title: "Windows Shared Folder Not Accessible: Fix Invisible Share on LAN"
seo_description: "Shared folder invisible to another PC? Diagnose SMB discovery, firewall, and share permissions step by step to restore access on your LAN."
keywords:
  - "windows shared folder not accessible"
date: 2026-11-15T19:17:45+08:00
publishDate: 2026-11-15T19:17:45+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

## Start with the exact symptom

You shared a folder on one Windows PC, but the other computer cannot see it in File Explorer or reach it by UNC path, so you are stuck before any real diagnosis. This is a **windows shared folder not accessible** situation, and the fix is to isolate whether discovery, firewall, or share permissions are blocking it.

## Check discovery and the UNC path

On the PC that cannot see the share, open File Explorer and type the UNC path directly: \\\\PC-NAME\\ShareName. Press Enter. If it opens, discovery is the problem, not the share. If it fails, note the exact error code. Then on the sharing PC, open Settings > Network & Internet > Advanced network settings and confirm network discovery and file and printer sharing are on for the current profile. A Private profile should show these enabled; a Public profile often blocks them.

## Check firewall and share permissions

On the sharing PC, open Windows Defender Firewall > Allow an app through firewall and confirm File and Printer Sharing is checked for Private. Next, right-click the folder > Properties > Sharing > Advanced Sharing > Permissions. Confirm the other PC's user account or Everyone has at least Read. Then check the Security tab and confirm the same account has access there too. If either list is missing the account, add it and retest the UNC path.

## Verification test

From the other PC, run ping PC-NAME, then net view \\\\PC-NAME. If ping succeeds but net view fails, the share or firewall is blocking SMB. If the UNC path now opens, the share is restored.

## Rollback note

If a change makes things worse, reverse the last permission or firewall edit before trying the next check. For a guided diagnosis,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).
