---
title: "Windows Share Rejects Correct Password: Fix the Credential Loop"
description: "Troubleshoot a Windows share that rejects the correct account. Check stored credentials, SMB security settings, and test access with net use to restore the expected outcome."
seo_title: "Windows Share Keeps Asking for Credentials: Fix Rejected Password"
seo_description: "Troubleshoot a Windows share that rejects the correct account. Check stored credentials, SMB security settings, and test access with net use to restore the expected outcome."
keywords:
  - "windows share keeps asking for credentials"
date: 2026-11-21T16:48:05+08:00
publishDate: 2026-11-21T16:48:05+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You open a shared folder on another LAN PC, enter the correct username and password, but Windows immediately rejects them and prompts again.

## Check stored credentials first
Open Credential Manager and look under Windows Credentials for entries matching the remote PC name or IP. If an old entry exists, delete it, then reconnect. A stale saved password is the most common cause of a **windows share keeps asking for credentials** loop. If the share opens after deletion, you have isolated the cause.

## Verify the account format
At the prompt, enter the username as `REMOTEPC\username` or `username@REMOTEPC`, not just `username`. Confirm the account has share and NTFS permissions on the host. If the account is a local account on the remote PC, use the remote PC name as the prefix. If it is a Microsoft account, use the email address.

## Test SMB directly
Open Command Prompt and run `net use \\REMOTEPC\ShareName /user:REMOTEPC\username`. Enter the password when prompted. If this succeeds, the problem is in Explorer's cached session, so sign out and back in. If it fails with system error 5, permissions are wrong. If it fails with error 1326, the password or account name is incorrect.

## Check SMB security settings
On the host PC, open Local Security Policy and confirm that LAN Manager authentication level is not set to refuse NTLM. Also verify that the guest account is disabled, because guest access is blocked by default.

## Recovery note
If changes make things worse, re-enable the previous security policy and restart the remote PC. Keep a note of any credential you deleted so you can restore it if needed.

If the rejection persists after these checks,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact error code from the net use test.
