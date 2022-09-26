设计链表的实现。您可以选择使用单链表或双链表。单链表中的节点应该具有两个属性：val 和 next。val 是当前节点的值，next 是指向下一个节点的指针/引用。如果要使用双向链表，则还需要一个属性 prev 以指示链表中的上一个节点。假设链表中的所有节点都是 0-index 的。

在链表类中实现这些功能：

get(index)：获取链表中第 index 个节点的值。如果索引无效，则返回-1。
addAtHead(val)：在链表的第一个元素之前添加一个值为 val 的节点。插入后，新节点将成为链表的第一个节点。
addAtTail(val)：将值为 val 的节点追加到链表的最后一个元素。
addAtIndex(index,val)：在链表中的第 index 个节点之前添加值为 val  的节点。如果 index 等于链表的长度，则该节点将附加到链表的末尾。如果 index 大于链表长度，则不会插入节点。如果index小于0，则在头部插入节点。
deleteAtIndex(index)：如果索引 index 有效，则删除链表中的第 index 个节点。





*这一题有以下几点需要注意*

> * 我们需要自己设计单链表的结构，因此要熟悉单链表的构造方法
> * 第四个函数和第五个函数看似类似，但是判断条件有轻微差别，其原因是addAtIndex这个函数允许index等于链表长度（**但是index其实是从0开始的，这其实算一种越界操作**），而deleteAtIndex则要求Index有效，所以两者需要加以区分。



```cpp
class Solution{
    public:
    	struct ListNode {
            int val;
            ListNode* next;
            ListNode(int val): val(val), next(nullptr) {}
        };
    	MyLinkedList {
            //初始化链表 因为DummyHead为虚拟头节点所以size为0
            _size = 0;
            DummyHead = nwe ListNode(0);
        }
    
    	int get(int index) {
            if (index < 0 || index > _size - 1) return -1;
            ListNode* cur = DummyHead;
            while(index--) {
                cur = cur->next;
            }
            return cur->next->val;
        }
    
    	void addAtHead(int val) {
            ListNode* node = new ListNode(val);
            node->next = DummyHead->next;
            DummyHead->next = node;
            _size++;
        }
    
    	void addAtTail(int val) {
            ListNode* node = new ListNode(val);
            ListNode* cur = DummyHead;
            while (cur->next) {
                cur = cur->next;
            }
            cur->next = node;
            _size++;
        }
    
    	void addAtIndex(int index, int val) {
            if (index < 0 || index > _size) return;
            ListNode* node = new ListNode(val);
            ListNode* cur = DummyHead;
            while(index--) {
                cur = cur->next;
            }
            node->next = cur->next;
            cur->next = node;
            _size++;
        }
    
    	void deleteAtIndex(int index) {
            if (index < 0 || index > _size - 1) return;
            ListNode* cur = DummyHead;
            while(index--) {
                cur = cur->next;
            }
            ListNode* tmp = cur->next;
            cur->next = cur->next->next;
            delete tmp;
            _Size--;
        }
    private:
    	int _size;
    	ListNode* DummyHead;
}
```



**从此题我们可以感受到，当你需要删除或者添加某个节点时，需要找到该节点应在位置的前一个节点。**