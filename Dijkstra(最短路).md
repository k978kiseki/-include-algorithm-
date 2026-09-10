### n : 结点数
### m : 边数
### s : 起点
### q : 询问次数
```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <climits>
using namespace std;

using ll = long long;
vector<ll> dist;
vector<vector<pair<int, int>>> adj;
void Dijkstra(int s) {
	dist[s] = 0;
	priority_queue <
		pair <ll, int>,
		vector<pair<ll, int>>,
		greater<pair<ll, int>>
	> pq;
	pq.push({ 0, s });
	while (!pq.empty()) {
		auto [cur_dist, u] = pq.top();
		pq.pop();
		if (cur_dist > dist[u])continue;
		for (auto& [v, l] : adj[u]) {
			ll temp = dist[u] + l;
			if (dist[v] > temp) {
				dist[v] = temp;
				pq.push({ dist[v], v });
			}
		}
	}
}
int main() {
	ios::sync_with_stdio(false), cin.tie(nullptr);
	int n, m, s, q;
	cin >> n >> m >> s >> q;
	dist.resize(n + 1, LLONG_MAX);
	adj.resize(n + 1);
	while (m--) {
		int u, v, l;
		cin >> u >> v >> l;
		adj[u].emplace_back(v, l), adj[v].emplace_back(u, l);
	}
	Dijkstra(s);
	while (q--) {
		int pos;
		cin >> pos;
		cout << (dist[pos] == LLONG_MAX ? -1 : dist[pos]) << '\n';
	}
}
```
### `dist[i]` : 从`起点(s)`到`结点(i)`的`最短路程`