---
title: ZERO JUDGE 解題紀錄
date: 2026-02-09
update: 2026-02-09
tags: code
categories: coding
keywords: code
description: ZERO JUDGE
top_img: /img/zero_judge/zerojudge.svg
cover: /img/zero_judge/zerojudge.svg
comments: false
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

# ℹ️總覽
這裡記錄了我在ZeroJudge**解題的思路及感想**，且按照題目分類整理。從基礎輸入輸出至演算法，每道題目皆**包含程式碼以及解題觀念**，較困難題目可能含有**詳細思路**。<br><br>
**目前包含題數**：8 題
**程式語言**：C & C++
<hr>

# 🟢基礎題庫 
**題庫網址**:https://zerojudge.tw/Problems?tabid=BASIC#tab00

## a001. 哈囉
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a001
**解題觀念**:基礎輸出控制
``` C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	string s;
	cin >> s;
	cout << "hello, " << s << '\n';
	return 0;
}
```

## a002. 簡易加法
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a002
**解題觀念**:基礎變數運算
``` C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	long long int a,b;
	cin >> a >> b;
	cout << a+b << '\n';
	return 0;
}
```

## a003. 兩光法師占卜術
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a003
**解題觀念**:基礎變數運算、條件判斷
``` C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	int m,d,s;
	cin >> m >> d;
	s=(m*2+d)%3;
	if(s==0)
		cout << "普通";
	else if(s==1)
		cout << "吉";
	else
		cout << "大吉";
	cout << '\n';
	return 0;
}
```

## a004. 文文的求婚
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a004
**解題觀念**:基礎條件判斷
``` C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	int y;
	while(cin >> y){
		if(y%4==0 && y%100!=0 || y%400==0)
			cout << "閏年";
		else
			cout << "平年";
		cout << '\n';
	}
	return 0;
}
```

## a005. Eva 的回家作業
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a005
**解題觀念**:基礎變數運算、條件判斷
``` C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	int n;
	cin >> n;
	while(n--){
		vector<int> v(4);
		for(int i=0;i<4;i++)
			cin >> v[i];
			
		if(v[1]-v[0]==v[2]-v[1]){
			for(int i:v)
				cout << i << ' ';
			cout << v[3]+(v[3]-v[2]);
		}else{
			for(int i:v)
				cout << i << ' ';
			cout << v[3]*(v[3]/v[2]);
		}
		
		cout << '\n';
	}
	return 0;
}
```

## a006. 一元二次方程式
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a006
**解題觀念**:基礎變數運算
``` C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	int a,b,c;
	cin >> a >> b >> c;
	int check=b*b-4*a*c;
	if(check==0){
		cout << "Two same roots x=" << (b*(-1))/(2*a);
	}else if(check<0)
		cout << "No real root";
	else{
		int r1=(b*(-1)+sqrt(check))/(2*a), r2=(b*(-1)-sqrt(check))/(2*a);
		cout << "Two different roots x1=" << max(r1,r2) << " , x2=" << min(r1,r2);
	}
	cout << '\n';
	return 0;
}
```

## a009. 解碼器
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a009
**解題觀念**:基礎變數運算
``` C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	string s;
	getline(cin,s);
	for(char c:s)
		cout << char(c-7); //參考  https://zh.wikipedia.org/zh-tw/ASCII 
	cout << '\n';
	return 0;
}
```

## a010. 因數分解
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a010
**解題觀念**:基礎變數運算、條件判斷
``` C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	long long int a,t;
	cin >> a;
	t=a;
	int i=2,f=0;
	while(i<=t){
		int c=0;
		while(a%i==0){
			a/=i; 
			c++;
		}
		if(c>0){
			if(f!=0)
				cout << " * ";
			else
				f++;
				
			if(c==1)
				cout << i;
			else
				cout <<i << "^" << c; 
		}
		i++;
	}
	cout << '\n';
	return 0;
}
```

<!--
## a013. 羅馬數字
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a013
**解題觀念**:基礎變數、輸入輸出控制、變數運算
``` C++

```

## 
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a
**解題觀念**:基礎變數、輸入輸出控制、變數運算
``` C++

```

## 
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a
**解題觀念**:基礎變數、輸入輸出控制、變數運算
``` C++

```

## 
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a
**解題觀念**:基礎變數、輸入輸出控制、變數運算
``` C++

```

## 
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a
**解題觀念**:基礎變數、輸入輸出控制、變數運算
``` C++

```

## 
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a
**解題觀念**:基礎變數、輸入輸出控制、變數運算
``` C++

``` 
-->