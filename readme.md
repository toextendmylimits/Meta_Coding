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
Approach 1 is to look from right to left, and maintain maxRight, if a building is larger than maxRight, add its index to the  result, and update maxRight. In the end, reverse result. TC O(N), SC O(1)  
Approach 2 is to look from left to right, if a building is blocked by current building, remove it from the result, otherwise add its index to the result. TC O(N), SC O(N)

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
              if topMostNode.right:
                  self.pushLeftChildren(topMostNode.right)
      
              return topMostNode.val       
      
          def hasNext(self) -> bool:
              return len(self.stack) > 0       
      ```
   </details>   

 1. 129 Sum Root to Leaf Numbers  
***Approach 1*** is to calculate sum in recursive preorder traversal. In each recursion call, the passed parameter is node and pathSum, return 0 if node is null; otherwise increase pathSum considering node value, then return pathSum if node is leaf; Otherwise recursively call left child and right child with pathSum, add them and then return. TC O(N) SC O(N)  
***Approach 2*** Iterative preorder traversal. Use a stack to store pair of node and current path sum. In each iteration, pop pair of node and curr path sum, then increase path sum considering node value. If node is leaf, then add it to total sum. If node's right is not null, add it to stack; If node.s left is not null, add it to stack.
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
              if topMostNode.right:
                  self.pushLeftChildren(topMostNode.right)
      
              return topMostNode.val       
      
          def hasNext(self) -> bool:
              return len(self.stack) > 0       
      ```
   </details>   
   
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
