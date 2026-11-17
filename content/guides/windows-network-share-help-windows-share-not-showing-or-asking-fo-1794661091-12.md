---
title: "Windows Share Rejects Correct Credentials: Test SMB Directly Before Changing Permissions"
description: "When Windows rejects the correct account for a LAN share, test SMB directly to separate credential, permission, and service issues before changing anything."
seo_title: "Windows Share Rejects Correct Credentials: Test SMB Directly"
seo_description: "When Windows rejects the correct account for a LAN share, test SMB directly to separate credential, permission, and service issues before changing anything."
keywords:
  - "Windows Share Not Showing or Asking for Credentials: Test SMB Directly"
date: 2026-11-17T08:19:56+08:00
publishDate: 2026-11-17T08:19:56+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You are entering the right username and password, but the Windows share still rejects the credentials, and you want a controlled diagnosis before changing permissions.

## Check the basics first
On the PC hosting the share, open an elevated Command Prompt and run `net share`. Confirm the share name exists and note its path. Then run `net user` and verify the account name is spelled exactly as it appears. A typo or a local account versus Microsoft account mismatch is a common cause. If the account is a Microsoft account, try the local username format `PCNAME\username` instead of the email address.

## Test SMB directly
From the client PC, open Command Prompt and run `net use \\HOSTNAME\ShareName /user:HOSTNAME\username`. Enter the password when prompted. Interpret the result precisely: error 1326 means the username or password is wrong; error 5 means authentication succeeded but access was denied; error 53 means the host or share name cannot be resolved. This is the core of **Windows Share Not Showing or Asking for Credentials: Test SMB Directly** because it bypasses File Explorer and cached prompts.

## Verification test
If `net use` succeeds, open the share in File Explorer using the same hostname and confirm access. If it fails with 1326, reset the account password on the host and retry. If it fails with 5, check the share permissions and NTFS permissions for that account.

## Rollback note
Before changing share or NTFS permissions, record the current entries. If a change makes things worse, restore the previous entries exactly. To clear a bad cached connection on the client, run `net use \\HOSTNAME\ShareName /delete` and retry.

If the direct test still rejects the correct account,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact error number.
