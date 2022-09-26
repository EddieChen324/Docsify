给你单链表的头节点 `head` ，请你反转链表，并返回反转后的链表。



**这一题可以指定两个指针，一个指向当前节点，一个指向当前节点的前节点**

*通过调换它们的顺序来实现一一翻转。*



```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* cur = head;
        ListNode* pre = NULL;
        //想清楚什么时候反转结束
        while(cur) {
            ListNode* tmp = cur->next;
            cur->next = pre;
            pre = cur;
            cur = tmp;
        }
        return pre;
    }
};
```

