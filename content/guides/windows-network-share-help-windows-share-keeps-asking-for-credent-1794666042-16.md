---
title: "Windows Share Keeps Asking for Credentials: When the Correct Account Is Rejected"
description: "When Windows share keeps asking for credentials and rejects the correct account, use these targeted checks to isolate the cause and restore access."
seo_title: "Windows Share Keeps Asking for Credentials: Fix Rejected Account"
seo_description: "When Windows share keeps asking for credentials and rejects the correct account, use these targeted checks to isolate the cause and restore access."
keywords:
  - "windows share keeps asking for credentials"
date: 2026-11-21T16:54:10+08:00
publishDate: 2026-11-21T16:54:10+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You are opening a shared folder from another LAN PC, and Windows rejects the account you know is correct, leaving you stuck before you can diagnose the problem.

## Check the credential being sent

First, confirm which account Windows is actually using. Open Credential Manager on the client PC and look under Windows Credentials for any entry matching the server's name or IP. If an old or wrong entry exists, remove it, then reconnect. A stale stored credential can override the correct one you type.

Next, test with the server's IP address instead of its hostname. If the IP works but the name fails, the issue is name resolution or a mismatched cached credential, not the password itself.

## Verify the account on the server

On the sharing PC, open Computer Management and check Local Users and Groups. Confirm the account exists, is not disabled, and has permission on the share and NTFS security tab. If the account is a Microsoft account, try the local account format (PCName\Username) instead of the email address.

## Run a direct verification test

From the client, open Command Prompt and run: net use \\SERVER\Share /user:SERVER\Username

Enter the password when prompted. If it connects, the GUI prompt was using a cached credential. If it returns System error 5, the server is actively rejecting the account, so focus on server-side permissions. If it returns error 1326, the username or password format is wrong.

## Rollback and recovery

Before changing permissions, note the current share and NTFS settings so you can restore them. If a change makes things worse, reapply the original entries. Disconnect test mappings with net use \\SERVER\Share /delete.

If the account is still rejected after these checks, the cause may be a policy or SMB configuration issue. For a guided diagnosis of why **windows share keeps asking for credentials**,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).
