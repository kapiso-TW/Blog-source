---
title: ZERO JUDGE 解題紀錄 - UVa
date: 2026-03-05
update: 2026-03-05
description: ZERO JUDGE UVa
comments: true
copyright_author: kapiso
copyright_author_href: https://kapiso-tw.github.io/
copyright_url: write by kapiso
layout: page
---

# ✳️UVA題庫
**題庫網址**:https://zerojudge.tw/Problems?tabid=UVA#tab03

---

## c039. 00100 - The 3n + 1 problem
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=c039
**解題觀念**:基礎條件判斷、迴圈使用
``` C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	int a,b;
	while(cin >> a >> b){
		int ans=-1;
		cout << a << ' ' << b << ' ';
		if(a>b)
			swap(a,b);
		while(a<=b){
			int i=a,n=1;
			while(i!=1){
				if(i%2==1)
					i=i*3+1;
				else
					i/=2;
				n++;
			}
			if(n>ans)
				ans=n;
			a++;
		}
		cout << ans << '\n';
	}
	return 0;
}
```

---

## d129. 00136 - Ugly Numbers
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=d129
**解題觀念**:DP
``` C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	vector<long long> ugly(1500);
	ugly[0]=1;
	int c2=0, c3=0, c5=0;
	for(int i=1;i<1500;i++){
		
		//找出下一最小的下一項
		long long n2=ugly[c2]*2;
		long long n3=ugly[c3]*3;
		long long n5=ugly[c5]*5;
		long long nex=min({n2,n3,n5}); 
		ugly[i]=nex;
		
		//如果是下一項則計數器(次方)增加 
		if(ugly[i]==n2)
			c2++;
		if(ugly[i]==n3)
			c3++;
		if(ugly[i]==n5)
			c5++;
	}
	cout << "The 1500'th ugly number is " << ugly[1499] << ".\n";
	return 0;
}
```