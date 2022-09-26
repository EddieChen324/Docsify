给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。

你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

![24.两两交换链表中的节点-题意](24.%E4%B8%A4%E4%B8%A4%E4%BA%A4%E6%8D%A2%E9%93%BE%E8%A1%A8%E4%B8%AD%E7%9A%84%E8%8A%82%E7%82%B9-%E9%A2%98%E6%84%8F.jpg)



**首先见到链表类的题目，第一步考虑是否有必要添加虚拟头节点。**

因为涉及链表的交换，采用虚拟头节点会方便很多，因此采用。

**第二个要思考的，是当我们两两交换节点时，究竟涉及对哪些节点进行操作呢？**

思考后可以得知，看似是两两交换，实际上每次涉及四个节点的改变

>* 两个节点的前置节点（因为交换了节点，所以前置节点应指向第二个节点）
>* 两个要交换的节点的改变。
>* 两个节点的后置节点（因为交换了节点，所以应由第一个节点来指向后置节点）

想清楚这些后，本题也就迎刃而解了。



```cpp
class Solution{
    public:
    	ListNode* swapPairs(ListNode* head) {
            //首先定义虚拟头节点
            ListNode* DummyHead = new ListNode(0);
            DummyHead->next = head;
            ListNode* cur = DummyHead;
            //想清楚while循环的判断逻辑应该是什么？
            //因为每次移动两个节点，所以应该写成如下格式
            while (cur->next && cur->next->next) {
                //注意提前保存第一个节点和后置节点的位置
                ListNode* tmp1 = cur->next;
                ListNode* tmp2 = cur->next->next->next;
                cur->next = cur->next->next;
                cur->next->next = tmp1;
                cur->next->next->next = tmp2;
                
                cur = cur->next->next;
            }
            return DummyHead->next;
        }
};
```

