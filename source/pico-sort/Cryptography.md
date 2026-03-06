---
title: picoCTF writeup - Cryptography
date: 2026-03-06
update: 2026-03-06
description: picoCTF writeup
comments: true
copyright_author: kapiso
copyright_author_href: https://kapiso-tw.github.io/
copyright_url: write by kapiso
---

# Cryptography
**題目類別連結**: https://play.picoctf.org/practice?category=2

## 🟢Easy

### hashcrack
**題目連結**: https://play.picoctf.org/practice/challenge/475

>A company stored a secret message on a server which got breached due to the admin using weakly hashed passwords. Can you gain access to the secret stored within the server?
Access the server using nc verbal-sleep.picoctf.net 57421

先連線查看內容

![image](/img/picoCTF/Cryptography/hashcrack/01.png)

看起來是要解碼 `482c811da5d5b4bc6d497ffa98491e38`，因為是32位的 hash，故嘗試 MD5

![image](/img/picoCTF/Cryptography/hashcrack/02.png)

![image](/img/picoCTF/Cryptography/hashcrack/03.png)

再解碼 `b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3`，因為是40位的 hash，故嘗試 SHA-1

![image](/img/picoCTF/Cryptography/hashcrack/04.png)

![image](/img/picoCTF/Cryptography/hashcrack/05.png)

再解碼 `916e8c4f79b25028c9e467f1eb8eee6d6bbdff965f9928310ad30a8d88697745`，因為是64位的 hash，故嘗試 SHA-256

![image](/img/picoCTF/Cryptography/hashcrack/06.png)

輸入完成即可獲得 flag

![image](/img/picoCTF/Cryptography/hashcrack/07.png)

``` txt
picoCTF{UseStr0nG_h@shEs_&PaSswDs!_4c95d69f}
```

---

### interencdec
**題目連結**: https://play.picoctf.org/practice/challenge/418

>Can you get the real meaning from this file.
Download the file [here](https://artifacts.picoctf.net/c_titan/111/enc_flag).

先下載檔案並觀察

![image](/img/picoCTF/Cryptography/interencdec/01.png)

此檔為 base64，使用線上解碼器解碼

![image](/img/picoCTF/Cryptography/interencdec/02.png)

解碼完成看起來還要進行一次 base64 解碼

![image](/img/picoCTF/Cryptography/interencdec/03.png)

這個看起來是 Caesar Cipher，使用線上解碼器

![image](/img/picoCTF/Cryptography/interencdec/04.png)

獲得 flag

``` txt
picoCTF{caesar_d3cr9pt3d_890d2379}
```

---

### Mod 26
**題目連結**: https://play.picoctf.org/practice/challenge/144

>Cryptography can be easy, do you know what ROT13 is?
[values.txt](https://challenge-files.picoctf.net/c_wily_courier/8b42cf1faceb5224789128447ae1c7682ae59c3e9810825a8fcef944e5687fdf/values.txt)

先將檔案下載並依照題目敘述，使用 ROT13 線上解碼器解碼即可獲得 flag

![image](/img/picoCTF/Cryptography/Mod_26/01.png)

``` txt
picoCTF{next_time_I'll_try_2_rounds_of_rot13_45559abd}
```