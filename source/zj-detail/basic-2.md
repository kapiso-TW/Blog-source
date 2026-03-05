---
title: ZERO JUDGE 解題紀錄 - Basic 2
date: 2026-03-05
update: 2026-03-05
description: ZERO JUDGE Basic 2
comments: true
copyright_author: kapiso
copyright_author_href: https://kapiso-tw.github.io/
copyright_url: write by kapiso
layout: page
---

# 🟢基礎題庫 
**題庫網址**:https://zerojudge.tw/Problems?tabid=BASIC#tab00

---

## a022. 迴文
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a022
**解題觀念**:基礎迴圈使用
``` C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	string s;
	int c=0;
	cin >> s;
	for(int i=0;i<s.length();i++)
		if(s[i]!=s[s.length()-1-i]){
			c=1;
			break;
		}
	if(c)
		cout << "no\n";
	else
		cout << "yes\n";
	return 0;
}
``` 

---

## a024. 最大公因數(GCD)
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a024
**解題觀念**:基礎迴圈使用
``` C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	long long a,b;
	cin >> a >> b;
	while(b!=0){
		a%=b;
		swap(a,b);
	}
	cout << a << '\n';
	return 0;
}
```

---

## a034. 二進位制轉換
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a034
**解題觀念**:基礎迴圈使用、進位轉換
``` C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	int n;
	while(cin >> n){
		vector<int> v;
		while(n){
			v.push_back(n%2);
			n/=2;
		}
		reverse(v.begin(),v.end());
		for(int i:v)
			cout << i;
		cout << '\n';
	}
	return 0;
}
```

---

## a038. 數字翻轉
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a038
**解題觀念**:基礎迴圈使用
``` C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	long long n;
	cin >> n;
	if(n<0){
		cout << '-';
		n*=-1;
	}
	while(n%10==0 && n>=10)
		n/=10;
	if(n==0)
		cout << "0\n";
	while(n){
		cout << n%10;
		n/=10;
	}
	cout << '\n';
	return 0;
}
```

---

## a040. 阿姆斯壯數
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a040
**解題觀念**:迴圈使用
``` C++
#include <bits/stdc++.h>
using namespace std;

//數出位數並回傳 
long long count(long long a){
	int i=0;
	while(a){
		i++;
		a/=10;
	}
	return i;
}

//依照題目說明計算阿姆斯壯數 
long long ch(long long n){
	long long ans=0;
	int dig=count(n);
	while(n){
		long long res=n%10,t=1;
		n/=10;
		for(int i=0;i<dig;i++)
			t*=res;
		ans+=t;
	}
	return ans;
}

int main() {
	long long a,b,check=0;
	cin >> a >> b;
	if(a>b)
		swap(a,b);
	while(a<=b){
		int am=ch(a);
		if(am==a){
			if(!check){
				cout << am;
				check=1;
			}else
				cout << " " << am;
		}
		a++;
	}
	if(!check)
		cout << "none";
	cout  << '\n';
	return 0;
}
```

---

## a042. 平面圓形切割
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a042
**解題觀念**:數學
``` C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	int n;
	while(cin >> n)
		cout << n*(n-1)+2 << '\n';
	return 0;
}
```

---

## a044. 空間切割
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a044
**解題觀念**:數學
``` C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	int n;
	while(cin >> n)
		cout << (n*n*n+5*n+6)/6 << '\n';
	return 0;
}
//in 0 1 2 3
//ot 1 2 4 8  解方程式 
```

---

## a053. Sagit's 計分程式
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a053
**解題觀念**:基礎條件判斷
``` C++
#include <bits/stdc++.h>
using namespace std;
int main() {
	int n;
	cin >> n;
	if(n<=10)
		cout << 6*n << '\n';
	else if(n<=20)
		cout << 40+2*n << '\n';
	else if(n<=40)
		cout << 60+n << '\n';
	else
		cout << "100\n";
	return 0;
}
```

---

## a054. 電話客服中心
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a054
**解題觀念**:數學
``` C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	int n,c,t=0;
	string s[10]={"BNZ","AMW","KLY","JVX","HU","GT","FS","ER","DOQ","CIP"};
	cin >> n;
	c=n%10;
	n/=10;
	for(int i=1;i<=8;i++){
		t+=i*n%10;
		n/=10;
		t%=10;
	}
	cout << s[(20-t%10-c)%10] << '\n';
	return 0;
}
```

---

## a058. MOD3
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a058
**解題觀念**:基礎條件判斷
``` C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	int n,l0=0,l1=0,l2=0;
	cin >> n;
	while(n--){
		int t;
		cin >> t;
		if(t%3==0)
			l0++;
		else if(t%3==1)
			l1++;
		else
			l2++;
	}
	cout << l0 << ' ' << l1 << ' ' << l2 <<'\n';
	return 0;
}
```

---

## a059. 完全平方和
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a059
**解題觀念**:基礎迴圈使用
``` C++
#include <bits/stdc++.h>
using namespace std;
int main() {
	int n,a,b,i=1;
	cin >> n;
	while(n--) {
		cin >> a >> b;
		int ans=0;
		while(a<=b) {
			if(int(sqrt(a))*int(sqrt(a))==a)
				ans+=a;
			a++;
		}
		cout << "Case " << i << ": " << ans << '\n';
		i++;
	}
	return 0;
}
```

---

## a065. 提款卡密碼
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a065
**解題觀念**:基礎字串處理
``` C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	string s;
	cin >> s;
	for(int i=0;i<s.length()-1;i++)
		cout << abs(s[i+1]-s[i]);
	cout << '\n';
	return 0;
}
```

## a104. 排序
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a104
**解題觀念**:基礎迴圈使用
``` C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	int n;
	while(cin >> n){
		vector<int> v(n);
		int z=0;
		for(int i=0;i<n;i++)
			cin >> v[i];
		sort(v.begin(),v.end());
		
		cout << v[0];
		for(int i=1;i<n;i++)
			cout << ' ' << v[i];
		cout << endl;
	}
	return 0;
}

```  

# [⬅️ 回到總覽索引](/2026/02/09/zero_judge/)