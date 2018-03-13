# 从尾到头打印链表

## 解法1 - 递归

```cpp
/**
*  struct ListNode {
*        int val;
*        struct ListNode *next;
*        ListNode(int x) :
*              val(x), next(NULL) {
*        }
*  };
*/
class Solution {
public:
    vector<int> printListFromTailToHead(ListNode* head) {
        if (head == NULL) return vector<int> ();
        vector<int> ans;
        help(head, ans);
        return ans;
    }
    
    void help(ListNode* node, vector<int>& ans) {
        if (!node) return;
        help(node -> next, ans);
        ans.push_back(node -> val);
    }
};
```

也可以不加辅助函数，但感觉下面这样写，还是不太好，每次返回值都是一个临时数组，再赋值给 ans，花销有点大，虽然可以改变函数返回值为 `vector<int>& printListFromTailToHead(ListNode* head)` 但还是不推荐，上面的解法可读性更高点。

```cpp
/**
*  struct ListNode {
*        int val;
*        struct ListNode *next;
*        ListNode(int x) :
*              val(x), next(NULL) {
*        }
*  };
*/
class Solution {
public:
    vector<int> ans;
    vector<int> printListFromTailToHead(ListNode* head) {
        if (head) {
            ans = printListFromTailToHead(head -> next);
            ans.push_back(head -> val);
        }
        return ans;
    }
};
```

> 看到有些答案使用的是 vector 的 insert 方法，殊不知，这样 insert 的复杂度是 $$O(n)$$ 感觉复杂度都赶上 $$O(n^2)$$ 了，与其要用 insert 还不如最后 reverse，复杂度能控制在 $$O(n)$$ 

## 解法2 - 栈

```cpp
/**
*  struct ListNode {
*        int val;
*        struct ListNode *next;
*        ListNode(int x) :
*              val(x), next(NULL) {
*        }
*  };
*/
class Solution {
public:
    vector<int> printListFromTailToHead(ListNode* head) {
        stack<int> nodes;
        while (head) {
            nodes.push(head -> val);
            head = head -> next;
        }
        
        vector<int> ans;
        while (!nodes.empty()) {
            ans.push_back(nodes.top());
            nodes.pop();
        }
        return ans;
    }
};
```

