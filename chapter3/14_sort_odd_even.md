# 调整数组顺序使奇数位于偶数前面

## Solution 1

这道题还真是坑，clion 和 nowcoder 在执行`if ((array[i] & 0x1) == 0)` 这句话的时候都会优先做 ==，但是我查了运算符优先级，命名是 & 的优先级更高啊。。想不明白。。后来知乎上 https://www.zhihu.com/question/20815930 有提到不要滥用 C 语言的运算符优先级，位运算（bitwise operator）一定要条件反射般加上括号！！！

```cpp
class Solution {
public:
    void reOrderArray(vector<int> &array) {
        vector<int> newVec;
        for (int i = 0; i < array.size(); ++i) {
            if ((array[i] & 0x1) == 1) newVec.push_back(array[i]);
        }
        for (int i = 0; i < array.size(); ++i) {
            if ((array[i] & 0x1) == 0) newVec.push_back(array[i]);
        }
        array = newVec;
    }
};
```

## Solution 2

由于这里的题和书本上要求不一样，多了不允许改变相对顺序，所以书上的做法自然就废了，上面的做法是用空间换时间，时间复杂度和空间复杂度都做到了 $$O(n)$$

下面用插入排序来做：



## Solution 3

