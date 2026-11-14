---
title: "Windows Share Rejects Correct Credentials: Test SMB Directly to Isolate the Cause"
description: "Correct account rejected when opening a Windows share? Test SMB directly to isolate credential, policy, or name-resolution faults before changing anything."
seo_title: "Windows Share Rejects Correct Credentials: Test SMB Directly"
seo_description: "Correct account rejected when opening a Windows share? Test SMB directly to isolate credential, policy, or name-resolution faults before changing anything."
keywords:
  - "Windows Share Not Showing or Asking for Credentials: Test SMB Directly"
date: 2026-11-14T19:58:38+08:00
publishDate: 2026-11-14T19:58:38+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You are opening a shared folder from another LAN PC, and Windows rejects the account you know is correct.

## Confirm the rejection is SMB-level, not Explorer-level

On the client PC, open Command Prompt and run:

net use \\SERVER\Share /user:SERVER\Username *

Replace SERVER, Share, and Username with your values. Enter the password at the prompt.

Interpret the result exactly:

- System error 5 (access denied): the credentials reached the server and were refused. The problem is account, permission, or policy, not the network path.
- System error 1326 (logon failure): the username or password format is wrong, or the account is locked or disabled.
- System error 53 or 67: the share name or server name did not resolve. This is a naming problem, not a credential problem.
- The command succeeds: Explorer is caching old credentials. Run net use * /delete, then retry the share in File Explorer.

## Check the account on the server

On the sharing PC, run net user Username and confirm the account is not locked, disabled, or expired. Then check the share permissions with net share ShareName and the folder's security tab. The account needs both share and NTFS permission.

## Verification test

After any change, repeat the same net use command from the client. Success means the credential path is fixed; then open the share in File Explorer to confirm the expected result.

## Rollback note

If a policy or permission change makes things worse, revert it immediately and re-run the test to return to the previous state. For a guided diagnosis of this exact rejection,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).

This **Windows Share Not Showing or Asking for Credentials: Test SMB Directly** check separates credential rejection from naming faults before you change server settings.
