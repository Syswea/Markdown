# Codeforces Round #810 (Div.2)

## [CONTESTS ADDRESS][https://codeforces.com/contest/1711]

## A

### 做法简述

因为 `i - 1 ` 无法整除 `i` 所以只要在第 `i` 个位置上放数字 `i - 1` 就可以让除了 `1` 之外的所有位置的贡献为 `0` 。

### 源代码

```c++
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define x first
#define y second
typedef pair<int, int> pii;
inline int read() {
    #ifndef gc
    #define gc() c=getchar()
    int x = 0, f = 0; char c; gc();
    for (; !isdigit(c); gc()) if (c == '-') f = 1;
    for (; isdigit(c); gc()) x = (x << 1) + (x << 3) + (c ^ '0');
    return f ? ~ x + 1: x;
    #endif
}
void solve () {
    int n; cin >> n;
    cout << n << ' ';
    for (int i = 1; i <= n - 1; i ++ ) cout << i << ' ';
    cout << endl;
}
signed main () {
    ios::sync_with_stdio(false);
    cin.tie(nullptr); cout.tie(nullptr);
    int tt; cin >> tt;
    while (tt -- )
        solve();
    return 0;
}
```

### 总结

构造。

## B

### 做法简述

如果有偶数组朋友参与，那就所有的人都邀请，这样结果就是 0 。

如果有奇数组朋友参与，邀请所有人的话必然会出现奇数个蛋糕，不符合题意。

我们可以剔除掉一个人，由他产生的奇数个蛋糕都会消失，这样 `unhappy = A[i]` 。

也可以剔除掉两个人，这两个人为朋友关系，且每一个人都有偶数个朋友，那么就会减少奇数个蛋糕，此时 `unhappy = A[i] + A[j]` 。

### 源代码

```c++
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define x first
#define y second
typedef pair<int, int> pii;
inline int read() {
    #ifndef gc
    #define gc() c=getchar()
    int x = 0, f = 0; char c; gc();
    for (; !isdigit(c); gc()) if (c == '-') f = 1;
    for (; isdigit(c); gc()) x = (x << 1) + (x << 3) + (c ^ '0');
    return f ? ~ x + 1: x;
    #endif
}
void solve () {
    int n, m; cin >> n >> m;
    #define pb push_back
    vector <int> A(n + 1), deg(n + 1);
    vector<vector<int> > vec(n + 1);
    for (int i = 1; i <= n; i ++ ) cin >> A[i];
    for (int i = 1; i <= m; i ++ ) {
        int u, v; cin >> u >> v;
        vec[u].pb(v); vec[v].pb(u);
        deg[u] ++ , deg[v] ++ ;
    }
    if (m % 2 == 0) cout << 0 << endl;
    else {
        int res = 1ll << 63 - 1;
        for (int i = 1; i <= n; i ++ ) {
            if (deg[i] % 2 == 1) res = min(res, A[i]);
            else for (int j = 0; j < vec[i].size(); j ++ ) if (deg[vec[i][j]] % 2 == 0) res = min(res, A[i] + A[vec[i][j]]);
        }
        cout << res << endl;
    }
}
signed main () {
    ios::sync_with_stdio(false);
    cin.tie(nullptr); cout.tie(nullptr);
    int tt; cin >> tt;
    while (tt -- )
        solve();
    return 0;
}
```

### 总结

图论，搜索。

## C

### 做法简述

要想满足条件必须要涂满一整行色块，且同样颜色的色块至少要涂满两行。

如果是偶数行需要涂满，保证每一种颜色都要大于 2 就行了。

如果是奇数行需要涂满，则额外需要至少一种颜色可以覆盖三行。

### 源代码

```c++
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define x first
#define y second
typedef pair<int, int> pii;
inline int read() {
    #ifndef gc
    #define gc() c=getchar()
    int x = 0, f = 0; char c; gc();
    for (; !isdigit(c); gc()) if (c == '-') f = 1;
    for (; isdigit(c); gc()) x = (x << 1) + (x << 3) + (c ^ '0');
    return f ? ~ x + 1: x;
    #endif
}
void solve () {
    int n, m, k; cin >> n >> m >> k;
    vector<int> A(k + 1);
    for (int i = 1; i <= k; i ++ ) cin >> A[i];
    int cnt = 0;
    int xmax = 0;
    for (int i = 1; i <= k; i ++ ) {
        int t = A[i] / n;
        xmax = max(xmax, t);
        if (t >= 2) cnt += t;
    }
    if (cnt >= m) {
        if (m % 2 == 0 || xmax >= 3) {
            cout << "YES" << endl;
            return ;
        }
    }
    cnt = 0;
    xmax = 0;
    for (int i = 1; i <= k; i ++ ) {
        int t = A[i] / m;
        xmax = max(xmax, t);
        if (t >= 2) cnt += t;
    }
    if (cnt >= n) {
        if (n % 2 == 0 || xmax >= 3) {
            cout << "YES" << endl;
            return ;
        }
    }
    cout << "NO" << endl;
    return ;
}
signed main () {
    ios::sync_with_stdio(false);
    cin.tie(nullptr); cout.tie(nullptr);
    int tt; cin >> tt;
    while (tt -- )
        solve ();
    return 0;
}
```

### 总结

思维题目。
