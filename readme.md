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
***Approach 1*** The idea is to save the last day that a task is completed in a hash map to allow easy retrieval later. Use variable result to store current day initialize to 0. So looping through the tasks, for each task, if it is last executed, then it must be executed after enough days pass since its last completion, so should be the max value of current day, and previous completion day + space, with addition of 1; If the task has never been executed, then it be executed on next day which is current day plus 1. Then update the last day that a task is completed. In the end, return current day. TC O(N), SC O(N)  
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
***Approach 1*** The idea is to find the minimum number of slots to execute the most frequent tasks, and then see if the remaining tasks can fit into the idle slots. First find the frequency of each tasks, then find the max frequency. If the idle is n, so to execute the most frequent tasks, we can have maxFreq group. From 1st to maxFreq group, one task can be executed, and there are n idle slots which can be used for other tasks. From the maxFreq th step, most frequent task can be executed. Let use result for the minimum number of slots requited, to consider 1st to (maxFreq - 1)th group, result should be (maxFreq - 1) * (n + 1). Now loop through the tasks, for each task, if its frequency is equal to maxFreq, then increase result by 1. This is for the task to be executed at the last group. In the end, if result is less than len(tasks), which means all tasks can fit into the current idle, return result; Otherwise, that means the above idle is not enough, and the remaining tasks can be added to the existing groups, so return len(tasks). TC S(N), SC O(N)  
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
For example [5, 4, 3, 2, 1, 6] then the greater number 6 is the next greater element for all previous numbers in the sequence. We use a stack to keep a decreasing sub-sequence, whenever we see a number x greater than stack.peek() we pop all elements less than x and for all the popped ones, their next greater element is x. For example [9, 8, 7, 3, 2, 1, 6] The stack will first contain [9, 8, 7, 3, 2, 1] and then we see 6 which is greater than 1 so we pop 1 2 3 whose next greater element should be 6. TC S(Nums2 length), SC O(Nums2 length)  
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
