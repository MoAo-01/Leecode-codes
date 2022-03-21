### 解题思路
- 都在注释里了

### 代码

```cpp
/*
[ ]+, ( )+:  表示方/圆括号里的模式出现 1次 或 多次
[ ]*, ( )*:  表示方/圆括号里的模式出现 0次 或 多次
[ ]?, ( )?:  表示方/圆括号里的模式出现 0次 或 1次
*/

class Solution {
private:
    regex r=regex("[a-z]*([a-z]-[a-z])?[a-z]*[!.,]?");
    string word;
public:
    int countValidWords(string sentence) {        
        int res=0;        
        for(istringstream iss(sentence);iss>>word;)res+=regex_match(word,r);
        return res;
    }
};
```
