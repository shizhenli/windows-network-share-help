---
title: "Network Credentials Prompt: Why the Correct Account Is Rejected and How to Confirm It"
description: "The correct account is rejected at the network credentials prompt when opening a LAN share. Run these checks to confirm the rejection and restore access."
seo_title: "Network Credentials Prompt Rejects Correct Account: Practical Fix"
seo_description: "The correct account is rejected at the network credentials prompt when opening a LAN share. Run these checks to confirm the rejection and restore access."
keywords:
  - "network credentials prompt"
date: 2026-11-21T16:51:11+08:00
publishDate: 2026-11-21T16:51:11+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You open a shared folder on another Windows PC, type the account you know is correct, and the **network credentials prompt** rejects it anyway.

## Confirm the rejection is consistent

First, separate a typo from a real rejection. Open the share again and enter the username as COMPUTERNAME\username, using the sharing PC's actual computer name. If the prompt reappears with the same error, the rejection is consistent, not a one-off typing mistake. If it accepts the name this time, you had a local-account format issue, and you can stop here.

## Check the account on the sharing PC

On the PC that hosts the folder, open Local Users and Groups and confirm the account exists, is enabled, and has a password. An account with a blank password is often blocked for network logon by default. Also check that the account is listed in the folder's share permissions and in the NTFS permissions on the Security tab. If it is missing from either, the rejection is expected; add it with at least Read access, then retry.

## Clear stale saved credentials

On the connecting PC, open Credential Manager and remove any Windows Credentials entry for the sharing PC's name or IP address. A saved old password can be sent silently and rejected before you are asked again. After removal, reconnect so the prompt asks fresh.

## Verification test

From the connecting PC, run net use \\COMPUTERNAME\ShareName /user:COMPUTERNAME\username in Command Prompt and enter the password when asked. A success message confirms the account works; an access-denied error confirms the rejection is real and points back to permissions or account state.

## Rollback note

If a permission change makes things worse, remove the added account from share and NTFS permissions to return to the previous state before trying another path. If the rejection persists after these checks,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).
