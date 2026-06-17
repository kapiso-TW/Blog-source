---
title: picoCTF writeup - Reverse Engineering
date: 2026-03-06
update: 2026-06-17
description: picoCTF writeup
comments: true
copyright_author: kapiso
copyright_author_href: https://kapiso-tw.github.io/
copyright_url: write by kapiso
---

# Reverse Engineering
**題目類別連結**: https://learn.cylabacademy.org/library?category=3&page=1

## 🟢Easy

### Flag Hunters
**題目連結**: https://learn.cylabacademy.org/library/472
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

# [⬅️ 回到總覽索引](/2026/01/11/picoCTF/)