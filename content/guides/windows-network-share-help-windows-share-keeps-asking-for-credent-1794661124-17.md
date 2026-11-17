---
title: "Windows Share Credentials Rejected: Fix the 'Correct Password' Loop Before Diagnosing"
description: "Your Windows share keeps asking for credentials and rejects the correct account. Use this focused check to isolate the rejected credential and restore access."
seo_title: "Windows Share Credentials Rejected: Fix the 'Correct Password' Loop"
seo_description: "Your Windows share keeps asking for credentials and rejects the correct account. Use this focused check to isolate the rejected credential and restore access."
keywords:
  - "windows share keeps asking for credentials"
date: 2026-11-17T12:11:29+08:00
publishDate: 2026-11-17T12:11:29+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You open a shared folder from another LAN PC, type the correct username and password, and Windows immediately returns you to the credentials prompt. Before you run a full diagnosis, isolate whether the rejection is coming from the stored credential or the account itself. This one check often resolves the loop.

## Check the Stored Credential First

On the PC that is being rejected, open Credential Manager and look under Windows Credentials. Find any entry for the sharing PC's name or IP address. If an old entry exists, expand it and choose Remove. Close Credential Manager, then open the share again and enter the account manually. If the prompt accepts it, the stored credential was stale and the loop is fixed.

## Interpret the Result

If the same account is still rejected, the problem is not the saved password. Confirm the account name exactly as it appears on the sharing PC, including any domain or PC-name prefix. A mismatch here causes repeated rejection even when the password is right. Also confirm the account is enabled and has share permissions, not just NTFS permissions.

## Verification Test

From the rejected PC, open Command Prompt and run: net use \\\\SHARING-PC\\ShareName /user:SHARING-PC\Username

Enter the password when prompted. A message that the command completed successfully means the credential works and the earlier loop was a cached-entry issue. An error such as access denied confirms the account or permission problem remains.

## Rollback Note

If removing the stored credential does not help, you can re-add it in Credential Manager with the same details so your previous setup is restored. This does not change share permissions.

If the rejection persists after these checks, the issue is likely account or permission configuration on the sharing PC. For a controlled next step,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).

A **windows share keeps asking for credentials** most often because a stale saved entry overrides the correct password; clearing it is the fastest test.
