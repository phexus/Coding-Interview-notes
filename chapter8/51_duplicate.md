# 数组中重复的数字

## Solution 1 - map

利用了 set，时间复杂度 $$O(n)$$ ，空间复杂度 $$O(n)$$

```cpp
class Solution {
public:
    // Parameters:
    //        numbers:     an array of integers
    //        length:      the length of array numbers
    //        duplication: (Output) the duplicated number in the array number
    // Return value:       true if the input is valid, and there are some duplications in the array number
    //                     otherwise false
    bool duplicate(int numbers[], int length, int* duplication) {
        if (numbers == NULL || length <= 0) return false;
        unordered_set<int> set;
        for (int i = 0; i < length; ++i) {
            if (set.count(numbers[i])) {
                *duplication = numbers[i];
                return true;
            } else {
                set.insert(numbers[i]);
            }
        }
        return false;
    }
};
```

## Solution 2 - swap

考虑到题目给定了元素的范围，可以通过 swap ，把空间复杂度降到 $$O(1)$$

```cpp
class Solution {
public:
    // Parameters:
    //        numbers:     an array of integers
    //        length:      the length of array numbers
    //        duplication: (Output) the duplicated number in the array number
    // Return value:       true if the input is valid, and there are some duplications in the array number
    //                     otherwise false
    bool duplicate(int numbers[], int length, int* duplication) {
        if (numbers == NULL || length < 1) return false;
        
        for (int i = 0; i < length; ++i) {
            if (numbers[i] < 0 || numbers[i] > length - 1) return false;
            
            while (numbers[i] != i) {
                if (numbers[i] == numbers[numbers[i]]) {
                    *duplication = numbers[i];
                    return true;
                } else {
                    swap(numbers[i], numbers[numbers[i]]);
                }
            }
        }
        return false;
    }
};
```

