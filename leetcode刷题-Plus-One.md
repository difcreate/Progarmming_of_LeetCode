---
title: leetcode刷题-Plus One
date: 2018-11-14 16:52:38
tags: [leetcode,数组,C++]
categories: [leetcode,数组,C++]
---

# 66. Plus One-加一

---

## 描述

给定一个由整数组成的非空数组所表示的非负整数，在该数的基础上加一。

最高位数字存放在数组的首位， 数组中每个元素只存储一个数字。

你可以假设除了整数 0 之外，这个整数不会以零开头。

示例 1:

```
输入: [1,2,3]
输出: [1,2,4]
解释: 输入数组表示数字 123。
```

示例 2:

```
输入: [4,3,2,1]
输出: [4,3,2,2]
解释: 输入数组表示数字 4321。
```

---

## 分析:
>高精度加法

- 解法一：

```c++
//时间复杂度O(n),空间复杂度O(1)
class Solution {
public:
    vector<int> plusOne(vector<int> &digits) {
        add(digits, 1);
        return digits;
    }
private:
// 0 <= digit <= 9
    void add(vector<int> &digits, int digit) {
        int c = digit; // carry, 进位
        for (auto it = digits.rbegin(); it != digits.rend(); ++it){
            *it += c;
            c = *it / 10;
            *it %= 10;
        }
        if (c > 0) //如果最前一位是9+1需要进位的话，那就在最前面的位置插入1
            digits.insert(digits.begin(), 1);  
    }
};
```

>*Tips:*
>c.rbegin() 返回一个逆序迭代器，它指向容器c的最后一个元素
>c.rend() 返回一个逆序迭代器，它指向容器c的第一个元素前面的位置
>对于反向迭代器，++ 运算将访问前一个元素，而 -- 运算则访问下一个元素

- 解法二：

```c++
//时间复杂度O(n),空间复杂度O(1)
class Solution {
public:
    vector<int> plusOne(vector<int> &digits) {
        add(digits, 1);
        return digits;
    }
private:
// 0 <= digit <= 9
    void add(vector<int> &digits, int digit) {
        int c = digit; // carry, 进位
        for_each(digits.rbegin(), digits.rend(), [&c](int &d){
            d += c;
            c = d / 10;
            d %= 10;
        });

        if (c > 0) 
            digits.insert(digits.begin(), 1);
    }
};
```

>*Tips:*
>这个解法没看明白......