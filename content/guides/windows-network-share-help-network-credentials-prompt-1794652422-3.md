---
title: "Network Credentials Prompt Rejects the Correct Account: Isolate the Stored Credential"
description: "The network credentials prompt keeps rejecting the correct account on a Windows LAN share. Check stored credentials, credential manager entries, and SMB signing to isolate the cause."
seo_title: "Network Credentials Prompt Rejects Correct Account: Fix Stored Credential"
seo_description: "The network credentials prompt keeps rejecting the correct account on a Windows LAN share. Check stored credentials, credential manager entries, and SMB signing to isolate the cause."
keywords:
  - "network credentials prompt"
date: 2026-11-14T19:58:38+08:00
publishDate: 2026-11-14T19:58:38+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You open the shared folder, type the account that works on the other PC, and the **network credentials prompt** rejects it again. Before changing share permissions, isolate whether Windows is sending a stale saved credential instead of the one you just typed.

## Check stored credentials first

On the PC opening the share, open Control Panel, then Credential Manager, then Windows Credentials. Look for entries matching the hostname or IP of the sharing PC. If an old entry exists, remove it, close File Explorer, and reconnect. Result interpretation: if the prompt now accepts the account, the stored credential was overriding your input. If the same rejection returns, continue below.

## Test the share by IP, not hostname

Open Command Prompt and run `net use \\192.168.1.20\Share /user:PC2\Alice *`, replacing the IP, share name, and account with yours. Enter the password at the prompt. Result interpretation: a success means name resolution or a cached hostname credential is the problem; an error 1326 means the account or password itself is being refused by the sharing PC.

## Verify the account on the sharing PC

On the sharing PC, open Computer Management, Local Users and Groups, and confirm the account name exactly, including spelling and domain prefix. Then check the share permissions and NTFS permissions for that account. Result interpretation: if the account is absent from both, the rejection is correct and permissions must be granted.

## Verification test

From the client PC, run `net use \\192.168.1.20\Share /delete`, then reconnect through File Explorer and enter the account once. A single clean prompt that accepts the password confirms the fix.

## Rollback note

If a change makes access worse, re-add the removed credential in Credential Manager or restore the previous share permission entry. Keep a note of the original values before editing.

If the rejection persists after these checks,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).
