---
title: "Network Credentials Prompt Rejects the Correct Account: Clear Cached Credentials"
description: "Correct account rejected at the network credentials prompt? Clear stale cached credentials, verify with a direct SMB test, and restore access to the LAN share."
seo_title: "Network Credentials Prompt Rejects Correct Account: Fix Cached Credentials"
seo_description: "Correct account rejected at the network credentials prompt? Clear stale cached credentials, verify with a direct SMB test, and restore access to the LAN share."
keywords:
  - "network credentials prompt"
date: 2026-11-21T16:48:05+08:00
publishDate: 2026-11-21T16:48:05+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You open a shared folder on another LAN PC, type the correct account, and the **network credentials prompt** rejects it immediately. Before you change permissions or reset passwords, isolate whether Windows is sending a cached credential instead of the one you just typed.

## Check the Stored Credential

On the PC that cannot connect, open Control Panel > Credential Manager > Windows Credentials. Look for entries containing the remote PC name or its IP address. If one exists, expand it and check the user name. A stale entry for the same host will be sent first, so the correct account never reaches the server. Remove only that entry, then reopen the share and retype the account as PCNAME\Username.

## Verify the Account Locally

On the sharing PC, open Computer Management > Local Users and Groups > Users. Confirm the account is enabled and the user name matches exactly, including spelling. A disabled account rejects every attempt regardless of password. If the account is a Microsoft account, try the local account format instead.

## Run a Direct SMB Test

From the connecting PC, open Command Prompt and run: net use \\PCNAME\Share /user:PCNAME\Username

Enter the password when asked. If it connects, the share and account are fine and the failure is cached credentials in File Explorer. If it returns System error 5, the server is rejecting the account itself, so recheck the local account and share permissions.

## Rollback Note

If clearing the credential does not help, recreate it in Credential Manager with the exact user name and password, then retest. This restores the previous stored state so you can compare results.

If the rejection persists after these checks,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact error text and the net use output.
