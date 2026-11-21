---
title: "Correct Password Rejected on a LAN Share: Test SMB Directly Before Changing Anything"
description: "When Windows rejects the correct account for a LAN shared folder, test SMB directly to see whether the failure is authentication or the client session, then recover cleanly."
seo_title: "Windows Share Rejects Correct Credentials: Test SMB Directly"
seo_description: "When Windows rejects the correct account for a LAN shared folder, test SMB directly to see whether the failure is authentication or the client session, then recover cleanly."
keywords:
  - "Windows Share Not Showing or Asking for Credentials: Test SMB Directly"
date: 2026-11-21T16:51:11+08:00
publishDate: 2026-11-21T16:51:11+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You open a shared folder on another LAN PC, type the account and password you know are right, and Windows rejects them anyway.

## Confirm the account is valid on the host
On the PC hosting the share, open Command Prompt and run `net user <account>`. A successful listing means the account exists. Then run `net share` and confirm the share name and path are present. If either command fails, stop here: the problem is the account or share definition, not SMB.

## Test SMB directly from the client
On the PC being rejected, open Command Prompt and run `net use \\<host>\<share> /user:<host>\<account> *`. Enter the password at the prompt. Read the result carefully:
- System error 5 means SMB reached the host and authentication was refused. The credential or its permissions are the cause.
- System error 53 or 67 means the name or share was not found, so SMB never reached authentication.
- System error 64 or a timeout points to the network or session layer, not the password.

This is the core of **Windows Share Not Showing or Asking for Credentials: Test SMB Directly**: the error number tells you which layer failed.

## Verification test
Run `net use` with no arguments. If the connection appears, open the share in File Explorer and confirm access. If error 5 returns, check the account name format and whether the account is disabled or locked on the host.

## Rollback and recovery
If the test connection succeeds but Explorer still prompts, run `net use \\<host>\<share> /delete` to remove the test session, then retry Explorer. This clears the stale session without touching the host configuration.

If error 5 persists with a verified account, the remaining cause is usually host-side permission or policy.

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact error number and the commands you ran.
