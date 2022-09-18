## smallest-even-multiple
### my-ans
```
def smallestEvenMultiple(self, n: int) -> int:
    for i in range(n, n*2+1):
        if i % 2 == 0 and i % n == 0:
            return i        
```

## length-of-the-longest-alphabetical-continuous-substring
### my-ans
```
def longestContinuousSubstring(self, s: str) -> int:
    dp = [1 for _ in range(len(s))]
    res = s[0]
    current = s[0]

    for i in range(1, len(s)):
        if ord(s[i]) - ord(s[i-1]) == 1:
            dp[i] += dp[i-1]
            current += s[i]
        else:
            current = s[i]
        if len(current) > len(res):
            res = current

    return  len(res)
```

## reverse-odd-levels-of-binary-tree
### my-ans
```
def reverseOddLevels(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
    queue = [root]
    level = 0

    while True and queue:
        newQueue = []
        value = []    

        while queue:
            node = queue.pop()
            if node.left:
                newQueue.append(node.left)
                value.append(node.left.val)                    
            if node.right:
                newQueue.append(node.right)
                value.append(node.right.val)                 

        if level % 2 == 0:
            value = value[::-1]
            i = 0
            for node in newQueue:
                node.val = value[i]
                i += 1
        level += 1
        queue = newQueue

    return root
```

## sum-of-prefix-scores-of-strings
### my-ans
```
def sumPrefixScores(self, words: List[str]) -> List[int]:
    root = {}

    for word in words:
        cur = root
        for c in word:
            if not c in cur:
                cur[c] = {}
            cur = cur[c]
            cur["words"] = cur.get("words", 0) + 1

    res = [0 for _ in range(len(words))]
    for i, word in enumerate(words):
        cur = root
        for c in word:
            cur = cur[c]     
            res[i] += cur.get("words")              

    return res
```
