# Codeforce Round #808 (div.2)

## [CONTEST ADDRESS][https://codeforces.com/contest/1708]

## A

### 做法简述

`A[i] = A[i] - A[i - 1]` 而且要求 `A[i] = 0` ，所以 `A[i]` 一定是 `A[i - 1]` 的倍数。

所以 `A[i]` 一定是 `A[0]` 的倍数。

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
    vector<int> A(n + 1);
    for (int i = 0; i < n; i ++ ) cin >> A[i];
    for (int i = 1; i < n; i ++ )
        if (A[i] % A[0]) {
            cout << "NO" << endl;
            return ;
        }
    cout << "YES" << endl;
    return ;
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

递推模拟。

## B

### 做法简述

令 `gcd(i, a[i]) = i` 只要在 `l ~ r` 中找到 `i` 的倍数即可。

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
void sovle () {
    int n, l, r;
    cin >> n >> l >> r;
    vector<int> A(n + 1);
    for (int i = 1; i <= n; i ++ ) {
        int x = l / i, y = r / i;
        if (l % i == 0) A[i] = l;
        else if (r % i == 0) A[i] = r;
        else {
            if (x == y) {
                cout << "NO" << endl;
                return ;
            }
            else {
                A[i] = y * i;
            }
        }
    }
    cout << "YES" << endl;
    for (int i = 1; i <= n; i ++ ) cout << A[i] << ' ';
    cout << endl;
    return ;
}
signed main () {
    ios::sync_with_stdio(false);
    cin.tie(nullptr); cout.tie(nullptr);
    int tt; cin >> tt;
    while (tt -- )
        sovle();
    return 0;
}
```

### 总结

构造。

## C

### 做法简述

最好的情况的最终 IQ 状态应该是 0 或者 1 。

所以可以从最后的地方开始倒退求解。

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
    #define gc() c = getchar()
    int x = 0, f = 0; char c; gc();
    for (; !isdigit(c); gc()) if (c == '-') f = 1;
    for (; isdigit(c); gc()) x = (x << 1) + (x << 3) + (c ^ '0');
    return f ? ~ x + 1: x;
    #endif
}
void sovle () {
    int n, q; cin >> n >> q;
    vector<int> A(n + 1);
    for (int i = 1; i <= n; i ++ ) cin >> A[i];
    vector<int> b(n + 1);
    int now_q = 0;
    for (int i = n; i >= 1; i -- ) {
        if (A[i] <= now_q) b[i] = 1;
        else if (now_q < q)  ++ now_q, b[i] = 1;
        else b[i] = 0;
    }
    for (int i = 1; i <= n; i ++ ) cout << b[i];
    cout << endl;
    return ;
}
signed main () {
    ios::sync_with_stdio(false);
    cin.tie(nullptr); cout.tie(nullptr);
    int tt; cin >> tt;
    while (tt -- )
        sovle();
    return 0;
}
```

### 总结

贪心。
