### 解题思路
- 统计词频为 `1` 的单词

### 代码

```python3 [1-Python3]
class Solution:
    def uncommonFromSentences(self, s1: str, s2: str) -> List[str]:
        dic=Counter(s1.split())+Counter(s2.split())        
        return [k for k,v in dic.items() if v==1]
```
```cpp [1-C++]
class Solution {
public:
    vector<string> uncommonFromSentences(string s1, string s2) {
        unordered_map<string,int>dict;
        stringstream s(s1+" "+s2);
        vector<string>ans;
        for(string word;s>>word;)dict[word]++;        
        for(auto&[k,v]:dict)if(v==1)ans.push_back(k);
        return ans;
    }
};
```
```java [1-龟速JAVA]
class Solution {
    public String[] uncommonFromSentences(String s1, String s2) {
        String s=s1+" "+s2;
        String[] words=s.split(" ");
        List<String> ans = new ArrayList<>();
        HashMap<String,Integer>dict=new HashMap<>();
        for(String word:words)dict.put(word, dict.getOrDefault(word, 0) + 1);
        for(Map.Entry<String,Integer>entry:dict.entrySet())if(entry.getValue()==1)ans.add(entry.getKey());
        return ans.toArray(new String[ans.size()]);
    }
}
```

```java [1-快速JAVA]
class Solution {
    public String[] uncommonFromSentences(String A, String B) {
        Map<String, Integer> count = new HashMap();
        for (String word: A.split(" "))
            count.put(word, count.getOrDefault(word, 0) + 1);
        for (String word: B.split(" "))
            count.put(word, count.getOrDefault(word, 0) + 1);

        List<String> ans = new ArrayList<>();
        
        for (String word: count.keySet()){
            if (count.get(word) == 1)
                ans.add(word);
        }
        return ans.toArray(new String[ans.size()]);
    }
}
```

## 后记
我真是个懒虫，讲道理，写这么多代码，其实应该打个包上传Git的
在此立个flag吧，寒假放完，把代码搬上Git，🤣🤣🤣
## GitHub
[https://github.com/MoAo-01](https://github.com/MoAo-01)
