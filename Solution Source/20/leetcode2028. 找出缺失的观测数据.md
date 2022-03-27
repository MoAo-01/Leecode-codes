### 解题思路
- 构造

### 代码

```cpp
//https://github.com/MoAo-01/Leecode-codes
class Solution {
public:
    vector<int> missingRolls(vector<int>& rolls, int mean, int n) {
        vector<int>ans;
        int m=rolls.size();
        int sum=accumulate(begin(rolls),end(rolls),0);        
        if(n+sum<=(n+m)*mean && (n+m)*mean<=sum+n*6){
            int reserve= (n+m)*mean-sum;
            // n*x+y=reserve
            int x=reserve/n,y=reserve-n*x;
            ans=vector<int>(n,x);
            for(int i=0;i<y;i++)ans[i]++;
        }
        return ans;
    }
};
```
