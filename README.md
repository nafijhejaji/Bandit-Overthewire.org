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



## 🔐 Bandit Level 0 → Level 1

### 🎯 Level Goal
Use SSH to connect to the Bandit game.

---

### 📝 Commands I Used
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

🔑 Password for Next Level
```bash
bandit0
```





## 🔐 Bandit Level 1 → Level 2

### 🎯 Level Goal
Read the file named `-` inside the home directory.

---

### ❗ Challenge
`cat -` does NOT work because `-` means **stdin** in Linux.

---

### 📝 Commands I Used
List files:
```bash
ls -la
```

Read the file using a path:
```bash
cat ./-
```
🔑 Password for Next Level
```bash
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```



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
```

🔑 Password for Next Level
```bash
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```
## ✅ What I Learned

How to handle filenames with spaces

Using quotes " " to wrap multi-word filenames





---

## 🔐 Bandit Level 3 → Level 4

### 🎯 Level Goal
Find a hidden file inside the `inhere` directory.

---

### 📝 Commands I Used
Navigate to the directory:
```bash
cd inhere
```
List hidden files:
```bash
ls -la
```

Read the file:
```bash
cat ./"...Hiding-From-You"
```
## ✅ What I Learned

Hidden files start with .

ls -la shows everything


---




## 🔐 Bandit Level 4 → Level 5

### 🎯 Level Goal
Among many files, find the one that is **human-readable**.

---

### 📝 Commands I Used

Identify file types:
```bash
file ./*
```

Read the ASCII text file:
```bash
cat ./"-file07"
```
🔑 Password for Next Level
```bash
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

## ✅ What I Learned

Using file to identify readable files

ASCII text vs binary files






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

```

Read the file:
```bash
cat ./maybehere07/.file2
```

🔑 Password for Next Level
```bash
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

## ✅ What I Learned

Used find to locate files by size, type, and permissions, and learned to search efficiently in nested directories.


## Bandit Level 6 → 7

### 🎯 Task  
Find a file owned by **user bandit7**, **group bandit6**, and exactly **33 bytes** in size.

---

### 🧠 What I Learned  
- How to use the `find` command to locate files based on user, group, and size  
- Meaning of `-type f` (regular file) and `33c` (33 bytes)

---

### 🛠️ Commands I Used  
```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
```
📍 Found the password here
```bash
cat /var/lib/dpkg/info/bandit7.password
```

🔐 Password
```bash
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

## ✅ What I Learned (Level 6 → 7)

How to use find to locate files by user, group, type, and exact size.

How to read system files and handle permission errors (2>/dev/null) efficiently.

2> = redirect error output

/dev/null = trash can

2>/dev/null = hide errors

Used with find, grep, cat, etc.




## 🔐 Bandit Level 7 → 8

### 🎯 Task  
Search inside `data.txt` to find the password for the next level. The file contains many key-value pairs on separate lines.

---

### 🛠️ Commands I Used
List files:
```bash
ls
```

Search for the keyword (Bandit provided keyword: millionth):
```bash
grep "millionth" data.txt
```

🔎 Output :
```bash
millionth	dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```


The password is the value after the tab.

🔐 Password for Level 8
```bash
dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

## ✅ What I Learned

How to use "grep" to search inside files for exact text
```bash
<search-command> "text" data.txt
```
How to extract the needed data quickly from structured text files





## 🔐 Bandit Level 8 → 9

### 🎯 Task  
The password for the next level is stored in `data.txt`, but the file contains **many lines**, and only one of them is unique.  
All other lines are duplicates.

---

### 🛠️ Steps I Took  

1. Viewed the file:
```bash
cat data.txt
```

Needed to find the only unique line.

Used sorting + unique flag:
```bash
sort data.txt | uniq -u
```

sort arranges lines in order

uniq -u prints only the lines that appear exactly once

The output showed a single unique string — which is the password.

🔐 Password for Level 9
```bash
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```


## ✅ What I Learned

How to combine commands using a pipe (|)

Why sort is needed before using uniq

How uniq -u helps find a single unique line in a large file



## 🔐 Bandit Level 9 → 10

### 🎯 Task  
The password for the next level is stored in `data.txt`, but the file contains **binary data**.  
Reading it with `cat` shows unreadable characters, so it's not a plain text file.

---

### 🛠️ Steps I Took  

1. Tried viewing the file:
```bash
cat data.txt
```

The output was full of random binary symbols.

Used the strings command to extract only the human-readable text:
```bash
strings data.txt
```

Among the readable output, one line clearly contained the password.

🔐 Password for Level 10
```bash
FGUW5 i 1LVJr×X9kMYMmIN4MgbpfMiqey
```


## ✅ What I Learned

How to extract readable text from binary files using strings

Why cat doesn’t work for binary data

How password clues can be hidden inside non-text files

Basic idea of analyzing unknown file types in Linux/CTFs




