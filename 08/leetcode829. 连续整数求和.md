### 题目简化
[剑指 Offer 57 - II. 和为s的连续正数序列](https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/solution/mo-ao-gao-si-qiu-he-gong-shi-bao-li-po-j-ac1t/)

### 解题思路
令 $s=sum([a,a+k-1])=a+(a+1)+(a+2)+...+(a+k-1)$

$\qquad\therefore s=\frac{(a+a+k-1)\times k}{2}=ak+\frac{(k-1)k}{2}$ 

$\quad$ 枚举区间长度 $k$

$\quad$ 若 $\exist$ 一个正整数解 $a$ 则对应一种构造方式

$\qquad\therefore ak=s-\frac{(k-1)k}{2}\ \exist a\in Z^{+}$

$\qquad\iff a\equiv s-\frac{(k-1)k}{2}\ (mod\ k)$

此时，带入题目条件：

$\qquad s=n$ 只需要循环枚举 $k$ 对表达式 `(n-(k-1)*k/2)%k==0` 求累和即可

分析上下界，最短区间对应 $k=1$, 理论上 $k$ 的数量级可以打到 $\sqrt{2n}$

$\qquad\therefore$ 循环枚举的上下界条件分别为 `k=1` 和 `k*k<=2n`

### 复杂度分析
- 时间复杂度: $O(\sqrt{2n})$
- 空间复杂度: $O(1)$


### 代码如下

```cpp
class Solution {
public:
    int consecutiveNumbersSum(int n) {
        int ans=0;
        for(int k=1;k*k<=2*n;k++)
            ans+=(n-(k-1)*k/2)%k==0;
        return ans;
    }
};
```
