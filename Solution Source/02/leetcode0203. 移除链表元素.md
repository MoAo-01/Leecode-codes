```cpp
//https://github.com/MoAo-01/Leecode-codes
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        if(head==nullptr)return nullptr;
        if(head->val==val)return removeElements(head->next,val);
        else return new ListNode(head->val,removeElements(head->next,val));
    }
};
```


```cpp
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        auto dummyHead=new ListNode(0,head);        
        for(auto node=dummyHead;node->next;)
            if(node->next->val==val) node->next=node->next->next;
            else node=node->next;
        return dummyHead->next;
    }
};
```
