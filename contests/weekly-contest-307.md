## minimum-hours-of-training-to-win-a-competition
### my-ans
```
class Solution:
    def minNumberOfHours(self, initialEnergy: int, initialExperience: int, energy: List[int], experience: List[int]) -> int:
        totalEngryNeed = sum(energy)
        minNumberOfHoursEnergy = max(0, totalEngryNeed + 1 - initialEnergy)
        
        minNumberOfHoursExp = 0
        accumulatedExp = 0
        for exp in experience:
            if not initialExperience + accumulatedExp + minNumberOfHoursExp >=  exp + 1:
                minNumberOfHoursExp = max(minNumberOfHoursExp, exp + 1 - (initialExperience + accumulatedExp))
            accumulatedExp += exp
    
        return minNumberOfHoursEnergy + minNumberOfHoursExp
```

## amount-of-time-for-binary-tree-to-be-infected
### my-ans
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def amountOfTime(self, root: Optional[TreeNode], start: int) -> int:
        parent = {} # child, parent
        
        infectedNode = None
        checkStack = deque([root])
        while checkStack:
            node = checkStack.popleft()
            if node == None:
                continue
            if node.val == start:
                infectedNode = node
                break
            else:
                if node.left:
                    checkStack.append(node.left)
                    parent[node.left.val] = node
                if node.right:
                    checkStack.append(node.right)
                    parent[node.right.val] = node
                
        stack = deque([infectedNode])
        infected = set([infectedNode.val]) 
        res = 0
        while stack:
            for i in range(len(stack)):
                node = stack.popleft()
                infected.add(node.val)
                parentNode = parent.get(node.val)
                if parentNode != None and not parentNode.val in infected:
                    stack.append(parent.get(node.val))
                if node.left and not node.left.val in infected:
                    stack.append(node.left)
                if node.right and not node.right.val in infected:
                    stack.append(node.right)
            res += 1
    
        return res -1 
```
## largest-palindromic-number
### my-ans
```
class Solution:
    def largestPalindromic(self, num: str) -> str:
        d = {}
        s = set()
        for digit in num:
            d[int(digit)] = d.get(int(digit), 0) + 1
            s.add(int(digit))
        s = sorted(s)
        res = ""

        s = s[::-1]
        for digit in s:
            counter = d.get(digit)
            if counter >= 2:
                while counter >=2:
                    res = res + str(digit) 
                    counter -= 2
                d[digit] = counter
        res += res[::-1]
        if not res or int(res) == 0:
            res = ""
        
        # larget -> small
        for digit in s:
            if d.get(digit) % 2 == 1:
                res = res[:len(res)//2] + str(digit) + res[len(res)//2:]
                break
        if not res:
            return "0"
        return res
```
