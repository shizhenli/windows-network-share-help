---
title: "Windows Share Not Showing or Asking for Credentials: Test SMB Directly to Confirm the Share Is Reachable"
description: "When a shared folder is invisible to another PC, test SMB directly to confirm whether the share is reachable before changing permissions or credentials."
seo_title: "Windows Share Not Showing or Asking for Credentials: Test SMB Directly"
seo_description: "When a shared folder is invisible to another PC, test SMB directly to confirm whether the share is reachable before changing permissions or credentials."
keywords:
  - "Windows Share Not Showing or Asking for Credentials: Test SMB Directly"
date: 2026-11-18T09:11:47+08:00
publishDate: 2026-11-18T09:11:47+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You shared a folder on one Windows PC, but the other computer cannot see it in File Explorer or by UNC path.

## Confirm the share exists on the host

On the PC that shares the folder, open Command Prompt and run `net share`. The folder name should appear with its local path. If it is missing, the folder was not actually shared; re-create the share before troubleshooting the network.

## Test SMB directly from the other PC

On the second computer, open Command Prompt and run `net view \\HOSTNAME` (replace HOSTNAME with the sharing PC's name). A list of shares means SMB is reachable and the problem is likely Explorer or credential caching. A system error such as 53, 64, or 1231 means the connection itself is failing, so focus on name resolution and network reachability rather than passwords.

Next, run `net use \\HOSTNAME\ShareName /user:HOSTNAME\Username` and enter the password when prompted. If this succeeds, the share is accessible and the earlier invisibility was a client-side display issue. If it returns access denied, the account or share permissions need review.

## Verification

After a successful `net use`, open `\\HOSTNAME\ShareName` in File Explorer. The folder contents should load without a credential prompt. If the prompt returns, disconnect the test connection with `net use \\HOSTNAME\ShareName /delete` and retry once to rule out a stale session.

## Rollback note

If you changed share or NTFS permissions during testing, record the original settings first and restore them if the test makes access worse. For a controlled diagnosis of **Windows Share Not Showing or Asking for Credentials: Test SMB Directly**, keep changes minimal and reversible. If the direct test still fails,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact error code.
