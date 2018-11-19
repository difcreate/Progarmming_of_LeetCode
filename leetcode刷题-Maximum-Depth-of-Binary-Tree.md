---
title: leetcode刷题-Maximum Depth of Binary Tree
date: 2018-11-17 13:56:48
tags: [leetcode,树]
categories: [leetcode,树]
---

# 104. Maximum Depth of Binary Tree-二叉树的最大深度

---

## 描述:
给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

说明: 叶子节点是指没有子节点的节点。

示例：
```
给定二叉树 [3,9,20,null,null,15,7]，

    3
   / \
  9  20
    /  \
   15   7
返回它的最大深度 3 。
```

---

**思路：**利用递归直接求解

代码：

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(root == nullptr) return 0;  //若树为空则返回0
        //最后返回根节点的左右子树中深度较大的那个深度，最后加上根节点的深度
        return max(maxDepth(root->left),maxDepth(root->right)) + 1;
    }
};
```