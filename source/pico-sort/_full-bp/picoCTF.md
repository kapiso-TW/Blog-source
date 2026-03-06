---
title: picoCTF writeup
date: 2026-01-11
update: 2026-02-11
tags: 資安
categories: coding
keywords:
    - CTF
    - picoCTF
    - 資安
    - 解題
description: picoCTF write up
top_img: /img/picoCTF/picoctf.svg
cover: /img/picoCTF/icon.png
comments: true
toc:
toc_number:
toc_style_simple:
copyright:
copyright_author: kapiso
copyright_author_href: https://kapiso-tw.github.io/
copyright_url: write by kapiso
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
swiper_index: 
top_group_index: 
background:
---

# Web Exploitation
**題目類別連結**: https://play.picoctf.org/practice?category=1

## 🟢Easy

### Crack the Gate 1
**題目連結**: https://play.picoctf.org/practice/challenge/520

> We’re in the middle of an investigation. One of our persons of interest, ctf player, is believed to be hiding sensitive data inside a restricted web portal. We’ve uncovered the email address he uses to log in: ctf-player@picoctf.org. Unfortunately, we don’t know the password, and the usual guessing techniques haven’t worked. But something feels off... it’s almost like the developer left a secret way in. Can you figure it out?
The website is running [here](http://amiable-citadel.picoctf.net:51437/). Can you try to log in?

先進入網站並隨意登入試試

![image](/img/picoCTF/Web_Exploitation/Crack_the_Gate_1/01.png)

看起來是有少了什麼，依據提示查看開發人員選項

![image](/img/picoCTF/Web_Exploitation/Crack_the_Gate_1/02.png)

發現一個 ROT13 加密的密文， 使用線上解碼器解碼

![image](/img/picoCTF/Web_Exploitation/Crack_the_Gate_1/03.png)

發現需要使用 header `X-Dev-Access: yes`，使用 burp suite 攔截並修改封包

![image](/img/picoCTF/Web_Exploitation/Crack_the_Gate_1/04.png)

![image](/img/picoCTF/Web_Exploitation/Crack_the_Gate_1/05.png)

即可獲得 flag

``` txt
picoCTF{brut4_f0rc4_49d1d186}
```

---

### head-dump
**題目連結**: https://play.picoctf.org/practice/challenge/476
>Welcome to the challenge! In this challenge, you will explore a web application and find an endpoint that exposes a file containing a hidden flag.
The application is a simple blog website where you can read articles about various topics, including an article about API Documentation. Your goal is to explore the application and find the endpoint that generates files holding the server’s memory, where a secret flag is hidden.
The website is running [picoCTF News](http://verbal-sleep.picoctf.net:51371/).

依照提示探索網站後發現 `#API Documentation` 可以被點擊，進入後依照提示尋找 heade dump 相關的區域

![image](/img/picoCTF/Web_Exploitation/head-dump/01.png)

找到後點擊 `Try it out` & `Execute` 即可獲得一串指令，整理後在 cmd 內使用發現吐出了許多數據

![image](/img/picoCTF/Web_Exploitation/head-dump/01.png)

改用 linux 下載檔案配合正則表達式 `strings heapdump | grep "picoCTF{.*}"` 找出 flag

``` TXT
picoCTF{Pat!3nt_15_Th3_K3y_871ffa9a}
```

---

### Unminify
**題目連結**: https://play.picoctf.org/practice/challenge/426

>I don't like scrolling down to read the code of my website, so I've squished it. As a bonus, my pages load faster!
Browse [here](http://titan.picoctf.net:55350/), and find the flag!

連線後開啟開發人員工具即可發現 flag

![image](/img/picoCTF/Web_Exploitation/Unminify/01.png)

``` txt
picoCTF{pr3tty_c0d3_743d0f9b}
```

---

### IntroToBurp
**題目連結**: https://play.picoctf.org/practice/challenge/419

>Try [here](http://titan.picoctf.net:55297/) to find the flag

先連線觀察網站

![image](/img/picoCTF/Web_Exploitation/IntroToBurp/01.png)

發現是一個註冊網站，先隨意嘗試看看

![image](/img/picoCTF/Web_Exploitation/IntroToBurp/02.png)

輸入後發現要驗證碼，結合題目的提示應該可以繞過驗證碼檢查，使用 burp suite 將 OPT 參數刪除即可獲得 flag

![image](/img/picoCTF/Web_Exploitation/IntroToBurp/03.png)

![image](/img/picoCTF/Web_Exploitation/IntroToBurp/04.png)

``` txt
picoCTF{#0TP_Bypvss_SuCc3$S_2e80f1fd}
```

---

### Includes
**題目連結**: https://play.picoctf.org/practice/challenge/274

>Can you get the flag?
Go to this [website](http://saturn.picoctf.net:51364/) and see what you can discover.

打開開發者工具即可在來源的兩個 css 檔中發現 flag，拼起來即可

![image](/img/picoCTF/Web_Exploitation/Includes/01.png)


![image](/img/picoCTF/Web_Exploitation/Includes/01.png)

``` txt
picoCTF{1nclu51v17y_1of2_f7w_2of2_b8f4b022}
```

---

### Local Authority
**題目連結**: https://play.picoctf.org/practice/challenge/278

>Can you get the flag?
Go to this [website](http://saturn.picoctf.net:54847/) and see what you can discover.

先連線觀察網站

![image](/img/picoCTF/Web_Exploitation/Local_Authority/01.png)

發現是一個登入網站，先隨意嘗試看看

![image](/img/picoCTF/Web_Exploitation/Local_Authority/02.png)

登入失敗，但是在開發人員工具的網路監控裡發現多了一個 js，且附上了帳號密碼，輸入後即可獲得 flag

``` txt
picoCTF{j5_15_7r4n5p4r3n7_a8788e61}
```

---

### Inspect HTML
**題目連結**: https://play.picoctf.org/practice/challenge/275

>Can you get the flag?
Go to this [website](http://saturn.picoctf.net:63132/) and see what you can discover.

連線後開啟開發人員工具即可獲得 flag

![image](/img/picoCTF/Web_Exploitation/Inspect_HTML/01.png)

``` txt
picoCTF{1n5p3t0r_0f_h7ml_1fd8425b}
```

---

### Cookie Monster Secret Recipe
**題目連結**: https://play.picoctf.org/practice/challenge/469?page=2

>Cookie Monster has hidden his top-secret cookie recipe somewhere on his website. As an aspiring cookie detective, your mission is to uncover this delectable secret. Can you outsmart Cookie Monster and find the hidden recipe?
You can access the Cookie Monster [here](http://verbal-sleep.picoctf.net:56097/) and good luck

先連線觀察

![image](/img/picoCTF/Web_Exploitation/Cookie_Monster_Secret_Recipe/01.png)

發現是一個登入網站，隨意輸入試試

![image](/img/picoCTF/Web_Exploitation/Cookie_Monster_Secret_Recipe/02.png)

登入後他說檢查 cookie，打開開發人員工具，應用程式 cookie

![image](/img/picoCTF/Web_Exploitation/Cookie_Monster_Secret_Recipe/03.png)

發現一個 base64 密文，解碼後即可獲得 flag

![image](/img/picoCTF/Web_Exploitation/Cookie_Monster_Secret_Recipe/04.png)

``` txt
picoCTF{c00k1e_m0nster_l0ves_c00kies_C430AE20}
```

---

### WebDecode
**題目連結**: https://play.picoctf.org/practice/challenge/427

>Do you know how to use the web inspector?
Start searching [here](http://titan.picoctf.net:63456/) to find the flag

先連線觀察網站

![image](/img/picoCTF/Web_Exploitation/WebDecode/01.png)

看起來沒甚麼特別的，原始碼也沒有異常，先點 ABOUT 試試

![image](/img/picoCTF/Web_Exploitation/WebDecode/02.png)

發現密文，試試 base64 解碼

![image](/img/picoCTF/Web_Exploitation/WebDecode/03.png)

獲得 flag

``` txt
picoCTF{web_succ3ssfully_d3c0ded_02cdcb59}
```

---

### Bookmarklet
**題目連結**: https://play.picoctf.org/practice/challenge/406

>Why search for the flag when I can make a bookmarklet to print it for me?
Browse [here](http://titan.picoctf.net:58038/), and find the flag!

先連線觀察

![image](/img/picoCTF/Web_Exploitation/Bookmarklet/01.png)

中間的格子有一串 javascript，看起來是要解碼被加密的 flag，寫一個 html 執行即可獲得 flag

``` html
<button onclick="decrypt()">Decrypt</button>
<script>
    function decrypt() {
        var encryptedFlag = "àÒÆÞ¦È¬ëÙ£ÖÓÚåÛÑ¢ÕÓÔÅÐÙí";
        var key = "picoctf";
        var decryptedFlag = "";
        for (var i = 0; i < encryptedFlag.length; i++) {
            decryptedFlag += String.fromCharCode((encryptedFlag.charCodeAt(i) - key.charCodeAt(i % key.length) + 256) % 256);
        }
        alert(decryptedFlag);
    };
</script>
```

![image](/img/picoCTF/Web_Exploitation/Bookmarklet/02.png)

``` txt
picoCTF{p@g3_turn3r_1d1ba7e0}
```

---

### Cookies
**題目連結**: https://play.picoctf.org/practice/challenge/173?page=5

>Who doesn't love cookies? Try to figure out the best one.
http://wily-courier.picoctf.net:64779/

先連線觀察，既然題目與 cookie 有關就先開啟開發人員工具觀察 cookie

![image](/img/picoCTF/Web_Exploitation/Cookies/01.png)

現在 name value 是 -1，改成 0 並重整觀察

![image](/img/picoCTF/Web_Exploitation/Cookies/02.png)

發現能成功連線，推測應該可以一直改，某個數字會有 flag，再改成 1 驗證想法

![image](/img/picoCTF/Web_Exploitation/Cookies/03.png)

想法成立，使用 Burp Suite Intruder 製作 playload，先使用 proxy 攔截封包並送入 Intruder

![image](/img/picoCTF/Web_Exploitation/Cookies/04.png)

再將 `Cookie: name` 設定成變量並設定其從 0 開始 playload

![image](/img/picoCTF/Web_Exploitation/Cookies/05.png)

完成後即可在 `Cookie: name=18` 處發現 flag

![image](/img/picoCTF/Web_Exploitation/Cookies/06.png)

``` txt
picoCTF{3v3ry1_l0v3s_c00k135_a4dadb49}
```

---

### Scavenger Hunt
**題目連結**: https://play.picoctf.org/practice/challenge/161

>There is some interesting information hidden around this site. Can you find it?
http://wily-courier.picoctf.net:53152/

先連線觀察

![image](/img/picoCTF/Web_Exploitation/Scavenger_Hunt/01.png)

感覺沒什麼，先開啟開發人員工具尋找線索，會先在 html 內找到 first part `picoCTF{t`

![image](/img/picoCTF/Web_Exploitation/Scavenger_Hunt/02.png)

那 css 與 js 內可能都有，先查看 css 可以找到 part 2 `h4ts_4_l0`

![image](/img/picoCTF/Web_Exploitation/Scavenger_Hunt/03.png)

就剩 js 了，打開會看到 `How can I keep Google from indexing my website?`

![image](/img/picoCTF/Web_Exploitation/Scavenger_Hunt/04.png)

說到阻止 gooogle 搜索就只有 robots.txt 了，進入即可找到 part 3 `t_0f_pl4c`

![image](/img/picoCTF/Web_Exploitation/Scavenger_Hunt/05.png)

他說還有 next part，同時提到這是使用 apache 開發的網站，但我沒使用過 apache，於是我請教 gemini 相關事項得知 最核心的隱藏檔案：`.htaccess`，進入看看

![image](/img/picoCTF/Web_Exploitation/Scavenger_Hunt/06.png)

得到 part 4 `3s_2_lO0k` ，但他說 `I love making websites on my Mac` 感覺還有 part 5，請教 gemini 得知 Mac 最常在資料夾中留下的「足跡」： `.DS_Store`，前往看看

![image](/img/picoCTF/Web_Exploitation/Scavenger_Hunt/07.png)

即可獲得最後一部份 `_9588550}` 組合後即可獲得 flag

``` txt
picoCTF{th4ts_4_l0t_0f_pl4c3s_2_lO0k_9588550}
```

---

## 🟠Medium

### MatchTheRegex
**題目連結**: https://play.picoctf.org/practice/challenge/356

>How about trying to match a regular expression
The website is running [here](http://saturn.picoctf.net:65046/).

連線並開啟開發人員工具觀察網站

![image](/img/picoCTF/Web_Exploitation/MatchTheRegex/01.png)

在 script 內發現了被註解的正則表達式 ^p.....F!?，其中 `^p` 表示必須以 p 開頭，`.....F` 五個點每一點表示任意一個字元，且須在最後接上 F，而最後的 `!?` 表示必須接上 ! ，但是 ? 表示匹配 0 次或 1 次，所以 ! 可有可無，解完後依照規則輸入即可獲得 flag

![image](/img/picoCTF/Web_Exploitation/MatchTheRegex/02.png)

``` txt
picoCTF{succ3ssfully_matchtheregex_f89ea585}
```

---

### Search source
**題目連結**: https://play.picoctf.org/practice/challenge/295

>The developer of this website mistakenly left an important artifact in the website source, can you find it?
The website is [here](http://saturn.picoctf.net:56826/)

題目說有留了東西在網站源碼裡面，先將整個網站下載下來在做搜索

![image](/img/picoCTF/Web_Exploitation/Search_source/01.png)

![image](/img/picoCTF/Web_Exploitation/Search_source/02.png)

即可獲得 flag

``` txt
picoCTF{1nsp3ti0n_0f_w3bpag3s_8de925a7}
```

---

### Roboto Sans
**題目連結**: https://play.picoctf.org/practice/challenge/291

>The flag is somewhere on this web application not necessarily on the website. Find it.
Check [this](http://saturn.picoctf.net:57473/) out.

根據題目所述 flag 不在網站本身，又題目名稱與 robots.txt 相似，去看看有沒有甚麼特別的

![image](/img/picoCTF/Web_Exploitation/Roboto_Sans/01.png)

有三條看起來像加密的東西，一一嘗試後只有第二列看起來像正常的東西

![image](/img/picoCTF/Web_Exploitation/Roboto_Sans/02.png)

進入後即可獲得 flag

``` txt
picoCTF{Who_D03sN7_L1k5_90B0T5_718c9043}
```

---

### Forbidden Paths
**題目連結**: https://play.picoctf.org/practice/challenge/270

>Can you get the flag?
We know that the website files live in /usr/share/nginx/html/ and the flag is at /flag.txt but the website is filtering absolute file paths. Can you get past the filter to read the flag?
Here's the [website](http://saturn.picoctf.net:63312/).

先連線觀察，發現是一個可以輸入 path 去瀏覽檔案的網站

![image](/img/picoCTF/Web_Exploitation/Forbidden_Paths/01.png)

依據題目所述輸入 `../../../../flag.txt` 即可獲得 flag

``` txt
picoCTF{7h3_p47h_70_5ucc355_e5a6fcbc}
```

---

### caas
**題目連結**: https://play.picoctf.org/practice/challenge/202

>Now presenting [cowsay as a service](https://caas.mars.picoctf.net/)
Challenge Endpoints
Download [index.js](https://artifacts.picoctf.net/picoMini+by+redpwn/Web+Exploitation/caas/index.js)

先連線觀察

![image](/img/picoCTF/Web_Exploitation/caas/01.png)

發現可以依照他所述讓網頁顯示訊息，同時觀察一下一同給與的 index.js

![image](/img/picoCTF/Web_Exploitation/caas/02.png)

發現第八行的 `exec` 會產生漏洞，exec 會將 `req.params.message` 直接當作 Shell 指令的一部分執行，因此可以透過特殊字符執行 shell 指令，使用後綴 `t;ls -la` 查看當前目錄

![image](/img/picoCTF/Web_Exploitation/caas/03.png)

發現有 falg 與 flag 相近，使用後綴 `t;cat falg.txt` 查看檔案即可獲得 flag

![image](/img/picoCTF/Web_Exploitation/caas/04.png)

``` txt
picoCTF{moooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo0o}
```

---

### findme
**題目連結**: https://play.picoctf.org/practice/challenge/349
>Help us test the form by submiting the username as test and password as test!
The website running [here](http://saturn.picoctf.net:59765/).

先連線並使用題目的 username & password，登入時注意到上面往只有跳轉，按一下返回上一頁即可看到頁面

![image](/img/picoCTF/Web_Exploitation/findme/01.png)

![image](/img/picoCTF/Web_Exploitation/findme/02.png)

是全白頁面，重點在網址，id 疑似是 base64 ，將兩段組起來進行解碼即可獲得 flag

![image](/img/picoCTF/Web_Exploitation/findme/03.png)

``` TXT
picoCTF{proxies_all_the_way_01e748db}
```

---

### Web Gauntlet
**題目連結**: https://play.picoctf.org/practice/challenge/88
>Can you beat the filters?
Log in as admin http://shape-facility.picoctf.net:51151/ http://shape-facility.picoctf.net:51151/filter.php

先進入兩個網站看看，index 就是登入網站， filter 根據網址判斷應該是會過濾什麼

![image](/img/picoCTF/Web_Exploitation/Web_Gauntlet/01.png)

![image](/img/picoCTF/Web_Exploitation/Web_Gauntlet/02.png)

亂輸入會輸出 SQL 的查詢指令，這題應該就是 SQL injection 了

![image](/img/picoCTF/Web_Exploitation/Web_Gauntlet/03.png)

既然過濾了 `or` 就使用 `admin'--` 將密碼判斷註解掉即可進入 round 2

![image](/img/picoCTF/Web_Exploitation/Web_Gauntlet/04.png)

![image](/img/picoCTF/Web_Exploitation/Web_Gauntlet/05.png)

round 2 是過濾了 `or and like = --`，那改用 `admin'/*` 同樣註解掉密碼判斷即可進入 round 3

![image](/img/picoCTF/Web_Exploitation/Web_Gauntlet/06.png)

![image](/img/picoCTF/Web_Exploitation/Web_Gauntlet/07.png)

round 3 過濾了 `or and = like > < --`，同樣使用 `admin'/*` 註解掉密碼判斷進入 round 4

![image](/img/picoCTF/Web_Exploitation/Web_Gauntlet/08.png)

![image](/img/picoCTF/Web_Exploitation/Web_Gauntlet/09.png)

round 4 過濾了 `or and = like > < -- admin`，使用 `ad'||'min'/*` 規避掉 admin 並註解掉密碼判斷即可進入 round 5

![image](/img/picoCTF/Web_Exploitation/Web_Gauntlet/10.png)

![image](/img/picoCTF/Web_Exploitation/Web_Gauntlet/11.png)

round 5 過濾 `or and = like > < -- union admin`，繼續使用 `ad'||'min'/*` 即可進入 round 6 並獲得 flag

![image](/img/picoCTF/Web_Exploitation/Web_Gauntlet/12.png)

![image](/img/picoCTF/Web_Exploitation/Web_Gauntlet/13.png)

``` TXT
picoCTF{y0u_m4d3_1t_79a0ddc6}
```

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

---

# Reverse Engineering
**題目類別連結**: https://play.picoctf.org/practice?category=3

## 🟢Easy

### Flag Hunters
**題目連結**: https://play.picoctf.org/practice/challenge/472
>Lyrics jump from verses to the refrain kind of like a subroutine call. There's a hidden refrain this program doesn't print by default. Can you get it to print it? There might be something in it for you.
The program's source code can be downloaded [here](https://challenge-files.picoctf.net/c_verbal_sleep/16af4dbf5dde07d6b920829561f50f7afe9e9e457733e422537c64525e1a6772/lyric-reader.py).
Connect to the program with netcat: $ nc verbal-sleep.picoctf.net 49285

先連線觀察發現可以輸入東西

![image](/img/picoCTF/Reverse_Engineering/Flag_Hunters/01.png)

解析檔案後發現在 `Print lyrics` 區域內有以下程式控制輸出

``` Python
for line in song_lines[lip].split(';'):
    if line == '' and song_lines[lip] != '':
        continue
    if line == 'REFRAIN':
        song_lines[refrain_return] = 'RETURN ' + str(lip + 1)
        lip = refrain
    elif re.match(r"CROWD.*", line):
        crowd = input('Crowd: ')
        song_lines[lip] = 'Crowd: ' + crowd
        lip += 1
    elif re.match(r"RETURN [0-9]+", line):
        lip = int(line.split()[1])
    elif line == 'END':
        finished = True
    else:
        print(line, flush=True)
        time.sleep(0.5)
        lip += 1
```

其中以 `;` 作為分割，判斷字串為何，其中注意到以下判斷式

``` Python
elif re.match(r"RETURN [0-9]+", line):
    lip = int(line.split()[1])
```

可以透過 `RETURN` 使歌詞跳轉到指定的行數，又因程式一開始將 flag 放在開頭了，所以只需使用指令 `a;RETURN 0` 即可使程式讀取並執行我們的指令並成功獲取 flag

![image](/img/picoCTF/Reverse_Engineering/Flag_Hunters/02.png)

``` TXT
picoCTF{70637h3r_f0r3v3r_836f0788}
```

---

# Forensics
**題目類別連結**: https://play.picoctf.org/practice?category=4

## 🟢Easy

### Riddle Registry
**題目連結**: https://play.picoctf.org/practice/challenge/530

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
**題目連結**: https://play.picoctf.org/practice/challenge/524

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
**題目連結**: https://play.picoctf.org/practice/challenge/523

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
**題目連結**: https://play.picoctf.org/practice/challenge/505

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
**題目連結**: https://play.picoctf.org/practice/challenge/460

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
**題目連結**: https://play.picoctf.org/practice/challenge/450

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
**題目連結**: https://play.picoctf.org/practice/challenge/444
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

## 🟠Medium

### DISKO 2
**題目連結**: https://play.picoctf.org/practice/challenge/506
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

---

# General Skills
**題目類別連結**: https://play.picoctf.org/practice?category=5

## 🟢Easy

### Log Hunt
**題目連結**: https://play.picoctf.org/practice/challenge/527

> Our server seems to be leaking pieces of a secret flag in its logs. The parts are scattered and sometimes repeated. Can you reconstruct the original flag?
Download the [logs](https://challenge-files.picoctf.net/c_amiable_citadel/49cec6157142f24a599f4164d5b63322c2494f801390d6f22eb91b3aa592bc66/server.log) and figure out the full flag from the fragments.

先下載檔案

![image](/img/picoCTF/General_Skills/Log_Hunt/01.png)

提示有說可以使用 grep 搜索文字，先使用 `grep picoCTF server.log` 搜索 picoCTF 試試

![image](/img/picoCTF/General_Skills/Log_Hunt/02.png)

發現有一部份的 flag 出現了，但少了一部份，改成使用前面的 INFO FLAGPART 搜索

![image](/img/picoCTF/General_Skills/Log_Hunt/03.png)

拼起來即可獲得 flag
``` txt
picoCTF{us3_y0urlinux_sk1lls_cedfa5fb}
```

---

### Corrupted file
**題目連結**: https://play.picoctf.org/practice/challenge/519

> This file seems broken... or is it? Maybe a couple of bytes could make all the difference. Can you figure out how to bring it back to life?
Download the file [here](https://challenge-files.picoctf.net/c_amiable_citadel/d5cf66acaae23a2634256d69988d9a77ff0dade995dc28432dc35e788699ea69/file).

先下載檔案

![image](/img/picoCTF/General_Skills/Corrupted_file/01.png)

依照提示使用 `xxd -l 10 file` 查看檔案前幾行部份，提示又說與 JPEG 有關，先查 JPEG headr format 應該為何

![image](/img/picoCTF/General_Skills/Corrupted_file/02.png)

應為 `FF D8` 明顯與檔案不符，推斷應該將前兩位元修復即可獲得 flag，使用 `printf '\xFF\xD8' | cat - <(tail -c +3 file) > fixed.jpg`，將檔案前兩位元替換並輸出成 jpg

![image](/img/picoCTF/General_Skills/Corrupted_file/03.png)

即可獲得 flag
``` txt
picoCTF{r3st0r1ng_th3_by73s_1512b52a}
```

---

### FANTASY CTF
**題目連結**: https://play.picoctf.org/practice/challenge/471

> Play this short game to get familiar with terminal applications and some of the most important rules in scope for picoCTF.
Connect to the program with netcat:
 $ nc verbal-sleep.picoctf.net 58089

連線後發現是一個要一直按 enter 的東西

![image](/img/picoCTF/General_Skills/FANTASY_CTF/01.png)

按到中間要選選項，都選 a 試試

![image](/img/picoCTF/General_Skills/FANTASY_CTF/02.png)

然後就拿到 flag 了

``` txt
picoCTF{m1113n1um_3d1710n_dd015572}
```

---

### Super SSH
**題目連結**: https://play.picoctf.org/practice/challenge/424?page=3

>Using a Secure Shell (SSH) is going to be pretty important.
Can you ssh as ctf-player to titan.picoctf.net at port 59265 to get the flag?
You'll also need the password f3b61b38. If asked, accept the fingerprint with yes.
If your device doesn't have a shell, you can use: https://webshell.picoctf.org
If you're not sure what a shell is, check out our Primer: https://primer.picoctf.com/#_the_shell

依照題目敘述使用指令 `ssh -p 59265 ctf-player@titan.picoctf.net` 並輸入密碼 `f3b61b38` 即可獲得 flag

![image](/img/picoCTF/General_Skills/Super_SSH/01.png)

``` txt
picoCTF{s3cur3_c0nn3ct10n_3e293eea}
```

---

### Time Machine
**題目連結**: https://play.picoctf.org/practice/challenge/425

>What was I last working on? I remember writing a note to help me remember...
You can download the challenge files here:
[challenge.zip](https://artifacts.picoctf.net/c_titan/161/challenge.zip)

先下載檔案並解壓縮

![image](/img/picoCTF/General_Skills/Time_Machine/01.png)

可以看到他創建了一個 `drop-in` 資料夾，進入看看

![image](/img/picoCTF/General_Skills/Time_Machine/02.png)

可以看到裡面有一個文字檔跟一個隱藏的資料夾，先查看文字檔

![image](/img/picoCTF/General_Skills/Time_Machine/03.png)

他說要查看 commit history，進入隱藏資料夾看看

![image](/img/picoCTF/General_Skills/Time_Machine/04.png)

可以看到裡面有個 `COMMIT_EDITMSG` 與 commit history 有關，查看這個檔案即可獲得 flag

![image](/img/picoCTF/General_Skills/Time_Machine/05.png)

``` txt
picoCTF{t1m3m@ch1n3_8defe16a}
```

---

### runme.py
**題目連結**: https://play.picoctf.org/practice/challenge/250

>Run the runme.py script to get the flag. Download the script with your browser or with wget in the webshell.
[Download runme.py Python script](https://artifacts.picoctf.net/c/34/runme.py)

依照題目敘述，下載檔案並運行即可獲得 flag

![image](/img/picoCTF/General_Skills/runme.py/01.png)

``` txt
picoCTF{run_s4n1ty_run}
```

---

### Big Zip
**題目連結**: https://play.picoctf.org/practice/challenge/322

>Unzip this archive and find the flag.
[Download zip file](https://artifacts.picoctf.net/c/503/big-zip-files.zip)

先下載並解壓縮

![image](/img/picoCTF/General_Skills/Big_Zip/01.png)

解壓縮時發現有非常多檔案，一個一個慢慢找肯定不行，於是使用指令 `grep -r "picoCTF"` 在資料夾內搜尋 flag

![image](/img/picoCTF/General_Skills/Big_Zip/02.png)

``` txt
picoCTF{gr3p_15_m4g1c_ef8790dc}
```

---

### fixme1.py
**題目連結**: https://play.picoctf.org/practice/challenge/240

>Fix the syntax error in this Python script to print the flag.
[Download Python script](https://artifacts.picoctf.net/c/25/fixme1.py)

先下載並開啟檔案

![image](/img/picoCTF/General_Skills/fixme1.py/01.png)

![image](/img/picoCTF/General_Skills/fixme1.py/02.png)

是一個 python，問題很明顯就是第二十行並未正確縮排，把前面的空格刪除並執行即可獲得 flag

![image](/img/picoCTF/General_Skills/fixme1.py/03.png)

``` txt
picoCTF{1nd3nt1ty_cr1515_6a476c8f}
```

---

### fixme2.py
**題目連結**: https://play.picoctf.org/practice/challenge/241

>Fix the syntax error in the Python script to print the flag.
[Download Python script](https://artifacts.picoctf.net/c/5/fixme2.py)

先下載並開啟檔案

![image](/img/picoCTF/General_Skills/fixme2.py/01.png)

![image](/img/picoCTF/General_Skills/fixme2.py/02.png)

是一個 python，問題很明顯就是第二十二行，if 判斷式應該使用 == 而不是 =，修正並執行即可獲得 flag

![image](/img/picoCTF/General_Skills/fixme2.py/03.png)

``` txt
picoCTF{3qu4l1ty_n0t_4551gnm3nt_4863e11b}
```

---

### Wave a flag
**題目連結**: https://play.picoctf.org/practice/challenge/170

>Can you invoke help flags for a tool or binary? This program has extraordinarily helpful information...
[warm](https://challenge-files.picoctf.net/c_wily_courier/1e14db3a752e16eae2b0e0d73d9779f9c4ddfd8942f60f3285a2986068480316/warm)

先下載檔案並根據提示運行檔案

![image](/img/picoCTF/General_Skills/Wave_a_flag/01.png)

發現權限不足，更改權限並重新運行

![image](/img/picoCTF/General_Skills/Wave_a_flag/02.png)

根據運行結果添加 `-h`，即可獲得 flag

![image](/img/picoCTF/General_Skills/Wave_a_flag/03.png)

``` txt
picoCTF{b1scu1ts_4nd_gr4vy_ac5832c}
```
---

### 2warm
**題目連結**: https://play.picoctf.org/practice/challenge/86

>Can you convert the number 42 (base 10) to binary (base 2)?

依照題目所述將 42 從十進位轉成二進位並放入 picoCTF{} 即可獲得 flag

``` txt
picoCTF{101010}
```

---

### Bases
**題目連結**: https://play.picoctf.org/practice/challenge/67

>What does this bDNhcm5fdGgzX3IwcDM1 mean? I think it has something to do with bases.

既然題目提到 base 第一個想到的就是 base64，使用 base64 線上解碼器試試

![image](/img/picoCTF/General_Skills/Bases/01.png)

看起來就是答案沒錯，用 picoCTF{} 包起來即可

``` txt
picoCTF{l3arn_th3_r0p35}
```

---

### First Find
**題目連結**: https://play.picoctf.org/practice/challenge/320
>Unzip this archive and find the file named 'uber-secret.txt'
[Download zip file](https://artifacts.picoctf.net/c/502/files.zip)

下載並解壓縮後使用指令 `find ./files -name "uber-secret.txt"` 即可找到檔案，再查看文件即可獲得 flag

![image](/img/picoCTF/General_Skills/First_Find/01.png)

---

### Binary Search
**題目連結**: https://play.picoctf.org/practice/challenge/442
>Want to play a game? As you use more of the shell, you might be interested in how they work! Binary search is a classic algorithm used to quickly find an item in a sorted list. Can you find the flag? You'll have 1000 possibilities and only 10 guesses.
Cyber security often has a huge amount of data to look through - from logs, vulnerability reports, and forensics. Practicing the fundamentals manually might help you in the future when you have to write your own tools!
You can download the challenge files here:
[challenge.zip](https://artifacts.picoctf.net/c_atlas/19/challenge.zip)
ssh -p 61206 ctf-player@atlas.picoctf.net
Using the password 1db87a14. Accept the fingerprint with yes, and ls once connected to begin. Remember, in a shell, passwords are hidden!

連線後發現是一個猜數字遊戲，根據題目標題，使用二分搜索概念配合輸出輸入數字即可獲得 flag

![image](/img/picoCTF/General_Skills/Binary_Search/01.png)

``` TXT
picoCTF{g00d_gu355_1597707f}
```

---

# Binary Exploitation
**題目類別連結**: https://play.picoctf.org/practice?category=6

## 🟢Easy

### PIE TIME
**題目連結**: https://play.picoctf.org/practice/challenge/490

> Can you try to get the flag? Beware we have PIE!
Connect to the program with netcat:
 $ nc rescued-float.picoctf.net 59661
The program's source code can be downloaded [here](https://challenge-files.picoctf.net/c_rescued_float/5179d3f9719eabf4dfd93cc8d0f6e8259e74cc9f7060d63e7639868edacd5dae/vuln.c). The binary can be downloaded [here](https://challenge-files.picoctf.net/c_rescued_float/5179d3f9719eabf4dfd93cc8d0f6e8259e74cc9f7060d63e7639868edacd5dae/vuln).

先連線看看

![image](/img/picoCTF/Binary_Exploitation/PIE_TIME/01.png)

看起來是需要知道某個位址然後跳過去，在下載檔案並打開來看看

![image](/img/picoCTF/Binary_Exploitation/PIE_TIME/02.png)
![image](/img/picoCTF/Binary_Exploitation/PIE_TIME/03.png)

看起來應該是要想辦法從 main 跳到 win 裡面取得 flag，因為 `實際位址 = PIE_base + 函式 offset --> win_real = main_real - main_offset + win_offset
`，剛好題目也有提供 Binary，可以直接做查詢並計算，使用 `nm vuln | grep "win"` 及 `nm vuln | grep " main"` 查詢兩者的位置

![image](/img/picoCTF/Binary_Exploitation/PIE_TIME/04.png)

位置差為 `133d - 12a7 = 96` 故只需將連線後提供的 main 位置減去 0x96 即可獲得 flag

![image](/img/picoCTF/Binary_Exploitation/PIE_TIME/05.png)

``` txt
picoCTF{b4s1c_p051t10n_1nd3p3nd3nc3_0392ebba}
```

---

# 參考資料(網站)
>https://www.dcode.fr/en
>https://www.base64decode.org/
>https://gemini.google.com/app
>https://10015.io/
>https://en.wikipedia.org/wiki/JPEG_File_Interchange_Format#HeroSection

# 發現本網站資料有任何錯誤之處，歡迎提供您的意見