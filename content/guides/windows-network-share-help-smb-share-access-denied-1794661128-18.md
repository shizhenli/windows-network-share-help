---
title: "SMB Share Access Denied: Fix Credential Rejection Before Diagnosis"
description: "Stuck at credential rejection when opening a Windows SMB share? Follow these targeted checks to isolate cached credentials, SMB signing, and share permissions, then verify access."
seo_title: "SMB Share Access Denied: Fix Rejected Credentials on Windows LAN"
seo_description: "Stuck at credential rejection when opening a Windows SMB share? Follow these targeted checks to isolate cached credentials, SMB signing, and share permissions, then verify access."
keywords:
  - "smb share access denied"
date: 2026-11-18T08:11:59+08:00
publishDate: 2026-11-18T08:11:59+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You open a shared Windows folder from another LAN PC, enter the correct account, and the credentials are rejected before you can run a controlled diagnosis.

## Check the Cached Credential First
On the client PC, open Command Prompt and run `net use`. If you see the share or server listed with an old session, clear it with `net use \\SERVER\SHARE /delete`. Then reopen the share. If the prompt now accepts the account, the rejection came from a stale cached credential, not from the server.

## Confirm the Account Format and Share Permissions
At the prompt, try `SERVER\username` instead of just `username`. On the sharing PC, right-click the folder, open Properties > Sharing > Advanced Sharing > Permissions, and confirm the account is listed with at least Read. Also check the Security tab for the same account. If the account is missing from either list, adding it should stop the rejection. If it is present in both, move to the SMB policy check.

## Test SMB Signing and Guest Fallback
On the sharing PC, run `Get-SmbServerConfiguration | Select RequireSecuritySignature, EnableSMB2Protocol`. If RequireSecuritySignature is True, the client must support signing; a mismatch can cause an **smb share access denied** result even with valid credentials. Temporarily set it to False with `Set-SmbServerConfiguration -RequireSecuritySignature $false`, then retry. If access works, update the client or re-enable signing after confirming compatibility.

## Verification Test
From the client, run `net use \\SERVER\SHARE /user:SERVER\username` and enter the password. A success message confirms the fix. Then open the share in File Explorer and create a test folder to confirm write access if expected.

## Rollback Note
If changing SMB signing does not help, restore it with `Set-SmbServerConfiguration -RequireSecuritySignature $true`. If the rejection persists after all checks,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact error text and `net use` output.
