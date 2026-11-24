---
title: "SMB Share Access Denied: Fix Credentials Rejected When Opening a Shared Folder"
description: "Credentials rejected when opening a Windows SMB share? Isolate stored credentials, SMB signing, and account permissions to fix smb share access denied."
seo_title: "SMB Share Access Denied: Fix Rejected Credentials on a Windows LAN Share"
seo_description: "Credentials rejected when opening a Windows SMB share? Isolate stored credentials, SMB signing, and account permissions to fix smb share access denied."
keywords:
  - "smb share access denied"
date: 2026-11-24T09:11:51+08:00
publishDate: 2026-11-24T09:11:51+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You are opening a shared Windows folder from another LAN PC, and the correct account is rejected at the credentials prompt.

## Confirm the rejection type
At the prompt, enter the account as HOSTNAME\username or .\username, not just the username. If the error is "logon failure: unknown user name or bad password," the account is not being matched. If it is "access is denied," authentication passed but authorization failed. These lead to different fixes, so note which one appears.

## Clear stored credentials on the client
Open Credential Manager, select Windows Credentials, and remove every entry for the host's name or IP. Close File Explorer, reconnect to \\HOSTNAME\Share, and retype the credentials. A stale saved entry often causes **smb share access denied** even when the password is correct.

## Check the account on the host
On the sharing PC, open Local Users and Groups and confirm the account exists, is enabled, and has a password. Blank passwords are blocked for network logon by default. Then check the folder's Share permissions and Security tab: the account needs at least Read in both places.

## Test SMB directly
From the client, run: net use \\HOSTNAME\Share /user:HOSTNAME\username
Enter the password when prompted. A success message means the share path and account work, so the fault is in File Explorer's cached session. An error 1326 means bad credentials; error 5 means permissions.

## Rollback note
If a change breaks access, re-add the removed credential entry or restore the previous share permission, then reconnect.

If the rejection persists after these checks,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact error text and both computer names.
