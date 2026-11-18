---
title: "Network Credentials Prompt: Fix the Rejected Correct Account"
description: "Fix the Windows network credentials prompt that rejects the correct account when opening a LAN share. Step-by-step checks, verification, and rollback."
seo_title: "Network Credentials Prompt Rejects Correct Account: Fix It"
seo_description: "Fix the Windows network credentials prompt that rejects the correct account when opening a LAN share. Step-by-step checks, verification, and rollback."
keywords:
  - "network credentials prompt"
date: 2026-11-18T10:42:42+08:00
publishDate: 2026-11-18T10:42:42+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You open a shared folder from another LAN PC, type the account you know is correct, and Windows returns you to the same **network credentials prompt** with the password rejected. This is a stored-credential mismatch, not a wrong password. The fix is to clear the cached entry, confirm the account format, and retest the share.

## Clear the Stored Credential

Open Control Panel, then Credential Manager, then Windows Credentials. Look for entries containing the remote PC name or its IP address. Expand each one and note the user name. Delete only those entries. If the share is opened by IP, a credential saved for the hostname will not be used, and the reverse is also true. After deleting, close File Explorer completely and reopen the share path. If the prompt now accepts the account, the cause was a stale cached credential.

## Confirm the Account Format

At the prompt, enter the remote PC name, a backslash, then the user name, for example DESKTOP-ABC\alex. A bare user name can resolve to the local machine instead of the remote one. Confirm the account exists on the remote PC under Local Users and Groups and that it has a password. Blank passwords are blocked for network logon by default.

## Verification Test

From the client PC, open Command Prompt and run: net use \\REMOTEPC\Share /user:REMOTEPC\alex *. Enter the password when asked. A message that the command completed successfully means the credential path is correct. An error 1326 confirms the account or password is still being rejected at the remote side, so check the remote account rather than the client.

## Rollback Note

If clearing credentials breaks another working share, recreate that entry in Credential Manager with the same user name and address you recorded before deleting it.

If the rejection persists after these checks,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact error text and the account format you used.
