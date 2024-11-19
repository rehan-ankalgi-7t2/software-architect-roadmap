# Best time to buy and sell stock II

<span style="padding: 4px 8px; background-color: #ffbb00; color: white;">Medium</span>

`Dynamic Programming` `stocks` `recursion`

You are given an integer array `prices` where `prices[i]` is the price of a given stock on the ith day.

On each day, you may decide to buy and/or sell the stock. You can only hold at most one share of the stock at any time. However, you can buy it then immediately sell it on the same day.

Find and return the maximum profit you can achieve.

### Example 1
```
Input: prices = [7,1,5,3,6,4]
Output: 7

Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
Total profit is 4 + 3 = 7.
```

### Example 2
```
Input: prices = [1,2,3,4,5]
Output: 4

Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
Total profit is 4.
```

### Example 3

```
Input: prices = [7,6,4,3,1]
Output: 0

Explanation: There is no way to make a positive profit, so we never buy the stock to achieve the maximum profit of 0.
```

**Constraints**:

`1 <= prices.length <= 105`

`0 <= prices[i] <= 104`

```Java
class Solution {
    public int f(int index, int isBuy, int[] prices, int[][] dp) {
        // Base case: if we reach the end of the array
        if (index == prices.length) {
            return 0;
        }

        // Check if the result is already computed
        if (dp[index][isBuy] != -1) {
            return dp[index][isBuy];
        }

        int profit = 0;

        if (isBuy == 1) {
            // Two choices: Buy or Skip
            profit = Math.max(
                -prices[index] + f(index + 1, 0, prices, dp), // Buy
                0 + f(index + 1, 1, prices, dp)               // Skip
            );
        } else {
            // Two choices: Sell or Skip
            profit = Math.max(
                prices[index] + f(index + 1, 1, prices, dp),  // Sell
                0 + f(index + 1, 0, prices, dp)               // Skip
            );
        }

        // Store the result in dp array
        dp[index][isBuy] = profit;

        return profit;
    }
    
    
    public int maxProfit(int[] prices) {
        int n = prices.length;
        // Create a memoization table initialized to -1
        int[][] dp = new int[n][2];
        for (int i = 0; i < n; i++) {
            dp[i][0] = -1;
            dp[i][1] = -1;
        }
        return f(0, 1, prices, dp);
    }
}
```

## Approach

- in this problem there are a lot of ways in which buying and selling actions can be performed
- Lots of ways -> try all the possible ways (`recursion`) -> select the best solution

- [x] write a recurrence relation -> express everything in terms in index
- [x] maintain a boolean variable which indicates whether buying is allowed or not
- [x] take the max of all profits made
- [x] write a base case

### Algorithm

```
// recurrence relation
function(index, isBuy){
    // base case
    if(index == n){
        return 0;
    }

    // all possibilities
    if(isBuy){
        profit = max(
            -prices[index] + function(index+1, 0) //buy, 
            0 + function(index+1, 0) // not buy
            ) // max of profit
    } else {
        profit = max(
            prices[index] + function(index+1, 1) //sell, 
            0 + function(index+1, 0) // not sell
            ) // max of profit
    }

    return profit
}
```

`TC: O(2n)`