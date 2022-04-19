### 解题思路
- $ O(N) $

### 代码

```cpp
//https://github.com/MoAo-01/Leecode-codes
class Solution {
public:
    vector<int> shortestToChar(string s, char c) {
        int n=s.size(),dis;
        vector<int>ans0(n),ans1(n),ans(n);
        dis=1e9;
        for(int i=0;i<n;i++){
            dis=s[i]==c?0:dis+1;
            ans0[i]=dis;
        }
        dis=1e9;
        for(int i=n-1;i>=0;i--){
            dis=s[i]==c?0:dis+1;
            ans1[i]=dis;
        }
        for(int i=0;i<n;i++){
            ans[i]=min(ans0[i],ans1[i]);
        }
        return ans;
    }
};
```
