---
title: "SMB Share Access Denied: Clear Stored Credentials to Stop Rejection"
description: "Correct account rejected when opening a Windows SMB share? Clear stored credentials and test access to resolve smb share access denied."
seo_title: "SMB Share Access Denied: Fix Rejected Credentials"
seo_description: "Correct account rejected when opening a Windows SMB share? Clear stored credentials and test access to resolve smb share access denied."
keywords:
  - "smb share access denied"
date: 2026-11-21T16:48:05+08:00
publishDate: 2026-11-21T16:48:05+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You are opening a shared folder from another Windows PC, but the account you know is correct is rejected before you can finish a controlled diagnosis.

## Check the credential being sent

On the PC that is being rejected, open Credential Manager and look under Windows Credentials. Find any entry for the server name or IP address. If an old or wrong username is stored there, Windows sends it automatically and ignores the prompt. Remove that entry, then try the share again. If the prompt appears and accepts the correct account, the stored credential was the cause.

## Confirm the account name format

At the credential prompt, enter the username as SERVER\Username or as the local account on the sharing PC, not the Microsoft account email unless that is how the share was configured. A rejection that disappears when you switch to SERVER\Username points to a name-format mismatch.

## Verification test

From the same PC, open Command Prompt and run: net use \\SERVER\Share /user:SERVER\Username. Enter the password when asked. If it connects, the graphical prompt was using a stale credential. If it still returns access denied, the account lacks share or NTFS permission, and the next step is to check those permissions on the sharing PC.

## Rollback note

If clearing the credential makes things worse, you can re-add it in Credential Manager with the same server name and username. This restores the previous automatic sign-in behavior.

If the rejection persists after these checks, this is a permissions or policy issue rather than a credential cache problem.

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact error text and the username format you used. That will resolve the **smb share access denied** condition without further guesswork.
