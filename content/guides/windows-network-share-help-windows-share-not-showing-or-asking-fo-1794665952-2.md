---
title: "Windows Share Not Showing? Test SMB Directly Before Changing Permissions"
description: "When another PC can't see your Windows shared folder, test SMB directly to isolate the cause before changing permissions or network settings."
seo_title: "Windows Share Not Showing? Test SMB Directly First"
seo_description: "When another PC can't see your Windows shared folder, test SMB directly to isolate the cause before changing permissions or network settings."
keywords:
  - "Windows Share Not Showing or Asking for Credentials: Test SMB Directly"
date: 2026-11-21T16:48:05+08:00
publishDate: 2026-11-21T16:48:05+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

## Troubleshooting

You've shared a folder on one Windows PC, but the other computer can't see it in Explorer or by its UNC path.

Before you touch permissions, confirm whether SMB itself is reachable. On the second PC, open Command Prompt and run `net view \\COMPUTERNAME` using the sharing PC's name. If you get system error 53 or 6118, name resolution or network discovery is failing, not share permissions. Next, run `net use \\IPADDRESS\SHARENAME` with the sharing PC's IPv4 address and the exact share name. A prompt for credentials means SMB is reachable and the problem is authentication; an immediate error means the connection never reached the share.

If the IP test connects but the name test fails, the share is fine and the name is the issue. If both fail, check that File and Printer Sharing is enabled in the sharing PC's network adapter settings and that Windows Firewall allows SMB-In on the current profile. This is the controlled diagnosis behind **Windows Share Not Showing or Asking for Credentials: Test SMB Directly**.

Verification: from the second PC, run `net use \\IPADDRESS\SHARENAME /user:COMPUTERNAME\USERNAME` with valid credentials. Success confirms SMB and authentication work; then retry the UNC path in Explorer. If Explorer still hides the share, the remaining fault is discovery, not access.

Rollback: if you changed firewall rules or sharing settings during testing, restore them to their previous state before finishing. If the direct test fails and you need guided help,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).

Repeat the same check after a restart and confirm the result twice.
