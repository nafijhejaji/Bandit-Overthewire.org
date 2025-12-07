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


## 🔐 Bandit OverTheWire — Level 10 → Level 11

### 🎯 Challenge Summary
In this level, the password was stored in a file but encoded using **base64**.  
The task was to decode it and retrieve the next level's password.

---

### 🧠 What I Learned
- How to identify base64-encoded text  
- How to decode data using:
  ```bash
  base64 -d filename
  ```
1.The difference between encoding and encryption
2.Better command-line navigation and file handling

## 🛠️ Steps I Took
# Check the file content
```bash
cat data.txt
```
# Decode the base64 encoded password
```bash
base64 -d data.txt
```
🔑 The password for next level is
```bash
dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```
### 🧠 What I Learned
- How to recognize base64-encoded text  
- How to decode base64 using `base64 -d`  
- The difference between readable text and encoded text  
- How Linux handles file contents that look random but are actually encoded  
- Improved confidence working with command-line utilities
- 


## Bandit Level 11 → Level 12

### 🔍 Goal  
The password for the next level is stored in `data.txt` but it is **ROT13 encoded**.  
ROT13 shifts every letter by 13 positions in the alphabet.

---

### 🧠 What I Had To Do  
- Read the contents of `data.txt`  
- Decode the ROT13 text to get the real password  

---

### 🛠️ What I Did  

#### 1️⃣ Listed the file
```bash
ls
```
2️⃣ Viewed the encoded text
```bash
cat data.txt
```
It showed something like:
```bash
Gur cnffjbeq vf 7k16JArUVv5LxVuJfsSVdbbtaHGlw9D4
```

3️⃣ Decoded using ROT13 with tr
```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```
This command shifts letters by 13 positions and reveals the actual password.
password for the next level:

```bash
7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

### 📘 What I Learned (Level 11 → 12)

- Learned about **ROT13 encoding**, a simple letter substitution cipher that shifts alphabet characters by 13 positions.
- Understood how ROT13 is *reversible* — applying ROT13 twice returns the original text.
- Used the **`tr` command** in Linux to translate characters from one set to another.
- Practiced decoding text using:
  ```bash
  tr 'A-Za-z' 'N-ZA-Mn-za-m'



## Bandit Level 12 → Level 13

### 🔍 Goal
The password for the next level is hidden inside multiple layers of compressed files.
The file data.txt is a hexdump, which must be reversed into its original binary form and then extracted repeatedly until the final password is found.
---

 
## 🔧 Solution
1. Convert the hexdump back to binary
```bash
xxd -r data.txt data.bin
```

3. Check the file type
```bash
file data.bin
```

5. Rename the file based on detected type

Examples:
```bash
mv data.bin data.gz
mv data.bin data.bz2
mv data.bin data.tar
```

4. Extract the file

Depending on the file type:

gzip:

gunzip data.gz


bzip2:

bunzip2 data.bz2


tar:

tar -xf data.tar

5. Repeat

Run file again on the new file:

file <newfile>


Rename → extract → repeat
Continue until a plain text file appears.

6. Read the final password
cat <finalfile>

🔑 Password
```bash
F05dwFsc0cbaIiHOh8J2eUks2vdTDwAn
```

### 📘 What I Learned

Converting hexdumps back to binary using xxd -r

Identifying file formats using file

Extracting different compression formats (gzip, bzip2, tar)

Handling multi-layer compressed files step-by-step




# Bandit Level 13 → Level 14

## Level Goal
The password for the next level is stored in `/etc/bandit_pass/bandit14`, but the normal `bandit13` user does not have permission.  
You must use the private SSH key provided in the home directory.

---

## 🔧 Solution

first of all we need to read the given sshkey.private file using "cat"
then 

### 1. Use the private SSH key to log in as bandit14

```bash
cat sshkey.private
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAxkkOE83W2cOT7IWhFc9aPaaQmQDdgzuXCv+ppZHa++buSkN+
gg0tcr7Fw8NLGa5+Uzec2rEg0WmeevB13AIoYp0MZyETq46t+jk9puNwZwIt9XgB
ZufGtZEwWbFWw/vVLNwOXBe4UWStGRWzgPpEeSv5Tb1VjLZIBdGphTIK22Amz6Zb
ThMsiMnyJafEwJ/T8PQO3myS91vUHEuoOMAzoUID4kN0MEZ3+XahyK0HJVq68KsV
ObefXG1vvA3GAJ29kxJaqvRfgYnqZryWN7w3CHjNU4c/2Jkp+n8L0SnxaNA+WYA7
jiPyTF0is8uzMlYQ4l1Lzh/8/MpvhCQF8r22dwIDAQABAoIBAQC6dWBjhyEOzjeA
J3j/RWmap9M5zfJ/wb2bfidNpwbB8rsJ4sZIDZQ7XuIh4LfygoAQSS+bBw3RXvzE
pvJt3SmU8hIDuLsCjL1VnBY5pY7Bju8g8aR/3FyjyNAqx/TLfzlLYfOu7i9Jet67
xAh0tONG/u8FB5I3LAI2Vp6OviwvdWeC4nOxCthldpuPKNLA8rmMMVRTKQ+7T2VS
nXmwYckKUcUgzoVSpiNZaS0zUDypdpy2+tRH3MQa5kqN1YKjvF8RC47woOYCktsD
o3FFpGNFec9Taa3Msy+DfQQhHKZFKIL3bJDONtmrVvtYK40/yeU4aZ/HA2DQzwhe
ol1AfiEhAoGBAOnVjosBkm7sblK+n4IEwPxs8sOmhPnTDUy5WGrpSCrXOmsVIBUf
laL3ZGLx3xCIwtCnEucB9DvN2HZkupc/h6hTKUYLqXuyLD8njTrbRhLgbC9QrKrS
M1F2fSTxVqPtZDlDMwjNR04xHA/fKh8bXXyTMqOHNJTHHNhbh3McdURjAoGBANkU
1hqfnw7+aXncJ9bjysr1ZWbqOE5Nd8AFgfwaKuGTTVX2NsUQnCMWdOp+wFak40JH
PKWkJNdBG+ex0H9JNQsTK3X5PBMAS8AfX0GrKeuwKWA6erytVTqjOfLYcdp5+z9s
8DtVCxDuVsM+i4X8UqIGOlvGbtKEVokHPFXP1q/dAoGAcHg5YX7WEehCgCYTzpO+
xysX8ScM2qS6xuZ3MqUWAxUWkh7NGZvhe0sGy9iOdANzwKw7mUUFViaCMR/t54W1
GC83sOs3D7n5Mj8x3NdO8xFit7dT9a245TvaoYQ7KgmqpSg/ScKCw4c3eiLava+J
3btnJeSIU+8ZXq9XjPRpKwUCgYA7z6LiOQKxNeXH3qHXcnHok855maUj5fJNpPbY
iDkyZ8ySF8GlcFsky8Yw6fWCqfG3zDrohJ5l9JmEsBh7SadkwsZhvecQcS9t4vby
9/8X4jS0P8ibfcKS4nBP+dT81kkkg5Z5MohXBORA7VWx+ACohcDEkprsQ+w32xeD
qT1EvQKBgQDKm8ws2ByvSUVs9GjTilCajFqLJ0eVYzRPaY6f++Gv/UVfAPV4c+S0
kAWpXbv5tbkkzbS0eaLPTKgLzavXtQoTtKwrjpolHKIHUz6Wu+n4abfAIRFubOdN
/+aLoRQ0yBDRbdXMsZN/jvY44eM+xRLdRVyMmdPtP8belRi2E2aEzA==
-----END RSA PRIVATE KEY-----
```
then we need to open up another terminal in our OS(not in bandit)
creare a file with "sshkey.private" name with nano/vim 'any text editor you use'
then pest the key and save. then use this command to enter into level 14 

```bash
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```

## 📘 What I Learned

How to authenticate using a private SSH key (ssh -i)

How to access another user's account securely

Understanding Linux file permissions and privilege boundaries





