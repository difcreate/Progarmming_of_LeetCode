---
title: leetcode刷题-Merge Two Sorted Lists
date: 2018-11-15 15:25:32
tags: [leetcode,链表,C++]
categories: [leetcode,链表,C++]
---

# 21. Merge Two Sorted Lists-合并两个有序链表

---

## 描述

将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

示例：

```
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

---

- 解法一:非递归版

>思路：
>新建一个链表用来存储新的有序链表，可以先让两个链表互相比较，新链表的指针指向更小的那个，依次遍历直到一方遍历结束，最后把剩下的那个链表的剩余部分连接到新链表的表尾

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
 //时间复杂度O(max(m,n)),空间复杂度O(m+n)
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode *t1 = l1;
        ListNode *t2 = l2;
        ListNode *newlist = new ListNode(0);    //新建一个链表用来存储
        ListNode *nl = newlist;    //让指针nl指向新链表，最后返回nl
        //两个链表相互比较大小，新链表指针指向更小的值
        while(t1 != nullptr && t2 != nullptr){
            if(t1->val > t2->val){
                newlist->next = t2;
                newlist = newlist->next;    //得到一个更小的值后指针后移
                t2 = t2->next;      //指针后移
            }
            else{
                newlist->next = t1;
                newlist = newlist->next;
                t1 = t1->next;
            }
        }
        //把当只剩下一个链表时，把链表剩余部分连接到新链表表尾
        if(t1 == nullptr && t2 != nullptr)
            newlist->next = t2;     
        if(t2 == nullptr && t1 != nullptr)
            newlist->next = t1;
        return nl->next;
    }
};
```