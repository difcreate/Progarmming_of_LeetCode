---
title: leetcode刷题-Transpose Matrix
date: 2018-11-13 16:00:30
tags: [leetcode,数组,C++,Python]
categories: [leetcode,数组,C++,Python]
---

# 867.Transpose Matrix-转置矩阵

---

给定一个矩阵 A， 返回 A 的转置矩阵。

矩阵的转置是指将矩阵的主对角线翻转，交换矩阵的行索引与列索引。

 

示例 1：

```
输入：[[1,2,3],[4,5,6],[7,8,9]]
输出：[[1,4,7],[2,5,8],[3,6,9]]
```

示例 2：

```
输入：[[1,2,3],[4,5,6]]
输出：[[1,4],[2,5],[3,6]]
``` 

>提示：
>1 <= A.length <= 1000
>1 <= A[0].length <= 1000

---

**解题思路：**

矩阵的行列互换，简单的二重循环就可以了,不过很可惜，可能是太久没实战编码了，虽然知道该怎么做，但还是没写出来正确可以运行的代码......

- C++版代码：

```c++
class Solution {
public:
    vector<vector<int>> transpose(vector<vector<int>>& A) {
        int m=A.size();
        int n=A[0].size();
        vector<int> B(m,0);
        vector<vector<int>> C(n,B);
        for(int i=0;i<m;i++)
        {
            for(int j=0;j<n;j++)
                C[j][i]=A[i][j];
        }
        return C;
    }
};
```
- Python版代码：

```python
class Solution(object):
    def transpose(self, A):
        R, C = len(A), len(A[0])
        ans = [[None] * R for _ in xrange(C)]
        for r, row in enumerate(A):
            for c, val in enumerate(row):
                ans[c][r] = val
        return ans

        #Alternative Solution:
        #return zip(*A)
```

>**复杂度分析:**
>
>时间复杂度：O(R * C)，其中 R 和 C 是给定矩阵 A 的行数和列数。
>
>空间复杂度：O(R * C)，也就是答案所使用的空间。