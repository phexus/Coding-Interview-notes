# 链表中倒数第 k 个结点

边界问题要小心处理

```cpp
/*
struct ListNode {
	int val;
	struct ListNode *next;
	ListNode(int x) :
			val(x), next(NULL) {
	}
};*/
class Solution {
public:
    ListNode* FindKthToTail(ListNode* pListHead, unsigned int k) {
        if (!pListHead) return NULL;
        
        ListNode *fast = pListHead, *slow = pListHead; // 写成一行每个都得带 *
        for (int i = 0; i < k; ++i) {
            if (fast) fast = fast -> next;
            else return NULL;
        }
        while (fast) {
            fast = fast -> next;
            slow = slow -> next;
        }
        return slow;
    }
};
```

