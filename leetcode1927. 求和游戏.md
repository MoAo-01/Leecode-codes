### 写在前面
- 预处理很快有了思路, 求答案不会，一直`WA`
- 你敢信比赛我`60/61`? 细节决定成败
- 人外有人，天外有天，菜鸡在中间
### 思路
- `sum` = 对左边数字加，对右边数字减
- `cnt` = 对左边问号加，对右边问号减
- 效果：左右相消，等价于两个人都足够聪明，所以达到了平衡抵消

对于无法消掉的`sum`, `cnt`
考虑，贪心策略：
`Alice`无非考虑两种情况：
1. 往大了整，全部填`9`
2. 往小了整，全部填`0`
如果能赢，就必胜

否则：

>考虑转移，`Bob`一定会使用凑`9`法
>
>`(0,9),(1,8),(2,7),(3,6),(4,5)`
>
>`(5,4),(6,3),(7,2),(8,1),(9,0)`


### 代码
```cpp [1-大神版]
class Solution {
public:
    bool sumGame(string num) {
        int n = num.size();
        int p = 0, s = 0, sum = 0;
        for (int i = 0; i < n / 2; i += 1) {
            if (num[i] == '?') p += 1;
            else sum += num[i] - '0';
        }
        for (int i = n / 2; i < n; i += 1) {
            if (num[i] == '?') s += 1;
            else sum -= num[i] - '0';
        }
        if ((p + s) & 1) return true;
        return sum != (s - p) / 2 * 9;
    }
};
```
```cpp [1-菜鸡版]
class Solution {
public:
    bool sumGame(string num) {
        int cnt=0;
        int sum=0;
        int n=num.size();
        for(int i=0;i<n;i++){
            if(i<n/2){
                if(num[i]=='?')cnt++;
                else sum+=(int)(num[i]-'0');
            }
            else{
                if(num[i]=='?')cnt--;
                else sum-=(int)(num[i]-'0');
            }
        }
        sum=abs(sum);
        cnt=abs(cnt);
        if(cnt==1)return true;
        if((cnt-((cnt+1)/2))*9<sum)return true;
        if(cnt*9<sum)return true;
        return (cnt+1)/2*9>sum;
    }
};
```
```cpp [1-整理版]
class Solution {
public:
    bool sumGame(string num) {
        int cnt=0,sum=0,n=num.size();
        for(int i=0;i<n;i++)
            if(num[i]=='?')cnt+=((i<n/2)?1:-1);
            else sum+=((int)(num[i]-'0'))*((i<n/2)?1:-1);        
        sum=abs(sum),cnt=abs(cnt);
        if((cnt-((cnt+1)/2))*9<sum||cnt*9<sum)return true;
        return (cnt+1)/2*9>sum;
    }
};
```
