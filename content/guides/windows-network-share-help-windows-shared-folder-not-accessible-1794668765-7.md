---
title: "Shared Folder Not Visible on Another PC: Check the Share Name and Path"
description: "Troubleshoot a Windows shared folder that is invisible to another LAN PC. Check the share name, path, and permissions to restore access."
seo_title: "Fix windows shared folder not accessible: Share Invisible to Other PC"
seo_description: "Troubleshoot a Windows shared folder that is invisible to another LAN PC. Check the share name, path, and permissions to restore access."
keywords:
  - "windows shared folder not accessible"
date: 2026-11-23T11:11:58+08:00
publishDate: 2026-11-23T11:11:58+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You've shared a folder on your Windows PC, but the other computer on your LAN can't see it in File Explorer or by UNC path.

## Confirm the Share Exists and Its Exact Name

On the host PC, open Command Prompt and run `net share`. Look for your folder in the list. If it's missing, the share wasn't created—recreate it via right-click > Properties > Sharing. Note the exact share name (e.g., `Docs`), not the folder path. If the name contains spaces or special characters, simplify it to letters and numbers only. This is a common reason for **windows shared folder not accessible** when the folder is invisible to the other PC.

## Test the UNC Path Directly

On the other PC, press Win+R and type `\\HOST-PC\ShareName` (replace with actual host name and share name). Press Enter. If you get an error like "Windows cannot access" or a credentials prompt, the share exists but permissions or name resolution is failing. If you get "The network path was not found," the host name isn't resolving—try the host's IP address instead (e.g., `\\192.168.1.10\ShareName`).

## Check Share Permissions

On the host, right-click the folder > Properties > Sharing > Advanced Sharing > Permissions. Ensure the other PC's user account (or Everyone, for testing) has at least Read access. Also check the Security tab for NTFS permissions. If the account isn't listed, add it with Read access.

## Verification Test

From the other PC, run `net view \\HOST-PC` in Command Prompt. You should see the share listed. Then try opening the UNC path again. If it opens, the issue is resolved.

## Rollback Note

If changes don't help, revert any permission changes to avoid locking yourself out. For persistent issues,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).
