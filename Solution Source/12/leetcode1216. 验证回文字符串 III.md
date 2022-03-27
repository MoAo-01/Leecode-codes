- 区间DP

```cpp
//https://github.com/MoAo-01/Leecode-codes
class Solution {
public:
    bool isValidPalindrome(string s, int k) {
        int n=s.size();
        auto f=vector<vector<int>>(n,vector<int>(n,0));
        for(int len=1;len<=n;len++){
            for(int l=0;l+len-1<n;l++){
                int r=l+len-1;
                if(l==r)f[l][r]=1;
                else{
                    if(s[l]==s[r]) f[l][r]=f[l+1][r-1]+2;
                    f[l][r]=max({f[l][r],f[l+1][r],f[l][r-1]});
                }
            }
        }
        return n-k<=f[0][n-1];
    }
};
```
