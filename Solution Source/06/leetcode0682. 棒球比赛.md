### 解题思路
- 模拟

### 代码

```cpp
//https://github.com/MoAo-01/Leecode-codes
class Solution {
public:
    int calPoints(vector<string>& ops) {
        vector<int>mark;
        for(auto&op:ops){
            if(op=="+")mark.push_back(mark[mark.size()-1]+mark[mark.size()-2]);
            else if(op=="D")mark.push_back(mark[mark.size()-1]*2);
            else if(op=="C")mark.pop_back();
            else mark.push_back(atoi(op.c_str()));
        }
        return accumulate(begin(mark),end(mark),0);
    }
};
```
