---
title: picoCTF writeup - General Skills
date: 2026-03-06
update: 2026-06-22
description: picoCTF writeup
comments: true
copyright_author: kapiso
copyright_author_href: https://kapiso-tw.github.io/
copyright_url: write by kapiso
---

# General Skills
**題目類別連結**: https://learn.cylabacademy.org/library?category=5&page=1

## 🟢Easy

### Log Hunt
**題目連結**: https://learn.cylabacademy.org/library/527

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
**題目連結**: https://learn.cylabacademy.org/library/519

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
**題目連結**: https://learn.cylabacademy.org/library/471

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
**題目連結**: https://learn.cylabacademy.org/library/424?page=3

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
**題目連結**: https://learn.cylabacademy.org/library/425

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
**題目連結**: https://learn.cylabacademy.org/library/250

>Run the runme.py script to get the flag. Download the script with your browser or with wget in the webshell.
[Download runme.py Python script](https://artifacts.picoctf.net/c/34/runme.py)

依照題目敘述，下載檔案並運行即可獲得 flag

![image](/img/picoCTF/General_Skills/runme.py/01.png)

``` txt
picoCTF{run_s4n1ty_run}
```

---

### Big Zip
**題目連結**: https://learn.cylabacademy.org/library/322

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
**題目連結**: https://learn.cylabacademy.org/library/240

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
**題目連結**: https://learn.cylabacademy.org/library/241

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
**題目連結**: https://learn.cylabacademy.org/library/170

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
**題目連結**: https://learn.cylabacademy.org/library/86

>Can you convert the number 42 (base 10) to binary (base 2)?

依照題目所述將 42 從十進位轉成二進位並放入 picoCTF{} 即可獲得 flag

``` txt
picoCTF{101010}
```

---

### Bases
**題目連結**: https://learn.cylabacademy.org/library/67

>What does this bDNhcm5fdGgzX3IwcDM1 mean? I think it has something to do with bases.

既然題目提到 base 第一個想到的就是 base64，使用 base64 線上解碼器試試

![image](/img/picoCTF/General_Skills/Bases/01.png)

看起來就是答案沒錯，用 picoCTF{} 包起來即可

``` txt
picoCTF{l3arn_th3_r0p35}
```

---

### First Find
**題目連結**: https://learn.cylabacademy.org/library/320
>Unzip this archive and find the file named 'uber-secret.txt'
[Download zip file](https://artifacts.picoctf.net/c/502/files.zip)

下載並解壓縮後使用指令 `find ./files -name "uber-secret.txt"` 即可找到檔案，再查看文件即可獲得 flag

![image](/img/picoCTF/General_Skills/First_Find/01.png)

---

### Binary Search
**題目連結**: https://learn.cylabacademy.org/library/442
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
**題目連結**:https://learn.cylabacademy.org/library/414
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
**題目連結**:https://learn.cylabacademy.org/library/411
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

---

### Undo
**題目連結**:https://learn.cylabacademy.org/library/766
>Can you reverse a series of Linux text transformations to recover the original flag?
Start searching for the flag here nc foggy-cliff.picoctf.net 51531

直接連線可以看到題目，要求輸入對應的指令。

![image](/img/picoCTF/General_Skills/Undo/01.png)

第一題是Base64 encoded string，使用指令 `base64 -d` 即可進入下一題

![image](/img/picoCTF/General_Skills/Undo/02.png)

第二題是Reversed text，使用指令 `rev` 即可進入下一題

![image](/img/picoCTF/General_Skills/Undo/03.png)

第三題是要用 _ 替代 -，使用指令 `tr '-' '_'` 即可進入下一題

![image](/img/picoCTF/General_Skills/Undo/04.png)

第四題是要用 {} 替換 ()，使用指令 `tr '()' '{}'` 即可進入下一題

![image](/img/picoCTF/General_Skills/Undo/05.png)

第五題要用 ROT13 進行轉換，使指令 `tr 'A-Za-z' 'N-ZA-Mn-za-m'` 即可獲得 flag

![image](/img/picoCTF/General_Skills/Undo/06.png)

```TXT
picoCTF{Revers1ng_t3xt_Tr4nsf0rm@t10ns_3a939318}
```

---

### MY GIT
**題目連結**:https://learn.cylabacademy.org/library/764
>I have built my own Git server with my own rules!
You can clone the challenge repo using the command below.
git clone ssh://git@foggy-cliff.picoctf.net:60852/git/challenge.git
Here's the password: 550851c0
Check the README to get your flag!

根據題目將檔案下載並查看 README

![image](/img/picoCTF/General_Skills/MY_GIT/01.png)

只有當 flag.txt 被 root:root@picoctf 上傳時才能獲取 flag，先透過`echo flag > flag.txt`創建檔案，並將名字與郵件設成題目所需

![image](/img/picoCTF/General_Skills/MY_GIT/02.png)

完成後 push 即可獲得 flag

![image](/img/picoCTF/General_Skills/MY_GIT/03.png)

```TXT
picoCTF{1mp3rs0n4t4_g17_345y_506743df}
```

---

### ping-cmd
**題目連結**:https://learn.cylabacademy.org/library/757
>Can you make the server reveal its secrets? It seems to be able to ping Google DNS, but what happens if you get a little creative with your input?
You can connect to the service here nc mysterious-sea.picoctf.net 51563

根據題目連線後發現可以自行輸入 IP 做使用，結合提示說可以執行多項指令，輸入 `8.8.8.8 | ls` 看看有什麼

![image](/img/picoCTF/General_Skills/ping-cmd/01.png)

發現有 flag.txt，改成 `cat flag.txt` 即可獲得 flag

![image](/img/picoCTF/General_Skills/ping-cmd/02.png)

```TXT
picoCTF{p1nG_c0mm@nd_3xpL0it_su33essFuL_b75fc848}
```

---

### bytemancy 0
>Can you conjure the right bytes? The program's source code can be downloaded [here](https://challenge-files.picoctf.net/c_candy_mountain/87600c43f9f35274d6269e8237fcd84602c631a5ebcf5251266fb11dc0e94f3b/app.py).
Connect to the program with netcat:
 $ nc candy-mountain.picoctf.net 59467

先連線觀察

![image](/img/picoCTF/General_Skills/bytemancy_0/01.png)

根據他的要求輸入`eee`，即可獲得 flag

![image](/img/picoCTF/General_Skills/bytemancy_0/02.png)

```TXT
picoCTF{pr1n74813_ch4r5_4daf27d8}
```

---

### bytemancy 1
**題目連結**:https://learn.cylabacademy.org/library/762
>Can you conjure the right bytes? The program's source code can be downloaded [here](https://challenge-files.picoctf.net/c_foggy_cliff/daa319a677eb71bb708aaa0943d7b89ed690c041c0ec5d554332f2e5432b4041/app.py).
Connect to the program with netcat: 
 $ nc foggy-cliff.picoctf.net 57579

先連線觀察

![image](/img/picoCTF/General_Skills/bytemancy_1/01.png)

發現他需要 連續發送 ASCII 值為 101(e) 的字連續 1751 次，且不能有空格，製作一個 python 發送字串即可獲得flag

```python
from pwn import *
p = remote('foggy-cliff.picoctf.net', 57579)
p.recvuntil(b'==>') 

payload = 'e' * 1751

p.sendline(payload)
p.interactive()
```

![image](/img/picoCTF/General_Skills/bytemancy_1/02.png)

```TXT
picoCTF{h0w_m4ny_e's???_e0d51f4b}
```

---

### Piece by Piece
**題目連結**:https://learn.cylabacademy.org/library/740
>After logging in, you will find multiple file parts in your home directory. These parts need to be combined and extracted to reveal the flag.
SSH to dolphin-cove.picoctf.net:57642 and login as ctf-player with password 1ad5be0d.

使用指令`ssh -p 57642 ctf-player@dolphin-cove.picoctf.net`並輸入密碼`1ad5be0d`連線，順便輸入`ls -la`看看有什麼檔案

![image](/img/picoCTF/General_Skills/Piece_by_Piece/01.png)

發現有一個`instructions.txt`，打開看看

![image](/img/picoCTF/General_Skills/Piece_by_Piece/02.png)

發現其他`part_a*`是被拆分的 flag，使用正則表達式`cat part_a* > combined_file && file combined_file`將分部組成原本的樣子，並使用查看是什麼檔案類型

![image](/img/picoCTF/General_Skills/Piece_by_Piece/03.png)

發現是 .zip 使用 `mv combined_file flag.zip && unzip flag.zip`重新命名並解壓縮。需輸入在 instructions 中提到的解壓縮密碼`supersecret`

![image](/img/picoCTF/General_Skills/Piece_by_Piece/04.png)

使用`flag.txt`查看解壓後檔案即可獲得 flag

```TXT
picoCTF{z1p_and_spl1t_f1l3s_4r3_fun_5b6e506b}
```

---

## binhexa
**題目連結**:https://learn.cylabacademy.org/library/404
>How well can you perfom basic binary operations?
Start searching for the flag here nc titan.picoctf.net 61269

連線後發現是要回答二進為運算問題，根據問題回答即可獲得 flag

![image](/img/picoCTF/General_Skills/binhexa/01.png)

`>>`與`<<`為右移與左移，是將原式向左或右移動後捨去該方向最後一位，另一方向補 0，詳細可參考 [Microsoft](https://learn.microsoft.com/zh-tw/cpp/cpp/left-shift-and-right-shift-operators-input-and-output?view=msvc-170) 提供之文檔。

```TXT
picoCTF{b1tw^3se_0p3eR@tI0n_su33essFuL_d6f8047e}
```

---

## repetitions
**題目連結**:https://learn.cylabacademy.org/library/371
>Can you make sense of this file?
Download the file [here](https://artifacts.picoctf.net/c/475/enc_flag).

先下載下來看看是什麼

![image](/img/picoCTF/General_Skills/repetitions/01.png)

看起來是要解碼 base64，結合題目名稱與提示，應該是要解碼好幾次，寫個python解

```python
import base64

def solve():
    with open('enc_flag', 'r') as f:
        data = f.read().strip()
    count = 0

    while True:
        try:
            decoded_bytes = base64.b64decode(data.encode())
            decoded_str = decoded_bytes.decode('utf-8', errors='ignore')
            if "picoCTF" in decoded_str:
                print(f"Flag: {decoded_str.strip()}")
                break
            data = decoded_str.strip()
        except Exception as e:
            print(f"\nERR last: {data}")
            break

if __name__ == "__main__":
    solve()
```

執行即可獲得 flag

```TXT
picoCTF{base64_n3st3d_dic0d!n8_d0wnl04d3d_492767d2}
```

# [⬅️ 回到總覽索引](/2026/01/11/picoCTF/)