---
title: "SMB Share Access Denied: Fix Credential Rejection on a LAN Share"
description: "Fix SMB share access denied when the correct account is rejected. Step-by-step checks for Windows LAN shares, credential caching, and verification."
seo_title: "SMB Share Access Denied: Fix Credential Rejection on a LAN Share"
seo_description: "Fix SMB share access denied when the correct account is rejected. Step-by-step checks for Windows LAN shares, credential caching, and verification."
keywords:
  - "smb share access denied"
date: 2026-11-23T08:11:46+08:00
publishDate: 2026-11-23T08:11:46+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You open a shared Windows folder from another LAN PC, type the correct account, and Windows rejects it—leaving you stuck before any controlled diagnosis.

## Confirm the exact rejection point

On the client PC, open File Explorer and enter the share path directly, such as \\SERVER\Share. When prompted, type the account as SERVER\Username or .\Username, not just Username. If the prompt reappears immediately, the client is not sending the credential you expect. If it returns "access denied" after a pause, the credential reached the server but was refused.

## Clear stored credentials

On the client, open Credential Manager, select Windows Credentials, and remove any entry for the server name or IP. Then retry the share. A stale saved credential can override what you type and cause **smb share access denied** even when the account is valid.

## Check share and NTFS permissions

On the host, right-click the folder, open Properties, then Sharing > Advanced Sharing > Permissions. Confirm the account or its group has at least Read. Next, open the Security tab and verify the same account has NTFS Read or Change. If the share allows access but NTFS denies it, the result is still access denied. Add the account to both places, then retry.

## Verification test

From the client, run `net use \\SERVER\Share /user:SERVER\Username *` in Command Prompt, enter the password, and note the result. A success message confirms the credential path works; an error 5 confirms a permission or account mismatch. Disconnect with `net use \\SERVER\Share /delete` afterward.

## Rollback note

If you changed permissions, record the original entries before editing. To recover, restore the previous share and NTFS entries exactly, then reconnect.

If the rejection persists after these checks,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).
