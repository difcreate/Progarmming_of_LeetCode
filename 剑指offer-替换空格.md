---
title: 剑指offer-替换空格
date: 2018-11-13 19:35:12
tags: [剑指offer,C++]
categories: [剑指offer,C++]
---

# 替换空格

---

**题目描述**

请实现一个函数，将一个字符串中的每个空格替换成“**%20**”。例如，当字符串为**We Are Happy**.则经过替换之后的字符串为**We%20Are%20Happy**.

---


**C++解题思路**

1. 可以新建一个string对象，从前向后遍历源字符串，遇到空格即替换成%20，不是空格直接拷贝，最后把string对象转换成C字符串拷贝给源字符串。

2. 先遍历源字符串得到空格的个数，得到替换后字符串的长度，使用两个指针，一个指向源串的最后，一个指向新字符串的最后，从后向前拷贝，遇到空格开始替换，同时后面的指针继续向前，直到两个指针相等，说明替换完成。注意不要在函数内新建一个数组来做，直接在源串上进行改动。这里给出第二种解题思路的代码：

```c++
void replaceSpace(char *str,int length) {
    int count = 0;
    char* pstr = str; 
    while(*pstr != '\0')     //得到空格的个数
    {
        if(*pstr == ' ')
        {
            count++;    
        }
        pstr++;
    }
    int newsize = length + 2*count;    //替换后的字符串长度
    str[newsize] = '\0';           //给新字符串末尾设置结束标志，不能省略。
    char* end = str + length - 1;     //源串的最后一个位置
    char* finish = str + newsize - 1;   //新串的最后一个位置
    while(end != finish)
    {
        if(*end != ' ')
        {
            *finish-- = *end--;    
        }
        else{                  //遇见空格开始替换。
            *finish-- = '0';
            *finish-- = '2';
            *finish-- = '%';
            end--;
        }
    }
}
```

---

**Python解题思路**

**Python**中的**replace()** 方法把字符串中的 old（旧字符串） 替换成 new(新字符串)，如果指定第三个参数max，则替换不超过 max 次。所以只需要在循环中判断字符是否是空格字符，如果是的话就替换成‘**%20**’就行了。

>*用法：* str.replace(old, new[, max])

```python
# -*- coding:utf-8 -*-
class Solution:
    # s 源字符串
    def replaceSpace(self, s):
        # write code here
        #s1 = dict(s)
        for x in s:
            if x == ' ':
                s = s.replace(' ', '%20')
        return s
```

>Tips:
>此解法是本菜鸡自己想出来的，所以可以得出并不是本菜鸡变厉害了，而是python相对于c++来说确实很好用。python真香~
