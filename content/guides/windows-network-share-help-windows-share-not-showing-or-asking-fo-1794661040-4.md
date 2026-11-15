---
title: "Windows Share Rejects Correct Credentials: Test SMB Directly"
description: "Fix Windows share rejecting correct credentials by testing SMB directly. Step-by-step checks and verification."
seo_title: "Windows Share Rejects Correct Credentials: Test SMB Directly"
seo_description: "Fix Windows share rejecting correct credentials by testing SMB directly. Step-by-step checks and verification."
keywords:
  - "Windows Share Not Showing or Asking for Credentials: Test SMB Directly"
date: 2026-11-15T19:17:45+08:00
publishDate: 2026-11-15T19:17:45+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You're opening a shared folder on another LAN PC, and Windows keeps rejecting the account you know is correct. Before you reset passwords or rebuild the share, test SMB directly to see whether the rejection comes from the share itself or from cached credentials on your PC.

## Check the share's permissions from the host
On the PC hosting the folder, right-click the folder, choose Properties, then Sharing, then Advanced Sharing, then Permissions. Confirm the account you're using is listed with at least Read access. Next, open the Security tab and verify the same account has matching NTFS permissions. If either list is missing the account, add it and retry. If both lists already include it, the rejection is likely client-side.

## Clear stale credentials on the client
On the PC trying to connect, open Credential Manager, select Windows Credentials, and remove any entries pointing to the host's name or IP. Then open Command Prompt and run `net use \\HOSTNAME\Share /delete` to drop any lingering session. This is your rollback point: if clearing credentials makes things worse, you can re-add the same entry manually.

## Test SMB directly
In Command Prompt, run `net use \\HOSTNAME\Share /user:DOMAIN\Username *`. Enter the password when prompted. If it connects, the share and account are fine, and the original rejection came from stored credentials or a mismatched username format. If it still rejects, the problem is on the host's permission or account side. This is the controlled diagnosis behind **Windows Share Not Showing or Asking for Credentials: Test SMB Directly**.

## Verification
After a successful `net use`, open the share in File Explorer. If it opens without a prompt, the fix held. If the prompt returns, repeat the credential removal and test again.

If the direct test still fails,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact error text.
