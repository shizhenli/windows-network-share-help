---
title: "SMB Share Access Denied: Fix Rejected Credentials from a Windows LAN PC"
description: "Correct account rejected when opening a Windows SMB share? Follow these focused checks to interpret the rejection, run a direct test, and recover safely."
seo_title: "SMB Share Access Denied: Fix Rejected Credentials on Windows LAN"
seo_description: "Correct account rejected when opening a Windows SMB share? Follow these focused checks to interpret the rejection, run a direct test, and recover safely."
keywords:
  - "smb share access denied"
date: 2026-11-16T12:36:13+08:00
publishDate: 2026-11-16T12:36:13+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You are opening a shared Windows folder from another LAN PC, and the account you know is correct is rejected at the credentials prompt. This is an **smb share access denied** symptom, so treat it as a credential or policy mismatch before changing the share itself.

## Check the exact rejection text and account format

At the prompt, enter the username as `PCNAME\username` or `username@PCNAME`, not just `username`. If the prompt reappears immediately, Windows did not accept the credential format or the account is blocked for network logon. If it accepts the format but still rejects the password, move to the next check.

On the sharing PC, open Local Users and Groups and confirm the account is enabled and not locked out. Then check Local Security Policy under Security Settings, Local Policies, User Rights Assignment: the account must not be listed under Deny access to this computer from the network. If it is, remove it there and retry.

## Run a direct verification test

On the client PC, open Command Prompt and run `net use \\SERVER\Share /user:SERVER\username *`. Enter the password when prompted. A success message confirms the share and credential work, so the earlier rejection came from a stored credential in File Explorer. A system error 5 confirms the rejection is policy or account related, not the share path.

## Rollback and recovery

If you changed group membership or user rights, record the original entries first. To roll back, restore those exact entries and run `net use * /delete` on the client to clear test connections. Do not leave broad Everyone permissions in place as a workaround.

If the direct test still fails after these checks, stop changing settings and

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact error text and the account format you used.
