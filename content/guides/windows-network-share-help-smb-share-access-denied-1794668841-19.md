---
title: "SMB Share Access Denied: Fix Credential Rejection When the Account Is Correct"
description: "Troubleshoot SMB share access denied when the correct account is rejected. Step-by-step checks for credential conflicts, security policy, and share permissions."
seo_title: "SMB Share Access Denied: Fix Correct Credentials Rejected"
seo_description: "Troubleshoot SMB share access denied when the correct account is rejected. Step-by-step checks for credential conflicts, security policy, and share permissions."
keywords:
  - "smb share access denied"
date: 2026-11-25T08:11:49+08:00
publishDate: 2026-11-25T08:11:49+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You are opening a shared folder from another LAN PC, and Windows rejects the account you know is correct.

## Clear Stored Credentials First

On the PC trying to connect, open Control Panel > Credential Manager > Windows Credentials. Look for entries containing the hostname or IP of the sharing PC. Remove them, then retry the share. If the prompt now accepts the account, a stale saved credential was the cause.

## Check the Security Policy

On the sharing PC, run secpol.msc. Go to Local Policies > Security Options and inspect Network security: LAN Manager authentication level. If it is set to Send NTLMv2 response only and the client is older, set it to Send LM & NTLM - use NTLMv2 session security if negotiated. Also check Accounts: Limit local account use of blank passwords to console logon only. If enabled, blank-password accounts are rejected over the network. Disable it only if the account truly has no password.

## Verify Share and NTFS Permissions

Right-click the shared folder > Properties > Sharing > Advanced Sharing > Permissions. Confirm the account is listed with at least Read. Then go to the Security tab and confirm the same account has NTFS access. A missing entry in either place produces an **smb share access denied** result even when the password is right.

## Verification Test

From the client PC, open Command Prompt and run net use \\SERVER\Share /user:SERVER\Username. Enter the password when prompted. A message that the command completed successfully confirms the credential path works. If it still fails, note the exact error number.

## Rollback Note

If you changed the LAN Manager level or blank-password policy, record the original setting before editing. Revert it if the change does not resolve the rejection, so other network services are not affected.

If these checks do not isolate the cause,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).
