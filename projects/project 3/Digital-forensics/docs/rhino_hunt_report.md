## 1 — Introduction
This document is a complete, step-by-step walkthrough of my investigation of the **Rhino Hunt** challenge dataset (USB image + network traces).  
Environment: **Windows host** (file prep) + **SIFT VM** (analysis).

## 2 — Files provided
- `RHINOUSB.dd` — USB image
- `rhino.log`, `rhino2.log`, `rhino3.log` — network trace files
## 3 — Tools & versions used
- Windows 11 — copying/sharing files to VM  
- **SIFT VM** — primary analysis environment  
- `foremost` — file carving (JPEG recovery)  
- `Wireshark` — network analysis (.log inspection)  
- `John the Ripper` — password cracking (when needed)  
- `stegdetect`, `stegbreak` — steganalysis & brute force on stego images  
- `jpseek`, `jphide` — JPEG steganography tools / verification  
- `md5sum`/`sha1sum` for integrity verification)

## 4 — Evidence preparation (Windows → SIFT VM)
1. Copy the image and log files from Windows to a shared folder accessible by the SIFT VM 
2. On SIFT VM, verify file integrity (if hashes provided):
   ```bash
   md5sum RHINOUSB.dd
   md5sum rhino.log rhino2.log rhino3.log
   ```
    ![Verify Hashes](../screenshots/verify_hashes.png)

## 5 — Step-by-step analysis (what I did)
5.2 Carve images with foremost
```bash
foremost -i RHINOUSB.dd  -t jpg,gif,png
```
![Run Foremost](../screenshots/foremost.png)

5.3 Inspected the recovered files, including docs,gif and jpg.
![Verify Foremost](../screenshots/verify_foremost.png) | ![Verify Foremost](../screenshots/verify_foremost2.png) 

I read the diary and I got a lead on what transpired, then I went through the network logs
![Read Diary](../screenshots/diary.png)

5.4 Network trace analysis with Wireshark

I opened rhino.log. I used the filter "tcp.port == 21". Then I found the FTP traffic where i retrieved the first rhino image using these steps
a. tcp.port == 21 
b. follow the stream
c. multiply the penultimate number by 256 and add the last number to it e.g 6*256 + 121 = 1657
d. do tcp.port == 1657
e. follow the stream and save the raw format
f. you would get back the original image/file that was transferred over the network
![Retrieve Rhino1](../screenshots/retrieve_rhino1.png) | ![Retrieve Rhino1](../screenshots/retrieve_rhino13.png) | ![Retrieve Rhino1](../screenshots/retrieve_rhino12.png)


