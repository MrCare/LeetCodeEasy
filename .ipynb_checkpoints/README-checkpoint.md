# LeetCodeEasy

This is the answer of some questions in LeetCode  

> I will try my best to update it !  

43 answers are already done~  

* NO.1 Two Sum  

> 暴力双循环  
> 哈希表增加空间换取时间增速

* NO.7 Reverse Integer  

* NO.9 Palindrome Number  

* NO.13 Rome to Integer  

* NO.14 Longest Common Prefix 

* NO.20 Valid Parentheses  

> This easy 20 is a little hard \[upset\]

* NO.21 Merge Two Sorted Lists

> Python has to stimulate the structure of ListNode which I'm not fimiliar

* NO.26 Remove Duplicates from Sorted Array

> Have learned some new thing in this one !

* NO.27 Remove Element

> Another one about list.remove()!

* NO.28 Implement strStr()

> list[0:0] is []  
> str.find(str2,begin,end = len(str))

* NO.35 Search Insert Position

* NO.38 Count And Say

> I use a subtle method to fix boundary problem in loops

* NO.53 Maximum Subarray (DP)

> The first DP quiz

* NO.58 Length of Last Word

> range(len(s)-1,-1,-1) loop from the back direction

* NO.66 Plus One

* NO.67 Add Binary

* NO.237 Delete Node in a Linked List

* NO.70 Climbing Stairs

> Fibonacci sequence!

* NO.104 Maximum Depth of Binary Tree

> 遍历二叉树，迭代和递归！第一道DFS深度优先搜索题~

* NO.121 Best Time to Buy and Sell Stock

> 股票类第一题，双指针循环！一个记录最小cost一个记录当前profit

* NO.292 Nim Game

> Nim游戏，4的倍数先手必输，反之先手必赢

* NO.344 Reverse String

* NO.557 Reverse Words in a String III

> 字符串不可变，常见的操作只有切片和索引

* NO.206 Reverse Linked List

* NO. 136 Single Number

> 异或（^） 二进制数的异或运算有如下性质：

```Python
a ^ a = 0  
a ^ 0 = a;  
a ^ b ^ a = a ^ a ^ b
```


* NO.141 Linked List Cycle

> 快慢指针判断环  
> 哈希表判断环  
> 置空法判断环

* NO.235 Lowest Common Ancestor of a Binary Search Tree

> 二分搜索树的递归查找

* NO.169 Majority Element

> 这里有一个优秀算法：投票法，时间复杂度为$O(n)$,空间复杂度为$O(1)$

* NO.122 Best Time to Buy and Sell Stock II

> DP 第二题，动态规划最重要的一步是要确定状态是什么，然后写出状态转移方程

* NO.217 Contains Duplicate

* NO.88 Merge Sorted Array

> 归并排序，理清尾部的逻辑很重要！

* NO.155 Min Stack

> 用 list 模拟 stack

* NO.231 Power of Two

> 按位与的操作很巧妙

* NO.160 Intersection of Two Linked Lists

> 双指针，8字法！

* NO.415 Add Strings

> 模拟加法过程

# LeetCodeMedium

* NO.8 String to Integer (atoi)

> 一手贼溜的正则表达式

* NO.15 3Sum

> Two Sum 的升级版，必须用排序加对撞指针解决

> 大概断更了10天，做了一些别的事情，现在站在人生的三岔口，觉得广阔的天地充满希望可又十分凶险，希望我能坚持奋斗，找到自己热爱的东西，通过自律达到自由！

* NO.5 Longest Palindromic Substring

> 动态规划判断回文字符串

* NO.2 Add Two Numbers

> 链表实现的加法，进位操作值得注意

* NO.11 Container With Most Water

> 双指针法加速，一次循环丢弃多余状态，体现了算法的威力！

* NO.16 3Sum Closest

> 排序 + 对撞指针 + 损失函数(目标函数)

* NO.33

> 二分查找法，时间复杂度为$O(log_2n)$，空间复杂度最小可为$O(1)$

> [二分查找法编程模版](https://leetcode-cn.com/problems/search-insert-position/solution/te-bie-hao-yong-de-er-fen-cha-fa-fa-mo-ban-python-/) 非常细致，值得详细钻研

> Python 内置的`in`方法采用的应当就是二分查找

* NO.43 Multiply String

> 模拟乘法过程，时间复杂度$O(m+n)$

* NO.46 Permutations(排列)

> 回溯法，递归实现,时间复杂度略快于$O(n \times n!)$，慢于$O(n!)$，空间复杂度为$O(n!)$
