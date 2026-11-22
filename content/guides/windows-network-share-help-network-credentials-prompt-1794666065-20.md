---
title: "Network Credentials Prompt Rejects the Correct Account: A Step-by-Step Fix"
description: "The correct account is rejected at the network credentials prompt when opening a shared folder. Follow these practical checks to isolate the cause and restore access."
seo_title: "Network Credentials Prompt Rejects Correct Account: Fix It"
seo_description: "The correct account is rejected at the network credentials prompt when opening a shared folder. Follow these practical checks to isolate the cause and restore access."
keywords:
  - "network credentials prompt"
date: 2026-11-22T08:11:53+08:00
publishDate: 2026-11-22T08:11:53+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You open a shared folder from another LAN PC, type the correct username and password at the **network credentials prompt**, and Windows rejects them.

## Check the account format first

On the PC hosting the share, open Computer Management > Local Users and Groups > Users. Confirm the account exists and is not locked out. Then, at the prompt on the client PC, enter the username as `HOSTPC\username` (replace HOSTPC with the sharing computer's name). If the prompt accepts the name but still rejects the password, the issue is credential matching, not the share itself.

## Clear stored credentials

On the client PC, open Control Panel > Credential Manager > Windows Credentials. Remove any entry pointing to the host PC or its IP address. Close and reopen the share. If the prompt now accepts the same password, a stale saved credential was overriding your input.

## Test SMB directly

Open Command Prompt and run `net use \\HOSTPC\ShareName /user:HOSTPC\username *`. Enter the password when asked. A success message means the share and account work, and the problem is in File Explorer's cached session. An error such as System error 86 or 1326 confirms the credential itself is being refused.

## Rollback note

If clearing credentials makes other mapped drives fail, re-add them from Credential Manager using the same host and account details. Do not delete entries for unrelated servers.

## Verification

Reopen the share from File Explorer. If the folder opens without a prompt, the fix holds. If the prompt returns, note the exact error and check the share permissions against NTFS permissions on the host.

If these steps do not resolve it,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact error text.
