## partition-equal-subset-sum
### ans
```
public boolean canPartition(int[] nums) {
    int sum = 0;
    
    for (int num : nums) {
        sum += num;
    }
    
    if ((sum & 1) == 1) {
        return false;
    }
    sum /= 2;
    
    int n = nums.length;
    boolean[] dp = new boolean[sum+1];
    Arrays.fill(dp, false);
    dp[0] = true;
    
    for (int num : nums) {
        for (int i = sum; i > 0; i--) {
            if (i >= num) {
                dp[i] = dp[i] || dp[i-num];
            }
        }
    }
    
    return dp[sum];
}
```

## best-time-to-buy-and-sell-stock-with-cooldown
### ans
```
class Solution {
    public int maxProfit(int[] prices) {
        if(prices == null || prices.length == 0) return 0;
        
        int n = prices.length;
        int[] M = new int[n];
        for(int i = 0; i < n; i++){
            if(i == 0) M[0] = 0;
            else if(i == 1) M[1] = Math.max(prices[1] - prices[0], 0);
            else{
                M[i] = M[i - 1];
                // linear scan
                for(int j = 0; j < i; j++){
                    int prev = j >= 2 ? M[j - 2] : 0;
                    M[i] = Math.max(M[i], prev + prices[i] - prices[j]);
                }
            }
        }
                
        return M[n - 1];
    }
}
```
## coin-change
### ans
```
class Solution {
public:
    int coinChange(vector<int>& coins, int n) {
        // creating the base dp array, with first value set to 0
        int dp[++n];
        dp[0] = 0;
        // more convenient to have the coins sorted
        sort(begin(coins), end(coins));
        // populating our dp array
        for (int i = 1; i < n; i++) {
            // setting dp[0] base value to 1, 0 for all the rest
            dp[i] = INT_MAX;
            for (int c: coins) {
                if (i - c < 0) break;
                // if it was a previously not reached cell, we do not add use it
                if (dp[i - c] != INT_MAX) dp[i] = min(dp[i], 1 + dp[i - c]);
            }
        }
        return dp[--n] == INT_MAX ? -1 : dp[n];
    }
};
```
