---
title: "Windows Share Rejects Correct Credentials: Stop the Rejected Password Loop"
description: "Correct account rejected when opening a Windows LAN share? Follow these practical checks to isolate stored credentials, SMB signing, and account mismatches, then verify access."
seo_title: "Fix: Windows Share Keeps Asking for Credentials (Rejected Password)"
seo_description: "Correct account rejected when opening a Windows LAN share? Follow these practical checks to isolate stored credentials, SMB signing, and account mismatches, then verify access."
keywords:
  - "windows share keeps asking for credentials"
date: 2026-11-28T22:29:26+08:00
publishDate: 2026-11-28T22:29:26+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You are opening a shared folder from another LAN PC, and Windows rejects the account you know is correct, leaving you stuck at the credentials prompt. This is a controlled diagnosis for that specific rejection, not a broad SMB guide.

## Check the account format and stored credential
At the prompt, enter the username as `PCNAME\username` or `username@PCNAME`, not just `username`. If it still fails, open Credential Manager on the client and remove any Windows Credentials entries for the host PC or its IP. Then retry the share. If the prompt now accepts the password, a stale stored credential was the cause.

## Confirm the account exists and is allowed
On the host PC, open Computer Management > Local Users and Groups and confirm the exact username. Then check the folder's Properties > Sharing > Advanced Sharing > Permissions and ensure that account or its group has access. Also confirm the account is not disabled or expired. If the account is valid but still rejected, move to the next check.

## Test SMB signing and guest fallback
On the client, open PowerShell as administrator and run `Get-SmbClientConfiguration | Select RequireSecuritySignature`. If it returns True, the host must also require signing. On the host, run `Get-SmbServerConfiguration | Select RequireSecuritySignature`. A mismatch can cause rejection. Also disable guest access on the client with `Set-SmbClientConfiguration -EnableInsecureGuestLogons $false`, then retry.

## Verification test
From the client, run `net use \\HOST\Share /user:PCNAME\username *` and enter the password. A successful mapping confirms the fix. If it still fails, note the exact error code.

## Rollback note
If a change breaks other shares, re-enable the previous setting, such as restoring the removed credential or reverting the signing value. For persistent rejection,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).

If the prompt still loops, the cause is likely a **windows share keeps asking for credentials** conflict between stored credentials and host policy, which the checks above isolate.
