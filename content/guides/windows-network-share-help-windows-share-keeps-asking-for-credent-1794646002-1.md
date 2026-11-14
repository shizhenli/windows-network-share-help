---
title: "Windows Share Keeps Asking for Credentials: Fix the Rejected Password Loop"
description: "Correct account rejected when opening a Windows share? Diagnose the credentials loop with clear checks, a verification test, and a safe rollback."
seo_title: "Fix: Windows Share Keeps Asking for Credentials (Rejected Password)"
seo_description: "Correct account rejected when opening a Windows share? Diagnose the credentials loop with clear checks, a verification test, and a safe rollback."
keywords:
  - "windows share keeps asking for credentials"
date: 2026-11-14T19:58:38+08:00
publishDate: 2026-11-14T19:58:38+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You open a shared folder from another LAN PC, type the correct username and password, and Windows immediately rejects them and prompts again.

## Confirm the exact logon format
On the PC hosting the share, open Command Prompt and run `whoami`. Note the result, for example `PC1\alex`. On the client, when prompted, enter the username as `PC1\alex` rather than just `alex`. If the host is on a domain, use `DOMAIN\alex`. Reopen the share. If the prompt disappears and the folder opens, the issue was the account name format.

## Check the account and share permissions
On the host, right-click the folder, choose Properties, then Sharing, then Advanced Sharing, then Permissions. Confirm the account is listed with at least Read. Next, open the Security tab and confirm the same account has Read or Change. If either list is missing the account, add it, apply, and retry. If the account exists in both places but is still rejected, the stored credential on the client is likely stale.

## Clear stale credentials on the client
On the client, open Credential Manager, select Windows Credentials, and remove any entry for the host name or IP. Then open the share again and enter the credentials fresh. This is also your rollback point: if clearing an entry makes another working share fail, re-add the same entry with the original username and password.

## Verification test
From the client, run `net use \\HOST\Share /user:HOST\alex *` in Command Prompt and enter the password at the prompt. A message that the command completed successfully confirms the account and permissions are correct. If it still fails, the problem is on the host account or permission side, not the client prompt.

If the rejection continues after these checks,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact error text and the `whoami` output so the next step is targeted. A **windows share keeps asking for credentials** loop is usually resolved by fixing the logon name, permissions, or stored credential, in that order.
