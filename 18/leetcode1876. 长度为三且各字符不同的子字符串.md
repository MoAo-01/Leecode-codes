## c++
```cpp 
class Solution {
public:
    int countGoodSubstrings(string s) {
        int n = size(s), ans = 0;
        for (int i = 0; i < n - 2; ++i)
            ans += (s[i] != s[i + 1] && s[i] != s[i + 2] && s[i + 1] != s[i + 2]);
        return ans;
    }
};
```
## Java
```java
class Solution {
    public int countGoodSubstrings(String s) {
        int n = s.length();
        if(n<3) return 0;
        int res=0;
        for (int i = 0; i < n - 2; i++) {
            if(s.charAt(i)!=s.charAt(i+1)&&s.charAt(i+2)!=s.charAt(i+1)&&s.charAt(i)!=s.charAt(i+2)){
                res++;
            }
        }
        return res;
    }
}
```
## python
```python
class Solution:
    def countGoodSubstrings(self, s: str) -> int:        
        res = 0
        for i in range(0, len(s) - 2):
            if s[i] != s[i + 1] and s[i] != s[i + 2] and s[i + 1] != s[i + 2]:
                res += 1
        return res
```
## go
```go
func countGoodSubstrings(s string) int {
    n:=len(s)
    ans:=0
    for i:=0;i<n-2;i++{
        if s[i]!=s[i+1] && s[i]!=s[i+2] && s[i+1]!=s[i+2] {
            ans++
        }
    }
    return ans
}
```
