---
title: "SMB Share Access Denied: Fix Rejected Credentials on a LAN Folder"
description: "Credentials rejected when opening a Windows LAN share? Isolate the cause with a direct SMB test, check stored credentials, and restore access safely."
seo_title: "SMB Share Access Denied: Fix Rejected Credentials on a LAN Folder"
seo_description: "Credentials rejected when opening a Windows LAN share? Isolate the cause with a direct SMB test, check stored credentials, and restore access safely."
keywords:
  - "smb share access denied"
date: 2026-11-21T16:51:11+08:00
publishDate: 2026-11-21T16:51:11+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You open a shared folder from another LAN PC, enter the correct account, and Windows rejects it before you can diagnose why.

## Confirm the rejection is credential-based
On the PC hosting the folder, open Command Prompt and run `net share`. Confirm the share name exists. Then run `net user <accountname>` and confirm the account is not locked or expired. If the account is locked, unlock it in Computer Management under Local Users and Groups. If the share is missing, you are fixing the wrong problem.

## Test SMB directly, bypassing Explorer
On the client PC, open Command Prompt and run `net use \\<hostname>\<sharename> /user:<hostname>\<accountname> *`. Enter the password when prompted. Read the result exactly: error 1326 means bad credentials or a name mismatch; error 5 means the account authenticated but lacks share or NTFS permission; error 53 means the host or share name is wrong. Only error 1326 confirms credential rejection.

## Clear stale stored credentials
If the direct test returns 1326, run `net use * /delete` to remove cached connections, then open Credential Manager and delete any Windows Credentials entries for that host. Retry the direct test. A successful connection here means Explorer was reusing an old password.

## Verification test
After clearing credentials, open the share in File Explorer and enter the account as `<hostname>\<accountname>`, not just the username. Access should now succeed. If it still fails, recheck the account name spelling on the host.

## Rollback note
Before changing share or NTFS permissions, record the current settings. If a permission change makes things worse, restore the previous entries exactly.

If the rejection persists after these checks, this is an **smb share access denied** condition that needs deeper log review.

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact error code from the direct test.
