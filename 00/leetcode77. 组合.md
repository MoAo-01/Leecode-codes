### 01枚举
- __builtin_popcount计数

```cpp
class Solution {
public:
    vector<vector<int>> combine(int n, int k) {
        vector<vector<int>> ans;
        for(int mask=1;mask<(1<<n);mask++){
            if(__builtin_popcount(mask)==k){
                vector<int>combination;
                for(int i=0;i<n;i++){
                    if(mask&(1<<i)){
                        combination.push_back(i+1);
                    }
                }
                ans.push_back(combination);
            }
        }
        return ans;
    }
};
```
