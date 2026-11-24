---
title: "Network Credentials Prompt Rejects the Correct Account: Clear Stale Credentials and Verify Access"
description: "Fix the network credentials prompt rejecting the correct account on a Windows LAN share by clearing stale credentials, checking account lockout, and verifying with a direct SMB test."
seo_title: "Network Credentials Prompt Rejects Correct Account: Fix Stale Credentials"
seo_description: "Fix the network credentials prompt rejecting the correct account on a Windows LAN share by clearing stale credentials, checking account lockout, and verifying with a direct SMB test."
keywords:
  - "network credentials prompt"
date: 2026-11-24T10:11:48+08:00
publishDate: 2026-11-24T10:11:48+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You open a shared folder from another LAN PC, type the correct username and password, and Windows returns you to the same **network credentials prompt** with an access error.

## Check for a stale stored credential first

On the PC opening the share, open Credential Manager and look under Windows Credentials for an entry matching the host name or IP of the sharing PC. If an old entry exists, remove it. Then open the share again and re-enter the account. If the prompt accepts the credentials now, the stored entry was the cause.

## Confirm the account is not locked or expired

On the sharing PC, open Local Users and Computers or Computer Management and check the account you are using. A locked-out or expired account rejects even a correct password. Unlock it or reset the password there, then retry from the other PC.

## Test SMB directly to separate prompt issues from Explorer issues

On the PC opening the share, run this in Command Prompt:

net use \\HOSTNAME\ShareName /user:HOSTNAME\Username *

Replace HOSTNAME and ShareName with the real values. Enter the password when asked. If this succeeds, Explorer was holding a stale session; disconnect any mapped drive and reconnect. If it fails with the same rejection, the problem is on the sharing PC's account or share permissions.

## Rollback note

If clearing credentials or changing the account breaks another working share, re-add the removed entry in Credential Manager with the original username and password.

## Verify the fix

Open the share from the other PC without being prompted, or confirm the net use command reports success. If rejection continues after these checks,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).
