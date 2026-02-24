---
title: THJCC CTF 2026 沒時間玩 :(
date: 2026-02-21
update: 2026-02-22
tags: CTF
categories: coding
keywords:
    - CTF
    - THJCC
    - 資安
description: THJCC CTF 2026
top_img: /img/THJCC_2026/THJCC_back.png
cover: /img/THJCC_2026/THJCC_logo.png
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

# Weclome

## Welcome to THJCC CTF
**Descript**:In this CTF, unless otherwise specified, the flag format is THJCC{.*}
**write up**:開啟開發人員工具即可發現flag
![img](/img/THJCC_2026/Welcome/01.png)
``` TXT
THJCC{We1c0m3-tO-tHjcC-c7F_2O26}
```

# Reverse

## Super baby reverse
**Descript**:My first C lang project can you find the hidden message inside?
**write up**:先查看整體組合語言
![img](/img/THJCC_2026/Super_baby_reverse/01.png)
發現有`strcmp`，用來比較兩字串，在此製造斷點並查看暫存器即可
![img](/img/THJCC_2026/Super_baby_reverse/02.png)
``` TXT
THJCC{BaBY_r3v3rs3_f0r_beggin3r}
```

## Fllllllag_ch3cker_again?
**Descript**:Flag chekcer again?????????
**write up**:使用 gdb 查看後發現是 C++
![img](/img/THJCC_2026/Fllllllag_ch3cker_again/01.png)
慢慢一個一個用 `echo '' | c++filt` 找 operator== ~~(我就爛~~
![img](/img/THJCC_2026/Fllllllag_ch3cker_again/02.png)
然後在 基底位址 + 偏移量 加上斷點並執行，查看暫存器即可
![img](/img/THJCC_2026/Fllllllag_ch3cker_again/03.png)

``` TXT
THJCC{A_Simpl3_R3v3r3_using_CPP_d0ing_X0R}
```

# Misc

## IMAGE?
**Descript**:Check the hex of this image
**write up**:使用 binwalk 檢查並提取檔案即可
![img](/img/THJCC_2026/IMAGE/01.png)
![img](/img/THJCC_2026/IMAGE/02.png)
``` TXT
THJCC{fRierEN-SO_cUTe:)}
```


# Web

## Las Vegas
**Descript**:Lucky 7 7 7
**write up**:使用 Burp Suite 修改拉下拉霸機後的封包並送出即可
![img](/img/THJCC_2026/Las_Vegas/01.png)
![img](/img/THJCC_2026/Las_Vegas/02.png)
``` TXT
THJCC{LUcKy_sEVen_7777777}
```

## 0422
**Descript**:A very simple challenge about a web exploit. Really simple. LOL.
**write up**:使用 Burp Suite 將登入時cookie帶的role改成admin即可
![img](/img/THJCC_2026/0422/01.png)
![img](/img/THJCC_2026/0422/02.png)
``` TXT
THJCC{c00k135_4r3_n07_53cur3_1f_n07_51gn3d_4nd_p13453_d0_7h3_53cur3_c0d1ng_r3v13w_101111}
```