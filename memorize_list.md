# Need to memorize answers for the following questions
1. [1570. Dot Product of Two Sparse Vectors](https://leetcode.com/problems/dot-product-of-two-sparse-vectors)  Need to break out of while loop once found the target index
2. [528. Random Pick with Weight](https://leetcode.com/problems/random-pick-with-weight) Beware if mid element > randNum, result = mid
3. [215. Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array) Practice quick select more.
4. [227. Basic Calculator II](https://leetcode.com/problems/basic-calculator-ii)  
   Should learn how to not use stack later.
5. [71. Simplify Path](https://leetcode.com/problems/simplify-path)  
   Remember to check whether stack is empty before popping. Also check not empty string and not . before adding to stack
6. [938. Range Sum of BST](https://leetcode.com/problems/range-sum-of-bst)
   Practice DFS more. Also practice BFS approach
7. [791. Custom Sort String](https://leetcode.com/problems/custom-sort-string/)
8. [670. Maximum Swap](https://leetcode.com/problems/maximum-swap)    
   Check digits[i] >= digits[right]. Don't neglect the ==  
   Use list(str(num)) to convert a number to string array. str(num).split() wouldn't really work.
9. [973. K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/) Learn quick select later.
10. [249. Group Shifted Strings](https://leetcode.com/problems/group-shifted-strings/)
11. [766. Toeplitz Matrix](https://leetcode.com/problems/toeplitz-matrix) Learn how to solve follow up questions later.
12. [31. Next Permutation](https://leetcode.com/problems/next-permutation) Very difficult so just memorize the code. Use example [2, 3, 6, 5, 4, 1]
13. [636. Exclusive Time of Functions](https://leetcode.com/problems/exclusive-time-of-functions) Very difficult. Practice more
19. [138. Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer) May learn approach of O(1) space later
20. [986. Interval List Intersections](https://leetcode.com/problems/interval-list-intersections) Difficult. Discard intervals based on end time
21. [23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists) Difficult. More practice.
22. [498. Diagonal Traverse](https://leetcode.com/problems/diagonal-traverse)  
    Refer https://leetcode.com/problems/diagonal-traverse/solutions/203060/java-solution-with-clear-explanation/  
    Very difficult.   
    for each even or odd diagonal, there are three cases:  
        1. there is room to go that direction   
        2. there is no row space to go further but there is col space   
        3. there is no col space to go further but there is row space 
24. [133. Clone Graph](https://leetcode.com/problems/clone-graph)  
    Difficult. Practice again.  

    Beware BFS, to always add neighbors regardless of whether the node has been copied before.   
25. [953. Verifying an Alien Dictionary](https://leetcode.com/problems/verifying-an-alien-dictionary) Should practice many more times to be super clear.
26. [523. Continuous Subarray Sum](https://leetcode.com/problems/continuous-subarray-sum) A little difficult. Practice more.
27. [173. Binary Search Tree Iterator](https://leetcode.com/problems/binary-search-tree-iterator)  Difficult. Practice many more times.
28. [163. Missing Ranges](https://leetcode.com/problems/missing-ranges/) Practice more to write code bug-free.
29. [38. Count and Say](https://leetcode.com/problems/count-and-say)  
   Difficult. Practice a few more times. 
30. [691. Stickers to Spell Word](https://leetcode.com/problems/stickers-to-spell-word/)
     Extremely difficult. Memorize the code. Refer https://leetcode.com/problems/stickers-to-spell-word/solutions/108333/rewrite-of-contest-winner-s-solution/
31. [426. Convert Binary Search Tree to Sorted Doubly Linked List](https://leetcode.com/problems/convert-binary-search-tree-to-sorted-doubly-linked-list)
32. [65. Valid Number](https://leetcode.com/problems/valid-number)  
   Very difficult. Refer https://leetcode.com/problems/valid-number/solutions/23942/ac-java-solution-with-clear-explanation/  
34. [139. Word Break](https://leetcode.com/problems/word-break/) Very difficult. Just memorize it
35. [140. Word Break II](https://leetcode.com/problems/word-break-ii/) Backtrack
36. [827. Making A Large Island](https://leetcode.com/problems/making-a-large-island)  
    https://leetcode.com/problems/making-a-large-island/solutions/127032/c-java-python-straight-forward-o-n-2-with-explanations/  
  Only 2 steps:
    1. Explore every island using DFS, count its area, give it an island index and save the result to a {index: area} map.
    1. Loop every cell == 0, check its connected islands and calculate total islands area.
37. [270. Closest Binary Search Tree Value](https://leetcode.com/problems/closest-binary-search-tree-value)
