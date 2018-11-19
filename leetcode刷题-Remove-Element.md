---
title: leetcode刷题-Remove Element
date: 2018-11-12 19:34:34
tags: [leetcode,数组,C++]
categories: [leetcode,数组,C++]
---

# 27. Remove Element-移除元素

---

给定一个数组 nums 和一个值 val，你需要原地移除所有数值等于 val 的元素，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。

元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

示例 1:
```
给定 nums = [3,2,2,3], val = 3,

函数应该返回新的长度 2, 并且 nums 中的前两个元素均为 2。

你不需要考虑数组中超出新长度后面的元素。
```
示例 2:
```
给定 nums = [0,1,2,2,3,0,4,2], val = 2,

函数应该返回新的长度 5, 并且 nums 中的前五个元素为 0, 1, 3, 0, 4。

注意这五个元素可为任意顺序。

你不需要考虑数组中超出新长度后面的元素。
```
说明:

为什么返回数值是整数，但输出的答案是数组呢?

请注意，输入数组是以“引用”方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。

你可以想象内部操作如下:
```
// nums 是以“引用”方式传递的。也就是说，不对实参作任何拷贝
int len = removeElement(nums, val);

// 在函数里修改输入数组对于调用者是可见的。
// 根据你的函数返回的长度, 它会打印出数组中该长度范围内的所有元素。
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```
- 解法一:
```c++
// LeetCode, Remove Element
// 时间复杂度 O(n)，空间复杂度 O(1)
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int index =0;
        for(int i=0;i<nums.size();i++){
            if(nums[i] != val){
                nums[index++] = nums[i];
            }
        }
        return index;
    } 
};
```

>*Tips:*
>本解法是受到了 **LeetCode** 上第26题 **Remove Duplicates from Sorted Array** 的解法一的启发。*PS*终于自己解出来了一道题，虽然是一道简单级别的题，并且两题解法很相似，但还是觉得受到了鼓舞^_^

- 解法二:
```c++
// LeetCode, Remove Element
// 使用 remove()，时间复杂度 O(n)，空间复杂度 O(1)
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        return distance(nums.begin(), remove(nums.begin(), nums.end(), val));
        
    } 
};
```

>**注意:**
>- **distance(iterator first,iterator last)** 函数表示返回两个迭代器 **first** 和 **last** 之间的距离;
>- **remove()** 函数表示返回新的end()迭代器但是不改变原来数组的end()迭代器的值，将范围内值等于val的元素用后一个元素替代。原先数组中 新的end()至原end()范围内的值仍为原来数组的值，但是这部分状态不可靠。
