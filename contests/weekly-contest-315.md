## largest-positive-integer-that-exists-with-its-negative
### my-ans
```
class Solution:
    def findMaxK(self, nums: List[int]) -> int:
        d = {}
        res = -1
        
        for num in nums:
            if num > 0:
                if d.get(-num) != None:
                    res = max(res, num)
                else:   
                    d[num] = True
            else:
                if d.get(-num) != None:
                    res = max(res, -num)
                else:
                    d[num] = True

        return res
```

## count-number-of-distinct-integers-after-reverse-operations
### my-ans
```
class Solution:
    def countDistinctIntegers(self, nums: List[int]) -> int:
        seen = set(nums)
        
        for num in nums:
            seen.add(int(str(num)[::-1]))
        
        return len(seen)
            
```

## sum-of-number-and-its-reverse
### my-ans
```
class Solution:
    def sumOfNumberAndReverse(self, num: int) -> bool:
        if num == 0:
            return True
        
        for i in range(num):
            if i + int(str(i)[::-1]) == num:
                return True
        return False
```
