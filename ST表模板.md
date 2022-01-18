运气糖果

Description

 

今天ZJ学长想转运，所以某某为他带来N颗运气糖果。

每颗运气糖果都有不同的幸运值。

既然ZJ学长想转运，自然希望自己的运气越来越好了，但ZJ学长最多又只能吃M颗(M≤N)糖果。

而且吃东西自然就不想思考了，于是ZJ学长把这个任务扔给了学acm的你，请你帮他从这N颗糖果中找出连续的k颗糖果(k≤M)，使得ZJ学长可以得到最大的幸运值。

Input

 

输入格式

第一行包含两个整数N和M，表示共有N颗糖果，ZJ最多只能吃M颗。

第二行包含空格隔开的N个整数，第i个整数Pi代表第i颗糖果的幸运值。

Output

 

输出格式

输出包含一个整数，为ZJ能够得到的最大幸运值。

数据范围

1≤N≤100000，1≤M≤100000,
−1000000≤Pi≤1000000

Sample Input 1 

5 2
1 2 3 4 5
Sample Output 1

9

```c++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
map<ll,ll> tp;
int parent[10000005];
const ll MOD = 1000000007;
ll a[10000000];
ll sum[10000000];
ll z[10000000];
ll f[500005][50];
vector<ll> V;
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);//读入优化
    ll n, m;
    cin >> n >> m;
    for(int i = 1; i <= n; i++)
    {
        cin >> a[i];
        sum[i] = sum[i - 1] + a[i];//前缀和
    }
    for(int i = 1; i <= n; i++)
    {
        f[i][0] = sum[i];//数组存进st表初始化
    }
    for(int j=1;(1<<j)<=n;++j)
    {
        for(int i=1;i+(1<<j)-1<=n;++i)
        {
            f[i][j] = min(f[i][j-1],f[i+(1<<j-1)][j-1]);
        }
    }//得到当前第i位向后2的k次方位的最小值
    ll k = log2(m);//求固定长度m的是2的几次方便于后面查询
    ll maxx = 0;
    for(int i = m; i <= n; i++)
    {
        maxx = max(maxx, f[i][0] - min(f[i-m][k], f[i-(1<<k)+1][k]));//当前位数的前缀和最大值减去我能查找到的区间的最小值前缀和就是这个区间的最大连续区间值
    }
    cout << maxx << "\n";
    return 0;
}
```
