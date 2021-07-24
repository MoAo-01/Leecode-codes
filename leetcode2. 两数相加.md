## 模拟进位
```cpp
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        var dummy=new ListNode(-1);
        var cur=dummy;
        for(int c=0;l1!=null||l2!=null||c!=0;c/=10){
            if(l1!=null){c+=l1.val;l1=l1.next;}
            if(l2!=null){c+=l2.val;l2=l2.next;}
            cur=cur.next=new ListNode(c%10);
        }
        return dummy.next;
    }
}
```
