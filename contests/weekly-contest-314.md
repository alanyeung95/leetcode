## the-employee-that-worked-on-the-longest-task
### my-ans
```
    def hardestWorker(self, n: int, logs: List[List[int]]) -> int:
        prevT = 0
        maxT = 0
        res = 0
        
        for log in logs:
            t = log[1] - prevT
            if t > maxT:
                maxT = t
                res = log[0]
            elif t == maxT:
                maxT = t
                res = min(res, log[0])              
            prevT = log[1]
        
        return res
```

## find-the-original-array-of-prefix-xor
### my-ans
```
    def findArray(self, pref: List[int]) -> List[int]:
        res = [0] * len(pref)
        res[0] = pref[0]
        prev = res[0] 
        
        for i in range(1, len(pref)):
            res[i] = pref[i] ^ prev
            prev = res[i] ^ prev
        return res
```
## paths-in-matrix-whose-sum-is-divisible-by-k
### my-ans-TLE
```
    def numberOfPaths(self, grid: List[List[int]], k: int) -> int:        
        def dfs(grid, row, col, k, pathSum, res):
            if row == len(grid)-1 and col == len(grid[0]) -1:
                if (pathSum + grid[row][col]) % k == 0:
                    res[0] += 1
                return
            
            if row >= len(grid) or col >= len(grid[0]):
                return
            
            dfs(grid, row+1, col, k, pathSum + grid[row][col], res)
            dfs(grid, row, col+1, k, pathSum + grid[row][col], res)
            
        res = [0]
        dfs(grid, 0, 0, k, 0, res)
        
        if res[0] >= pow(10,9) + 7:
            return (pow(10,9) + 7) % res[0]
        return res[0]
```
