---
title: leetcode刷题-Single Number
date: 2018-11-19 14:33:55
tags: [leetcode,数组]
categories: [leetcode,数组]
---

# 136. Single Number-只出现过一次的数字

---

## 描述：

给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

>*说明：*
>你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

示例 1:
```
输入: [2,2,1]
输出: 1
```
示例 2:
```
输入: [4,1,2,1,2]
输出: 4
```

---

**思路：**

题中要求，线性时间复杂度，而且不使用额外空间，那么就要从数组本身入手，同时只循环扫描一遍数组

我们可以考虑 异或运算 ，它是满足交换律和结合的，也就是说 a ^ b  ^c = a ^ c ^ b，这样当我们遍历数组，顺次进行异或运算，那么最终的结果就是唯一的不重复数字。

示例：
```
[4,1,2,1,2]，
4^1^2^1^2 = 1^1^2^2^4 = 0^0^4=4
```

**代码一：**

```c++
//时间复杂度O(n),空间复杂度O(1)
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int x = 0;
        //顺次异或，每当某个数字重复出现偶次都会被消除为0
        for (auto i : nums) {
            x ^= i;
        }
        return x;
    }
};

// class Solution {
// public:
//     int singleNumber(int A[], int n) {
//         int result = 0;
//         for(int i = 0;i < n;i++){
//             result = result ^ A[i];
//         }
//         return result;
//     }
// };
```

**代码二：**

```c++
//时间复杂度O(n),空间复杂度O(1)
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        //accumulate()函数用来求和，初始值为0，范围从begin到end的所有向量以位异或的方式求和
        return accumulate(nums.begin(), nums.end(), 0, bit_xor<int>());
    }
};
```