## minimum-size-subarray-sum
### ans
```
public int minSubArrayLen(int s, int[] a) {
  if (a == null || a.length == 0)
    return 0;
  
  int i = 0, j = 0, sum = 0, min = Integer.MAX_VALUE;
  
  while (j < a.length) {
    sum += a[j++];
    
    while (sum >= s) {
      min = Math.min(min, j - i);
      sum -= a[i++];
    }
  }
  
  return min == Integer.MAX_VALUE ? 0 : min;
}
```

## longest-substring-without-repeating-characters
### ans
```
    def lengthOfLongestSubstring(self, s: str) -> int:
        seen = set()
        res = 0
        tailPtr = 0
        
        for c in s:
            while c in seen:
                seen.remove(s[tailPtr])
                tailPtr += 1            

            seen.add(c)
            res = max(res, len(seen))   
            
        return res
```
