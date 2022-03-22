### 解题思路
- 注意边界

### 代码

```cpp
//https://github.com/MoAo-01/Leecode-codes
class Solution {
public:
    vector<int> getRange(int l,int r){
        if(l>r)return{};
        if(l==r)return{l};
        return{l,r};
    }

    string getRangeToString(vector<int>&a){
        if(a.size()==1)return to_string(a[0]);
        return to_string(a[0])+"->"+to_string(a[1]);
    }

    vector<string> findMissingRanges(vector<int>& nums, int lower, int upper) {
        vector<string>ans;
        int last=lower;
        for(int i=0;i<nums.size();i++){
            int pos=nums[i]-1;
            auto range=getRange(last,pos);
            if(range.size()>0)ans.push_back(getRangeToString(range));
            last=nums[i]+1;
        }
        auto range=getRange(last,upper);
        if(range.size()>0)ans.push_back(getRangeToString(range));
        return ans;
    }
};
```
