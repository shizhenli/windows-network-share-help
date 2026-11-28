---
title: "SMB Share Access Denied: Fix the Credential Rejection Before Diagnosing"
description: "Stuck at 'credentials are rejected' when opening a Windows LAN share? Follow this focused fix to restore the expected outcome: credentials are rejected."
seo_title: "SMB Share Access Denied: Fix Credential Rejection on Windows LAN Share"
seo_description: "Stuck at 'credentials are rejected' when opening a Windows LAN share? Follow this focused fix to restore the expected outcome: credentials are rejected."
keywords:
  - "smb share access denied"
date: 2026-11-28T22:29:26+08:00
publishDate: 2026-11-28T22:29:26+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

**smb share access denied**. You open a shared folder on another LAN PC, enter the correct account, and Windows rejects it before you can run a controlled diagnosis. This article fixes that specific stop: the credentials are rejected step, so you can reach the expected outcome: credentials are rejected.

## Confirm the rejection is credential-based
At the prompt, type the account as PCNAME\Username (not just Username). If the prompt reappears immediately, the rejection is credential-based, not a network timeout. A timeout or "network path not found" means stop here and check connectivity instead.

## Check the account on the sharing PC
On the PC hosting the folder, open Local Users and Groups and confirm the account exists and is enabled. Then check the share permissions: right-click the folder, Properties, Sharing, Advanced Sharing, Permissions. The account must be listed with at least Read. If it is missing, add it and retry. If it is listed but rejected, the stored credential on the client is likely stale.

## Clear the stored credential on the client
Open Credential Manager, Windows Credentials, and remove any entry for the sharing PC's name or IP. Close File Explorer, reopen the share, and enter the account again. A prompt that now accepts the password confirms a stale stored credential was the cause.

## Verification test
From the client, run net use \\PCNAME\Share /user:PCNAME\Username in Command Prompt. Success shows "The command completed successfully." If it still returns access denied, the rejection is confirmed at the SMB layer, and you can proceed to controlled diagnosis.

## Rollback note
If clearing credentials breaks other mapped drives, re-add the entry in Credential Manager with the original username and password. For persistent rejection,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).

A correct account rejected here is a credential or permission mismatch, not a broken share. Confirm the account, clear stale credentials, and verify with net use before deeper diagnosis.
