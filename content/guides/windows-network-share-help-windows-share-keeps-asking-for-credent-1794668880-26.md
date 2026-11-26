---
title: "Correct Password Rejected on a Windows Share: Isolate the Credential Cache Before Changing Permissions"
description: "The correct account is rejected when opening a Windows LAN share. Run these targeted checks to isolate stored credentials, SMB signing, and account policy before changing permissions."
seo_title: "Windows Share Keeps Asking for Credentials: Fix Rejected Password"
seo_description: "The correct account is rejected when opening a Windows LAN share. Run these targeted checks to isolate stored credentials, SMB signing, and account policy before changing permissions."
keywords:
  - "windows share keeps asking for credentials"
date: 2026-11-26T08:10:11+08:00
publishDate: 2026-11-26T08:10:11+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

**windows share keeps asking for credentials**. You open a shared folder on another LAN PC, type the account you know is correct, and Windows immediately rejects it, so the share keeps asking for credentials.

## Clear the stored credential first

Windows often reuses a cached credential for the server name, and an old password overrides the one you type. Open Credential Manager, choose Windows Credentials, and remove every entry whose address matches the sharing PC (its name or IP). Do not remove unrelated entries. Reopen the share and enter the account again. If the prompt now accepts it, the cached entry was the cause; if it is rejected again, continue below.

## Confirm the account format and policy

At the prompt, type the username as PCNAME\username, where PCNAME is the sharing computer, not your own. Check the sharing PC under Local Users and Groups that the account is enabled, not locked out, and has a password. A blank password is blocked by default for network logon. Also confirm the account is listed in the folder's share permissions and NTFS permissions; being an administrator is not enough on its own.

## Test SMB directly

On your PC, open Command Prompt and run: net use \\PCNAME\ShareName /user:PCNAME\username

Enter the password when asked. A success message means the GUI prompt or cached credential was at fault. System error 5 means the account is authenticated but lacks permission. System error 1326 means the credentials themselves are rejected, pointing to the account or password on the sharing PC.

## Rollback note

If you changed share or NTFS permissions while testing, restore the previous entries before finishing. If you removed a credential that later proves necessary, re-add it in Credential Manager with the correct password.

If the direct test still returns error 1326 with a verified password, the remaining causes are local account policy or SMB signing mismatch.

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact error number and account format you used.
