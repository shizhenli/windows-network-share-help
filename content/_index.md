---
title: Windows Network Share Help
seo_title: Windows Network Share Help | Missing or Credential Loop
seo_description: Remote help for Windows shares that disappear, ask for credentials repeatedly, or deny access.
keywords:
- windows network share not showing
- windows share keeps asking for credentials
- smb share access denied
hero_kicker: LOCAL NETWORK FILE SHARING
hero_h1: Windows share missing or asking for credentials?
hero_lead: Verify one source PC and one client, then separate discovery, SMB, account, and permission failures before changing the share.
hero_proof:
- One source PC and one client
- Discovery, SMB, and account checked
- A named file opened from the client
hero_alt: Multiple laptops and monitors on a desk showing shared files
hero_title: Windows network share across several displays
body_alt: Windows File Explorer showing a network share and credential prompt
body_title: Windows SMB share and credential verification
body_caption: The test ends with a specific file readable from the client, not just the PC appearing in Network.
failures_kicker: THE THREE FAILURES WE SEE
failures_heading: What is going wrong?
test_kicker: HOW WE TEST
test_heading: Find the failing layer, then prove the fix.
scope_kicker: SERVICE SCOPE
scope_heading: What is included
scope_note: The session covers one agreed device and one verified path. Anything outside the written scope is quoted separately before work starts.
faq_kicker: FAQ
faq_heading: Before you book
consult_heading: Tell us what is happening.
consult_lead: Send the device, software, exact symptom, and what you have already tried. We will confirm scope and a fixed quote before booking.
form_placeholder: Device, software version, exact symptom, and what you have tried.
first_guide_url: /guides/windows-network-share-help/
symptoms:
- title: The share is not listed
  text: The source PC is visible in Network, but the shared folder does not appear on the client.
- title: Credentials repeat forever
  text: The client accepts the username/password, then prompts again or reports access denied.
- title: Access denied after connecting
  text: The share opens, but the client cannot read or write the intended folder.
checks:
- title: Test by address, not browse
  text: Open `\\source-pc\share` directly from the client. This separates discovery from the SMB service.
- title: Confirm the account
  text: Use a local account with a password and note whether it is a Microsoft account. Check the credential Windows is actually sending.
- title: Check share and NTFS permissions
  text: Both the share permission and the folder's NTFS permission must allow the account. Review effective access, not just the share tab.
- title: Open a named file
  text: Create a small text file, open it from the client, and check read/write as agreed.
included:
- One source PC and one client
- Direct SMB path and discovery checks
- Account and permission review
- One file read/write verification
excluded:
- Router or VLAN reconfiguration
- Domain controller administration
- Data recovery from a failed disk
- Guaranteeing every Windows edition
faqs:
- q: Why does the PC show but not the share?
  a: Discovery and file sharing are separate. A direct `\\pc\share` test shows whether SMB works even when browsing does not.
- q: Should I disable password-protected sharing?
  a: Not as a permanent fix. Use a proper account and permissions; disabling protection weakens the share.
- q: Can you recover files?
  a: No. The session fixes access to an existing share; recovery from a failed drive is separate.
---
