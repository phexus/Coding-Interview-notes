# 数字在排序数组中出现的次数

本题和 leetcode 的 search for a range 有点像，都是 求 lower bound 返回 start（或 end + 1），求 upper bound 返回 end （或 start - 1）

```cpp
class Solution {
public:
    int GetNumberOfK(vector<int> data ,int k) {
        if (data.empty()) return 0;
        int len = data.size();
        int start = 0, end = len - 1;
        int mid;
        
        while (start <= end) {
            mid = start + (end - start) / 2;
            if (data[mid] == k) break;
            
            if (data[mid] > k) end = mid - 1;
            else start = mid + 1;
        }
        
        if (data[mid] != k) return 0;
        
        int midId = mid;
        start = 0, end = midId;
        while (start <= end) {
            mid = start + (end - start) / 2;
            if (data[mid] == k) end = mid - 1;
            else start = mid + 1; 
        }
        int firstId = start;  // 也可以是 end + 1
        
        start = midId, end = len - 1;
        while (start <= end) {
            mid = start + (end - start) / 2;
            if (data[mid] == k) start = mid + 1;
            else end = mid - 1;
        }
        int lastId = end;  // 也可以是 start - 1
        
        return lastId - firstId + 1;
    }
};
```

上面的做法反而麻烦了，其实可以用两次就可以了，做好判断就好。

这里的判断比较精髓 `if (start >= len || data[start] != k) return 0;` 因为如果找不到的话，要么 start >= len,要么 `data[start] != k` 因为 start 是不可能 < 0 的。

```cpp
class Solution {
public:
    int GetNumberOfK(vector<int> data ,int k) {
        if (data.empty()) return 0;
        int len = data.size();
        int start = 0, end = len - 1;
        
        while (start <= end) {
            int mid = start + (end - start) / 2;
            if (data[mid] >= k) end = mid - 1;
            else start = mid + 1;
        }
        if (start >= len || data[start] != k) return 0;
        int lowerBound = start;
        
        start = 0, end = len - 1;
        while (start <= end) {
            int mid = start + (end - start) / 2;
            if (data[mid] <= k) start = mid + 1;
            else end = mid - 1;
        }
        int upperBound = end;
        
        return upperBound - lowerBound + 1;
    }
};
```

