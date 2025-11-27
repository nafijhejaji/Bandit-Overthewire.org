# BANDIT overthewire.org
#In sha allah i'll remain consistent this time <br>


<!-- PROJECT TITLE -->
# 🐧 Bandit Wargame Walkthrough

A clean, consistent, and GitHub-friendly README for documenting OverTheWire Bandit levels.  
Works perfectly with GitHub’s Markdown renderer (no external styling required).

---

<!-- BADGES -->
<p align="left">
  <a href="https://overthewire.org/wargames/bandit/"><img src="https://img.shields.io/badge/Wargame-Bandit-1f6feb?labelColor=0d1117" alt="Bandit"></a>
  <img src="https://img.shields.io/badge/Markdown-GitHub%20Flavored-2ea043?labelColor=0d1117" alt="Markdown">
  <img src="https://img.shields.io/badge/Status-In%20Progress-f85149?labelColor=0d1117" alt="Status">
</p>

---

## 📚 Table of contents
- [Overview](#overview)
- [How to use this guide](#how-to-use-this-guide)
- [Conventions](#conventions)
- [Tips](#tips)

---

## Overview
This repo documents each Bandit level with the goal, the pitfall, the correct command, and the reason it works—kept short, accurate, and reproducible.

---

## How to use this guide
- **Copy a level section** and paste for the next one.
- Keep commands in fenced code blocks with a language tag (e.g., `bash`) for syntax highlighting.
- Use collapsible sections for clean navigation.

---

## Conventions
- **Prompt style:** `banditX@bandit:~$` (replace X with level number)
- **Commands:** in `bash` fenced code blocks
- **Passwords:** in separate fenced blocks for clarity
- **Explanations:** bullet points only, no fluff

---

## Levels

### Bandit Level 2 → Level 3

> Filename with spaces and leading `--` in the home directory.

#### 🎯 Goal
Find the password stored inside:



#### ❓ Problem
- Leading `--` is parsed as an option by many commands.
- Spaces break naive `cat` usage without quoting.

#### 💡 Solution
```bash
bandit2@bandit:~$ ls -la
bandit2@bandit:~$ cat ./"--spaces in this filename--"
```bash












## 🔐 Bandit Level 5 → Level 6

### 🎯 Level Goal
Find the file inside the `inhere` directory that is:
- a regular file  
- human-readable  
- **1033 bytes**  
- **NOT executable**

---

### 🧠 Approach
We use the `find` command with multiple conditions to filter the correct file based on:
- file type  
- size  
- permissions  

---

### 📝 Commands I Used

#### 1. Navigate into the directory:
```bash
cd inhere
find . -type f -size 1033c ! -executable





