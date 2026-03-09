---
title: picoCTF writeup - General Skills
date: 2026-03-06
update: 2026-03-09
description: picoCTF writeup
comments: true
copyright_author: kapiso
copyright_author_href: https://kapiso-tw.github.io/
copyright_url: write by kapiso
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

### endianness
**題目連結**:https://play.picoctf.org/practice/challenge/414
>Know of little and big endian?
[Source](https://artifacts.picoctf.net/c_titan/79/flag.c)
nc titan.picoctf.net 49874

先下載檔案並觀察，查看 `main function` 後發現是一個比對字串的遊戲。

``` C++
char *find_little_endian(const char *word)
{
    size_t word_len = strlen(word);
    char *little_endian = (char *)malloc((2 * word_len + 1) * sizeof(char));

    for (size_t i = word_len; i-- > 0;)
    {
        snprintf(&little_endian[(word_len - 1 - i) * 2], 3, "%02X", (unsigned char)word[i]);
    }

    little_endian[2 * word_len] = '\0';
    return little_endian;
}
```

再深入查看要比對字串的函式定義後發現 `"%02X"` ，推測目標字串應該是十六進位的，且有正反兩個目標。結合其變數名稱 `Little/Big Endian` ，應該是將原指 **記憶體寫入方式** 的定義轉化為 **字串正反轉後的十六進位數值**。

![image](/img/picoCTF/General_Skills/endianness/01.png)

連線獲得字串後分別使用 `echo "fzcgq" | rev | xxd -p -u` 與 `echo "fzcgq" | xxd -p -u`，獲得 Little/Big Endian 後輸入即可獲得 flag

![image](/img/picoCTF/General_Skills/endianness/02.png)

![image](/img/picoCTF/General_Skills/endianness/03.png)

``` TXT
picoCTF{3ndi4n_sw4p_su33ess_d58517b6}
```

---

### Commitment Issues
**題目連結**:https://play.picoctf.org/practice/challenge/411
>I accidentally wrote the flag down. Good thing I deleted it!
You download the challenge files here:
[challenge.zip](https://artifacts.picoctf.net/c_titan/138/challenge.zip)

先下載並解壓縮進入資料夾探索

![image](/img/picoCTF/General_Skills/Commitment_Issues/01.png)

解壓縮時發現有 `.git` 資料夾，題目應該和其有關，根據提示使用 `git log` 檢查 commit，發現 commit b562f... 有 creat flag ，使用 `git checkout b562f0b425907789d11d2fe2793e67592dc6be93` 將版本切換至其即可獲得 flag

![image](/img/picoCTF/General_Skills/Commitment_Issues/02.png)

``` TXT
picoCTF{s@n1t1z3_c785c319}
```

# [⬅️ 回到總覽索引](/2026/01/11/picoCTF/)