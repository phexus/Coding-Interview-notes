# 栈的压入、弹出序列

题目限制了所有数字均不相等，降低了难度，只要按着顺序模拟入栈出栈就好了。

一开始做的时候，觉得这道题的难点在于循环的控制条件，后面想想其实只要想清楚只有当 `i == len && j == len && st.empty()` 成立的时候，才返回 true。这里外层 loop 的条件是 `i < len` ，因为一旦 i == len 的时候，一定会进入这个循环 `while (j < len && (!st.empty() && st.top() == popV[j]))` ，也就能判断返回 true 的情况了。

```cpp
class Solution {
public:
    bool IsPopOrder(vector<int> pushV,vector<int> popV) {
        if (pushV.empty() || popV.empty()) return false;
        
        stack<int> st;
        int i = 0, j = 0, len = pushV.size();
        while (i < len) {
            while (i < len && (st.empty() || st.top() != popV[j])) st.push(pushV[i++]);
            
            while (j < len && (!st.empty() && st.top() == popV[j])) {
                st.pop();
                ++j;
            }
            
            if (i == len && j == len && st.empty()) return true;
        }
        return false;
    }
};
```

如果要把外层 loop 改为 j < len 的话（书上的解法），就得 break 了，否则会死循环，感觉不如上面的写法更加直观。

```cpp
class Solution {
public:
    bool IsPopOrder(vector<int> pushV,vector<int> popV) {
        if (pushV.empty() || popV.empty()) return false;
        
        stack<int> st;
        int i = 0, j = 0, len = pushV.size();
        while (j < len) {
            while (i < len && (st.empty() || st.top() != popV[j])) st.push(pushV[i++]);
            
            if (st.top() != popV[j]) break;
            
            while (j < len && (!st.empty() && st.top() == popV[j])) {
                st.pop();
                ++j;
            }
            
            if (i == len && j == len && st.empty()) return true;
        }
        return false;
    }
};
```

