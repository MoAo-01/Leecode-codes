### 解题思路
- STL

### 代码

```cpp
//https://github.com/MoAo-01/Leecode-codes
class Solution {
public:
    int day(string&date){
        int y,m,d;
        sscanf(date.c_str(),"%d-%d-%d",&y,&m,&d);
        tm timeInfo={0};
        timeInfo.tm_year=y-1900;
        timeInfo.tm_mon=m-1;
        timeInfo.tm_mday=d;
        return mktime(&timeInfo)/(24*60*60);
    }
    
    int daysBetweenDates(string date1, string date2) {
        return abs(day(date1)-day(date2));
    }
};
```
