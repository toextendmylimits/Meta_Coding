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

1. 29 Divide Two Integers
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

1. 129 Sum Root to Leaf Numbers  
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
