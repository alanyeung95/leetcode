## most-frequent-even-element
### my-ans
```
class Solution:
    def mostFrequentEven(self, nums: List[int]) -> int:
        d = {}
        
        for num in nums:
            if num % 2 == 0:
                d[num] = d.get(num, 0) + 1
        
        minV = float('inf')
        minCount = 0
        
        if len(d) == 0:
            return -1
        
        for k in d:
            if d.get(k) > minCount:
                minV = k
                minCount = d.get(k)
            elif d.get(k) == minCount:
                if k < minV:
                    minV = k
                    minCount = d.get(k)                    
                
        return minV
```

## optimal-partition-of-string
### my-ans
```
class Solution:
    def partitionString(self, s: str) -> int:
        res = 1
        current = ""
        
        for c in s:
            if not c in current:
                current += c
            else:
                res += 1
                current = c
        
        return res
```

## divide-intervals-into-minimum-number-of-groups
### my-ans
```
class Solution:
    def minGroups(self, intervals: List[List[int]]) -> int:
        intervals.sort(key = lambda x: x[0])
        stack = []

        for interval in intervals:
            if not stack:
                heappush(stack, interval[1])
            else:
                if interval[0] > stack[0]:
                    heappop(stack)                   
                heappush(stack, interval[1])

        return len(stack)
```
