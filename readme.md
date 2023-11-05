# A list of Meta high-frequency coding questions 

1. 199 Binary Tree Right Side View Variation
   
   ***Approach 1 BFS*** TC O(N) N is number of nodes since one has to visit each node, SC is O(D) to keep the queues, where D is a tree diameter.                  
   ***Approach 2 DFS*** - TC O(N) N is number of nodes since one has to visit each node, SC is O(N) to keep the recursion stack, where H is a tree height. Use DFS to get left view and right view separately and then join it. When getting left view, check left child first while getting right view check right child first.  
   <details>
       
      ```python
       #BFS
            def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
              if not root:
                  return []
              
              resultLeft = []
              resultRight = []
              queue = deque([root])
              while queue:
                  levelSize = len(queue)
                  for i in range(levelSize):
                      node = queue.popleft()
                      if i == 0:
                          resultLeft.append(node.val)
                      if i == levelSize - 1:
                          resultRight.append(node.val)
                      
                      if node.left:
                          queue.append(node.left)
                      
                      if node.right:
                          queue.append(node.right)
      
              return resultLeft + resultRight[::-1]
         
      #DFS
        def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        result = []

        def dfs(node, level):
            if level == len(result):
                result.append(node.val)
            
            if node.right:
                dfs(node.right, level + 1)
            
            if node.left:
                dfs(node.left, level + 1)

        if not root:
            return []
        
        dfs(root, 0)
        return result
      ```
   </details>     
   
1. 347 Top K Frequent Elements  
Classic probem in heap, should learn quick select at some point

1. 1762 Buildings with an occean view  
***Approach 1*** is to look from right to left, and maintain maxRight, if a building is larger than maxRight, add its index to the  result, and update maxRight. In the end, reverse result. TC O(N), SC O(1)  
***Approach 2*** is to look from left to right, if a building is blocked by current building, remove it from the result, otherwise add its index to the result. TC O(N), SC O(N)
   <details>
       
      ```python
       # From right to left
       def findBuildings(self, heights: List[int]) -> List[int]:
           result = []
           maxRightHeight = -1
           for i in range(len(heights) -1, -1, -1):
               if heights[i] > maxRightHeight:
                   result.append(i)
                   maxRightHeight = heights[i]
           result.reverse()
           return result
         
      #From left to right
       def findBuildings(self, heights: List[int]) -> List[int]:
           result = []
           for i, height in enumerate(heights):
               while len(result) > 0 and heights[result[-1]] <= height:
                   result.pop()
               result.append(i)
           
           return result
      ```
   </details>    

1. 129 Sum Root to Leaf Numbers  
***Approach 1*** is to calculate sum in recursive preorder traversal. In each recursion call, the passed parameter is node and pathSum, return 0 if node is null; otherwise increase pathSum considering node value, then return pathSum if node is leaf; Otherwise recursively call left child and right child with pathSum, add them and then return. TC O(N) SC O(N)  
***Approach 2*** Iterative preorder traversal. Use a stack to store pair of node and current path sum. In each iteration, pop pair of node and curr path sum, then increase path sum considering node value. If node is leaf, then add it to total sum. If node's right is not null, add it to stack; If node.s left is not null, add it to stack.O(N)
   <details>
       
      ```python
   # Recursive
    def sumNumbers(self, root: Optional[TreeNode]) -> int:
        def dfs(node, pathSum):         
            if not node:                
                return 0
   
            pathSum = pathSum * 10 + node.val
            if node.left is None and node.right is None:
                return pathSum
                
            return dfs(node.left, pathSum) + dfs(node.right, pathSum)
        
        return dfs(root, 0)
     
      # Iterative
    def sumNumbers(self, root: Optional[TreeNode]) -> int:
        total = 0
        stack = [(root, 0)]
        while stack:
            node, pathSum = stack.pop()
   
            pathSum = pathSum * 10 + node.val
            if node.left is None and node.right is None:
                total += pathSum
            
            if node.right is not None:
                stack.append((node.right, pathSum))
            
            if node.left is not None:
                stack.append((node.left, pathSum))
        
        return total     
      ```
   </details> 

1. 173 Binary Search Tree Iterator  
***Approach 1*** is to flatten the tree using inorder DFS, save the result in an array, and set currCursorPosition = -1. When calling next, increase currCursorPosition. hasNext just need to check whether currCursorPosition + 1 is less than last index. TC O(1) SC O(N)  
***Approach 2*** is to use a stack to store all the left children. In constructor, push all the left children. In next, pop from the stack, and if it has right child, then push all the left children of that node. In hasNext, only check whether stack is empty.   TC O(1) for hasNext, and O(1) on average for next(as for n calls, the total TC is O(N)), SC O(H) where H is the height of the tree
   <details>
      
      ```python
      class BSTIterator:
          def __init__(self, root: Optional[TreeNode]):
              self.stack = []
              self.pushLeftChildren(root)
              
          def pushLeftChildren(self, node):
              while node:
                  self.stack.append(node)
                  node = node.left
                        
          def next(self) -> int:
              topMostNode = self.stack.pop()
              self.pushLeftChildren(topMostNode.right)
      
              return topMostNode.val       
      
          def hasNext(self) -> bool:
              return len(self.stack) > 0       
      ```
   </details>   

1. 29 Divide two integers  
***Approach 1*** Firsly determine whether the result is positive or negative. Try to convert both dividen and divisor to its absolute value, and then do the divide. Beare edge cases that could overflow, i.e. when either dividend or divisor is MIN_INT. The idea is to find the quotient in its binary form. Imagine the quotient is represented as X31, X30 ..., X0. So loop from 31 to 0, at each step, if shift dividend by i bits(equivalent to dividend/ 2 power i and the result is greater than b, then increase quotient with (1 << i equivalent to 2 power i), and reduce divident by b << i equivalent to b multiply 2 power i. In the end, return quotient or -quotient based on it's positive or negative
   <details>
    
      ```python
    def divide(self, dividend: int, divisor: int) -> int:
        MIN_INT = -2 ** 31
        MAX_INT = 2 ** 31 - 1
        if dividend == MIN_INT and divisor == MIN_INT:
            return 1
        elif divisor == MIN_INT:
            return 0
        elif dividend == MIN_INT:
            if divisor == -1:
                return MAX_INT
            elif divisor > 0:
                return -1 + self.divide(dividend + divisor, divisor)
            else:
                return 1 + self.divide(dividend - divisor, divisor)

        isPositive = (dividend > 0) == (divisor > 0)
        dividend = abs(dividend)
        divisor = abs(divisor)
        quotient = 0
        for i in range(31, -1, -1):
            if (dividend >> i) >= divisor:
                quotient += (1 << i)
                dividend -= (divisor << i)
        
        return quotient if isPositive else -quotient  
      ```
   </details>  


1. 2365 Task Scheduler II  
***Approach 1***
The idea is to save the last day that a task is completed in a hash map to allow easy retrieval later. Use variable result to store current day initialize to 0. So looping through the tasks, for each task, if it is last executed, then it must be executed after enough days pass since its last completion, so should be the max value of current day, and previous completion day + space, with addition of 1; If the task has never been executed, then it be executed on next day which is current day plus 1. Then update the last day that a task is completed. In the end, return current day. TC O(N), SC O(N)  
   <details>
    
      ```python
      # Use normal dict {}
       def taskSchedulerII(self, tasks: List[int], space: int) -> int:
           result = 0
           taskLastComplete = defaultdict(lambda : -2 - space)
           for task in tasks:
               if task in taskLastComplete:
                   result = max(result, taskLastComplete[task] + space) + 1
               else:
                   result += 1
                   
               taskLastComplete[task] = result
   
           return result
            
      # Use defaultdict
       def taskSchedulerII(self, tasks: List[int], space: int) -> int:
           result = 0
           taskLastComplete = defaultdict(lambda : -2 - space)
           for task in tasks:
               result = max(result, taskLastComplete[task] + space) + 1
               taskLastComplete[task] = result
   
           return result
      ```
   </details>  

1. 621 Task Scheduler  
***Approach 1*** The idea is to find the minimum number of slots to execute the most frequent tasks, and then see if the remaining tasks can fit into the idle slots. TC S(N), SC O(N).   
   1. First count the number of occurrences of each task.   
   1. Let the max frequency seen be M for task T
   1. We can schedule the first M-1 occurrences of T, each T will be followed by at least N CPU cycles in between successive schedules of T. Total CPU cycles after scheduling M-1 occurrences of T = (M-1) * (N + 1) // 1 comes for the CPU cycle for T itself
   1. Now schedule the final round of tasks. We will need at least 1 CPU cycle of the last occurrence of T. If there are multiple tasks with frequency M, they will all need 1 more cycle. Run through the frequency dictionary and for every element which has frequency == M, add 1 cycle to result.
   1. In the end, If we have more number of tasks than the max slots we need as computed above we will return the length of the tasks array as we need at least those many CPU cycles.   
   <details>
    
      ```python
       def leastInterval(self, tasks: List[str], n: int) -> int:
           counter = Counter(tasks)
           maxFreq = max(counter.values())
           result = (maxFreq - 1) * (n + 1)
           for taskName, freq in counter.items():
               if freq == maxFreq:
                   result += 1
           
           return max(len(tasks), result)
      ```
   </details>  

1. 496 Next Greater Element I  
***Approach 1*** 
Key observation:  
Suppose we have a decreasing sequence followed by a greater number  
For example [5, 4, 3, 2, 1, 6] then the greater number 6 is the next greater element for all previous numbers in the sequence.  
We use a stack to keep a decreasing sub-sequence, whenever we see a number x greater than stack.peek() we pop all elements less than x and for all the popped ones, their next greater element is x. For example [9, 8, 7, 3, 2, 1, 6] The stack will first contain [9, 8, 7, 3, 2, 1] and then we see 6 which is greater than 1 so we pop 1 2 3 whose next greater element should be 6. TC S(Nums2 length), SC O(Nums2 length)  
   <details>
    
      ```python
       def nextGreaterElement(self, nums1: List[int], nums2: List[int]) -> List[int]:
           stack = []
           nextGreater = {}
           for num in nums2:
               while stack and stack[-1] < num:
                   nextGreater[stack.pop()] = num
               stack.append(num)
           
           result = [-1] * len(nums1)
           for i, num in enumerate(nums1):
               if num in nextGreater:
                   result[i] = nextGreater[num]
           
           return result
      ```
   </details>  

1. 503 Next Greater Element II
***Approach 1*** Keep a stack with indexes, and the number that the index represent are in decreasing order from bottom to top. TC O(N), SC O(N)  
   <details>
    
      ```python
       def nextGreaterElements(self, nums: List[int]) -> List[int]:
           stack = []
           numsLen = len(nums)
           result = [-1] * numsLen
           for i in range(numsLen * 2):
               num = nums[i % numsLen]
               while stack and nums[stack[-1]] < num:
                   result[stack.pop()] = num
   
               if i < numsLen:
                   stack.append(i)
           
           return result
      ```
   </details>  

1. 50 Pow(x, n) should solve the problem both recursively and iteratively
1. 88 Merge Sorted Array 
1. Find First and Last Position of Element in Sorted Array  
Binary search

1. 424 Longest Repeating Character Replacement  
Key observation is that the longest substring should consists characters that appears more often, and then replace the less frequent ones. So the idea is to expand the window of substrings that has k chracters to replace. We maintain a window of substring, and the most frequent character in that substring. Use left pointer for start of the window, and right pinter for end of the window. Loop all characters, in each iteration increase frequency of right character, and update max frequency if necessary. If there are more chracters to replace than k, i.e. the window is invalid, (start - end + 1 > maxFreq + k), advance left pointer. Then the window should be valid, so update maxLen if necessary. In the end, return maxLen. TC O(N), SC O(N)
   <details>
    
      ```python
       def characterReplacement(self, s: str, k: int) -> int:
           counter = Counter()
           left = 0
           maxFreq = 0
           maxLen = 0
           for right in range(len(s)):
               counter[s[right]] += 1
               if counter[s[right]] > maxFreq:
                   maxFreq = counter[s[right]]
   
               if right - left + 1 > maxFreq + k:
                   counter[s[left]] -= 1
                   left += 1
               
               maxLen = max(maxLen, right - left + 1)
           return maxLen
      ```
   </details>  

1. 973 K Closest Points to Origin  
***Use heap but should learn quick select later***

1. 1570 Dot Product of Two Sparse Vectors  
Approach 1 - Save a list of index and value pairs for non zero element. If only one vector is sparse, apply binary search to find its idx  
Approach 2 - Use hash map to store index and value   

    <details>
    
      ```python
      # Save a list of index and value pairs
      class SparseVector:
          def __init__(self, nums: List[int]):
              self.nonZeroIdxVal = []
              for i, n in enumerate(nums):
                  self.nonZeroIdxVal.append((i, n))
              
              
      
          # Return the dotProduct of two sparse vectors
          def dotProduct(self, vec: 'SparseVector') -> int:
              result = 0
              i = 0
              j = 0
              while i < len(self.nonZeroIdxVal) and j < len(vec.nonZeroIdxVal):
                  ownIdxVal = self.nonZeroIdxVal[i]
                  otherIdxVal = vec.nonZeroIdxVal[j]
                  if ownIdxVal[0] == otherIdxVal[0]:
                      result += ownIdxVal[1] * otherIdxVal[1]
                      i += 1
                      j += 1
                  elif otherIdxVal[0] < otherIdxVal[0]:
                      i += 1
                  else:
                      j += 1
              
              return result

      # Binary Search
      class SparseVector:
          def __init__(self, nums: List[int]):
              self.nonZeroIdxVal = []
              for i, n in enumerate(nums):
                  self.nonZeroIdxVal.append((i, n))
              
          def dotProduct(self, vec: 'SparseVector') -> int:
              result = 0
              if len(self.nonZeroIdxVal) > len(vec.nonZeroIdxVal):
                  return vec.dotProduct(self.nonZeroIdxVal)        
      
              for i, idxVal in enumerate(self.nonZeroIdxVal):
                  idx = self.__findIdx(vec.nonZeroIdxVal, idxVal[0])
                  result += idxVal[1] * vec.nonZeroIdxVal[idx][1]
              
              return result
          
          def __findIdx(self, idxValList, idx):
              left = 0
              right = len(idxValList) - 1
              while left <= right:
                  mid = left + (right - left) // 2
                  midIdxVal = idxValList[mid]
                  if midIdxVal[0] == idx:
                      return mid
                  elif midIdxVal[0] < idx:
                      left = mid + 1
                  else:
                      right -= 1
              
              return -1

      # Use Hash map
      class SparseVector:
          def __init__(self, nums: List[int]):
              self.nonZeroIdxValMap = {}
              for i, num in enumerate(nums):
                  if num != 0:
                      self.nonZeroIdxValMap[i] = num
              
              
      
          # Return the dotProduct of two sparse vectors
          def dotProduct(self, vec: 'SparseVector') -> int:
              result = 0
              for i, num in vec.nonZeroIdxValMap.items():
                  if i in self.nonZeroIdxValMap:
                      result += num * self.nonZeroIdxValMap[i]
              return result      
      ```
   </details>  

1. 543 Diameter of Binary Tree
1. 1213 Intersection of Three Sorted Arrays  
1. [71. Simplify Path](https://leetcode.com/problems/simplify-path)
1. [560. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k)
1. [523. Continuous Subarray Sum](https://leetcode.com/problems/continuous-subarray-sum)   
1. [938. Range Sum of BST](https://leetcode.com/problems/range-sum-of-bst) 
1. [162. Find Peak Element](https://leetcode.com/problems/find-peak-element/) 
1. [202. Happy Number](https://leetcode.com/problems/happy-number)
1. [314. Binary Tree Vertical Order Traversal](https://leetcode.com/problems/binary-tree-vertical-order-traversal)
1. [987. Vertical Order Traversal of a Binary Tree](https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree)
1. [408. Valid Word Abbreviation](https://leetcode.com/problems/valid-word-abbreviation)
1. [1249. Minimum Remove to Make Valid Parentheses](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/) 
1. [680 Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii)
1. [1650. Lowest Common Ancestor of a Binary Tree III](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree-iii)
1. [227. Basic Calculator II](https://leetcode.com/problems/basic-calculator-ii)  
1. [528. Random Pick with Weight](https://leetcode.com/problems/random-pick-with-weight)
1. [339. Nested List Weight Sum](https://leetcode.com/problems/nested-list-weight-sum)
1. [791. Custom Sort String](https://leetcode.com/problems/custom-sort-string) 
1. [249. Group Shifted Strings](https://leetcode.com/problems/group-shifted-strings)
1. [146. LRU Cache](https://leetcode.com/problems/lru-cache)
1. [266. Palindrome Permutation](https://leetcode.com/problems/palindrome-permutation)  
1. [958. Check Completeness of a Binary Tree](https://leetcode.com/problems/check-completeness-of-a-binary-tree/)
1. [636. Exclusive Time of Functions](https://leetcode.com/problems/exclusive-time-of-functions)
1. [1331. Rank Transform of an Array](https://leetcode.com/problems/rank-transform-of-an-array)
1. [109. Convert Sorted List to Binary Search Tree](https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree)
1. [986. Interval List Intersections](https://leetcode.com/problems/interval-list-intersections)
1. [670. Maximum Swap](https://leetcode.com/problems/maximum-swap)
1. [1740. Find Distance in a Binary Tree](https://leetcode.com/problems/find-distance-in-a-binary-tree)  
1. [219. Contains Duplicate II](https://leetcode.com/problems/contains-duplicate-ii)  
1. [401. Binary Watch](https://leetcode.com/problems/binary-watch)
1. [26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array)
1. [448. Find All Numbers Disappeared in an Array](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array)
1. [921. Minimum Add to Make Parentheses Valid](https://leetcode.com/problems/minimum-add-to-make-parentheses-valid)
1. [708. Insert into a Sorted Circular Linked List](https://leetcode.com/problems/insert-into-a-sorted-circular-linked-list)
1. [234. Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list)
1. [647. Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings)
1. [766. Toeplitz Matrix](https://leetcode.com/problems/toeplitz-matrix)
1. [516. Longest Palindromic Subsequence](https://leetcode.com/problems/longest-palindromic-subsequence) 
 
# Not high-frequency
1. [233. Number of Digit One](https://leetcode.com/problems/number-of-digit-one)
 
# Difficult to work on later
1. [549. Binary Tree Longest Consecutive Sequence II](https://leetcode.com/problems/binary-tree-longest-consecutive-sequence-ii)
1. [1081. Smallest Subsequence of Distinct Characters](https://leetcode.com/problems/smallest-subsequence-of-distinct-characters), same as 316
1. [865. Smallest Subtree with all the Deepest Nodes](https://leetcode.com/problems/smallest-subtree-with-all-the-deepest-nodes)
