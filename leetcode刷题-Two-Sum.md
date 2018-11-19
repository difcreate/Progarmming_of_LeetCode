---
title: leetcode刷题-Two Sum
date: 2018-11-12 13:21:52
tags: [leetcode,数组,C++,Java]
categories: [leetcode,数组,C++,Java]
---

### 算法真的好难之刚开始就要被虐哭~~~

---

## 先吐槽一波~~~ 

之前看了一段时间的基础知识，感觉一边学一边忘是不行的，于是静极思动，决定从今天开始直接刷LeetCode的题，实践出真知！（手动滑稽=_=），开始刷题了觉得自己当初是有多高估自己才选择算法，真是简单级别的题目都要难倒我了，真是可怕！不过事已至此只能拼命学了。好了，话不多说，正式记录自己的苦逼刷题之旅......

---

## 1.Two Sum--两数之和

给定一个整数数组和一个目标值，找出数组中和为目标值的两个数。

你可以假设每个输入只对应一种答案，且同样的元素不能被重复利用。

**Example:**

``` code

Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].

```

---

## 解决方案

### 方法一：暴力法

之前准备用C++直接写暴力法，但是可惜算法思路正确了，就是C++基础还是不够扎实，提交代码还是有问题，所以这里引用了系统的**Java**版参考代码。暴力法很简单。遍历每个元素 x，并查找是否存在一个值与 target - x 相等的目标元素。

*java:*

```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        map.put(nums[i], i);
    }
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement) && map.get(complement) != i) {
            return new int[] { i, map.get(complement) };
        }
    }
    throw new IllegalArgumentException("No two sum solution");
}
```

**复杂度分析：**

*时间复杂度：* O(n^2)，对于每个元素，我们试图通过遍历数组的其余部分来寻找它所对应的目标元素，这将耗费O(n)的时间。因此时间复杂度为O(n^2)。

*空间复杂度：* O(1)。

### 方法二：哈希表

借助Hash求解，这是较为标准的解法，首先将数组中每个数存入Hash表，然后枚举数组内数字（假设当前枚举数字为A，则在Hash表中查询target- A是否存在，找到则返回解），枚举一趟中一定因为有解的存在而返回，时间复杂度O(n)；（实际时间使用情况，10ms[Java]以内）

*C++:*

``` C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        // map存储数组信息 vector存储结果
		map<int, int> m;
		vector<int> ans;
		// 遍历数组查询结果
		for (int i = 0; i < nums.size(); ++i) {
			// 查找到配对元素
			if (m.find(target - nums[i]) != m.end()) {
				ans.push_back(m[target - nums[i]]);
				ans.push_back(i);
				return ans;
			}
			// 否则将现在元素插入map
			m.insert(pair<int, int>(nums[i], i));
		}
		return ans;
    }
};

```

*复杂度分析：*

*时间复杂度：* O(n)， 我们只遍历了包含有 n 个元素的列表一次。在表中进行的每次查找只花费 O(1) 的时间。

*空间复杂度：* O(n)， 所需的额外空间取决于哈希表中存储的元素数量，该表最多需要存储 n 个元素。