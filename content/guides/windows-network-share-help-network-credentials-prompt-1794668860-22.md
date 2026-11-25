---
title: "Network Credentials Prompt: Fix the Rejected Account Before Diagnosing Further"
description: "Fix the network credentials prompt rejecting the correct account on a Windows LAN share. Practical checks, exact result interpretation, and a verification test."
seo_title: "Network Credentials Prompt Rejects Correct Account: Fix It"
seo_description: "Fix the network credentials prompt rejecting the correct account on a Windows LAN share. Practical checks, exact result interpretation, and a verification test."
keywords:
  - "network credentials prompt"
date: 2026-11-25T09:11:52+08:00
publishDate: 2026-11-25T09:11:52+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You open a shared folder on another Windows PC, type the account you know is correct, and the **network credentials prompt** rejects it before you can finish a controlled diagnosis.

## Check the account format and the prompt itself

At the prompt, enter the username as `PCNAME\username` or `username@PCNAME`, where PCNAME is the computer sharing the folder. A bare username can be resolved against the wrong local account. If the prompt reappears immediately after you submit, Windows is not accepting the credential at all; if it accepts and then the folder fails to open, the problem is permissions, not the password.

## Rule out a stale stored credential

Open Credential Manager, look under Windows Credentials, and remove any entry for the sharing PC's name or IP address. Then reopen the share. If the prompt now accepts the same account, a stale saved credential was being replayed. If it still rejects, continue.

## Confirm the account exists on the sharing PC

On the sharing PC, check Local Users and Groups and confirm the exact username, spelling, and that the account is enabled and not locked out. A disabled or locked account produces the same rejection as a wrong password. Also confirm the account has been granted share and NTFS permissions.

## Verification test

From the client PC, open Command Prompt and run `net use \\PCNAME\Share /user:PCNAME\username *`, then enter the password. A message that the command completed successfully confirms the credential works and the earlier failure was the prompt or a stored credential. An access-denied error points to permissions or account state.

## Rollback note

If you removed stored credentials, you can recreate them in Credential Manager with the same target name and account. If a change made things worse, restore the previous permission entries before continuing. For a guided review,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).
