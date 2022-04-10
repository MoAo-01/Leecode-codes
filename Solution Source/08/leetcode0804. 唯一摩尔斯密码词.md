### 解题思路
- 模拟

### 代码

```cpp
//https://github.com/MoAo-01/Leecode-codes
class Solution {
public:
    int uniqueMorseRepresentations(vector<string>& words) {
        vector<string> morse={".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."};
        unordered_set<string>set;
        for(auto&word:words){
            string code;
            for(auto&c:word)code+=morse[c-'a'];
            set.insert(code);
        }
        return set.size();
    }
};
```
