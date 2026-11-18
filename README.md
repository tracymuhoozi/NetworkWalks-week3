# NetworkWalks-week3
Week 3 Project module
# NetworkWalks — Week 3: Password Cracking

Cybersecurity & Ethical Hacking Internship — Week 3 project work.

This repository documents two password-cracking labs in which the passwords of
two protected PDF files were recovered and the hidden flag inside each file was
captured. Module 1 uses **John the Ripper (JTR)** with the **Johnny** GUI;
Module 2 uses the browser-based **NetworkWalks Hash Calculator** and
**Password Cracker**.

> ⚠️ **Ethical use only.** All tools here were used against the training files
> provided for this authorised lab. Password-cracking tools must only be used
> with permission and in line with local laws and organisational policies.

---

## Table of Contents
- [Objective](#objective)
- [Background](#background)
- [Tools & Environment](#tools--environment)
- [Module 1 — Password Cracking with JTR](#module-1--password-cracking-with-jtr)
- [Module 2 — Password Cracking with NetworkWalks Tools](#module-2--password-cracking-with-networkwalks-tools)
- [Results Summary](#results-summary)
- [Key Learnings](#key-learnings)
- [Repository Structure](#repository-structure)

---

## Objective

Recover the passwords of two password-protected PDF files and capture the flag
inside each one, using two different cracking approaches:

- **Module 1** — Crack `My Locked PDF1.pdf` using John the Ripper (JTR) and the
  Johnny GUI on Windows.
- **Module 2** — Crack `My Locked PDF2.pdf` using the NetworkWalks Hash
  Calculator and Password Cracker (dictionary attack) in a web browser.

## Background

When a PDF is locked, the password itself is **not** stored in the file — a
one-way **hash** of the password is stored instead. To recover the password you
first **extract the hash** from the file, then run it through a cracking tool
that hashes candidate passwords and compares them against the target hash until
a match is found. This same two-stage workflow applies whether you use a desktop
tool (John the Ripper) or browser-based tools (NetworkWalks).

## Tools & Environment

| Tool / Component | Details |
|---|---|
| John the Ripper | 1.9.0-jumbo-1 OMP (cygwin 64-bit, x86_64, AVX2, AC) |
| Johnny GUI | Graphical front end for John the Ripper |
| Online Hash Crack | `onlinehashcrack.com` PDF Hash Extractor (pdf2john format) |
| NetworkWalks Hash Calculator | `networkwalks.com/hash-calculator/` |
| NetworkWalks Password Cracker | `networkwalks.com/password-cracker/` (dictionary attack) |
| Browser | Microsoft Edge |
| OS | Microsoft Windows |

---

## Module 1 — Password Cracking with JTR

**Steps**

1. Installed John the Ripper (jumbo build) and the Johnny GUI on Windows.
2. In Johnny → **Settings**, set the JTR executable path to `run\john.exe`.
   Johnny detected `John the Ripper 1.9.0-jumbo-1 OMP [cygwin 64-bit x86_64 AVX2 AC]`.
3. Used the Online Hash Crack **PDF Hash Extractor** to pull the crackable hash
   (pdf2john format) from `My Locked PDF1.pdf`.
4. Saved the full hash (starting with `$pdf$`) into `hash1.txt`.
5. In Johnny → **Open password file** → selected `hash1.txt` → **Start new attack**.
6. Johnny recovered the password — status `100% (1/1: 1 cracked, 0 left) [format=PDF]`.
7. Opened `My Locked PDF1.pdf` with the recovered password to reveal Flag 1.

**Extracted hash**

```
$pdf$4*4*128*-1028*1*16*ca7f72f11459cba469f1005a8765ed51*32*f32d8fa1bfbe2648226dffc39f7909ea0021446990b9e4114071a4d9104984c1*32*9322f50c29569712067a775264635e4954ccb1b99e209d664984054ffad30a6a
```

**Result**

- Recovered password: `good-luck`
- 🚩 **Flag 1:** `nw{cybersecurity_flag_captured_2608}`

---

## Module 2 — Password Cracking with NetworkWalks Tools

**Steps**

1. Opened the NetworkWalks **Hash Calculator** → **PDF** tab.
2. Selected `My Locked PDF2.pdf` (204.7 KB). The tool parsed the PDF locally,
   confirmed it was encrypted, and extracted a pdf2john / hashcat-compatible hash.
3. Copied the complete hash value (starting with `$pdf$`).
4. Opened the NetworkWalks **Password Cracker**, pasted the hash, and started the
   **dictionary attack**.
5. The tool hashed each word in its wordlist and matched it against the PDF hash —
   cracked after trying **91 / 100** candidates.
6. Opened `My Locked PDF2.pdf` with the recovered password to reveal Flag 2.

**Extracted hash**

```
$pdf$4*4*128*-1028*1*16*0853f2cde0ef15b1c0f93ed229d3b1ad*32*8f13ce5aa39ad974364d36a057da76790021446990b9e4114071a4d9104984c1*32*ceecdac74b19b5a62688d3b3524e1374c955cbb9cc3c45316494d9446ef81af1
```

**Result**

- Recovered password: `password1`
- 🚩 **Flag 2:** `nw{networkwalks_persistence_jtr_270521}`

---

## Results Summary

| Module | Tool / Method | Target File | Password | Flag |
|---|---|---|---|---|
| 1 | John the Ripper / Johnny GUI | My Locked PDF1.pdf | `good-luck` | `nw{cybersecurity_flag_captured_2608}` |
| 2 | NetworkWalks dictionary attack | My Locked PDF2.pdf | `password1` | `nw{networkwalks_persistence_jtr_270521}` |

## Key Learnings

- A locked file stores a **one-way hash**, not the password — extraction must
  come before cracking.
- The **extract-then-crack** workflow is the same for desktop and browser tools.
- **Johnny** makes John the Ripper beginner-friendly by replacing long commands
  with a point-and-click interface.
- A **dictionary attack** cracks common passwords (`password1`) and simple
  phrases (`good-luck`) almost instantly — which is exactly why weak passwords
  are dangerous.
- Cracking is mostly about **patience and the right wordlist** — the core mindset
  of a real security tester.

## Repository Structure

```
NetworkWalks-week3/
├── README.md
├── report/
│   └── W3_Password_Cracking_Report.docx   # full write-up with screenshots
└── screenshots/                           # step-by-step evidence (Module 1 & 2)
```

---

*Cybersecurity & Ethical Hacking Internship — NetworkWalks, Week 3.*
