```cpp
class Solution {
public:
    string maximumTime(string time) {
        string ans="??:??";
        for(int h=0;h<24;h++)
            for(int m=0;m<60;m++){
                string s=(h>9?to_string(h):"0"+to_string(h))+":";
                s+=m>9?to_string(m):"0"+to_string(m);
                bool flag=true;
                for(int i=0;i<s.size();i++)
                    if(time[i]!='?'&&s[i]!=time[i]){
                        flag=false;break;
                    }
                if(flag)ans=s;
            }
        return ans;
    }
};
```
