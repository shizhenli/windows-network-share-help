---
title: 'Windows Share Not Showing or Asking for Credentials: Test SMB Directly'
description: A direct SMB test that separates discovery, credentials, share permissions, and NTFS access.
seo_title: Windows Network Share Missing or Credential Loop
seo_description: A direct SMB test that separates discovery, credentials, share permissions, and NTFS access.
keywords:
- windows network share not showing
- windows share keeps asking for credentials
- smb share access denied
date: '2026-11-13'
draft: false
categories:
- File Sharing
category_slug: file-sharing
---

**windows network share not showing**. 

<p>Windows can show a computer in Network while the share is unreachable, or accept a password and still deny the folder. Test the SMB path directly.</p>
<h2>Before you start</h2><ul>
<li>Source Windows PC and one client</li>
<li>A local account with a password</li>
<li>The exact share name</li>
<li>Permission to read or write one test file</li>
</ul>
<h2>Step-by-step checks</h2>
<h3>Step 1: Open the share by path</h3>
<p>On the client, press Win+R and enter `\\source-pc\share`. Use the source PC's name and the exact share name, not a mapped drive.</p>
<p>Check: The client reaches a credential prompt or the share contents.</p>
<h3>Step 2: Clear stale credentials</h3>
<p>Open Credential Manager and remove old entries for the source PC. Reconnect and enter the intended local account once.</p>
<p>Check: The client sends the current account, not an old cached one.</p>
<h3>Step 3: Check both permission layers</h3>
<p>On the source, review the share permission and the folder's NTFS permissions for the account. Confirm the client's effective access.</p>
<p>Check: The account has the required share and NTFS access.</p>
<h3>Step 4: Test read and write</h3>
<p>Create a small text file from the client in the agreed folder, reopen it, and edit it. Check whether the result matches the promised access.</p>
<p>Check: The client can read and write the test file.</p>
<h3>Step 5: Reconnect after restart</h3>
<p>Disconnect the mapped drive or session, restart the client, and open the share again. Confirm the credential persists correctly.</p>
<p>Check: Access works after a client restart without a loop.</p>
<h2>Verify the result</h2>
<p>The client opens the share by path, authenticates with the intended account, and reads/writes a test file after reconnecting.</p>
<h2>Rollback</h2>
<p>Remove only the test file and test mapping. Restore previous share permissions if a change is rejected.</p>
<p><a href="/#consult">Ask for help with this exact symptom</a> · All troubleshooting guides</p>
