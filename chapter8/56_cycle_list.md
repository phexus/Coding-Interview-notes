# 链表中环的入口结点

### 错误解答

```cpp
/*
struct ListNode {
    int val;
    struct ListNode *next;
    ListNode(int x) :
        val(x), next(NULL) {
    }
};
*/
class Solution {
public:
    ListNode* EntryNodeOfLoop(ListNode* pHead) {
        if (!pHead || !pHead -> next) return NULL;
        
        ListNode *fast = pHead, *slow = pHead;
        while (fast != slow) { // 这里错了，因为初始值就是相等的，所以最后一定返回 pHead
            fast = fast -> next -> next;
            slow = slow -> next;
        }
        
        slow = pHead;
        while (fast != slow) {
            fast = fast -> next;
            slow = slow -> next;
        }
        return fast;
    }
};
```

### 正确解答

```cpp
/*
struct ListNode {
    int val;
    struct ListNode *next;
    ListNode(int x) :
        val(x), next(NULL) {
    }
};
*/
class Solution {
public:
    ListNode* EntryNodeOfLoop(ListNode* pHead) {
        if (!pHead || !pHead -> next) return NULL;
        
        ListNode *fast = pHead, *slow = pHead;
        while (fast && fast -> next) {
            slow = slow -> next;
            fast = fast -> next -> next;
            if (slow == fast) {
                fast = pHead;
                while (slow != fast) {
                    slow = slow -> next;
                    fast = fast -> next;
                }
                return slow;
            }
        }
        return NULL;
    }
};
```

