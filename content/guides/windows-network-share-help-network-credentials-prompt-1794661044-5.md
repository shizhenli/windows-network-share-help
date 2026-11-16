---
title: "Network Credentials Prompt Rejects the Correct Account: Clear the Stale Credential"
description: "The network credentials prompt keeps rejecting the correct account when opening a Windows LAN share. Clear the stale stored credential, retest, and restore access."
seo_title: "Fix: Network Credentials Prompt Rejects the Correct Account"
seo_description: "The network credentials prompt keeps rejecting the correct account when opening a Windows LAN share. Clear the stale stored credential, retest, and restore access."
keywords:
  - "network credentials prompt"
date: 2026-11-16T08:11:25+08:00
publishDate: 2026-11-16T08:11:25+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You open a shared Windows folder on another LAN PC, type the account you know is correct, and the **network credentials prompt** rejects it again. Before assuming the share permissions are wrong, isolate the stored credential Windows is silently reusing. One stale entry in Credential Manager can override what you type.

## Check the stored credential

On the PC opening the share, open Control Panel, then Credential Manager, then Windows Credentials. Look for entries containing the host name or IP of the sharing PC. If one exists, expand it and note the user name. A user name that differs from the account you are typing is the likely cause. Remove only that entry, then reconnect to the share and enter the account again. If the prompt now accepts it, the stored credential was the fault.

## Confirm the account format

If no stored entry exists, check the user name format. For a local account on the sharing PC, use the sharing PC name, a backslash, then the user name, for example SHAREPC\alex. A bare user name can resolve to the wrong machine. Also confirm the account is not locked or expired on the sharing PC.

## Verification test

From the PC opening the share, open Command Prompt and run net use \\SHAREPC\ShareName /user:SHAREPC\alex. Enter the password when asked. A message that the command completed successfully confirms the credential works and the earlier rejection came from the stored entry or format, not the password.

## Rollback note

If clearing the credential does not help, re-add it in Credential Manager with the same host name and user name so the original state is restored before further diagnosis. If the rejection persists after these checks,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).
