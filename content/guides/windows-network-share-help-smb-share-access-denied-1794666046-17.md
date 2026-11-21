---
title: "SMB Share Access Denied: Why the Correct Account Is Rejected Before Diagnosis"
description: "Credentials rejected when opening a Windows SMB share? Isolate the cause with a direct test, check stored credentials and share permissions, then verify access."
seo_title: "SMB Share Access Denied: Fix Rejected Credentials on Windows LAN"
seo_description: "Credentials rejected when opening a Windows SMB share? Isolate the cause with a direct test, check stored credentials and share permissions, then verify access."
keywords:
  - "smb share access denied"
date: 2026-11-21T16:54:10+08:00
publishDate: 2026-11-21T16:54:10+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You are opening a shared Windows folder from another LAN PC, and the account you know is correct is rejected at the credentials prompt.

## Confirm the rejection is consistent

First, cancel the prompt and reopen the share. If the same account fails every time, the problem is not a typo. Note the exact error text. "Access is denied" points to permissions or policy; "logon failure" points to the account or credential cache.

## Test SMB directly, bypassing File Explorer

On the client PC, open Command Prompt and run:

```
net use \\SERVER\Share /user:SERVER\Username *
```

Enter the password when prompted. If this succeeds, File Explorer is using a stale stored credential. If it fails with the same error, the rejection is at the server. This separates a client cache problem from a share permission problem.

## Check stored credentials on the client

Open Credential Manager and look under Windows Credentials for entries for the server name or IP. Remove any stale entry, then retry the direct test. A cached old password will keep overriding the correct one, producing an **smb share access denied** result even when the account is valid.

## Check share and NTFS permissions on the host

On the server, right-click the folder, open Properties, and review Sharing and Security. Confirm the account is listed with at least Read in both places. If the account is missing, add it and retry.

## Verification test

Run the direct net use command again. A successful connection with no prompt confirms the fix. Then open the share in File Explorer to confirm normal access.

## Rollback note

If changes make things worse, remove any credential entries you added and restore the original share permissions before continuing. For a guided review,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).
