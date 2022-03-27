```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
```


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
