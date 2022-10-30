## determine-if-two-events-have-conflict
### my-ans
```
class Solution:
    def haveConflict(self, event1: List[str], event2: List[str]) -> bool:
        if event1[0] > event2[0]:
            event1, event2 = event2, event1
        
        if event2[0] <= event1[1]:
            return True
        else:
            return False
```

## number-of-subarrays-with-gcd-equal-to-k
### my-ans-TLE
```
class Solution:
    def subarrayGCD(self, nums: List[int], k: int) -> int:
        def dfs(nums, path, res):
            if not nums:
                return

            for i in range(len(nums)):
                if nums[i] % k == 0:
                    res.append(nums[:i+1])
                else:
                    break
            dfs(nums[1:], [], res)                

        def gcd (a,b):
            if (b == 0):
                return a
            else:
                 return gcd (b, a % b)
        
        res = []
        dfs(nums, [], res)
        
        ctr = 0
        for i in range(len(res)):
            if k in res[i]:
                ctr += 1
            else:
                tmp = res[i][0]
                for c in res[i]:
                    tmp = gcd(tmp , c)    
                if tmp == k:
                    ctr += 1
        return ctr
```

## minimum-cost-to-make-array-equal
### my-ans-TLE
```
class Solution:
    def minCost(self, nums: List[int], cost: List[int]) -> int:     
        dp = [0] * len(nums)
        for i in range(len(dp)):          
            for j in range(len(nums)):
                dp[i] += abs(nums[j]-nums[i]) * cost[j]
        return min(dp)
    
    def minCostTLE(self, nums: List[int], cost: List[int]) -> int:
        minV = nums[0]
        maxV = nums[0]
        
        for num in nums:
            minV = min(minV, num)
            maxV = max(maxV, num)
        
        if minV == maxV:
            return 0
        
        dp = [0] * (maxV-minV+1)
        for i in range(len(dp)):
            target = minV + i
            
            for j in range(len(nums)):
                dp[i] += abs(nums[j]-target) * cost[j]
        
        return min(dp)
```
