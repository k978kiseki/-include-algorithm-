```cpp
#include <iostream>
#include <vector>
#include <cstring>
using namespace std;

const int N = 3e6 + 5; //输入字符串的总长度
int trie[N][62], sum[N], cntEnd[N];
int GetNum(char x) {
	if (x >= 'A' && x <= 'Z')
		return x - 'A';
	else if (x >= 'a' && x <= 'z')
		return x - 'a' + 26;
	else return x - '0' + 52;
}
int Query(string& t) {
	int p = 0;
	for (char ch : t) {
		int u = GetNum(ch);
		if (!trie[p][u])
			return 0;
		p = trie[p][u];
	}
	return cntEnd[p];
}
int QueryPrefix(string& t) {
	int p = 0;
	for (char ch : t) {
		int u = GetNum(ch);
		if (!trie[p][u])
			return 0;
		p = trie[p][u];
	}
	return sum[p];
}
int main() {
	ios::sync_with_stdio(false), cin.tie(nullptr);
	int T, n, q, idx = 0;
	cin >> T;
	while (T--) {
		memset(trie, 0, (idx + 1) * sizeof trie[0]);
		memset(sum, 0, (idx + 1) * sizeof sum[0]);
		memset(cntEnd, 0, (idx + 1) * sizeof cntEnd[0]);
		cin >> n >> q;
		idx = 0;
		string s, t;
		for (int i = 0; i < n; i++) {
			cin >> s;
			int p = 0;
			for (char ch : s) {
				int u = GetNum(ch);
				if (!trie[p][u])
					trie[p][u] = ++idx;
				p = trie[p][u];
				sum[p]++;
			}
			cntEnd[p]++;
		}
		while (q--) {
			cin >> t;
			cout << Query(t) << '\n'; //查找字符串t的个数
			//cout << QueryPrefix(t) << '\n'; //以t作为前缀串查找
		}
	}
}
```