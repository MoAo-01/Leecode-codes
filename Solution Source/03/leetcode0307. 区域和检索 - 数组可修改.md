### 解题思路
- 单点修改
- 区间查询
- 树状数组
- 板子题

### 代码

```cpp
//https://github.com/MoAo-01/Leecode-codes
class NumArray {
public:
    vector<int>nums;
    vector<int>t;
    void add(int i,int x){for(;i<t.size();i+=(i&(-i)))t[i]+=x;}
    int sum(int i){int ans=0;for(;i>0;i-=(i&(-i)))ans+=t[i];return ans;}
    int sum(int l,int r){return sum(r)-sum(l-1);}
    NumArray(vector<int>& nums):nums(nums),t(nums.size()+1) {
        for(int i=0;i<nums.size();i++)add(i+1,nums[i]);        
    }
    void update(int index, int val) {add(index+1,val-nums[index]);nums[index]=val;}
    int sumRange(int left, int right) {return sum(left+1,right+1);}
};
```
