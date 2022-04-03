```cpp
//https://github.com/MoAo-01/Leecode-codes
class Solution {
public:
    char nextGreatestLetter(vector<char>& letters, char target) {
        auto x=upper_bound(begin(letters),end(letters),target);
        return (x!=end(letters))?(*x):letters[0];
    }
};
```
