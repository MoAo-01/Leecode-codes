### 解题思路
练习vector

### 代码

```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        vector<int>res;
        for(int i=0;i<nums.size();i++){
            if(i>0&&nums[i-1]==nums[i])continue;
            res.push_back(nums[i]);
        }
        nums.clear(),nums.assign(res.begin(),res.end());
        return res.size();
    }
};
```
