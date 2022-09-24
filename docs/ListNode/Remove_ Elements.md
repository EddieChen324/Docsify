给你一个链表的头节点 `head` 和一个整数 `val` ，请你删除链表中所有满足 `Node.val == val` 的节点，并返回 **新的头节点** 。

示例

```
输入：head = [1,2,6,3,4,5,6], val = 6
输出：[1,2,3,4,5]
```





**既然要删除链表中具有指定数据域的节点，我们就要首先找到该节点的前一个节点。**



>  遍历链表时，需要确定条件究竟是while(cur) 还是 while(cur->next) ?
>
> 通过模拟可以知道，如果指定的是while(cur)，访问到最后一个节点时，cur->next由于是空节点，所以无法取它的数据域，因此这里会报错。所以要用while(cur->next)。



```C++
class Solution{
public:
    ListNode* removeElements(ListNode* head, int val) {
    //虚拟头节点
    ListNode* DummyHead = new ListNode(0);
    ListNode* cur = DummyHead;
    while (cur->next) {
        if (cur->next->val == val) {
            ListNode* tmp = cur->next;
            cur->next = cur->next->next;
            delete tmp;
        }
        else {
            cur = cur->next;
        }
    }
    return DummyHead->next;
}
};
```

