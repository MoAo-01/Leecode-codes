### 解题思路
- 快速 `sort`
- 一维降序，二维升序
- 对二维 `defense防御力` 贪心

### 代码

```cpp
class Solution {
public:
    typedef vector<int> ad;
    int numberOfWeakCharacters(vector<ad>& p) {
        sort(begin(p),end(p),[](ad&x,ad&y){return x[0]>y[0]||(x[0]==y[0]&&x[1]<y[1]);});
        int maxd=p[0][1],ans=0;
        for(auto&np:p)
            maxd>np[1]?ans++:maxd=np[1];        
        return ans;
    }
};
```
### 桶排序
- 根据题目特点，为了换取更高的时间效率
- 我们开辟较大的空间，即使用`桶排序(的变形)`


```cpp
class Solution {
public:
    int numberOfWeakCharacters(vector<vector<int>>& properties) {
        int maxn=100000,ans=0;
        vector<int>t(maxn+5,0);
        for(auto&p:properties)t[p[0]]=max(t[p[0]],p[1]);
        for(int i=maxn;i>0;i--)t[i]=max(t[i],t[i+1]);
        for(auto&p:properties)if(t[p[0]+1]>p[1])ans++;
        return ans;
    }
};
```
