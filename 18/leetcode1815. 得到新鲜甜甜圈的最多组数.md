### 题意
>对于多波购买甜甜圈的顾客，每次一炉只能供应batchSize个甜甜圈。
>对于每个顾客，如果自己买到的批次是和其他波次的顾客"拼"的甜甜圈，则不高兴。
>对于每波顾客，当且仅当所有人都高兴，该波顾客高兴。
>问如何安排顾客的波次，使得高兴的波次最大化。

#### 模拟退火
迭代27次，起始温度50000℃，温度变化率0.97，是极限了
>随机打散原来的排列，直接计算高兴的组数作为每次的估价
>随机交换其中两波的排列，对新状态估价
>若新状态优于前者，则保留该次交换
>否则，在随机概率允许的条件下，取消本次交换

#### 记忆化搜索
先贪心，后搜索
>贪心相当于预处理，是最优化剪枝
`人数 MOD batchSize==0，直接判定happy`
>对于人数 `groups[i] MOD batchSize + groups[j] MOD batchSize == batchSize`
>直接更新答案`happy 计数器++`优化后,即:
>`happy 计数器+=`
>`min(counter[groupPerson'sNumber],counter[batchSize-groupPerson'sNumber])`

#### 多维DP
>由于batchSize最多为9
>对于每波顾客的人数取余，只有8种情况（整除直接更新答案）
>可以直接用8维的dp记录当前状态

### 三份代码
```cpp [sol-模拟退火]
class Solution {
private:
    int b, n, ans;
	vector<int> w;
	int calc() {
		int res = 0, s = 0;
		for(int i = 0;i < w.size();i++) {
			s += w[i];
			if(s % b == 0) res++, s = 0;
		}
		if(s > 0) res++;
		ans = max(ans,res);
		return res;
	}
    void simulate_anneal() {
        random_shuffle(w.begin(),w.end());
		for(double t = 5e4;t > 1e-5;t *= 0.97) {
			int i = rand() % n, j = rand() % n;
			int x = calc(); swap(w[i],w[j]); int y = calc();
            int delta = y - x;
			if(delta < 0 && (exp(delta / t) < (double) rand() / RAND_MAX)) swap(w[i],w[j]);
			//一定概率保留原来的位置不交换
		}
        return ;
    }
public:
    int maxHappyGroups(int b0, vector<int>& g) {
        b = b0;
        if(b == 1) return g.size();
        w.clear();
        int res  =  0;
        for(auto& gi : g)
            if(gi % b == 0) res++;
            else w.push_back(gi % b);
        n = w.size();
        if(n < 2) return res + n;
		ans = 0;
        for(int i = 0;i < 27;i++)simulate_anneal();
        return ans + res;
    }
};
```
```cpp [sol-记忆化搜索]
class Solution {
private:
    struct hashNode {
        size_t operator()(const vector<int>&nums) const {
            size_t hashValue=0;
            for(int num:nums)hashValue=hashValue*5+num;
            return hashValue;
        }
    }; 
    unordered_map<vector<int>,int,hashNode>hashmap;   
    int dfs(vector<int>&u,int&n) {
        if(hashmap.count(u))return hashmap[u];
        int res=0;
        for(int i=1;i<n;i++)
            if (u[i]) {
                auto v=u;
                v[i]--,v[0]=(v[0]+i)%n;
                res=max(res,(!u[0])+dfs(v,n));
            }
        return hashmap[u]=res;
    }
public:
    int maxHappyGroups(int batchSize,vector<int>& groups) {
        int ans=0;
        vector<int>counter(batchSize,0);
        for(int &group:groups)counter[group%=batchSize]++;        
        ans=counter[0],counter[0]=0;
        for(int i=1;i<=(batchSize-1)/2;i++) {
            int minValue;
            ans+=minValue=min(counter[i],counter[batchSize-i]);
            counter[batchSize-i]-=minValue;
            counter[i]-=minValue;
        }
        return ans+dfs(counter,batchSize);
    }
};
```
```cpp [sol-多维DP]
#define LOOP(x,i) for(int x=0;x<=q[i];x++)
#define dp(a,b,c,d,e,f,g,h) dp[a][b][c][d][e][f][g][h]
#define DP(a,b,i) (a)=max((a),(b)+((sum-i)%batchSize==0))

class Solution {
public:
    int maxHappyGroups(int batchSize, vector<int>& groups) {
        int *q=new int[9]{0};
        int res=0;
        for (int i=0;i<groups.size();i++)
            if(groups[i]%batchSize==0)res++;            
            else q[groups[i]%batchSize]++;
        for (int i=1;i<=(batchSize-1)/2;i++){
            int minValue;
            res+=minValue=min(q[i],q[batchSize-i]);
            q[batchSize-i]-=minValue;
            q[i]-=minValue;            
        }
        if (batchSize%2==0){
            res+=q[batchSize/2]/2;
            q[batchSize/2]-=((q[batchSize/2]/2)*2);
        }
        int dp[q[1]+1][q[2]+1][q[3]+1][q[4]+1][q[5]+1][q[6]+1][q[7]+1][q[8]+1];
        LOOP(a,1) LOOP(b,2) LOOP(c,3) LOOP(d,4)
            LOOP(e,5) LOOP(f,6) LOOP(g,7) LOOP(h,8){
                dp(a,b,c,d,e,f,g,h)=0;
                int sum=a*1+b*2+c*3+d*4+e*5+f*6+g*7+h*8;
                if (a) DP(dp(a,b,c,d,e,f,g,h),dp(a-1,b,c,d,e,f,g,h),1);
                if (b) DP(dp(a,b,c,d,e,f,g,h),dp(a,b-1,c,d,e,f,g,h),2);
                if (c) DP(dp(a,b,c,d,e,f,g,h),dp(a,b,c-1,d,e,f,g,h),3);
                if (d) DP(dp(a,b,c,d,e,f,g,h),dp(a,b,c,d-1,e,f,g,h),4);
                if (e) DP(dp(a,b,c,d,e,f,g,h),dp(a,b,c,d,e-1,f,g,h),5);
                if (f) DP(dp(a,b,c,d,e,f,g,h),dp(a,b,c,d,e,f-1,g,h),6);
                if (g) DP(dp(a,b,c,d,e,f,g,h),dp(a,b,c,d,e,f,g-1,h),7);
                if (h) DP(dp(a,b,c,d,e,f,g,h),dp(a,b,c,d,e,f,g,h-1),8);
            }
        return res+dp(q[1],q[2],q[3],q[4],q[5],q[6],q[7],q[8]);
    }
};
```
