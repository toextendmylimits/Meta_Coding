# A list of Meta high-frequency coding questions 

1. 199. Binary Tree Right Side View Variation
   TC O(N) N is number of nodes since one has to visit each node, SC is O(D) to keep the queues, where D is a tree diameter.
     <details>
         
         ```python
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
         ```
       </details>
