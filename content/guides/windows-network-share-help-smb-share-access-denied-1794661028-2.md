---
title: "SMB Share Access Denied: Fix the Rejected Credentials Before You Reset Anything"
description: "The correct account is rejected when opening a Windows LAN share. Test the SMB connection directly, isolate stored credentials, and restore access without resetting the account."
seo_title: "SMB Share Access Denied: Fix Rejected Credentials on a LAN Share"
seo_description: "The correct account is rejected when opening a Windows LAN share. Test the SMB connection directly, isolate stored credentials, and restore access without resetting the account."
keywords:
  - "smb share access denied"
date: 2026-11-15T19:17:45+08:00
publishDate: 2026-11-15T19:17:45+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You open a shared Windows folder from another PC, type the account you know is correct, and Windows rejects it with an **smb share access denied** message before you can finish a controlled diagnosis.

## Confirm the account and share path
On the host PC, open Command Prompt and run `net share`. Confirm the share name and path match what you are opening. Then run `net user <account>` and check that the account is not locked out or expired. If the account is disabled or locked, credentials will always be rejected; unlock it first, then retest.

## Test SMB directly, bypassing File Explorer
On the client PC, open Command Prompt and run `net use \\<host>\<share> /user:<host>\<account> *`. Enter the password when prompted. A success message means Explorer is reusing a stale credential. An error such as 1326 or 5 means the host is rejecting the logon itself. Record the exact error number.

## Clear stored credentials on the client
Open Credential Manager and remove any Windows Credentials entries for the host name or IP. Then repeat the `net use` test. If it now succeeds, the old saved credential was the cause. If it still fails, the problem is on the host side, not the client.

## Check share and NTFS permissions on the host
Right-click the folder, open Properties, then Sharing and Advanced Sharing, and confirm the account is listed under Share Permissions with at least Change. Next, open the Security tab and confirm the same account has NTFS access. A missing entry in either place rejects a valid password.

## Verification test
From the client, run `net use` with no arguments to list connections, then open the share path in File Explorer. Access should open without a prompt. If it does not, note the exact error and

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).

## Rollback note
If a change makes things worse, re-add the original permission entry or restore the previous credential, then retest with `net use` before changing anything else.
