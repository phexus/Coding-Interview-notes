# 第四章  解决面试题的思路

## 面试题23  从上往下打印二叉树

- 广度优先遍历一个有向图，同样可以基于队列实现。树是图的一种特殊退化形式，从上到下按层遍历二叉树，从本质上说就是广度优先遍历二叉树。

## 面试题24  二叉搜索树的后序遍历序列

- 处理一棵二叉树的遍历序列，可以先找到二叉树的根结点，再基于根结点把整棵树的遍历序列拆分成左子树对应的子序列和右子树对应的子序列，接下来再递归处理这两个子序列。

## 面试题25  二叉树中和为某一值的路径

- 只有前序遍历是先访问根结点的。
- 递归调用的本质就是一个压栈和出栈的过程。

## 面试题27  二叉搜索树与双向链表

- 中序遍历算法的特点是按照从小到大的顺序比那里二叉树的每一个结点。

## 面试题28  字符串的排列

- 按照一定要求摆放若干个数字，可以先求出这些数字的所有排列，再一一判断每个排列是不是满足题目给定的要求。

- 要对递归有深刻的理解！！！