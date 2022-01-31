```cpp
class Solution {
public:
    bool isPalindrome(int x) {
        string s=to_string(x),rs=s;
        reverse(rs.begin(),rs.end());
        return s==rs;
    }
};
```

```cpp
class Solution {
public:
    bool isPalindrome(int x) {
        if(x<0)return false;
        stringstream ss;ss<<x;
        char s[15]={0};
        int len=ss.str().length(); 
        strcpy(s,ss.str().c_str());
        for(int i=0;i<len/2;i++)if(s[i]!=s[len-i-1])return false;
        return true;
    }
};
```
