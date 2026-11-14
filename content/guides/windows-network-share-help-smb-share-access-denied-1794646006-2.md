---
title: "SMB Share Access Denied: When the Correct Account Is Rejected"
description: "Correct account rejected when opening a Windows LAN share? Diagnose SMB share access denied with exact checks, a verification test, and a safe rollback note."
seo_title: "SMB Share Access Denied: Fix Correct Account Rejected on LAN"
seo_description: "Correct account rejected when opening a Windows LAN share? Diagnose SMB share access denied with exact checks, a verification test, and a safe rollback note."
keywords:
  - "smb share access denied"
date: 2026-11-14T19:58:38+08:00
publishDate: 2026-11-14T19:58:38+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You open a shared folder from another LAN PC, type the account you know is correct, and Windows rejects it anyway.

## Confirm what the rejection actually means

On the client, open Command Prompt and run `net use \\SERVER\Share /user:SERVER\Username`. If it fails, read the exact message. "Logon failure: unknown user name or bad password" points to credential or account-state problems. "Access is denied" points to share or NTFS permissions. Write down which one appears before changing anything.

## Check the account and share permissions

On the host, run `net user Username` and confirm the account is enabled and not locked out. Then open the folder's Properties > Sharing > Advanced Sharing > Permissions and confirm the account or its group is listed with at least Read. Next check Security tab permissions for the same identity. A missing entry in either place produces rejection even with a correct password.

## Rule out cached credentials

On the client, run `net use` to list existing connections. If the server is already mapped with old credentials, run `net use \\SERVER\Share /delete`, then retry with the full `SERVER\Username` format. This clears stale sessions that override the password you type.

## Verification test

From the client, run `net use \\SERVER\Share /user:SERVER\Username` again. Success means the connection is established and Explorer should open the folder. If the same rejection returns, compare the error text with your earlier note to see whether the cause is account state or permissions.

## Rollback note

If a change makes things worse, re-add any removed permission entries exactly as they were and delete test mappings with `net use \\SERVER\Share /delete`. Keep a note of original settings before editing.

If the rejection persists after these checks, this is a controlled **smb share access denied** case that needs deeper review.

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).
