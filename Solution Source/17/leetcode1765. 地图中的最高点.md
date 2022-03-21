### 先放结果
![image.png](https://pic.leetcode-cn.com/1643418459-tEDRcg-image.png)


### 解题思路
- 抽象一下，其实就是有多个起点（水域）
- 然后从起点，向四周扩展
- 四个方向的扩展，等价于看出左上到右下，和右下到左上，`2` 种扩展方式
- 令 `dp[x][y]` 为最近的水域到其距离（即答案）
- 显然有转移方程 `dp(this_poit)=min(dp(this_point), dp(next_to_poit)+1)`
- 于是得到 `DP` 代码如下

### 引用参考
[https://leetcode.com/problems/map-of-highest-peak/discuss/1074638/dp%3A-2d-matrix-two-direction-traversal](https://leetcode.com/problems/map-of-highest-peak/discuss/1074638/dp%3A-2d-matrix-two-direction-traversal)

### 代码


```cpp [1-展开版]
class Solution {
public:
    vector<vector<int>> highestPeak(vector<vector<int>>& isWater) {
        //dp: the distance to 0
        int m=isWater.size(),n=isWater[0].size(),mn=m*n;
        vector<vector<int>>dp(m,vector<int>(n,0));
        for(int i=0;i<m;i++)for(int j=0;j<n;j++)
            dp[i][j]=
                !isWater[i][j]?
                    min(
                        i?dp[i-1][j]:mn,
                        j?dp[i][j-1]:mn
                    )+1
                :0;
        for(int i=m-1;i>=0;i--)for(int j=n-1;j>=0;j--)
            dp[i][j]=
                !isWater[i][j]?
                    min(
                        dp[i][j],
                        min(
                            i+1<m?dp[i+1][j]:mn,
                            j+1<n?dp[i][j+1]:mn
                        )+1
                    )
                :0;
        return dp;
    }
};
```

```cpp [1-精简版]
class Solution {
public:
    vector<vector<int>> highestPeak(vector<vector<int>>& isWater) {
        //dp: the distance to 0
        int m=isWater.size(),n=isWater[0].size(),mx=m*n;
        vector<vector<int>> dp(m,vector<int>(n,0));
        for(int i=0;i<m;i++)for(int j=0;j<n;j++)
            dp[i][j]=isWater[i][j]==0?(min(i?dp[i-1][j]:mx,j?dp[i][j-1]:mx)+1):0;
        for(int i=m-1;i>=0;i--)for(int j=n-1;j>=0;j--)
            dp[i][j]=isWater[i][j]==0?min({dp[i][j],min(i+1<m?dp[i+1][j]:mx,j+1<n?dp[i][j+1]:mx)+1}):0;
        return dp;
    }
};
```
