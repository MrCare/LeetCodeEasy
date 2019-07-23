
# LeetCode

## NO.1 Two Sum

题目：

* Given an array of integers, return indices of the two numbers such that they add up to a specific target.You may assume that each input would have exactly one solution, and you may not use the same element twice.

题解：

* 第一种解法：暴力递进双循环

* 时间复杂度为$O(n^2)$，空间复杂度为$O(1)$


```python
class Solution:
    def twoSum(self, nums, target):
        for i,k in enumerate(nums[:-1]):
            for j,w in enumerate(nums[i+1:]):
                if k + w == target:
                    return [i,i+1+j]
                else:
                    pass
a = Solution()
%time a.twoSum([3,2,4],6)
```

    Wall time: 0 ns
    




    [1, 2]



* 第二种解法：哈希表快速查找,将列表元素作为键，将列表的索引作为值建立哈希表

* 时间复杂度与空间复杂度均为$O(n)$

* Python 中 dict.get(key, default=None)，返回键的值，如键不存在则返回 None


```python
    def tow_sum_with_dict(nums, target: int):
        d = {}
        for i, k in enumerate(nums):
            d[k] = i

        for i, k in enumerate(nums):
            j = d.get(target - k)
            if j is not None and i != j:
                return [i, j]
```

* 第三种解法：一次循环完成构建哈希表并返回结果


```python
    def tow_sum_with_dict(nums, target: int):
        d = {}
        for i, k in enumerate(nums):
            if d.get(target - k):
                return [i, d.get(target - k)]
            d[k] = i #这很有意思，竟然可以不用else
```

## NO.7 Reverse Integer

题目：

* Given a 32-bit signed integer, reverse digits of an integer.

* Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: ($−2^{31}$, $2^{31} − 1$). For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

题解：

* 列表反向取数的时候[3:0:-1]相当于从后往前不包含0，包含3，也可以两步切片，会快一点。


```python
class Solution:
    def reverse(self, x: int) -> int:
        tem = str(x)
        if tem[0] != '-':
            tem_f = tem[::-1]
            return (int(tem_f) if int(tem_f) < (2**31-1) else 0)
        else:
            tem_f = tem[:0:-1]
            print(tem_f)
            return (-int(tem_f) if int(tem_f) < (2**31+1) else 0)
a = Solution()
%time a.reverse(-123)
```

    321
    Wall time: 0 ns
    




    -321



## NO.9 Palindrome Number

题目：

* Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forwad.

题解：

* 将字符串从后向前索引 看是否与原字符串相同，注意：字符串不可变


```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        x = str(x)
        y = x[::-1]
        if x == y:
            return True
        else:
            return False
a = Solution()
%time a.isPalindrome(-121)
```

    Wall time: 0 ns
    




    False



## NO.13 Rome to Integer

题目：

* 将罗马数字转为正数

罗马数字的计算规则：

* 总体来说是将每一位出现的数字用加或减的方式组合起来，如果某一个数字比它后一个数字大或者与后一个数字相等，那么最终的结果就应当加上它

* 否则就减去它。

* 值得注意的是，因为最后一个数字没有后面的数字，所以最后一个数字总是需要加上的。


```python
class Solution:
    def romanToInt(self, s: str) -> int:
        s_0 = "IVXLCDM"
        s_1 = [1,5,10,50,100,500,1000]
        s_d = dict(zip(s_0,s_1))
        sum = 0
        for i in range(len(s)-1):
            if s_d[s[i]] >= s_d[s[i+1]]:
                sum += s_d[s[i]]
            else:
                sum -= s_d[s[i]]
        sum += s_d[s[-1]]
        return sum
a = Solution()
%time a.romanToInt('MCMXCIV')  
```

    Wall time: 0 ns
    




    1994



## NO.14 Longest Common Prefix

题目：

* Write a function to find the longest common prefix(前缀) string amongst an array of strings.

* If there is no common prefix, return an empty string 


非常巧妙的思路，是利用zip将所有可迭代对象做一个类似于转置操作的重组，利用到zip()函数如下几点性质：

* zip(可迭代对象) 返回的列表长度由其中最短的输入对象决定

* zip()返回的是一个由元组构成的列表

* \*list 相当于将list内的元素解压出来，在此例中list的元素恰好是str也是可迭代对象

* set()集合化函数，会自动将重复的元素合并为集合的“键”

* 返回zip object 需手动list()


```python
class Solution:
    def longestCommonPrefix(self, strs) -> str:
        r = ''
        for each in zip(*strs):
            if len(set(each)) == 1:
                r += each[0]
            else:
                break
        return r
a = Solution()
strs = ["flower","float","flame"]
%time a.longestCommonPrefix(strs)
print(list(zip(*strs)))
```

    Wall time: 0 ns
    [('f', 'f', 'f'), ('l', 'l', 'l'), ('o', 'o', 'a'), ('w', 'a', 'm'), ('e', 't', 'e')]
    

## NO.20 Valid Parentheses

题目：

* 判断括号是否合理，仅仅关注单个括号的数量和是否格式正确两个方面，不考虑顺序（小括号必须在最里面，大括号必须在最外面，这样的要求是不考虑的）

这里遇到了栈$stack$的应用,简单来说就是用list.append()和list.pop()完成数据后进后出的操作

* list.pop()会在list中去掉最后一个值，并返回此值

* 这里要考虑三种输入情况：
    
    1. 空值  
    
    2. 正确的输入  
    
    3. 没有左括号的错误输入  
    
    4. 有左括号的错误输入  

* 注意 [] 不是 None


```python
class Solution:
    def isValid(self, s: str) -> bool:
        if len(s) % 2 == 1:
            return False
        d = {'{':'}','[':']','(':')'}
        l = []
        for each in s:
            if each in d:
                l.append(each)
            else:
                if not l or d[l.pop()] != each:
                    return False
        return l==[]
a = Solution()
a.isValid(')[{}]')
```




    False



**在python中如果有空列表循环的情况发生，相当于pass，程序会越过这个循环继续执行：如下，没有 out**


```python
l = []
for x in l:
    print()
```

## NO.21 Merge Two Sorted Lists

题目：

* Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists. 

**多行注释：ctrl+/**  

这道题粘贴了官方题解，不太了解Python的链表结构，缺少了这一环，我猜测如果以1->2->4为例应当是这样的一个方式:  

* l1 = ListNode(1,ListNode(2,ListNode(4,None).val).val)  

但是不清楚内部定义ListNode的代码到底是怎么写的，这题先放这里，钻研明白后再补全


```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def mergeTwoLists(self, l1, l2):
        # maintain an unchanging reference to node ahead of the return node.
        prehead = ListNode(-1)
        prev = prehead
        while l1 and l2:
            if l1.val <= l2.val:
                prev.next = l1
                l1 = l1.next
            else:
                prev.next = l2
                l2 = l2.next            
            prev = prev.next

        # exactly one of l1 and l2 can be non-null at this point, so connect
        # the non-null list to the end of the merged list.
        prev.next = l1 if l1 is not None else l2

        return prehead.next
# a = Solution()
# a.mergeTwoLists([1,2,4],[2,3,4])
```

## NO.26 Remove  Duplicates from Sorted Arry

题目：

* Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

* Do not allocate extra space for another array, you must do this by modifying the input array in-place with $O(1)$ extra memory.

题解：

* 删除列表元素的三种方式：

    1. list.remove(元素)  
    
    2. list.pop(索引)
    
    3. del list[索引]  

* 如果采用遍历列表删除的思路需要注意，当删除元素之后，列表后位元素会前移，而循环次数则不会变，最后造成下标越界的错误  

* 正确的遍历列表并删除元素的几种方式：  
    
    1. filter()函数 过滤（会占用额外内存）  
    
    2. 逆序遍历 * 推荐  
    
    3. set()是去重复最快的方式，但不适用于其他条件    

虽然下面这段代码很酷，然而还是理解错了题意，题目要求修改原序列并返回一个长度值，而不是返回新序列  


```python
class Solution:
    def removeDuplicates(self, nums) -> int:
        for i in range(len(nums)-1,0,-1):
            if nums[i] == nums[i - 1]:
                nums.pop(i)
        return nums
a = Solution()
%time a.removeDuplicates([1,1,2,3,4,4,5])
```

    Wall time: 0 ns
    




    [1, 2, 3, 4, 5]



正确的题解是这样的：


```python
class Solution:
    def removeDuplicates(self, nums) -> int:
        if not nums: # 如果列表为空
            return 0
        t = 1
        for i,x in enumerate(nums[:-1]):
            if x != nums[i + 1]:
                nums[t] = nums[i + 1]
                t += 1 
        return t
a = Solution()
%time a.removeDuplicates([1,1,2])
```

    Wall time: 0 ns
    




    2



## NO.27 Remove Element

题目：

* Given an array nums and a value val, remove all instances of that value in-place and return the new length.

* Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

* The order of elements can be changed. It doesn't matter what you leave beyond the new length.

题解：

* 这个与26很相似，一开始也采用了26的思路，但是用list.remove方法会更好

* list.remove(x) :在list中去除一个x 这是不占用另外空间的做法


```python
class Solution:
    def removeElement(self, nums, val: int) -> int:
        l = len(nums)
        for i in range(l-1,-1,-1):
            if nums[i] == val:
                nums.remove(val)
        print(nums)
        return len(nums)
a = Solution()
%time a.removeElement([1],1)
```

    []
    Wall time: 0 ns
    




    0



## NO.28 Implement strStr()  

题目：

* Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

题解：

* list[0:0] 为 []  

* strStr(l1,l2)是 C 语言中的函数，在l1中查找l2返回值有三种情况：  
    
    1. l2在l1中存在，返回l2出现的位置
    
    2. l2在l1中不存在，返回-1
    
    3. l2为空"",则返回 0，据说是比较常见的面试题  

* python 的内置函数为:
   
    * str.find(str2,begin,end = len(str))用begin与end可以定义查找范围


```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        l1 = len(haystack)
        l2 = len(needle)
        t = 0
        for i in range(l1 - l2 + 1):
            if haystack[i:i + l2] == needle:
                t += 1
                return i
        if t == 0:
            return -1
a = Solution()
%time a.strStr("hello","ll")
```

    Wall time: 0 ns
    




    2



## NO.35 Search Insert Position

题目：
 
* Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

* You may assume no duplicates in the array.

题解：

* 永远要考虑边界情况，把list想象成在方格子（索引）里的数（元素）


```python
class Solution:
    def searchInsert(self, nums, target: int) -> int:
        for i,each in enumerate(nums):
            if target <= each:
                return i
        return len(nums)
a = Solution()
a.searchInsert([1,3,5,6],7)
```




    4



## NO.38 Count And Say

题目：

* The count-and-say sequence is the sequence of integers with the first five terms as following:

| NO. | Nums |
| :-: | :-: |
| 1. | 1 |
| 2. | 11 |
| 3. | 21 |
| 4. | 1211 |
| 5. | 111221 |

* 1 is read off as "one 1" or 11.

* 11 is read off as "two 1s" or 21.

* 21 is read off as "one 2, then one 1" or 1211.

* Given an integer n where $1 \leq n \leq 30$, generate the nth term of the count-and-say sequence.

* Note: Each term of the sequence of integers will be represented as a string.

题解：

* 按照规律用递推公式递归编写即可

这道题最棒的一处就是No.7行处在待循环数组后加一个字符串s，就可以不用特殊地考虑队尾边界的情况了！


```python
class Solution:
    def countAndSay(self, n: int) -> str:
        if n == 1:
            return '1'
        else:
            r = ''
            l = self.countAndSay(n - 1) + 's' 
            co =1
            for i in range(len(l)-1):
                if l[i] == l[i + 1]:
                    co += 1
                else:
                    r += str(co) + l[i]
                    co = 1
            return r
a = Solution()
for i in range(1,6):
    print(a.countAndSay(i))
```

    1
    11
    21
    1211
    111221
    

## NO.53 Maximum Subarray (DP)

题目：

* Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

题解：

* 动态规划问题：
    
    * Subarray(子序列)指的是相连的序列，且这个序列包含在了原序列中
    
    * 最大和指的是若干个连续元素相加，所能得到的最大的那个数
    
    * dp相当于“以nums[i]结尾的子序列最大和”  
    
    * “以nums[i+1]结尾的子序列的最大和”是max(dp+nums[i], nums[i])
    
    * for循环一遍后，dp相当于“以nums尾部元素结尾的子序列的最大和”
    
    * 我们要求的结果就是所有的for循环得到的dp中最大的那个

《数学之美》中提到的维特比算法用于求代价最小路径也是动态规划的思想，假设我们的人生也可以分为连续的几个阶段，幼儿，青年，中年，老年，濒死。假设前4个阶段都走了最优路径，那么最后濒死阶段的最优路径就是没有遗憾的离开这个世界，然后往回推，需要考虑的除了最后的已经明白的选择，还有就是当前阶段未确定的选择。感觉等于没说，好吧，强行哲理了一波哈哈哈~


```python
class Solution:
    def maxSubArray(self, nums) -> int:
        dp = nums[0]
        s = dp
        for i,each in enumerate(nums[1:]):
            if dp + each >= each:
                dp = dp + each
            
            else:
                dp = each
            if dp > s:
                s = dp
        return s
a = Solution()
a.maxSubArray([-2,1,-3,4,-1,2,1,-5,4])
```




    6



## NO.58 Length of Last Word

题目：

* Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.

* If the last word does not exist, return 0.

* Note: A word is defined as a character sequence consists of non-space characters only.

题解：反向循环找到最后一位非空元素  

* range(len(s)-1,-1,-1)


```python
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        s_1 = s.split(" ")
        for i in range(len(s_1)-1,-1,-1):
            if s_1[i] != "":
                return len(s_1[i])
        return 0
a = Solution()
a.lengthOfLastWord("hello world") # ""(空字符) "a "（空格结尾字符）
```




    5



## NO.66 Plus One

题目：

* Given a non-empty array of digits representing a non-negative integer, plus one to the integer.

* The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.

* You may assume the integer does not contain any leading zero, except the number 0 itself.

题解：先把列表变为数字，加一后再返回新列表  

* list(map(function,iteration))

* str.split() 默认以空格为分隔符，包含"\n"

* "".join(list or str)


```python
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:
        s = list(map(str, digits))
        s_0 = str(int(''.join(s)) + 1)
        s_1 = ",".join(s_0)
        l = s_1.split(',')
        return list(map(int, l))
```

## NO.67 Add Binary

题目：

* Given two binary strings, return their sum (also a binary string).

* The input strings are both non-empty and contains only characters 1 or 0.

题解：

* int(a,2) 将2进制表示的数转换为10进制表示的数

* bin(a) 输出结果为'0b+...'


```python
class Solution:
    def addBinary(self, a: str, b: str) -> str:
        s = int(a,2) + int(b, 2)
        return str(bin(s)[2:])
```

## NO.237 Delete Node in a Linked List

与其删除，不如更换指向


```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def deleteNode(self, node):
        """
        :type node: ListNode
        :rtype: void Do not return anything, modify node in-place instead.
        """
        node.val = node.next.val
        node.next = node.next.next
```

## NO.70 Climbing Stairs

题目：

* You are climbing a stair case. It takes n steps to reach to the top.

* Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

* Note: Given n will be a positive integer.

题解：斐波那契数列的变体：

* 只能以one或two step的方式爬n级楼梯，有几种方式？

* 递归算法的复杂度为O(n)，迭代算法的复杂度也是O(n)但是如果递推公式右边包含n项，递归的时间将是迭代的n倍

* Python的互换赋值并不需要中间变量


```python
class Solution:
    def climbStairs(self, n: int) -> int:
        a = 0
        b = 1
        for _ in range(n):
            a, b = b, a + b
        return b # 以0开头正常的斐波那契数列第n项应返回a，这里是依照题意返回的b
a = Solution()
a.climbStairs(4)
```




    5



## NO.104 Maximum Depth of Binary Tree

第一种做法：递归 

$$D_0 = 0$$

$$D_{n+1} = D_n + 1$$

* 时间复杂度：每个结点只访问一次，因此时间复杂度为 $O(N)$， 其中 $N$ 是结点的数量。

* 空间复杂度：在最坏的情况下，树是完全不平衡的，例如每个结点只剩下左子结点，递归将会被调用 $N$ 次（树的高度），因此保持调用栈的存储将是 $O(N)$。但在最好的情况下（树是完全平衡的），树的高度将是 $logN$。因此，在这种情况下的空间复杂度将是 $O(logN)$


```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def maxDepth(self, root) -> int:
        if root == None:
            return 0
        else:
            l = self.maxDepth(root.left)
            r = self.maxDepth(root.right)
            return max(l, r) + 1
```

第二种做法：迭代法

* 转自LeetCode官网，利用栈进行DFS(深度优先搜索)，非常牛掰


```python
# 方法二 迭代
class Solution:
    """
    迭代法
    """
    def maxDepth(self, root):
        stack = []                                              # 定义一个空栈，栈中的元素是结点及其对应的深度
        if root:                                                # 如果根结点不为空
            stack.append((root, 1))                             # 则将根节点及其对应深度1组成的元组入栈
        max_depth = 0                                           # 初始化最大深度为零
        while stack:                                            # 当栈非空时
            tree_node, cur_depth = stack.pop()                  # 弹出栈顶结点及其对应的深度
            if tree_node:                                       # 如果该结点不为空
                max_depth = max(max_depth, cur_depth)           # 更新当前最大深度，如果该结点深度更大的话
                stack.append((tree_node.left, cur_depth+1))     # 将该结点的左孩子结点及其对应深度压入栈中
                stack.append((tree_node.right, cur_depth+1))    # 将该结点的右孩子结点及其对应深度压入栈中
        return max_depth
```

## NO.121 Best Time to Buy and Sell Stock

第一个思路是暴力循环，这种方式的时间复杂度是$O(N^2)$，提交之后需要较长时间，超出时间限制


```python
class Solution:
    def maxProfit(self, prices) -> int:
        r = 0
        for i,each in enumerate(prices[:-1]):
            t = max(prices[i + 1:])
            if t - each > r:
                r = t - each
        return r
a = Solution()
a.maxProfit([7,1,5,3,6,4])
```




    5



这个算法的思路是双指针一次循环，两个指针一个记录已经循环过的值中最小值作为cost另一个指针记录当前的利润，时间复杂度是$O(N)$


```python
class Solution:
    def maxProfit(self, prices) -> int:
        cost = float('inf')
        profit = 0
        for price in prices:
            cost = min(cost,price)
            profit = max(profit, price - cost)
        return profit
a = Solution()
a.maxProfit([7,1,5,3,6,4])
```




    5



## NO.292 Nim Game 

发现需要抄题了不然很多东西再看的时候就忘了：

* You are playing the following Nim Game with your friend: There is a heap of stones on the table, each time one of you take turns to remove 1 to 3 stones. The one who removes the last stone will be the winner. You will take the first turn to remove the stones.Both of you are very clever and have optimal strategies for the game. Write a function to determine whether you can win the game given the number of stones in the heap.

* Stones如果是 4 那么先手就赢不了，因为无论拿走1，2，3，最后剩余的都是被对手拿走

题解：

* 这是个脑筋急转弯，只要写出来几项就可以发现规律，如果 stones 的数量是4的倍数先手就会输，反之先手就会赢

* 对于高手这样子写一行代码最牛掰，我一开始用了一个 if else 条件语句，可读性不错然而多了很多不必要的判断


```python
class Solution:
    def canWinNim(self, n: int) -> bool:
        return  n % 4 != 0
a = Solution()
a.canWinNim(4)
```




    False



## NO.344 Reverse String

题目：

* Write a function that reverses a string. The input string is given as an array of characters char[].Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

题解：

* 两个指针分别从头尾开始向中间循环，并交换数值


```python
class Solution:
    def reverseString(self, s) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        t1, t2 = 0, len(s)-1
        for _ in range(len(s)//2):
            s[t1], s[t2] = s[t2], s[t1]
            t1 += 1
            t2 -= 1
a = Solution()
s = ",".join("I love her").split(",")
a.reverseString(s)
s
```




    ['r', 'e', 'h', ' ', 'e', 'v', 'o', 'l', ' ', 'I']



## NO.557 Reverse Words in a String III

题目：

* Given a string, you need to reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

题解：

* 第一次想到的方式是利用双重循环实现，如下，注意 r 末尾有一个空格，返回时需要用到切片避免这个空格


```python
class Solution:
    def reverseWords(self, s: str) -> str:
        r = ''
        for k in s.split():
            l = ''
            for i in range(len(k)-1,-1,-1):
                l += k[i]
            r = r + l + ' '
        return r[:-1]
a = Solution()
a.reverseWords('I love you')
```




    'I evol uoy'



* 更为 pythonic 的做法是利用字符串反向索引 str[::-1] 来翻转字符串，点睛之笔是从列表翻转第一次，得到逆序排列的句子，此时单词是正序。之后把列表 join 为一个字符串，再整个翻转，得到句子顺序不变，单词顺序改变的结果
    
    1. 注意在将列表 join 成一个字符串的时候要加入 " " 做分隔符


```python
class Solution:
    def reverseWords(self, s: str) -> str:
        r = ' '.join(s.split()[::-1])[::-1]
        return r
a = Solution()
a.reverseWords('I love you')
```




    'I evol uoy'



## NO.206 Reverse Linked List

题目：

* Reverse a singly linked list.

题解：

* 保持节点的 val 不变，next指向前一个节点

* 循环链表需采用 while 的形式


```python
class Solution:
    def reverseList(self, head):
        if not head:                        # 如果head 没有值
            return                          # 则返回空
        pre = None                          # 用pre储存之前的一个head
        while head.next:                    # 当 head.next 有值时，循环
            nex = head.next                 # 用 nex 储存下一个 node
            head.next = pre                 # 转换指向方向
            pre = head                      # 更新pre
            head = nex                      # 更新head
        head.next = pre                     # 循环结束时最后一个head还没有转换指向方向。转换过来
        return head
```

## NO. 136 Single Number

题目：

* Given a non-empty array of integers, every element appears twice except for one. Find that single one.

* Note:Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

题解：

* 第一种自己做出来的,为了追求空间复杂度为$O(1)$，时间复杂度达到了$O(nlogn)$,思路是先对列表进行排序，排序后循环判断偶数位元素是否与奇数位元素相等你，若不等则返回当前偶数位。

    * Python 内置排序函数的时间复杂度是$O(nlogn)$空间复杂度为$O(1)$



```python
class Solution:
    def singleNumber(self, nums) -> int:
        nums.sort()
        for i in range(len(nums)//2):
            if nums[2*i+1] != nums[2*i]:
                return nums[2*i]
        return nums[-1]
a = Solution()
a.singleNumber([1,2,3,3,2,1,4])
```




    4



* 第二种思路是用一个集合充当容器，如果列表里的元素不在集合中就加入集合，在集合中就从从集合中除去，最后返回集合中的元素，这种方法时间复杂度和空间复杂度都是$O(n)$

    * 向字典中添加键的方法 dict.update(key = value)

    * 删除键的方法 dict.pop(key)

    * 返回字典键的方法 list(dict.keys()) 以列表形式返回，不加 list() 返回的是迭代器


```python
class Solution:
    def singleNumber(self, nums) -> int:
        s = {}
        for each in nums:
            if each not in s:
                s[each] = 0
            else:
                s.pop(each)
        return list(s.keys())[0]
a = Solution()
a.singleNumber([1,2,3,3,2,1,4])
```




    4



* 第三种思路是题目最优解,时间复杂度为$O(n)$,空间复杂度为$O(1)$
    
    * 异或（^） 二进制数的异或运算有如下性质：
        
        * `a ^ a` = `0`
        
        * `a ^ 0` = `a`
        
        * `a ^ b ^ a` = `a ^ a ^ b`
    
    * 以题目为例：`1 ^ 2 ^ 3 ^ 3 ^ 2 ^ 1 ^ 4` = `1 ^ 1 ^ 2 ^ 2 ^ 3 ^ 3 ^ 4` = `4`
    
    * 我是服了，真滴牛逼


```python
class Solution:
    def singleNumber(self, nums) -> int:
        a = 0
        for each in nums:
            a ^= each
        return a
a = Solution()
a.singleNumber([1,2,3,3,2,1,4])
```




    4



## NO.141 Linked List Cycle

题目：

* Given a linked list, determine if it has a cycle in it.

题解：

* 第一种思路是快慢指针，把链表想象成跑道，如果跑道是直线的，那么快指针一定会先到达终点，而如果是循环的链表则快慢指针会相遇


```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        if not head or not head.next :
            return False
        slow = head
        fast = head.next
        while slow != fast:
            if not fast or not fast.next:
                return False
            slow = slow.next
            fast = fast.next.next
        else:
            return True
```

* 第二种思路，使用哈希表，将节点依次存入哈希表，如果没有再可以存入的节点则链表中不存在循环，如果待存入节点已经在哈希表中存在，则说明链表中存在循环。

* 特殊方法置空法，也是利用了哈希表的思想，while 遍历每一个节点，然后将每一个节点的 val 设为 None，当 node.val 不为空，而 node.next 为空的时候，就说明到了列表的自然末尾，而如果 node.val 与 node.next 均为空时说明回到了链表之中，则有循环。这种方法比哈希表法节省内存，空间复杂度为$O(1)$


```python
    def hasCycle(self, head):
        if not head:
            return False
        while head.next and head.val:
            head.val = None  # 遍历的过程中将值置空
            head = head.next
        if not head.next:  # 如果碰到空发现已经结束，则无环
            return False
        return True  # 否则有环
```
