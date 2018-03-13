# 二叉树的镜像

## Solution 1 - 递归

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
    void Mirror(TreeNode *pRoot) {
        if (!pRoot) return;
        
        swap((pRoot -> left), (pRoot -> right));
        Mirror(pRoot -> left);
        Mirror(pRoot -> right);
    }
};
```

## Solution 2 - 迭代

本质上还是交换 curr -> left 和 curr -> right，left 和 right 的先后入栈顺序为所谓。所以实际上用 队列都可以

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
    void Mirror(TreeNode *pRoot) {
        if (!pRoot) return;
        
        stack<TreeNode*> st;
        st.push(pRoot);
        
        while (!st.empty()) {
            TreeNode* curr = st.top();
            st.pop();
            swap(curr -> left, curr -> right);
            if (curr -> left) st.push(curr -> left); // 这里先后顺序无所谓
            if (curr -> right) st.push(curr -> right);
        }
    }
};
```

### 用队列

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
    void Mirror(TreeNode *pRoot) {
        if (!pRoot) return;
        
        queue<TreeNode*> q;
        q.push(pRoot);
        
        while (!q.empty()) {
            TreeNode* curr = q.front();
            q.pop();
            swap(curr -> left, curr -> right);
            if (curr -> left) q.push(curr -> left);
            if (curr -> right) q.push(curr -> right);
        }
    }
};
```



