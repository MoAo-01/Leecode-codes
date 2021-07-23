#### 朴素法
> 使用穷举的方法，暴力枚举染色方式（先不考虑非法）

实现方式
- $DFS$ 或者
- 循环枚举（直接对应 $[0,3^{size})$ ）
- 最后写一个$O(nm)$的$check$

最大深度：$size = n * m$
时间复杂度: $O(nm·3^{m+n})$
评测结果：$TLE$
代码作用：验证小数据答案的正确性，OR为进阶提供思路

#### 进阶法
实现方式
1. 打表递推
2. 动态规划

思路一（打表递推）：
>顾名思义，由于本题$m$极小，只有$m\in [1,5]$
>所以，可以直接拆解为$5$道独立的递推题

根据**朴素法**打表：
>$m=1\Rightarrow[3,6,12,24,48,96,···]$
>$\therefore ans[n]=3·2^{n-1}$

>$m=2\Rightarrow[6,18,54,162,486,···]$
>$\therefore ans[n]=2·3^{n}$

>$m=3\Rightarrow[12,54,246,1122,5118,···]$
>$\therefore ans[n]=5ans[n-1]-2ans[n-2]$

规律逐渐变态(不推荐)
>$m=4\Rightarrow[24,162,1122,7812,···]$
>$\therefore ans[n]=9ans[n-1]-15ans[n-2]+6ans[n-3]$

>$m=5\Rightarrow[48,486,5118,54450,···]$
>$\therefore ans[n]=16ans[n-1]-65ans[n-2]+92ans[n-3]-48ans[n-4]+8ans[n-5]$

$PS$：对于$m=5$，可令$ans[0]=6$

思路二（动态规划）：
一个比较容易的思路：
>如果按照列来从前往后递推，那么第$n$列的各种状态，为第$n-2$列转移过来的>
>因为此题错$color$的种类和行数$m$均很小，可以考虑暴力存储（状态压缩）

实现步骤：
1. 把一列的所有合法的染色方案，全部存储下来
2. 然后，就只需要从前往后枚举两个不同的$state$，转移即可

时间复杂度：$O(n+3^m)$
评测结果：$AC$

#### 高阶法
考虑，在此题情景中，递推法$OR$状态压缩动态规划的本质
- 在底维度时，本质上是直接求一个数的幂，
- 在高维度时，本质上是求一个矩阵的幂。

所以，可以考虑直接使用矩阵快速幂，加速求解答案的过程

时间复杂度：$O(log(n)+3^m)$
评测结果：当然也是$AC$啦，不过还没写

### 随便贴一个（状压DP的）代码
```cpp [c++/状压DP]
class Solution {
public:
    vector<vector<int>> states;
    
    typedef long long LL;
    int mod = 1e9 + 7;
    
    int generate_valid(int m){
        if (m == 5)
            for (int i = 0; i < 3; i ++)
            for (int j = 0; j < 3; j ++)
            for (int k = 0; k < 3; k ++)
            for (int h = 0; h < 3; h ++)
            for (int l = 0; l < 3; l ++)
            if (i != j && j != k && k != h && h != l)
                states.push_back({i, j, k, h, l});
        
        if (m == 4)
            for (int i = 0; i < 3; i ++)
            for (int j = 0; j < 3; j ++)
            for (int k = 0; k < 3; k ++)
            for (int h = 0; h < 3; h ++)
            if (i != j && j != k && k != h)
                states.push_back({i, j, k, h});
        
        if (m == 3)
            for (int i = 0; i < 3; i ++)
            for (int j = 0; j < 3; j ++)
            for (int k = 0; k < 3; k ++)
            if (i != j && j != k)
                states.push_back({i, j, k});
        
        if (m == 2)
            for (int i = 0; i < 3; i ++)
            for (int j = 0; j < 3; j ++)
            if (i != j)
                states.push_back({i, j});
        
        if (m == 1)
            for (int i = 0; i < 3; i ++)
                states.push_back({i});
        return states.size();
    }
    
    bool is_valid(int st1, int st2, int m){
        for (int i = 0; i < m; i ++)
            if (states[st1][i] == states[st2][i]) return false;
        return true;
    }

    int colorTheGrid(int m, int n) {
        int s = generate_valid(m);
        LL dp[n + 1][s];
        memset(dp, 0, sizeof dp);
        for (int i = 0; i < s; i ++)dp[1][i] = 1;        
        if (n == 1) return s;
        for (int i = 2; i <= n; i ++)
            for (int sti = 0; sti < s; sti ++)
                for (int stj = 0; stj < s; stj ++)
                    if (is_valid(sti, stj, m))
                        dp[i][sti] = (dp[i][sti] + dp[i - 1][stj]) % mod;
        LL cnt = 0;
        for (int i = 0; i < s; i ++) cnt = (cnt + dp[n][i]) % mod;        
        return (int) cnt;
    }
};
```

