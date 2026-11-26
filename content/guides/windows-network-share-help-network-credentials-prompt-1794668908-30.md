---
title: "Network Credentials Prompt Rejects the Correct Account: Clear Stale Credentials"
description: "Fix a Windows network credentials prompt that rejects the correct account by clearing stale credentials, checking the logon type, and verifying with a direct SMB test."
seo_title: "Network Credentials Prompt Rejects Correct Account: Fix Stale Credentials"
seo_description: "Fix a Windows network credentials prompt that rejects the correct account by clearing stale credentials, checking the logon type, and verifying with a direct SMB test."
keywords:
  - "network credentials prompt"
date: 2026-11-26T09:10:04+08:00
publishDate: 2026-11-26T09:10:04+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You open a shared folder on another LAN PC, type the account and password you know are correct, and the **network credentials prompt** rejects them again. This usually means Windows is resending an old saved credential, not that the password is wrong.

## Clear the stored credential first

Open Credential Manager and look under Windows Credentials for entries matching the remote PC name or its IP address. Delete them. The same stale entry can exist in a command prompt: run `cmdkey /list` and note any target containing the remote host. Remove it with `cmdkey /delete:TargetName`. If the share is mapped, disconnect it in File Explorer first so the old session is not reused.

## Check which account is being sent

At the prompt, confirm the user name is entered as `REMOTEPC\username` or `username@REMOTEPC`, not a local account on your own machine. A bare name can resolve to the wrong local account. On the hosting PC, check that the account is enabled and that its password has not expired.

## Verification test

From your PC, run `net use \\REMOTEPC\ShareName /user:REMOTEPC\username` in Command Prompt. Enter the password when asked. If it connects, the stored credential was the cause. If it still fails with the same account, the problem is on the hosting side and needs a controlled diagnosis.

## Rollback note

If clearing credentials makes other shares unreachable, reconnect them and re-enter the password once. Do not delete credentials for unrelated servers, and record the target names before removing anything.

If the direct test still rejects the account,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) so the hosting PC's share and security settings can be checked.
