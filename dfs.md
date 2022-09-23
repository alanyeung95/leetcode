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

## bfs vs dfs

### Data Structure	
BFS(Breadth First Search) uses Queue data structure for finding the shortest path.	DFS(Depth First Search) uses Stack data structure.

### Definition	
BFS is a traversal approach in which we first walk through all nodes on the same level before moving on to the next level.  	DFS is also a traversal approach in which the traverse begins at the root node and proceeds through the nodes as far as possible until we reach the node with no unvisited nearby nodes.

### Suitable for	
BFS is more suitable for searching vertices closer to the given source.	DFS is more suitable when there are solutions away from source.

### Decision Trees
BFS considers all neighbors first and therefore not suitable for decision-making trees used in games or puzzles.	DFS is more suitable for game or puzzle problems. We make a decision, and the then explore all paths through this decision. And if this decision leads to win situation, we stop.

### Optimality	
BFS is optimal for finding the shortest path.	DFS is not optimal for finding the shortest path.

## Speed	
BFS is slow as compared to DFS.	DFS is fast as compared to BFS.

## When to use?	
When the target is close to the source, BFS performs better. 	When the target is far from the source, DFS is preferable. 
