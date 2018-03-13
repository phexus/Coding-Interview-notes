# 把数组排成最小的数

不能直接用 sort 来排序，我们要自己定义 compare，可以写在外面，也可以写在里面，用 static 修饰

```cpp
class Solution {
public:
    string PrintMinNumber(vector<int> numbers) {
        if (numbers.empty()) return "";
        
        vector<string> strNum;
        for (int i : numbers) strNum.push_back(to_string(i));
        
        sort(strNum.begin(), strNum.end(), compare);
        
        string ans;
        for (string& str : strNum) ans.append(str);
        return ans;
    }
    static bool compare(const string& str1, const string& str2) {
        return str1 + str2 < str2 + str1;
    }
};
```

上面的写法维持了一个 string 的 vector 向量，其实也可以改成下面这样，直接对原来的 vector 排序

```cpp
class Solution {
public:
    string PrintMinNumber(vector<int> numbers) {
        if (numbers.empty()) return "";
        
        sort(numbers.begin(), numbers.end(), compare);
        
        string ans;
        for (int i : numbers) ans.append(to_string(i));
        return ans;
    }
    static bool compare(const int num1, const int num2) {
        return to_string(num1) + to_string(num2) < to_string(num2) + to_string(num1);
    }
};
```

