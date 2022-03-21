### 解题思路
- 同样的，不想写搜索
- 于是考虑位运算转字符串分段
- 二进制枚举字符串的划分

### 代码

```cpp
//https://github.com/MoAo-01/Leecode-codes
class Solution {
public:
    bool check(string&s,vector<string>&p){
        unordered_map<char,string>c2s;
        unordered_map<string,char>s2c;
        for(int i=0;i<s.size();i++){
            if(s2c.count(p[i])>0&&s2c[p[i]]!=s[i])return false;            
            if(c2s.count(s[i])>0&&c2s[s[i]]!=p[i])return false;
            s2c[p[i]]=s[i];
            c2s[s[i]]=p[i];            
        }
        return true;
    }

    vector<string> getStrings(int&mask,int&m,string&s){
        vector<int>id;
        id.push_back(0);
        for(int i=0;i<m;i++)if(mask&(1<<i))id.push_back(i);
        id.push_back(m);
        //其实可以优化掉id的存储，直接构造字符串，算了
        vector<string>ans;
        ans.push_back(s.substr(id[0],id[1]-id[0]+1));
        for(int i=1;i<id.size()-1;i++)
            ans.push_back(s.substr(id[i]+1,id[i+1]-(id[i]+1)+1));
        return ans;
    }

    bool wordPatternMatch(string pattern, string s) {
        int n=pattern.size()-1,m=s.size()-1;
        if(pattern.size()==1)return true;
        for(int mask=1;mask<(1<<m);mask++){            
            if(__builtin_popcount(mask)==n){
                auto splits=getStrings(mask,m,s);
                if(check(pattern,splits))return true;
            }
        }
        return false;
    }
};
```
