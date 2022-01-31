### 解题思路
压行

### 代码

```cpp
class Solution {
public:
    int romanToInt(string s) {
        int m['Z'],res=0;m['I']=1,m['V']=5,m['X']=10,m['L']=50,m['C']=100,m['D']=500,m['M']=1000;
        for(int n=s.size(),i=n-1;i>=0;i--)res+=(i!=n-1 && m[s[i+1]]>m[s[i]])?-m[s[i]]:m[s[i]];
        return res;
    }
};
```
