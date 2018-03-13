# 两个链表的第一个公共结点

## Solution 1

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
    ListNode* FindFirstCommonNode(ListNode* pHead1, ListNode* pHead2) {
        if (!pHead1 || !pHead2) return NULL;
        int len1 = getListLen(pHead1);
        int len2 = getListLen(pHead2);
        
        ListNode* p1 = pHead1;
        ListNode* p2 = pHead2;
        if (len1 < len2) {
            swap(p1, p2);
            swap(len1, len2); // 注意，这里 len1，len2 也要交换！！！
        }
        
        for (int i = 0; i < len1 - len2; ++i) p1 = p1 -> next;
        
        while (p1 && p2 && p1 != p2) {
            p1 = p1 -> next;
            p2 = p2 -> next;
        }
        
        return p1; // 即使不存在，此时 p1 也为 NULL
    }
    
    int getListLen(ListNode* head) {
        int ans = 0;
        while (head) {
            ++ans;
            head = head -> next;
        }
        return ans;
    }
};
```

