---
title: leetcode刷题-Remove Duplicates from Sorted Array
date: 2018-11-12 16:18:08
tags: [leetcode,数组,C++]
categories: [leetcode,数组,C++]
---

# 26. Remove Duplicates from Sorted Array-删除排序数组中的重复项

**内容：** 给定一个排序数组，你需要在原地删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。

示例 1:
```
给定数组 nums = [1,1,2], 

函数应该返回新的长度 2, 并且原数组 nums 的前两个元素被修改为 1, 2。 

你不需要考虑数组中超出新长度后面的元素。
```
示例 2:
```
给定 nums = [0,0,1,1,1,2,2,3,3,4],

函数应该返回新的长度 5, 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4。

你不需要考虑数组中超出新长度后面的元素。
```
说明:

为什么返回数值是整数，但输出的答案是数组呢?

请注意，输入数组是以“引用”方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。

你可以想象内部操作如下:
```
// nums 是以“引用”方式传递的。也就是说，不对实参做任何拷贝
int len = removeDuplicates(nums);

// 在函数里修改输入数组对于调用者是可见的。
// 根据你的函数返回的长度, 它会打印出数组中该长度范围内的所有元素。
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```
>*Tips：*
>这道题开始还是没有做出来，暴力破解法的思路错误了，不能一直试图用for循环来解决，应该着重于数组本身的变化以及要在STL上面寻求更好的解题思路

- 解法一：
```c++
// LeetCode, Remove Duplicates from Sorted Array
// 时间复杂度 O(n)，空间复杂度 O(1)
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if (nums.empty()) return 0;
        int index = 0;
        for (int i = 1; i < nums.size(); i++) {
            if (nums[index] != nums[i])
            nums[++index] = nums[i];
        }
        return index + 1;
    }
};
```

- 解法二：
```c++
// LeetCode, Remove Duplicates from Sorted Array
// 时间复杂度 O(n)，空间复杂度 O(1)
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        return distance(nums.begin(), unique(nums.begin(), nums.end()));
    }
};
```

>**注意:**
>- **distance(iterator first,iterator last)** 函数表示返回两个迭代器 **first** 和 **last** 之间的距离;
>- **unique(iterator it_1,iterator it_2)** 函数表示其中这两个参数表示对容器中[it_1，it_2)范围的元素进行去重(注：区间是前闭后开，即不包含it_2所指的元素),返回值是一个迭代器，它指向的是去重后容器中不重复序列的最后一个元素的下一个元素。

- 解法三：
```c++
// LeetCode, Remove Duplicates from Sorted Array
// 时间复杂度 O(n)，空间复杂度 O(1)
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        return distance(nums.begin(), removeDuplicates(nums.begin(), nums.end(), nums.begin()));
    }
    template<typename InIt, typename OutIt>
    OutIt removeDuplicates(InIt first, InIt last, OutIt output) {
    while (first != last) {
        *output++ = *first;
        first = upper_bound(first, last, *first);
    }
    return output;
    }
};
```