```cpp
//https://github.com/MoAo-01/Leecode-codes
class Solution {
public:
    vector<int> selfDividingNumbers(int left, int right) {
        auto isSelfDividingNumber=[](int num){
            string s=to_string(num);
            for(auto&c:s)
                if((c=='0')||num%(c-'0')!=0)return false;
            return true;
        };
        vector<int>ans;
        for(int i=left;i<=right;i++)if(isSelfDividingNumber(i))ans.push_back(i);
        return ans;
    }
};
```
