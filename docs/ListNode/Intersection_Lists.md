给你两个单链表的头节点 headA 和 headB ，请你找出并返回两个单链表相交的起始节点。如果两个链表没有交点，返回 null 。

图示两个链表在节点 c1开始相交：![20211219221657](20211219221657.png) 

**这一题首先求出两个链表的长度，若B比A长则交换位置，然后将指针对齐到同一位置后开始移动，若相等则相交。**

```cpp
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode* curA = headA;
        ListNode* curB = headB;
        int lengthA = 0;
        int lengthB = 0;
        while (curA) {
            curA = curA->next;
            lengthA++;
        }
        while (curB) {
            curB = curB->next;
            lengthB++;
        }
        if (lengthA < lengthB) {
            swap(lengthA, lengthB);
            swap(headA, headB);
        }
        curA = headA;
        curB = headB;
        int subLength = lengthA - lengthB;
        while (subLength--) {
            curA = curA->next;
        }
        while (curA && curB) {
            if (curA == curB) {
                return curA;
            }
            curA = curA->next;
            curB = curB->next;
        }
        return NULL;
    }
};
```

