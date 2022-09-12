## python syntax
### counter
```
c = Counter(['eggs', 'ham'])
```

### conditional expression
```
sign = [1,-1][x < 0]
# or sign = 1 if x > 0 else -1
```

### sort with different key
```
intervals.sort(key = lambda x: (x[0], -x[1]))
```

### heap and deque
```
from collections import deque
numbers = deque([1, 2, 3, 4])
numbers.popleft()
numbers.appendleft(2)
```
```
import heapq
queue = []
heappush(queue, val)
heappop(queue)      
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
