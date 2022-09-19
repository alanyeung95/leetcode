## python syntax

| counter |conditional expression | sort with different key
| ------------- | ------------- |  ------------- |
| ```c = Counter(['eggs', 'ham'])``` <br> ```c['eggs'] -= 1```<br> ```total = sum(c.values())``` | ```sign = [1,-1][x < 0]```  or <br> ```sign = 1 if x > 0 else -1```  | ```intervals.sort(key = lambda x: (x[0], -x[1]))```

| check is number  |  remove space |  int-char conversaion | limit decimal |
| ------------- | ------------- |------------- | ------------- |
| ```if c.isnumeric()```  |  ```newS = s.strip()``` | ```>>> chr(97) -> 'a'``` <br>``` >>> ord('a') -> 97```| ```print("%.2f" % a)``` |

| heap |  deque | Node class|  |
| ------------- | ------------- |------------- | ------------- |
``` from collections import deque``` <br> ```numbers = deque([1, 2, 3, 4])``` <br> ```numbers.popleft()``` <br> ```numbers.appendleft(2)``` |  ```import heapq``` <br> ```queue = []``` <br> ```heappush(queue, val)``` <br> ```heappop(queue)``` | ```class Node:```<br>```def __init__(self, val = 0, next = None):```<br>```self.val = val```<br>```self.next = next```<br><br>```a = Node(1)```
 | |



## topological-sort
```
def canFinishBFS(self, n, prerequisites):
    G = [[] for i in range(n)]
    inDegree = [0] * n
    for i, j in prerequisites:
        # [1, 0] means 1 depends on 0, so 1 -> 0
        G[i].append(j)
        inDegree[j] += 1
    bfs = [i for i in range(n) if inDegree[i] == 0]
    for i in bfs:
        for j in G[i]:
            inDegree[j] -= 1
            if inDegree[j] == 0:
                bfs.append(j)
    return len(bfs) == n
```

## binary-search
```
    def search(self, nums: List[int], target: int) -> int:
        left=0
        right=len(nums)-1
        while(left <= right):
            mid=(left+right)//2
            if nums[mid]==target:
                return mid
            elif nums[mid] < target:
                 left=mid+1
            else:
                right=mid-1
        return -1
```

## binary-tree-inorder
4,2,5,1,6,3,7

### iteratively   
```
def inorderTraversal(self, root):
    res, stack = [], []
    while True:
        while root:
            stack.append(root)
            root = root.left
        if not stack:
            return res
        node = stack.pop()
        res.append(node.val)
        root = node.right
``` 
        
## binary-tree-preorder
1,2,4,5,3,6,7

### iteratively
```
def preorderTraversal(self, root):
    stack, res = [root], []
    while stack:
        node = stack.pop()
        if node:
            res.append(node.val)
            stack.append(node.right)
            stack.append(node.left)
    return res            
```            

## binary-tree-postorder
4,5,2,6,7,3,1

### iteratively    
```    
def postorderTraversal(self, root):
    res, stack = [], [root]
    while stack:
        node = stack.pop()
        if node:
            res.append(node.val)
            stack.append(node.left)
            stack.append(node.right)
    return res[::-1]
```

## reverse-linked-list
```
def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
    prev = None
    current = head

    while current:
        next = current.next
        current.next = prev
        prev = current
        current = next

    return prev
```

## sliding-window
```
def lengthOfLongestSubstring(self, s: str) -> int:
    seen = set(), res = 0, tailPtr = 0
    for c in s:
        while c in seen:
            seen.remove(s[tailPtr])
            tailPtr += 1            
        seen.add(c)
        res = max(res, len(seen))   
    return res
```

## palindrome
```
class Solution(object):
    def longestPalindrome(self, s):
        res = ""
        for i in range(len(s)):
            res = max(self.helper(s,i,i), self.helper(s,i,i+1), res, key=len)
        return res
    def helper(self,s,l,r):     
        while 0<=l and r < len(s) and s[l]==s[r]:
                l-=1; r+=1
        return s[l+1:r]          
```

## quicksort
```
def partition(l, r, nums):
    # Last element will be the pivot and the first element the pointer
    pivot, ptr = nums[r], l
    for i in range(l, r):
        if nums[i] <= pivot:
            nums[i], nums[ptr] = nums[ptr], nums[i]
            ptr += 1
    nums[ptr], nums[r] = nums[r], nums[ptr]
    return ptr
def quicksort(l, r, nums):
    if len(nums) == 1:  # Terminating Condition for recursion. VERY IMPORTANT!
        return nums
    if l < r:
        pi = partition(l, r, nums)
        quicksort(l, pi-1, nums)  # Recursively sorting the left values
        quicksort(pi+1, r, nums)  # Recursively sorting the right values
    return nums
```
