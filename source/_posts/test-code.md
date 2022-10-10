---
title: test_code
tags: test
categories: test
abbrlink: 726c1a57
date: 2022-10-06 09:41:20
---

```cpp
#include <bits/stdc++.h>

using namespace std;

string word[23];
char tar;
bool can[23][23];
int vis[23], ans;
int n;

int chong(int x, int y){
	bool pp=true; 
	int ky=0;
	for(int k=word[x].size()-1;k>=0;k--){
		for(int kx=k;kx<word[x].size();kx++){
			if(word[x][kx]!=word[y][ky++]){
				pp=false;
				break;
			}
		}
		if(pp==true){
			return word[x].size()-k;        
		} 
		ky=0;
		pp=true;
	}
	return 0;
}

void dfs(int ind, int len) {
	ans = max(ans, len);
	for (int i = 1; i <= n; i++) {
		if(ind==i) continue;
		if(can[ind][i]==word[i].size()||can[ind][i]==word[ind].size()) continue;
		if (can[ind][i] && vis[i] < 2) {
			vis[i]++;
			dfs(i, len + word[i].size()-can[ind][i]);
			vis[i]--;
		}
	}
	
}


int main() {
	cin >> n;
	for (int i = 1; i <= n; i++) {
		cin >> word[i];
	}
	cin >> tar;
	for (int i = 1; i <= n; i++) {
		for (int j = 1; j <= n; j++) {
			if(i==j) continue;
			can[i][j] = chong(i,j);
		}
	}
	for (int i = 1; i <= n; i++) {
		for (int j = 1; j <= n; j++) {
			cout << word[i] << " " << word[j] << " " << can[i][j] << endl;
		}
	}
	for (int i = 1; i <= n; i++) {
		if (word[i][0] == tar) {
			vis[i]++;
			dfs(i, word[i].size());
			vis[i] = 0;
		}
	}
	cout << ans;
	return 0;
}


```
