## 集合运算：对称差

```cpp
class Solution {
public:
    bool closeStrings(string word1, string word2) {
        int n=word1.size();
        vector<int>cnt1(256,0),cnt2(256,0);
        //统计字频
        for(auto&c:word1)cnt1[c]++;
        for(auto&c:word2)cnt2[c]++;
        set<int>set1,set2;
        //将出现过的字符存入两个集合
        for(int i=0;i<256;i++){
            if(cnt1[i])set1.insert(i);
            if(cnt2[i])set2.insert(i);
        }
        //求两个集合的对称差
        vector<int>SSD;
        set_symmetric_difference(set1.begin(),set1.end(),set2.begin(),set2.end(),back_inserter(SSD));
        //对称差非空，不可互化
        if(SSD.size()>0)return false;
        //if( set{c in word1} == set{c in word2} ) 
        //排序<=>进行迭代交换
        sort(cnt1.begin(),cnt1.end());
        sort(cnt2.begin(),cnt2.end());
        //判等
        for(int i=0;i<256;i++)if(cnt1[i]!=cnt2[i])return false;
        return true;
    }
};
```
