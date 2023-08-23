## total-distance-traveled
### my-ans
```
class Solution:
    def distanceTraveled(self, mainTank: int, additionalTank: int) -> int:
        res = 0
        
        while mainTank >= 5 and additionalTank:
            fuelUsage = min(5, mainTank)
            
            res += fuelUsage*10
            mainTank -= fuelUsage
            additionalTank-=1
            mainTank+=1
                        
        if mainTank:
            res += mainTank*10
        
        return res
```

## find-the-value-of-the-partition
### my-ans
```
class Solution:
    def findValueOfPartition(self, nums: List[int]) -> int:
        nums.sort()
        
        minDiff = float('inf')
        
        for i in range(1, len(nums)):
            minDiff = min(minDiff, nums[i]- nums[i-1])

        return minDiff

```

## special-permutations
### my-ans-TLE
```
class Solution:
    def specialPerm(self, nums: List[int]) -> int:
        def backtracking(prevNum, nums) -> int:
            if len(nums) == 0:
                return 1
            
            total = 0
            
            for i in range(len(nums)):
                if prevNum % nums[i] == 0 or nums[i] % prevNum == 0:
                    total += backtracking(nums[i], nums[:i]+nums[i+1:])
            
            return total
        
        res = 0
        
        for i in range(len(nums)):
            res += backtracking(nums[i], nums[:i]+nums[i+1:])

        return res
```
