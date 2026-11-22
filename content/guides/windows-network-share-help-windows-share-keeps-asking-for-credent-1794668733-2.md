---
title: "Windows Share Credentials Rejected: Check the Account Name Format and Stored Credential"
description: "When the correct account is rejected opening a Windows share, check the username format and stored credential, then verify with a direct SMB test."
seo_title: "Windows Share Keeps Asking for Credentials: Fix Rejected Login"
seo_description: "When the correct account is rejected opening a Windows share, check the username format and stored credential, then verify with a direct SMB test."
keywords:
  - "windows share keeps asking for credentials"
date: 2026-11-22T12:12:19+08:00
publishDate: 2026-11-22T12:12:19+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

**windows share keeps asking for credentials**. You open a shared folder from another LAN PC, type the account you know is correct, and Windows rejects it, so the share keeps asking for credentials.

## Check the username format first
On the PC hosting the share, open Computer Management > Local Users and Groups > Users and confirm the exact account name. Then, at the prompt on the other PC, enter the name as HOSTNAME\Username or .\Username if it is a local account. A bare name can be matched to the wrong account, so the correct password is rejected. Result: if the prompt accepts the HOSTNAME\Username form, the earlier failure was a name resolution issue, not a wrong password.

## Clear the stored credential
On the PC being rejected, open Control Panel > Credential Manager > Windows Credentials. Remove any entry for the host name or IP. Close File Explorer, reopen the share, and enter the credentials again. Result: a new prompt with no error means a stale saved credential was overriding your input.

## Verification test
Open Command Prompt and run net use \\HOSTNAME\ShareName /user:HOSTNAME\Username. Enter the password when asked. Result: 'The command completed successfully' confirms the account and password are valid and the fault was in the saved credential or the typed name. An 'Access is denied' result points to share or NTFS permissions, not the password.

## Rollback note
Before removing credentials, note the entry name and target. If access worsens, recreate it in Credential Manager with the same name and target so the previous state is restored.

If the prompt still rejects the account after these checks,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact error text and the net use output.
