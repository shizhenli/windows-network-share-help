---
title: "Network Credentials Prompt Rejects Correct Account: Clear Stored Credentials and Reconnect"
description: "Correct account rejected at the network credentials prompt? Clear stored credentials, verify share permissions, and reconnect to the Windows share with a clean session."
seo_title: "Fix Network Credentials Prompt Rejecting Correct Account"
seo_description: "Correct account rejected at the network credentials prompt? Clear stored credentials, verify share permissions, and reconnect to the Windows share with a clean session."
keywords:
  - "network credentials prompt"
date: 2026-11-23T10:11:54+08:00
publishDate: 2026-11-23T10:11:54+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You open a shared folder from another LAN PC, type the correct username and password, and Windows immediately returns you to the **network credentials prompt** with the same rejection. This usually means a stale saved credential or a mismatched security context is being reused, not that the password is wrong.

## Check Stored Credentials First

On the PC opening the share, open Control Panel > Credential Manager > Windows Credentials. Look for entries containing the remote PC name or its IP address. If one exists, expand it and choose Remove. Do not edit it; remove it so Windows asks fresh. The result you want is no cached entry for that target before you retry.

## Verify the Account Format

At the prompt, enter the username as RemotePC\Username or RemotePC\LocalAccount, not just the bare name. If the remote PC uses a Microsoft account, use the MicrosoftAccount\email@example.com format. A bare username can be silently rejected when the local and remote machines have accounts with the same name.

## Confirm Share and NTFS Permissions

On the hosting PC, right-click the folder > Properties > Sharing > Advanced Sharing > Permissions. Confirm the account has at least Read. Then check the Security tab and confirm the same account has NTFS access. If either layer is missing, the credential will be rejected even when correct.

## Verification Test

Open Command Prompt and run: net use \\RemotePC\Share /user:RemotePC\Username. Enter the password when prompted. A message that the command completed successfully confirms the account and permissions are valid. If it still fails, the issue is on the host, not the client.

## Rollback Note

If clearing credentials causes other mapped drives to stop connecting, re-add them through File Explorer > Map network drive and tick Reconnect at sign-in. Keep a note of removed entries so you can restore any that were still needed.

If the rejection persists after these checks,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact error text and the net use output.
