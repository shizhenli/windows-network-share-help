---
title: "Windows Share Rejects Correct Credentials: Test SMB Directly to Confirm the Rejection"
description: "When a Windows share rejects the correct account, test SMB directly to confirm the rejection and isolate the cause. Step-by-step checks and verification."
seo_title: "Windows Share Rejects Correct Credentials: Test SMB Directly"
seo_description: "When a Windows share rejects the correct account, test SMB directly to confirm the rejection and isolate the cause. Step-by-step checks and verification."
keywords:
  - "Windows Share Not Showing or Asking for Credentials: Test SMB Directly"
date: 2026-11-21T16:48:05+08:00
publishDate: 2026-11-21T16:48:05+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You open a shared folder from another LAN PC, enter the correct username and password, and Windows immediately rejects them. Before changing any settings, you need to confirm whether the rejection comes from SMB itself or from a cached credential. This is the moment for **Windows Share Not Showing or Asking for Credentials: Test SMB Directly**.

## Check the share path and account format

On the client PC, open Command Prompt and run `net use \\SERVER\ShareName /user:SERVER\Username`. Replace SERVER with the hostname or IP of the sharing PC, ShareName with the folder name, and Username with the exact account. Press Enter when prompted for the password. If you see System error 5, the credentials are rejected at the SMB layer. If you see System error 53, the share path is wrong. If you see System error 64, the server is unreachable.

## Clear stale credentials and retry

A cached credential can override the correct password. Run `net use * /delete` and confirm. Then repeat the `net use` command above. If the error changes from 5 to 0, the stored credential was the problem. If error 5 persists, the rejection is real and comes from the server side.

## Verification test

From the same client, run `net use \\SERVER\ShareName /user:SERVER\Username` again after clearing credentials. A successful connection returns “The command completed successfully.” That confirms the account works and the earlier rejection was cached. If it still fails with error 5, test the same account locally on the server by opening the share path in File Explorer. If local access also fails, the account lacks share or NTFS permission.

## Rollback note

If you changed share permissions during testing, restore the previous permission entries before finishing. Removing a test account or permission change can lock out other users.

If the direct SMB test still rejects the correct account,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact error number and the command you ran.
