### 解题思路
- 直接找-直接翻转

### 代码

```cpp
class Solution {
public:
    string reversePrefix(string word, char ch) {
        auto i=word.find(ch);
        return(i==-1)?word:(reverse(begin(word),begin(word)+i+1),word);
    }
};
```

### 或者手写
```cpp
class Solution {
public:
    string reversePrefix(string word, char ch) {
        int i=0,j=0;
        while(word[j]!=ch && j<word.size())j++;
        if(j>=word.size())return word;
        while(i<=j)swap(word[i++],word[j--]);
        return word;
    }
};
```
