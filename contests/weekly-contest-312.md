## sort-the-people
### my-ans
```
class Solution:
    def sortPeople(self, names: List[str], heights: List[int]) -> List[str]:
        merged = []
        
        for i in range(len(names)):
            merged.append([heights[i], names[i]])
            
        merged.sort(reverse=True)
        res = []
        for item in merged:
            res.append(item[1])
        return res
        
```

## longest-subarray-with-maximum-bitwise-and
### my-ans
```
class Solution:
    def longestSubarray(self, nums: List[int]) -> int:
        maxV = max(nums)
        dp = [1 for _ in range(len(nums))]
        
        for i in range(1, len(nums)):
            if nums[i] == nums[i-1]:
                dp[i] = dp[i-1] + 1
        
        res = 1
        for i in range(1, len(nums)):
            if nums[i] == maxV:
                res = max(res, dp[i])
        return res
```
