# 数组中的逆序对

这里没有采用书上的做法，书上的做法不需要最后把临时数组的数据填入原数组，递归调用的时候要颠倒 data 和 tmp ，`help(tmp, data， start1, end1)`

```cpp
class Solution {
public:
    int InversePairs(vector<int>& data) {
        if (data.empty()) return 0;
        vector<int> tmp = vector<int> (data.size());
        return help(data, tmp, 0, data.size() - 1);
    }
    
    int help(vector<int>& data, vector<int>& tmp, int start, int end) {
        if (start >= end) return 0;
        
        int mid = start + (end - start) / 2;
        int start1 = start, end1 = mid;
        int start2 = mid + 1, end2 = end;
        int left = help(data, tmp, start1, end1) % 1000000007;
        int right = help(data, tmp, start2, end2) % 1000000007;
        
        int count = 0;
        int k = end;
        while (end1 >= start1 && end2 >= start2) {
            if (data[end1] > data[end2]) {
                tmp[k--] = data[end1--];
                count += end2 - start2 + 1;
                if (count > 1000000007) count %= 1000000007;
            } else {
                tmp[k--] = data[end2--];
            }
        }
        while (end1 >= start1) tmp[k--] = data[end1--];
        while (end2 >= start2) tmp[k--] = data[end2--];
        
        for (k = start; k <= end; ++k) data[k] = tmp[k];
        return (count + left + right) % 1000000007;
    }
};
```

