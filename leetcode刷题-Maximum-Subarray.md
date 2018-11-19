---
title: leetcode刷题-Maximum Subarray
date: 2018-11-16 19:42:14
tags: [leetcode,动态规划,C++]
categories: [leetcode,动态规划]
---

# 53. Maximum Subarray-最大子序和

---

## 描述：

给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

示例:
```
输入: [-2,1,-3,4,-1,2,1,-5,4],
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
```

>*进阶:*
>如果你已经实现复杂度为 O(n) 的解法，尝试使用更为精妙的分治法求解。

---

- 解法一：动态规划

**思路：**
当我们从头到尾遍历这个数组时，对于数组里的一个整数，他有几种选择呢？它只有两种选择：
1. 加入之前的SubArray;
2. 自己另起一个SubArray。那什么时候会出现这两种情况呢？

如果之前SubArray的总体之和大于0的话，那么就认为它对后续结果是有贡献的,这种情况下我们选择加入之前的SubArray;

如果之前SubArray的总体之和小于等于0的话，那么就认为它对后续结果是没有贡献的,甚至是有害的（小于0时），这种情况下我们选择以这个数字开始另起一个SubArray;

设状态为f[j]，表示以S[j]结尾的最大l连续子序列和，则状态转移方程如下：**<div align=center>$f[j]$ = $max${$f[j-1]$ + $S[j]$,$S[j]$},$其中$ 1 $\leq j \le$ n  </div><br><div align=center>$target$ = $max${$f[j]$} , $其中$ 1 $\leq j \le$ n </div>**

解释如下：
- 情况一：S[j]不独立，与前面的某些数组成一个连续子序列，则最大连续子序列和为f[j-1]+S[j]
- 情况二：S[j]独立划分成一段,即连续子序列仅包含一个数S[j]，则最大连续子序列和为S[j]

```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int result = INT_MIN, f = 0;
        for (int i = 0; i < nums.size(); ++i) {
          f = max(f + nums[i], nums[i]);
           result = max(result, f);
        }
        return result;
    }
};
```
