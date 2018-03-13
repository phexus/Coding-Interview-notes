# 二叉搜索树与双向链表

## Solution 1 - 递归

本质上讲就是中序遍历。开头的 `if (!pRootOfTree) return NULL;` 一定要处理，否则 ` while (head -> left)` 就会报空指针，所以不要偷懒，该处理的总得处理，不要总想着跟后面的代码合并后就不用处理了。

```cpp
/*
struct TreeNode {
	int val;
	struct TreeNode *left;
	struct TreeNode *right;
	TreeNode(int x) :
			val(x), left(NULL), right(NULL) {
	}
};*/
class Solution {
public:
    TreeNode* Convert(TreeNode* pRootOfTree) {
        if (!pRootOfTree) return NULL;
        
        TreeNode* pre = NULL;
        help(pRootOfTree, pre);
        
        TreeNode* head = pRootOfTree;
        while (head -> left) head = head -> left;
        return head;
    }
    
    void help(TreeNode* curr, TreeNode*& pre) {
        if (!curr) return;
        
        if (curr -> left) help(curr -> left, pre);
        
        curr -> left = pre;
        if (pre) pre -> right = curr;
        pre = curr;
        
        if (curr -> right) help(curr -> right, pre);
        
    }
};
```

## Solution 2 - 迭代

其实也就是中序遍历的迭代写法，之后补充。。。