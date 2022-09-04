## longest-subsequence-with-limited-sum
### my-ans
```
class Solution:
    def answerQueries(self, nums: List[int], queries: List[int]) -> List[int]:
        nums.sort()
        res = []
        
        for query in queries:
            currentSum = 0
            for i, num in enumerate(nums):
                if currentSum + num > query:
                    res.append(i)
                    break
                else:
                    currentSum += num
                    if i == len(nums) -1:
                        res.append(i+1)
        
        return res
```

## removing-stars-from-a-string
### my-ans
```
class Solution:
    def removeStars(self, s: str) -> str:
        stack = []
        
        for char in s:
            if char == "*":
                stack.pop()
            else:
                stack.append(char)
        
        return "".join(list(stack))
```

## minimum-amount-of-time-to-collect-garbage
### my-ans
```
class Solution:
    def garbageCollection(self, garbage: List[str], travel: List[int]) -> int:
        d = {}
        lastStop = {}
        
        for i, stop in enumerate(garbage):
            for char in stop:
                d[char] = d.get(char, 0) + 1
                lastStop[char] = i-1
        
        totalTravelTime = 0
        for k in lastStop:
            totalTravelTime += sum(travel[:lastStop.get(k)+1]) 
        
        totalPickUpTime = 0
        for k in d:
            totalPickUpTime += d.get(k)     
        
        return totalTravelTime + totalPickUpTime
```

## build-a-matrix-with-conditions
### my-ans
```
class Solution:
    def buildMatrix(self, k: int, rowConditions: List[List[int]], colConditions: List[List[int]]) -> List[List[int]]:
        G = [[] for i in range(k+1)]
        degree = [0] * (k+1)
        degreeCol = [0] * (k+1)

        for row in rowConditions:
            G[row[1]].append(row[0])
            degree[row[0]] += 1
            
        bfs = [i for i in range(1,k+1) if degree[i] == 0]
        for i in bfs:
            for j in G[i]:
                degree[j] -= 1
                if degree[j] == 0:
                    bfs.append(j)
        
        bfs = bfs[::-1] 
        
        G = [[] for i in range(k+1)]
        for col in colConditions:
            G[col[1]].append(col[0])
            degreeCol[col[0]] += 1
            
        bfsCol = [i for i in range(1,k+1) if degreeCol[i] == 0]
        for i in bfsCol:
            for j in G[i]:
                degreeCol[j] -= 1
                if degreeCol[j] == 0:
                    bfsCol.append(j)
        
        bfsCol = bfsCol[::-1] 
        
        if len(bfsCol) != k or len(bfs) != k :
            return []
        
        d = {} # key, [row, col]
        
        for i, row in enumerate(bfs):
            if row == 0: continue
            d[row] = [i]
        for j, col in enumerate(bfsCol):
            if col == 0: continue
            d[col] = d.get(col) + [j]   
        
        res = [[0 for _ in range(k)]for _ in range(k)]
        
        for k in d:
            coord = d.get(k)
            res[coord[0]][coord[1]] = k
        
        return res        
```
