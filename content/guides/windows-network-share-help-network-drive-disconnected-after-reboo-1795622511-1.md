---
title: "Mapped Drive Gone After Restart: Diagnose the Disconnect Before Re-Mapping"
description: "A mapped drive disappears after a restart. Follow these checks to diagnose why the network drive disconnected after reboot and restore the persistent connection."
seo_title: "Network Drive Disconnected After Reboot: Controlled Diagnosis"
seo_description: "A mapped drive disappears after a restart. Follow these checks to diagnose why the network drive disconnected after reboot and restore the persistent connection."
keywords:
  - "network drive disconnected after reboot"
date: 2026-11-28T22:01:46+08:00
publishDate: 2026-11-28T22:01:46+08:00
draft: false
categories:
  - "File Sharing"
category_slug: "file-sharing"
---

You mapped a shared folder from another LAN PC, but after restarting Windows the drive letter is missing from File Explorer.

## Check the share is reachable first

Open Command Prompt and run `ping <hostname>` using the sharing PC's name. A reply means name resolution works. If it fails, try `ping <IP address>`; a reply there points to a name-resolution problem, not a broken mapping. Next run `net use` to list current connections. If your drive letter is absent, the mapping was not restored at logon.

## Check persistence and credentials

In File Explorer, right-click the missing drive if it still appears under This PC, choose Properties, and confirm the connection type. Then open Credential Manager and look under Windows Credentials for the sharing PC's entry. A stale or mismatched saved credential can prevent reconnection. Remove only that entry, then reconnect and tick Reconnect at sign-in. This is the usual point where a **network drive disconnected after reboot** can be confirmed as a persistence or credential issue rather than a network fault.

## Verification test

Reconnect the drive with `net use Z: \\HOST\Share /persistent:yes`, replacing the letter, host, and share name. Sign out and back in, then restart once. Open File Explorer and confirm the drive letter and its contents appear without manual reconnection.

## Rollback note

If the drive still vanishes, run `net use Z: /delete` and remap without the persistent flag, then reconnect manually after each restart while you investigate further. For a guided review of your configuration,

![Windows File Explorer showing a network share and credential prompt](/images/service-detail-960.webp "Windows SMB share and credential verification")

[Ask for help](/#consult).
