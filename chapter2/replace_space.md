## 替换空格

先看我的错误实现

1. 想当然的直接在源字符串后面添加新元素，会有越界访问的问题，不过从参数类型和返回值来看，参数类型是指针，而不是指向指针的指针，所以指针我们是没法修改的，智能 in-place 来做，默认输入的字符串后面有足够多的空闲内存。	
2. 仅仅统计了空格个数，而且新的字符串长度应该是除了空格以外的字符数量 + 空格数量 * 3 才对。
3. 没有考虑 字符串末尾的 '\0' 也要移动。

```cpp
class Solution {
public:
	void replaceSpace(char *str,int length) {
        if (str == NULL || length == 0) return;
        int spaceNum = 0;
        for (int i = 0; i < length; ++i) {
            if (str[i] == ' ') ++spaceNum;
        }
        
        int i = length - 1;
        int j = length - 1 + spaceNum * 3;
        while (i < j) {
            if (str[i--] == ' ') {
                str[j--] = '0';
                str[j--] = '2';
                str[j--] = '%';
            } else {
                str[j--] = str[i--];
            }
        }
	}
};
```

### 正确解法

1. length 仅仅是用来标识总的容量的，要按照 '\0' 来统计原来字符串的长度
2. `int newLen = originLen + 2 * spaceNum;` 注意这里是 2 ，新增的长度
3. length 不够长要直接返回，判断条件是 `newLen + 1 > length`，因为得考虑加上 '\0' 的实际占用长度 ，感觉书本上有问题
4. while 条件设为了 `i < j` ，感觉书本上多余了，没有必要再判断 i >= 0，前面的长度已经经过精确计算了，最终 i 一定会等于 j 的。

```cpp
class Solution {
public:
	void replaceSpace(char *str,int length) {
        if (str == NULL || length <= 0) return;
        int spaceNum = 0, originLen = 0;
        for (int i = 0; str[i] != '\0'; ++i) {
            if (str[i] == ' ') ++spaceNum;
            ++originLen;
        }
        
        int newLen = originLen + 2 * spaceNum;
        if (newLen + 1 > length) return; // 长度不够，直接返回
        
        int i = originLen;
        int j = newLen;
        while (i < j) {
            if (str[i] == ' ') {
                str[j--] = '0';
                str[j--] = '2';
                str[j--] = '%';
            } else {
                str[j--] = str[i];
            }
            --i; // 统一 --i
        }
	}
};
```

