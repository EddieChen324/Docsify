给你一个链表，删除链表的倒数第 n 个结点，并且返回链表的头结点。

进阶：你能尝试使用一趟扫描实现吗？

![20210510085957392](20210510085957392.png)

> 输入：head = [1,2,3,4,5], n = 2 
>
> 输出：[1,2,3,5] 
>
> 示例 2：
>
> 输入：head = [1], n = 1 输出：[] 
>
> 示例 3：
>
> 输入：head = [1,2], n = 1 输出：[1]

**这题需要定义快慢指针，快指针先走n次，再快慢指针同时走，慢指针即指向要删除节点的前置节点。**



```cpp
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* DummyHead = new ListNode(0);
        DummyHead->next = head;
        ListNode* fast = DummyHead;
        while (n--) {
            fast = fast->next;
        }
        ListNode* slow = DummyHead;
        while (fast->next) {
            fast = fast->next;
            slow = slow->next;
        }
        ListNode* tmp = slow->next;
        slow->next = slow->next->next;
        delete tmp;
        return DummyHead->next;
    }
};
```

