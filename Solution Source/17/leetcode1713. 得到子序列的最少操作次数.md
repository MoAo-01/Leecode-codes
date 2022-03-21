### 解题思路
- 将`target[i]`的键值映射到其下标`i`
- 遍历数组`arr`的每一个元素，`arr[i]`
- 安照`arr[i]`的值对应下标`idx`
- 插入我们维护的（下标）不下降子序列`a`
- 最后答案为：`n`-数组`a`的大小

### 复杂度
- 时间：$O(Nlog(N))$
- 空间：$O(N)$


### 代码

```cpp
class Solution {
public:
    int minOperations(vector<int> &target, vector<int> &arr) {
        int n=target.size();
        unordered_map<int,int>pos;
        for(int i=0;i<n;i++)pos[target[i]]=i;
        vector<int>a;
        for(int val:arr)
            if(pos.count(val)){
                int idx=pos[val];
                auto it=lower_bound(a.begin(),a.end(),idx);
                if(it!=a.end())*it=idx;
                else a.push_back(idx);                
            }
        return n-a.size();
    }
};
```
