---
title: "Windows Share Rejects Correct Credentials: Test SMB Directly Before Resetting"
description: "Fix a Windows share that rejects the correct account by testing SMB directly, checking credential conflicts, and verifying with a clean session."
seo_title: "Windows Share Rejects Correct Credentials: Test SMB Directly"
seo_description: "Fix a Windows share that rejects the correct account by testing SMB directly, checking credential conflicts, and verifying with a clean session."
keywords:
  - "Windows Share Not Showing or Asking for Credentials: Test SMB Directly"
date: 2026-11-21T16:54:10+08:00
publishDate: 2026-11-21T16:54:10+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You are opening a shared folder on another LAN PC, and Windows rejects the account you know is correct, so you need a controlled diagnosis before changing anything.

## Check the credential conflict first

On the PC trying to connect, open Command Prompt and run `net use`. If you see the server name or IP listed with an existing connection, Windows may be reusing an old session. Run `net use \\SERVER\Share /delete` and try again. If the share now opens, the stored session was the problem; no password change is needed.

## Test SMB directly

Still in Command Prompt, run `net use \\SERVER\Share /user:SERVER\Username`. Enter the password when prompted. Read the result carefully: error 1326 means the username or password is wrong as typed; error 5 means the account authenticated but lacks share or NTFS permission; error 53 means the server name cannot be reached. This **Windows Share Not Showing or Asking for Credentials: Test SMB Directly** step separates a credential problem from a permission or network problem.

## Verify with a clean session

If the direct test succeeds, disconnect with `net use \\SERVER\Share /delete`, then open the share in File Explorer. It should open without a prompt. If it still prompts, clear stored credentials under Credential Manager, Windows Credentials, and repeat the direct test.

## Rollback note

Before changing share or NTFS permissions, record the current entries. If access worsens, restore those entries and reconnect with `net use` using the same account that worked in the direct test. If the direct test still rejects the correct account, stop changing permissions and

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).
