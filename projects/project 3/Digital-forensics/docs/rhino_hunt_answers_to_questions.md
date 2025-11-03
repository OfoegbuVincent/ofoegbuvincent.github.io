# 🦏 Rhino Hunt — Questions & Answers

> **Author:** Dagbo  
> This document contains my direct answers to the Rhino Hunt challenge questions, with evidence and references from my forensic analysis.

---

## Q1 — Who gave the accused a telnet/ftp account? 
**Answer:**  
Jeremy gave him.  
This information was found in the diary file recovered from the USB image.

**Evidence:**  
- Diary excerpt showing Jeremy’s mention.  
- File location: (../screenshots/diary.png) or text reference in `rhino_hunt_report.md`.

---

## Q2 — What’s the username/password for the account?
**Answer:**  
From the first network log (`rhino.log`):
- **Username:** `gnome`  
- **Password:** `gnome123`

**Evidence:**  
- FTP authentication event observed in `rhino.log` (see packet capture / Wireshark screenshot).  
- Saved screenshot: `../screenshots/retrieve_rhino1.png`

---

## Q3 — What relevant file transfers appear in the network traces?
**Answer:**  
The following files were transferred across the network traces:

- **`rhino1.jpg`** — retrieved from FTP activity in `rhino.log`.  
- **`rhino2.jpg`** — extracted from a password-protected ZIP file retrieved via FTP in `rhino.log`.  
- **`rhino3.jpg`** —retrieved from FTP activity in `rhino.log`.  
- **`rhino4.jpg`** and **`rhino5.jpg`** — exported as HTTP objects from `rhino2.log`.  
- **`rhino.exe`** — retrieved from `rhino3.log`.

**Evidence:**  
- FTP streams from `rhino.log` show multiple image transfers and the passworded ZIP containing `rhino2.jpg`.  
- HTTP object exports from `rhino2.log` contain `rhino4.jpg` and `rhino5.jpg`.  
- An executable (`rhino.exe`) was extracted from `rhino3.log`.  
- Screenshots and exports are stored in:  
  - `../screenshots'
 


---

## Q4 — What happened to the hard drive in the computer?  Where is it now?
**Answer:**  
It was **zapped and thrown into the Mississippi River.**

**Evidence:**  
- Statement obtained from the diary entry referencing the hard drive’s disposal.  
- Screenshot / excerpt available in `../screenshots/diary.png`.

---

## Q5 — What happened to the USB key?
**Answer:**  
The USB key was **formatted**, but forensic carving recovered deleted files from its image (`RHINOUSB.dd`) using `foremost`.

**Evidence:**  
- Diary screenshot located in `../screenshots/diary.png`.  

---

## Q6 — What is recoverable from the dd image of the USB key?
**Answer:**  
From the USB image (`RHINOUSB.dd`), the following items were recoverable:
- Multiple **deleted rhino images** carved with `foremost`.  
- The **diary file** containing critical information (mention of Jeremy).  
- Two hidden images extracted via steganalysis (`rhino9.jpg`, `rhino10.jpg`).

**Evidence:**  
- Carving results in `../screenshots`  


---

## Q7 — Is there any evidence that connects the USB key and the network traces? If so, what?
**Answer:**  
**Yes.**  
A clear connection exists between the USB key and the network traces:
- The **image (`rhino2.jpg`) recovered from the ZIP file in `rhino.log`** matches the **image carved from the formatted USB** (same hash and visual match).  

**Evidence:**  
- Matching MD5 hash of `rhino2.jpg` (USB vs. ZIP).   
- Screenshots:  
  - `../screenshots/verify_rhino2.png`  

---

**Summary:**  
- **Total images recovered:** 10  
- **Tools used:** foremost, Wireshark, zip2john, John the Ripper, stegdetect, stegbreak, jphide  
- **Main correlation:** rhino2.jpg (ZIP from `rhino.log`) matched a carved USB image  


---

**End of Questions & Answers**
