# Recent interviews as 01/06/2024
## Coding
1. 62 Unique Paths   
  Need to output path
1. 19 Remove Nth Node From End of List
2. 1721 Swapping Nodes in a Linked List
3. 958 Check Completeness of a Binary Tree  
    仪器而已稍有不同，是指定两个node的位置，比如交换第二个和第三个，这俩位置作为input的一部分  
    其他的题差不多的  
    面试官是国人，年级比较大的面试官，可能没有紧跟近期的面经吧   
    https://www.1point3acres.com/bbs/thread-1068970-1-1.html
1. 138 Copy List with Random Pointer
2. 140 Word Break II
3. 270 Closest Binary Search Tree Value
4. 273 Integer to English Words
5. 277 Find the Celebrity
6. 282 Expression Add Operators
7. 28 Find the Index of the First Occurrence in a String
8. 783 Minimum Distance Between BST Nodes
9. 1207 Unique Number of Occurrences
10. 43 Multiply Strings
11. 48 Rotate Image
12. 54 Spiral Matrix
13. 323 Number of Connected Components in an Undirected Graph
1. 79 Word Search
2. 939 Minimum Area Rectangle
3. 350 Intersection of Two Arrays II
4. 224 Basic Calculator
5. 1356 Sort Integers by The Number of 1 Bits
6. 5 Longest Palindromic Substring
7. 46 Permutations
8. 1041 Robot Bounded In Circle
9. 456 132 Pattern
10. 1944 Number of Visible People in a Queue
11. 549 Binary Tree Longest Consecutive Sequence II
12. 21 Merge Two Sorted Lists
13. 983 Minimum Cost For Tickets
14. 124 Binary Tree Maximum Path Sum
### 根据面经自己整理的
16. 7 Reverse Integer
17. 160 Intersection of Two Linked Lists
18. 有点像leetcode interval intersection list 但是找的是union  
    https://www.1point3acres.com/bbs/thread-1067273-1-1.html
1.  121 Best Time to Buy and Sell Stock
2.  140. Word Break II  
    要四零 （这道题我写出来之后加问了如果dictionary很长如何优化：经提示修改了code，答案如下：先把input dictionary list存成一个dictionary，举个例子 如果given string是 “abcd” 那么可能的word是 [a,ab,abc,abcd] 看一下是否在dictionary 里面 再按照愿题的方法dfs）  
    https://www.1point3acres.com/bbs/thread-1067273-1-1.html
1.  695 Max Area of Island
2.  207 Course Schedule  
    followup是有没有别的做法，复杂度是什么  
    https://www.1point3acres.com/bbs/thread-1067172-1-1.html
1.  739 Daily Temperatures
2.  - calculator变种， 表达式只有加法和乘法， 商量了一下能不能用stack做，被拒绝了，要求constant space，最后写完口头跑test的时候发现有点bug
1.  1541 Minimum Insertions to Balance a Parentheses String      
## 电面
1. 第一题给了去程和返程航班的价格，求最便宜的往返航班总价  
   第二题是给两个BST，输出排序后的数组，要求不能‍‌‌‌‌‍‍‌‌‍‌‍‌‍‌‍‌‌‌‌‍递归要用栈  
   https://www.1point3acres.com/bbs/thread-1069124-1-1.html

   第一题解答见 https://www.1point3acres.com/bbs/thread-1044373-1-1.html
1. 680 Valid Palindrome II   
   Should think how to expand to k (which will be a follow up), then also mention 1216. Valid Palindrome III if possible
1. 437 Path Sum III
    https://www.1point3acres.com/bbs/thread-1068242-1-1.html
1. 133 Clone Graph
2. 71 Simplify Path  
   https://www.1point3acres.com/bbs/thread-1067772-1-1.html
1. 1047 Remove All Adjacent Duplicates In String
2. 23 Merge k Sorted Lists
  https://www.1point3acres.com/bbs/thread-1067616-1-1.html
1. 236 Lowest Common Ancestor of a Binary Tree
2. 426 Convert Binary Search Tree to Sorted Doubly Linked List  
   follow up问了iterative的解法  
   https://www.1point3acres.com/bbs/thread-1067294-1-1.html
1. 1570 Dot Product of Two Sparse Vectors  
   被问了点乘最优解 又写了个index存list的，一开始用的hashmap。  
   https://www.1point3acres.com/bbs/thread-1067270-1-1.html
1. 1249 Minimum Remove to Make Valid Parentheses
1. 332 Reconstruct Itinerary
   第一題是332簡化版, 不用考慮重複的機票
3. 根据字符顺利把字符串排序  
  Input words = ["cat", "bat", "tab"]  
  Input Alphabet = ["c", "b", "a", "t"]  
  Output: True  
  順序是c<b<a<b  
  所以cat<bat<tab  
  https://www.1point3acres.com/bbs/thread-1067091-1-1.html
1. 1650 Lowest Common Ancestor of a Binary Tree III
2. 347 Top K Frequent Elements
   https://www.1point3acres.com/bbs/thread-1067090-1-1.html
1. 498 Diagonal Traverse  
   第一题对角线遍历矩阵，不需要改变方向。也就是简化版的死酒吧  
   https://www.1point3acres.com/bbs/thread-1066750-1-1.html
1. 346 Moving Average from Data Stream
1. 33 Search in Rotated Sorted Array
2. 499 The Maze III  
   https://www.1point3acres.com/bbs/thread-1066706-1-1.html
1. 65 Valid Number
2. 227 Basic Calculator II， 224 Basic Calculator， 772 Basic Calculator III
3. 19 Remove Nth Node From End of List
4. 543 Diameter of Binary Tree
## System Design
1. l‍‌‌‌‌‍‍‌‌‍‌‍‌‍‌‍‌‌‌‌‍eetcode
2. 设计news feed API  
   https://www.1point3acres.com/bbs/thread-1068372-1-1.html
1. * Live comment
* Leetcode coding contest website  
  hackerrank 比赛系统 加一个全局用户分数排序https://www.1point3acres.com/bbs/thread-1067090-1-1.html
* Presence indicator
* Ins bidding
*‍‌‌‌‌‍‍‌‌‍‌‍‌‍‌‍‌‌‌‌‍ News feed
* Dropbox
* Ads click aggregation
* Proximity
  设计一个nearby live event的推荐系统
* Youtube
  Refer important link https://www.1point3acres.com/bbs/thread-1067711-1-1.html
1. Design Instagram post photos, get feed, follow/unfollow user  
   https://www.1point3acres.com/bbs/thread-1067696-1-1.html
1. SD (product track): Design a chess game, 要求可以撤回上一步  
   https://www.1point3acres.com/bbs/thread-1067280-1-1.html
1. detect fraud information  
   https://www.1point3acres.com/bbs/thread-1068267-1-1.html
1. Design Spotify
2. System Design Product：Ticketmaster for cinemas https://www.1point3acres.com/bbs/thread-1067076-1-1.html
3. Product Architecture Design: design dropbox. 全程drive对话，自己说哪里是bottleneck，如何解决，面试官的问题都回答上了，后期dive in主要着重于how to chunk large file in detail, get updated file list 的时候如何提高performance，get updated file list的时候有什么edge case吗，如何解决。面试官最后looking very good。
4. 第一个SD是爬虫，有一些限定条件，比如说一万台机器，尽可能让每台机器的load evenly distributed。这道题做了非常多的back of envelope calculation，要计算 different instance types handling different types of work，应该是比较贴近production的一道题。

 爬虫 照着alex xu的材料答出来了，deep dive了一部分，但这个题目还有个限制条件，降低带宽使用，毛子指着我设计一个部分问有没啥问题，我说了bottleneck，他点点头，然后就接‍‌‌‌‌‍‍‌‌‍‌‍‌‍‌‍‌‌‌‌‍着design了
第二个SD是status查询，重点是考察怎么建索引要搜索更高效。
   Target E6  
  https://www.1point3acres.com/bbs/thread-1066514-1-1.html  
## BQ
1. BQ: 常规问题。自豪项目，conflict
2. BQ: 常规，conflict，有没有被push back，什么时候step up to do something out of your sco‍‌‌‌‌‍‍‌‌‍‌‍‌‍‌‍‌‌‌‌‍pe
3. Failure/proud/conflict when right/conflict when wrong/push back/Feedback/Difficult colleague/Incomplete info
4. proud proj, chanllenge, conflict, bias for action, useful feedback
5. hardest replatiship，conflict, what did you learn from your tech lead, what do you want to improve?
6. BQ都是常规问题，most proud project/conflict resolution/g‍‌‌‌‌‍‍‌‌‍‌‍‌‍‌‍‌‌‌‌‍rowth area/make quick decision/etc。
