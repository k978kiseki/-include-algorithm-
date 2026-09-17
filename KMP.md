```cpp
#include <iostream>
#include <vector>
using namespace std;
string s, p;
vector<int> pi;
void get_pi() {
	for (int i = 1; i < p.size(); i++) {
		int j = pi[i - 1];
		while (j > 0 && p[i] != p[j]) {
			j = pi[j - 1];
		}
		if (p[i] == p[j]) {
			j++;
		}
		pi[i] = j;
	}
}
int main() {
	cin >> s >> p;
	pi.resize(p.size());
	get_pi();
	//start KMP
	vector<int> pos; //用于记录p在s中出现的位置(升序，从下标0开始)
	int j = 0;
	for (int i = 0; i < s.size(); i++) {
		while (j > 0 && s[i] != p[j]) {
			j = pi[j - 1];
		}
		if (s[i] == p[j]) {
			j++;
		}
		if (j == p.size()) {
			pos.push_back(i - p.size() + 1);
			j = pi[j - 1];
		}
	}
}
```