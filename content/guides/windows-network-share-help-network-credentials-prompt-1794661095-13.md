---
title: "Network Credentials Prompt: Fix Rejected Credentials for a LAN Share"
description: "Fix the Windows network credentials prompt that rejects the correct account when opening a LAN shared folder. Step-by-step checks, verification, and rollback."
seo_title: "Network Credentials Prompt Rejects Correct Account: Fix LAN Share Login"
seo_description: "Fix the Windows network credentials prompt that rejects the correct account when opening a LAN shared folder. Step-by-step checks, verification, and rollback."
keywords:
  - "network credentials prompt"
date: 2026-11-17T09:36:48+08:00
publishDate: 2026-11-17T09:36:48+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You open a shared folder from another LAN PC, type the account that should work, and Windows immediately returns you to the **network credentials prompt** with the password rejected.

## Check the account format first
On the PC hosting the share, open Computer Management > Local Users and Groups > Users and confirm the exact username. In the prompt, enter it as HOSTPC\username (the sharing computer's name, not your own). If the account is a Microsoft account, try the email address instead. A wrong format looks identical to a wrong password.

## Confirm the account has share and NTFS rights
On the host, right-click the shared folder > Properties > Sharing > Advanced Sharing > Permissions, and check the account is listed with at least Read. Then open the Security tab and confirm the same account has Read there too. If either list is missing the account, add it; share permissions and NTFS permissions are both required.

## Clear stale stored credentials
On the PC you are browsing from, open Control Panel > Credential Manager > Windows Credentials and remove any entry for the host PC name. A saved old password is sent automatically and causes repeated rejection even when you type the right one.

## Verification test
From the browsing PC, open Command Prompt and run: net use \\HOSTPC\ShareName /user:HOSTPC\username
Enter the password when asked. If it reports success, open the share in File Explorer. If it still fails, note the exact error number; error 1326 means bad credentials, while 5 means permissions.

## Rollback note
Before changing permissions, record the existing entries so you can restore them. If access worsens, re-add the original groups exactly as recorded.

If these checks do not resolve it,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact error number.
