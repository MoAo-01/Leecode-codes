### 解题思路
- pair + 排序

### 代码

```cpp
https://github.com/MoAo-01/Leecode-codes
class Solution {
public:
    string sortSentence(string s) {
        stringstream ss(s);        
        vector<pair<char,string>>words;
        for(string word;ss>>word;)
            words.emplace_back(word.back(),word.substr(0,word.size()-1));
        sort(begin(words),end(words));
        string sentence;
        for(auto&word:words)
            sentence+=word.second+" ";
        if(sentence.size()>0)sentence.pop_back();
        return sentence;
    }
};
```
