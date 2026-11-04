# Comparing-Hash-Values-to-Verify-File-Integrity# Comparing Hash Values to Verify File Integrity

A hands-on forensics lab using MD5 Calculator to compute file hashes directly from the Windows context menu, then comparing them against pre-recorded baseline hashes to verify whether evidence files had been modified.

## Scenario
A forensic investigator needs to verify that copies of sensitive files still match their known-good state, by comparing current hash values against a trusted baseline recorded earlier. This lab worked through that exact comparison using two evidence files with deliberately different outcomes.

## What I did

### 1. Installed MD5 Calculator and computed a hash
- Right-clicked an evidence image file directly in Windows Explorer and selected MD5 Calculator from the context menu — no separate file picker needed, hash computed and displayed immediately

### 2. Established the baseline
- Opened `Hashes.txt` in the evidence folder, containing pre-recorded, trusted MD5 hash values for several files captured at an earlier, known-good point in time

### 3. Compared `Kitty.jpg` against its known hash
- Copied the recorded hash from `Hashes.txt`
- Right-clicked `Kitty.jpg` → MD5 Calculator, pasted the known value into the **Compare To** field
- Result: **match** — confirmed the file was identical, bit for bit, to the version the baseline hash represented

### 4. Compared `Model.png` against its known hash
- Same process, same source for the baseline value
- Result: **mismatch** — the current file's hash did not match the recorded baseline
- This flags the file for further investigation; a mismatch alone doesn't explain what changed, only that something did (the lab pointed to a later anti-forensics module covering exactly this kind of finding, e.g. steganography or payload tampering)

## Key takeaways
- A hash mismatch is a flag, not a diagnosis — it tells you precisely that a file differs from a trusted baseline, not why or how, and marks exactly where further investigation needs to focus
- The technique is only as trustworthy as the baseline itself — `Hashes.txt` (or its real-world equivalent) needs its own protection and chain of custody, since a baseline an attacker could also tamper with defeats the whole check
- Automated hash comparison matters because manual comparison of two 32-character hex strings is unreliable — a single differing character is nearly impossible to catch by eye but represents a completely different underlying file
- This is a narrower, more specific check than looking a hash up against an external database (e.g. VirusTotal, from an earlier lab) — it answers "is this exact file still what it's supposed to be," not "has anyone else flagged this file as malicious"
- Tool-level integration (right-click → hash, directly in the file system) reduces friction and error across repeated checks on many files, which matters in a real investigation involving more than a handful of files

## Tools
MD5 Calculator

---
*Completed in an isolated training lab environment using provided evidence files and a pre-recorded hash baseline.*
