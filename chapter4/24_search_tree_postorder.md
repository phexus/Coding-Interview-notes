# 二叉搜索树的后序遍历序列

感觉这道题清楚二叉搜索树的定义，定义好子问题递归就好了。

感觉下面的写法比书上的更加清晰，递归的几个要素：

1. 退出条件 `if (start >= end) return true;` 代表只有一个结点或为空
2. return 的两个分支，`if (j != end) return false;` `return left && right;`

另外，讲道理空树应该也算二叉搜索树的，结果空序列要返回 false，比较郁闷。

```cpp
class Solution {
public:
    bool VerifySquenceOfBST(vector<int> sequence) {
        if (sequence.empty()) return false;
        return help(sequence, 0, sequence.size() - 1);
    }
    
    bool help(vector<int> sequence, int start, int end) {
        if (start >= end) return true;
        
        int i = start;
        int root = sequence[end];
        while (sequence[i] < root) ++i;
        int j = i;
        while (sequence[j] > root) ++j;
        if (j != end) return false;
        
        bool left = help(sequence, start, i - 1);
        bool right = help(sequence, i, end - 1);
        return left && right;
    }
};
```

## 非递归

迭代的做法比较巧妙

```cpp
//链接：https://www.nowcoder.com/questionTerminal/a861533d45854474ac791d90e447bafd
//来源：牛客网

//非递归 
//非递归也是一个基于递归的思想：
//左子树一定比右子树小，因此去掉根后，数字分为left，right两部分，right部分的
//最后一个数字是右子树的根他也比左子树所有值大，因此我们可以每次只看有子树是否符合条件
//即可，即使到达了左子树左子树也可以看出由左右子树组成的树还想右子树那样处理
 
//对于左子树回到了原问题，对于右子树，左子树的所有值都比右子树的根小可以暂时把他看出右子树的左子树
//只需看看右子树的右子树是否符合要求即可
class Solution {
public:
    bool VerifySquenceOfBST(vector<int> sequence) {
        int size = sequence.size();
        if(0==size)return false;
 
        int i = 0;
        while(--size)
        {
            while(sequence[i++]<sequence[size]);
            while(sequence[i++]>sequence[size]);
 
            if(i<size)return false;
            i=0;
        }
        return true;
    }
};
```

