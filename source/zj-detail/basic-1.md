---
title: ZERO JUDGE 解題紀錄 - Basic 1
date: 2026-03-05
update: 2026-03-05
description: ZERO JUDGE Basic 2
comments: true
copyright_author: kapiso
copyright_author_href: https://kapiso-tw.github.io/
copyright_url: write by kapiso
---

# 🟢基礎題庫 
**題庫網址**:https://zerojudge.tw/Problems?tabid=BASIC#tab00

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

## a013. 羅馬數字
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a013
**解題觀念**:變數運算、邏輯判斷
``` C++
#include <bits/stdc++.h>
using namespace std;
int cti(char c){		//單一羅馬數字轉數字
	switch(c){
		case 'I': return 1;
		case 'V': return 5;
		case 'X': return 10;
		case 'L': return 50;
		case 'C': return 100;
		case 'D': return 500;
		case 'M': return 1000;
		default : return 0;
	}
}

int rti(string s){		//分解羅馬數字並判斷加減
	int p=0,ans=0;		//p為上一位數
	for(char c:s){
		int n=cti(c);
		ans+=n;
		if(n>p)
			ans-=2*p;	//MCM
		p=n;		
	}
	return ans;
}

string itr(int n){		//數字轉羅馬
	if(n==0)
		return "ZERO";
	
	int v[]=   {1000, 900, 500, 400, 100, 90 , 50, 40 , 10,  9 , 5 , 4  ,  1};
    string s[]={"M" ,"CM", "D","CD", "C","XC","L","XL","X","IX","V","IV","I"};
    
    string ans="";
    for(int i=0;i<13;i++){
    	while(n>=v[i]){		//重複減直到小於當前檢查的數字
    		n-=v[i];
    		ans+=s[i];
		}
	}
	return ans;
}

int main(){
	string s;
	while(getline(cin,s) && s!="#"){
		string f="",t="";
		for(int i=0;i<s.length();i++){
		 	if(s[i]==' '){
		 		for(int j=i+1;j<s.length();j++)
		 			t+=s[j];
		 		break;
			}else
				f+=s[i];
		}
		cout << itr(abs(rti(t)-rti(f))) << '\n';
	}
	return 0;
}
```

---

## a015. 矩陣的翻轉
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a015
**解題觀念**:基礎迴圈控制
``` C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	int a,b;
	while(cin >> a >> b){
		vector<vector <int>> v(a,vector<int>(b));
		for(int i=0;i<a;i++){
			for(int j=0;j<b;j++)
				cin >> v[i][j];
		}
		
		for(int i=0;i<b;i++){
			for(int j=0;j<a;j++)
				cout << v[j][i] << ' ';
			cout << '\n';
		}
	}
	return 0;
}
```

---

## a017. 五則運算
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a017
**解題觀念**:變數運算、轉換、迴圈控制
``` C++
#include <bits/stdc++.h>
using namespace std;

//解無括號之算式 
long long slove(string s){
	
	//https://www.runoob.com/cplusplus/cpp-libs-sstream.html
	stringstream ss(s);
	
	//暫存器 
	string a;
	vector<long long> v;	//運算元儲存器 
	vector<string> c;		//運算子儲存器
	
	//字串拆分 
	while(ss >> a){
		if(isdigit(a[0]) || (a.length()>1 && a[0]=='-'))
			v.push_back(stoll(a));
		else
			c.push_back(a);
	}
	
	// * / % 先計算 
	for(int i=0;i<c.size();i++){
		if(c[i]=="*"){
			c.erase(c.begin()+i);
			v[i]*=v[i+1];
			v.erase(v.begin()+i+1);
			
			//避免因前一元素擦除而忽略元素或溢位
			i--; 
		}else if(c[i]=="/"){
			c.erase(c.begin()+i);
			v[i]/=v[i+1];
			v.erase(v.begin()+i+1);
			i--;
		}else if(c[i]=="%"){
			c.erase(c.begin()+i);
			v[i]%=v[i+1];
			v.erase(v.begin()+i+1);
			i--;
		}
	}
	
	// + - 後處理 
	for(int i=0;i<c.size();i++){
		if(c[i]=="+"){
			c.erase(c.begin()+i);
			v[i]+=v[i+1];
			v.erase(v.begin()+i+1);
			i--;
		}else if(c[i]=="-"){
			c.erase(c.begin()+i);
			v[i]-=v[i+1];
			v.erase(v.begin()+i+1);
			i--;
		}
	}
	
	//回傳解 
	return v[0];
}

//含有括號的算式處理 
long long re_slove(string s){
	while(1){
		
		//左右括號索引暫存器
		int l=-1,r=-1;
		
		//尋找一對括號 
		for(int i=0;i<s.length();i++){
			if(s[i]=='(')
				l=i;
			else if(s[i]==')'){
				r=i;
				break;
			}	
		}
		
		//未找到則跳出迴圈 
		if(l==-1)
			break;
			
		//找到則計算並替換原有括號處 
		long long m=slove(s.substr(l+1,r-l));
		s.replace(l,r-l+1,to_string(m));
	}
	return slove(s);
}

int main(){
	string s;
	while(getline(cin,s))
		cout << re_slove(s) << '\n';
	return 0;
}
```

---

## a020. 身分證檢驗
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a020
**解題觀念**:基礎邏輯判斷、變數運算
``` C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	string s;
	int t=0;
	cin >> s;
	
	if(s[0]=='I')
		t=34;
	else if(s[0]=='O')
		t=35;
	else if(s[0]=='W')
		t=32;
	else if(s[0]=='X')
		t=30;
	else if(s[0]=='Y')
		t=31;
	else if(s[0]=='Z')
		t=33;
	else if(s[0]>='A' && s[0]<='H')
		t=s[0]-'A'+10;
	else if(s[0]>='J' && s[0]<='N')
		t=s[0]-'J'+18;
	else if(s[0]>='P' && s[0]<='V')
		t=s[0]-'P'+23;

	t=(t%10)*9+t/10;
	
	for(int i=1;i<s.length()-1;i++)
		t+=(s[i]-'0')*(9-i);
	t+=s[s.length()-1]-'0';
	
	if(t%10==0)
		cout << "real\n";
	else
		cout << "fake\n";
	return 0;
}
```

---

## a021. 大數運算
**題目網址**:https://zerojudge.tw/ShowProblem?problemid=a021
**解題觀念**:變數運算、陣列應用、函式運用
``` C++
#include <bits/stdc++.h>
using namespace std;

//a<b回傳 -1; a>b回傳 1; 一樣回傳0;
int compare(string a, string b){ 
	if(a.length()>b.length())
		return 1;
	if(a.length()<b.length())
		return -1;
	if(a>b)
		return 1;
	if(a<b)
		return -1;
	return 0;
	
}

//加法 
string pluss(string a, string c){
	string ans="";
	int p=0;	//進位計數器
	
	//始終以 a 為較大者 
	if(compare(c,a)<0)
		swap(a,c);
		
	reverse(a.begin(),a.end());
	reverse(c.begin(),c.end());
	for(int i=0;i<a.length();i++){
		int n=a[i]-'0'+p;
		
		//如果已超過 c 的位數則忽略 c 
		if(i<c.length())
			n+=(c[i]-'0');
		ans+=n%10+'0';
		p=n/10;
	}
	
	//若計數器有殘餘則加回 
	if(p!=0)
		ans+=p+'0';
		
	reverse(ans.begin(),ans.end());
	return ans;
}

//乘法 (直式乘法)
string cross(string a, string c){
	string ans="";
	vector<int> v(a.length()+c.length(),0);	//直式位數暫存器 
	reverse(a.begin(),a.end());
	reverse(c.begin(),c.end());
	
	//直式乘法 
	for(int i=0;i<c.length();i++){
		for(int j=0;j<a.length();j++){
			int n=(a[j]-'0')*(c[i]-'0');
			v[j+i]+=n;
		}
	}
	
	//進位處理 
	int p=0;
	for(int i=0;i<v.size();i++){
		int c=v[i]+p;
		ans+=c%10+'0';
		p=c/10;
	}
	
	//殘餘進位補回 
	while(p){
		ans+=p%10+'0';
		p/=10;
	}
	
	//去除可能出現在首位的 0
	while (ans.size()>1 && ans.back()=='0')
        ans.pop_back();
	
	reverse(ans.begin(),ans.end());
	return ans;
}

//減法 (輸入前須做大小檢查，前者需為較大者)
string minuss(string a, string c){
	string ans="";
	reverse(a.begin(),a.end());
	reverse(c.begin(),c.end());
	
	int m=0;	//借位暫存器 
	
	//以較短位數為目標施行減法
	for(int i=0;i<c.length();i++){ 
		int n=(a[i]-'0')-(c[i]-'0')-m;
		if(n<0){
			m=1;
			n+=10;
		}else
			m=0;
		ans+=n%10+'0';
	}
	
	//補回較長者剩餘位數
	for(int i=c.length();i<a.length();i++){ 
		int n=(a[i]-'0')-m;
		if(n<0){
			m=1;
			n+=10;
		}else
			m=0;
			ans+=n%10+'0';
	}
	reverse(ans.begin(), ans.end());
	
	//去除可能出現在首位的 0 
	while(ans.length()>1 && ans[0]=='0')
       	ans.erase(0, 1);
	return ans;
}

//除法 (長除法)
string divded(string a, string c){
	if(compare(a,c)<0)
		return "0";
	string ans="0";
	string q="";	//被除數 
	
	
	for(int i=0;i<a.length();i++){
		
		q+=a[i];	//一次取一位
		
		//去除可能出現在首位的 0 
		while(q.length()>1 && q[0]=='0')
            q.erase(0, 1);
        
        //商數計數器 
		int n=0;
		
		//以減法取代除法
		while(compare(q,c)>=0){ 
			q=minuss(q,c);
			n++;
		}
		ans+=n+'0';
	}
	
	//去除可能出現在首位的 0 
	while(ans.length() > 1 && ans[0]=='0')
        ans.erase(0, 1);
    return ans;
}

int main(){
	string s,a,b,c;
	getline(cin,s);
	stringstream ss(s);	//https://www.runoob.com/cplusplus/cpp-libs-sstream.html
	ss >> a >> b >> c;	//分離 數字(a,c)及運算子(c)
	
	if(b=="+"){
		cout << pluss(a,c) << '\n';
	}else if(b=="*"){
		cout << cross(a,c) << '\n';
	}else if(b=="-"){
		if(compare(a,c)<0)
			cout << '-' << minuss(c,a) << '\n';
		else
			cout << minuss(a,c) << '\n';
	}else if(b=="/"){
		cout << divded(a,c) << '\n';
	}
	return 0;
}
```  

# [⬅️ 回到總覽索引](/2026/02/09/zero_judge/)