## number-of-common-factors
### my-ans
```
    def commonFactors(self, a: int, b: int) -> int:
        if b > a:
            a, b = b, a
        res = 0
        for i in range(1, b+1):
            if a%i == 0 and b %i ==0:
                res += 1
        return res
```

## maximum-sum-of-an-hourglass
### my-ans
```
    def maxSum(self, grid: List[List[int]]) -> int:
        def calculate(i,j) -> int:
            if not i + 3 <= len(grid) and not j+3 <= len(grid[0]):
                return 0
            return sum(grid[i][j:j+3]) + grid[i+1][j+1] + sum(grid[i+2][j:j+3])
        res = 0
        for i in range(len(grid)-3+1):
            for j in range(len(grid[0])-3+1):   
                val = calculate(i,j)
                res = max(res, val)

        return res
```
