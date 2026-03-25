## 二分 + Dijkstra

```c++
#include <bits/stdc++.h>

using namespace std;

int n, m, b;

const int N = 5e4 + 10;

const int M = 1e5 + 10;

int f[N];

int h[N], e[M], ne[M], w[M], idx;

int dist[N];

bool vis[N];

bool flag = false;

void add(int a, int b, int c) {

    e[idx] = b;

    w[idx] = c;

    ne[idx] = h[a];

    h[a] = idx ++;

}

  

bool check(int mid ) {

    memset(dist, 0x3f, sizeof dist);

    memset(vis, false, sizeof vis);

  

    dist[1] = 0;

    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<>> q;

    if(f[1] > mid) return false;

    q.push({dist[1], 1});

  

    while(!q.empty()) {

        int u = q.top().first;

        int v = q.top().second;

        q.pop();

        if(v == n && f[n] <= mid) {

            return true;

        }

        if(f[v] > mid) continue;

        if(vis[v]) continue;

        vis[v] = true;

  

        for(int i = h[v]; i != -1; i = ne[i]) {

            int t = e[i];

            int s = w[i];

            if(dist[t] > dist[v] + s) {

                dist[t] = dist[v] + s;

                if(dist[t] > b) continue;

                else q.push({dist[t], t});

            }

        }

    }

    return false;

}

  

int main() {

    cin >> n >> m >> b;

    int max_sum = 0;

    for(int i = 1; i <= n; i ++ ) {

        cin >> f[i];

        max_sum = max(max_sum, f[i]);

    }

    memset(h, -1, sizeof h);

  

    for(int i = 0; i < m; i ++ ) {

        int a, x, c;

        cin >> a >> x >> c;

        add(a, x, c);

        add(x, a, c);

    }

  

    int l = 0, r = max_sum;

    while(l < r) {

        int mid = l + r >> 1;

        if(check(mid)) r = mid;

        else l = mid + 1;

    }

    if(check(l)) cout << l;

    else cout << "AFK";

    return 0;

}

```
