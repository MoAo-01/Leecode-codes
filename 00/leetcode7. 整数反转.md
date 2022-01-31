```cpp
class Solution {
public:
    int reverse(int x) {
        long long f=(x>0)?1:-1,res=0,a[20]={0},cnt=0;
        for(x=abs(x);x;x/=10)a[++cnt]=x%10;
        for(int i=1;i<=cnt;i++)res=res*10+a[i];
        return res*f>2147483647||res*f<-2147483648?0:res*f;
    }
};
```
