## max-area-of-island
### my ans
```
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        maxArea = 0
        
        for i in range(len(grid)):
            for j in range(len(grid[i])):
                if grid[i][j] == 1:
                    subArea = self.helper(grid, i, j)
                    maxArea = max(maxArea, subArea)
        return maxArea
    
    def helper(self, grid, i, j) -> int:
        if not 0 <= i < len(grid) or not 0 <= j < len(grid[i]) or not grid[i][j] == 1:
            return 0
        else:
            grid[i][j] = -1
            ans = 1
            ans += self.helper(grid, i+1, j)
            ans += self.helper(grid, i-1, j)   
            ans += self.helper(grid, i, j+1)
            ans += self.helper(grid, i, j-1)  
            
            return ans
```
