---
title: picoCTF writeup - Forensics
date: 2026-03-06
update: 2026-06-17
description: picoCTF writeup
comments: true
copyright_author: kapiso
copyright_author_href: https://kapiso-tw.github.io/
copyright_url: write by kapiso
---

# Forensics
**題目類別連結**: https://learn.cylabacademy.org/library?category=4&page=1

## 🟢Easy

### Riddle Registry
**題目連結**: https://learn.cylabacademy.org/library/530

> Hi, intrepid investigator! 📄🔍 You've stumbled upon a peculiar PDF filled with what seems like nothing more than garbled nonsense. But beware! Not everything is as it appears. Amidst the chaos lies a hidden treasure—an elusive flag waiting to be uncovered.
Find the PDF file here [Hidden Confidential Document](https://challenge-files.picoctf.net/c_amiable_citadel/ec88ce83253c1bd53af98533a401b9ea0b37602fd6276271c724d5cdd126b285/confidential.pdf) and uncover the flag within the metadata.

先下載檔案
![image](/img/picoCTF/Forensics/Riddle_Registry/01.png)

根據提示使用 `pdfinfo confidential.pdf` 檢查 PDF 的 metadata 後發現 Author 看起來像 Base64

![image](/img/picoCTF/Forensics/Riddle_Registry/02.png)

使用線上解密器解密後即可獲得 flag

![image](/img/picoCTF/Forensics/Riddle_Registry/03.png)

``` txt
picoCTF{puzzl3d_m3tadata_f0und!_0e2de5a1}
```

---

### Hidden in plainsight
**題目連結**: https://learn.cylabacademy.org/library/524

> You’re given a seemingly ordinary JPG image. Something is tucked away out of sight inside the file. Your task is to discover the hidden payload and extract the flag.
Download the jpg image [here](https://challenge-files.picoctf.net/c_amiable_citadel/618fe22499d6c52fd1de495424be4ee540886e1d066fad4b2474d695757a50da/img.jpg).

先下載檔案

![image](/img/picoCTF/Forensics/Hidden_in_plainsight/01.png)

根據提示使用 `file img.jpg` 檢查 img 的 metadata 後發現 comment 看起來像 Base64

![image](/img/picoCTF/Forensics/Hidden_in_plainsight/02.png)

使用線上解密器解密

![image](/img/picoCTF/Forensics/Hidden_in_plainsight/03.png)

解密後得到 `steghide:cEF6endvcmQ=`，看起來像一個指令接一個 Base64 加密字串，查詢後得知前半部分為意指令，可以將資料嵌入檔案或提取隱藏資料 (參考自此[網站](https://www.geeksforgeeks.org/linux-unix/how-to-use-steghide-and-stegosuite-steganography-tools-in-kali-linux/))

先使用 `steghide info img.jpg` 查看是否有隱藏資料

![image](/img/picoCTF/Forensics/Hidden_in_plainsight/04.png)

發現要提取崁入的檔案需要密碼，驗證後半部份為加密後的密碼，使用線上解密器解密得到密碼

![image](/img/picoCTF/Forensics/Hidden_in_plainsight/05.png)

使用 `steghide extract -sf img.jpg` 並輸入解碼後的密碼即可獲得 flag

![image](/img/picoCTF/Forensics/Hidden_in_plainsight/06.png)

``` txt
picoCTF{h1dd3n_1n_1m4g3_67479645}
```

---

### Flag in Flame
**題目連結**: https://learn.cylabacademy.org/library/523

> The SOC team discovered a suspiciously large log file after a recent breach. When they opened it, they found an enormous block of encoded text instead of typical logs. Could there be something hidden within? Your mission is to inspect the resulting file and reveal the real purpose of it. The team is relying on your skills to uncover any concealed information within this unusual log.
Download the encoded data here: [Logs Data](https://challenge-files.picoctf.net/c_amiable_citadel/3c1d1fea48e203c9c5d64c32d94aa1f091a6b72b4cebd35a761b09d4f9c0f0d2/logs.txt). Be prepared—the file is large, and examining it thoroughly is crucial .

先下載檔案

![image](/img/picoCTF/Forensics/Flag_in_Flame/01.png)

因為提示裡面說用 Base64 解碼並轉換成圖片因此使用指令 `cat logs.txt | base64 --decode > output.jpg` 得到一張圖片

![image](/img/picoCTF/Forensics/Flag_in_Flame/02.png)

得到 `7069636F4354467B666F72656E736963735F616E616C797369735F69735F616D617A696E675F35646161346132667D` 這串 16 進位，因為答案是 picoCTF{...} 因此推斷應該是要 Hex to ASCII，使用線上解碼器

![image](/img/picoCTF/Forensics/Flag_in_Flame/03.png)

``` txt
picoCTF{forensics_analysis_is_amazing_5daa4a2f}
```

---

### DISKO 1
**題目連結**: https://learn.cylabacademy.org/library/505

>Can you find the flag in this disk image?
Download the disk image [here](https://artifacts.picoctf.net/c/538/disko-1.dd.gz).

先下載檔案

![image](/img/picoCTF/Forensics/DISKO_1/01.png)

看到副檔名為 .gz，先使用`gzip -d disko-1.dd.gz` 解壓縮檔案獲得 `disko-1.dd`

![image](/img/picoCTF/Forensics/DISKO_1/02.png)

根據提示使用 `strings disko-1.dd` 試試

![image](/img/picoCTF/Forensics/DISKO_1/03.png)

然後就跑出了一大串資料，顯然直接在裡面找 flag 是不切實際得，因此使用 `strings disko-1.dd | grep picoCTF` 在輸出時同時搜索 picoCTF 並印出搜索結果，即可獲得 flag

![image](/img/picoCTF/Forensics/DISKO_1/04.png)

``` txt
picoCTF{1t5_ju5t_4_5tr1n9_e3408eef}
```

---

### RED
**題目連結**: https://learn.cylabacademy.org/library/460

>RED, RED, RED, RED
Download the image: [red.png](https://challenge-files.picoctf.net/c_verbal_sleep/831307718b34193b288dde31e557484876fb84978b5818e2627e453a54aa9ba6/red.png)

先使用 `binwalk` 檢查圖片

![image](/img/picoCTF/Forensics/RED/01.png)

發現沒有隱藏東西，根據提示應該與像素有關，查詢網路後常是指令 `zsteg red.png`

![image](/img/picoCTF/Forensics/RED/02.png)

發現疑似 base64 密文，解密後即可獲得 flag

![image](/img/picoCTF/Forensics/RED/03.png)

``` TXT
picoCTF{r3d_1s_th3_ult1m4t3_cur3_f0r_54dn355_}
```

---

### Verify
**題目連結**: https://learn.cylabacademy.org/library/450

>People keep trying to trick my players with imitation flags. I want to make sure they get the real thing! I'm going to provide the SHA-256 hash and a decrypt script to help you know that my flags are legitimate.
ssh -p 56484 ctf-player@rhea.picoctf.net
Using the password 6abf4a82. Accept the fingerprint with yes, and ls once connected to begin. Remember, in a shell, passwords are hidden!
Checksum: b09c99c555e2b39a7e97849181e8996bc6a62501f0149c32447d8e65e205d6d2
To decrypt the file once you've verified the hash, run ./decrypt.sh files/<file>.

先連線進入，根據題目與提示，要找到 `./files` 內哪一個檔案的 sha256 是 `checksum.txt` 內的數值，使用以下指令以找出檔案

``` sh
sha256sum ./files/* | grep "b09c99c555e2b39a7e97849181e8996bc6a62501f0149c32447d8e65e205d6d2"
```

![image](/img/picoCTF/Forensics/Verify/01.png)

找到後使用 `./decrypt.sh ./files/451fd69b` 將檔案解密即可獲得 flag

``` TXT
picoCTF{trust_but_verify_451fd69b}
```

---

### Scan Surprise
**題目連結**: https://learn.cylabacademy.org/library/444
>I've gotten bored of handing out flags as text. Wouldn't it be cool if they were an image instead?
You can download the challenge files here:
[challenge.zip](https://artifacts.picoctf.net/c_atlas/3/challenge.zip)
The same files are accessible via SSH here:
ssh -p 63198 ctf-player@atlas.picoctf.net
Using the password 6dd28e9b. Accept the fingerprint with yes, and ls once connected to begin. Remember, in a shell, passwords are hidden!

連線後發現有一個 QR code，使用 `zbarimg flag.png` 即可獲得 flag

![image](/img/picoCTF/Forensics/Scan_Surprise/01.png)

``` TXT
picoCTF{p33k_@_b00_a81f0a35}
```

---

### Secret of the Polyglot
**題目連結**: https://learn.cylabacademy.org/library/423
>The Network Operations Center (NOC) of your local institution picked up a suspicious file, they're getting conflicting information on what type of file it is. They've brought you in as an external expert to examine the file. Can you extract all the information from this strange file?
Download the suspicious file [here](https://artifacts.picoctf.net/c_titan/9/flag2of2-final.pdf).

先下載檔案並使用 `file` 檢查檔案格式

![image](/img/picoCTF/Forensics/Secret_of_the_Polyglot/01.png)

發現為 `PNG image`，複製一份並改為 `.png` 即可獲得前半個 flag，後半個直接開啟 pdf 即可獲得

![image](/img/picoCTF/Forensics/Secret_of_the_Polyglot/02.png)

![image](/img/picoCTF/Forensics/Secret_of_the_Polyglot/03.png)

``` TXT
picoCTF{f1u3n7_1n_pn9_&_pdf_7f9bccd1}
```

---

### CanYouSee
**題目連結**: https://learn.cylabacademy.org/library/408
>How about some hide and seek?
Download this file [here](https://artifacts.picoctf.net/c_titan/129/unknown.zip).

下載並解壓所檔案會獲得一張圖片，使用各種指令檢查後在 `head ukn_reality.jpg` 內發現疑似 base64 的文字

![image](/img/picoCTF/Forensics/CanYouSee/01.png)

使用 `echo "cGljb0NURntNRTc0RDQ3QV9ISUREM05fYjMyMDQwYjh9Cg==" | base64 -d` 即可獲得 flag

``` TXT
picoCTF{ME74D47A_HIDD3N_b32040b8}
```

---

## 🟠Medium

### DISKO 2
**題目連結**: https://learn.cylabacademy.org/library/506
>Can you find the flag in this disk image? The right one is Linux! One wrong step and its all gone!
Download the disk image [here](https://artifacts.picoctf.net/c/540/disko-2.dd.gz).

下載並解壓縮檔案後有一個 .dd 檔，先使用 `file disko-2.dd` 檢查檔案

![image](/img/picoCTF/Forensics/DISKO_2/01.png)

輸出顯示有兩個分區，使用 `mmls disko-2.dd` 讀取分區資訊

![image](/img/picoCTF/Forensics/DISKO_2/02.png)

因為題目有提到 `The right one is Linux!`，故正確分區應為 002 ，start at 2048, end at 51200 使用 `dd if=disko-2.dd of=partition1.dd bs=512 skip=2048 count=51200` 提取分區並使用 `strings partition1.dd | grep "picoCTF{.*}"` 查找即可獲取 flag

![image](/img/picoCTF/Forensics/DISKO_2/03.png)

``` TXT
picoCTF{4_P4Rt_1t_i5_a93c3ba0}
```

# [⬅️ 回到總覽索引](/2026/01/11/picoCTF/)