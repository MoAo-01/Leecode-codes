```cpp
//https://github.com/MoAo-01/Leecode-codes
class Solution {
public:
    int countPrimeSetBits(int left, int right) {
        unordered_set<int>primes{2,3,5,7,11,13,17,19,23,29,31};
        int ans=0;
        for(int num=left;num<=right;num++)
            ans+=primes.count(__builtin_popcount(num))>0;
        return ans;
    }
};
```
