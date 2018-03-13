# 和为 s 的连续正数序列

书本上的 while 嵌套 while，感觉比较 ugly，下面的解法就一个 while 配合 if else 做判断，更加清晰

```cpp
class Solution {
public:
    vector<vector<int> > FindContinuousSequence(int sum) {
        if (sum < 3) return vector<vector<int>> ();
        
        int start = 1, end = 2, middle = (1 + sum) / 2;
        int curr = 3;
        vector<vector<int>> ans;
        while (start < end && end <= middle) {
            if (curr == sum) addSequence(start, end, ans);
            
            if (curr < sum) {
                ++end;
                curr += end;
            } else {
                curr -= start;
                ++start;
            }
        }
        return ans;
    }
    
    void addSequence(int start, int end, vector<vector<int>>& ans) {
        vector<int> curr;
        for (int i = start; i <= end; ++i) {
            curr.push_back(i);
        }
        ans.push_back(curr);
    }
};
```

