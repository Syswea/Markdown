# Codeforces Round #809 (Div.2)

## [CONTESTS ADDRESS][https://codeforces.com/contest/1706]

## A

### 做法简述

找到较小的位置，如果是不`A`就更改，如果是`A`就更改较大的位置。

### 源代码

``` c++
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
    vector<char> S(m);
    for (int i = 0; i < m; i ++ ) S[i] = 'B';
    for (int i = 0; i < n; i ++ ) {
        int x; cin >> x; -- x;
        if (S[min(x, m - 1 - x)] != 'A') S[min(x, m - 1 - x)] = 'A';
        else S[max(x, m - 1 - x)] = 'A';
    }
    for (auto x : S) cout << x ;
    cout << endl;
    return ;
}
signed main () {
    ios::sync_with_stdio(false);
    cin.tie(nullptr); cout.tie(nullptr);
    int tt; cin >> tt;
    while (tt -- ) solve ();
    return 0;
}
```

### 总结

普通模拟。

## B

### 做法简述

简单分析一下，如果两个相同颜色的色块想要纵向并列排放，由于是顺序放置，所以两两之间需要偶数个色块。

邻接表`vec[x]`存储颜色是x的位置下标，然后dp一下即可。

色块想要相连，中间需要偶数个色块，那么处于奇数位置上的色块就要贪心的找到前一个偶数位置的色块，偶数则同理。

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
    #define pb push_back
    int n; cin >> n;
    vector<vector<int> > vec(n + 1);
    for (int i = 1; i <= n; i ++ ) {
        int x; cin >> x;
        if (vec[x].size() == 0) vec[x].pb(0);
        vec[x].pb(i);
    }
    for (int k = 1; k <= n; k ++ ) {
        auto a = vec[k];
        if (a.size() == 0) {
            cout << 0 << ' ' ;
            continue;
        }
        vector<int> dp(a.size()); dp[0] = 0;
        int i = 0, j = 0;
        for (int t = 1; t < a.size(); t ++ ) {
            if (a[t] & 1) dp[t] = max(dp[t], dp[j] + 1), i = t;
            else dp[t] = max(dp[t], dp[i] + 1), j = t;
        }
        cout << dp[a.size() - 1] << ' ';
    }
    cout << endl;
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

顺序模拟，简单dp。

## C

### 做法简述

如果是奇数个房子就直接统计答案。

如果是偶数个，先去头去尾，两两分组，分别为`first` ` second`。

若有一组中选择`first`那么之前的所有组都要选择`first`。

同理，若有一组中选择`second`那么之后的所有组都要选择`second`。

所以可以对所有`first`做前缀和，对所有的`second`做后缀和，再选择最优。

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
    for (int i = 1; i <= n; i ++ ) cin >> A[i];
    if (n & 1) {
        int res = 0;
        for (int i = 2; i <= n - 1; i += 2)
            res += max(max(A[i - 1], A[i + 1]) + 1 - A[i], 0ll);
        cout << res << endl;
        return ;
    }
    else  {
        #define pb push_back
        vector<int> per, rep;
        per.pb(0);
        rep.pb(0);
        for (int i = 2; i <= n - 2; i += 2 )
            per.pb(per.back() + max(max(A[i - 1], A[i + 1]) + 1 - A[i], 0ll));
        for (int i = n - 1; i >= 3; i -= 2 )
            rep.pb(rep.back() + max(max(A[i - 1], A[i + 1]) + 1 - A[i], 0ll));
        int res = 1ll << 63 - 1;
        for (int i = 0; i <= (n - 1) / 2; i ++ )
            res = min(res, per[i] + rep[(n - 1) / 2 - i]);
        cout << res << endl;
        return ;
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

分类讨论。