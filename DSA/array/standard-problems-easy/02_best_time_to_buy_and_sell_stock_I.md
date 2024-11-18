# Best time to buy and sell stock I

<span style="padding: 4px 8px; background-color: green; color: white;">Easy</span>

You are given an array prices where prices[i] is the price of a given stock on the ith day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

### Example 1

**Input**: prices = [7,1,5,3,6,4]

**Output**: 5

**Explanation**: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.

### Example 2

**Input**: prices = [7,6,4,3,1]

**Output**: 0

**Explanation**: In this case, no transactions are done and the max profit = 0.

**Constraints**:

1 <= prices.length <= 105

0 <= prices[i] <= 104

```Java
class Solution {
    public int maxProfit(int[] prices) {
        if(prices == null || prices.length == 0){
            return 0;
        }
        
        int mini = prices[0];
        int maxProfit = 0;

        for(int i=1; i<prices.length; i++){
            int cost = prices[i] - mini;
            maxProfit = Math.max(maxProfit, cost);
            mini = Math.min(mini, prices[i]);
        }

        return maxProfit;
    }
}
```

## Approach
- if you buy it on the `ith` day
- you sell it on the day falling in the range; 1st price till (i - 1)th Day
- i.e. 1st element to (i-1) element (day before selling)

### Algorithm

1. mark minimum price at 0th index (first element), let profit = 0
2. iterate from the second element
    1. calculate cost = prices[i] - minimum price
    2. calculate profit = maximum of (current profit, cost)
    3. calculate minimum price = minimum of (current minimum price, price[i])
3. return the profit
