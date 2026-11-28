---
title: "Shared Folder Not Visible on Another PC: Check These Three Things First"
description: "A practical troubleshooting guide to fix a Windows shared folder that is invisible to another PC on the same LAN. Step-by-step checks for network discovery, sharing permissions, and UNC path verification."
seo_title: "Windows Network Share Not Showing: Fix Invisible Shared Folder"
seo_description: "A practical troubleshooting guide to fix a Windows shared folder that is invisible to another PC on the same LAN. Step-by-step checks for network discovery, sharing permissions, and UNC path verification."
keywords:
  - "windows network share not showing"
date: 2026-11-28T22:01:46+08:00
publishDate: 2026-11-28T22:01:46+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

## Check Network Discovery and Sharing Settings

You've shared a folder on one Windows PC, but the other computer can't see it in File Explorer or via UNC path. Before changing anything, confirm that both PCs are on the same network profile and that network discovery is enabled. On the sharing PC, open Settings > Network & Internet > Ethernet (or Wi-Fi), click the active connection, and ensure the network profile is set to Private. Then go to Control Panel > Network and Sharing Center > Advanced sharing settings and turn on network discovery and file and printer sharing for the Private profile. If the other PC still cannot see the share, try accessing it directly by typing \\SharingPCName\ShareName in the Run dialog (Win+R). If that works, the issue is discovery, not the share itself. If it fails, continue below.

## Verify Share Permissions and SMB Service

On the sharing PC, right-click the folder, choose Properties > Sharing > Advanced Sharing, and confirm the share is enabled. Click Permissions and ensure the account used by the other PC has at least Read access. Next, check that the Server (LanmanServer) service is running: open services.msc and verify Server is started and set to Automatic. A stopped Server service makes the share completely invisible, which is a common cause of **windows network share not showing**. Also confirm Windows Firewall allows File and Printer Sharing on the Private profile.

## Verification Test

From the other PC, open Command Prompt and run net view \\SharingPCName. If the share appears, try net use Z: \\SharingPCName\ShareName. A successful mapping confirms the share is reachable. If net view returns error 53 or 6118, the problem is network-level, not permissions.

## Rollback and Recovery

If you changed the network profile or firewall rules and the share still fails, revert those settings to their previous state. Document any permission changes so you can restore them if needed. For persistent UNC errors,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult) with the exact error code.
