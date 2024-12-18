# Overview
We have an integer array prices listing the prices of items from a shop. Items can receive a special discount based on the price of the next item on the list that is less than or equal to it (if such an item exists). In other words, the discount for prices[i] is prices[j], where j > i, prices[j] <= prices[i], and j is the smallest such index that satisfies these conditions.

The task is to calculate the final price for each item, after applying this special discount, and return these final prices in an array called answer.

## Approach 1: `Brute-Force`
**Intuition**

Since the constraints are small, we can solve this problem using a brute-force approach. For each item in the prices array, we need to find a price that is smaller or equal to it and appears later in the array. This price will be our discount amount. We then subtract this discount from the original price to get the final discounted price.

To implement this, let's start by creating a copy of the prices array called result. We'll loop through the prices array and apply the discount we find for each element to the corresponding element in the result array.

For each element in the prices array, we'll run another loop starting from the next element to the right. If we find a price that is less than or equal to the current element, we'll subtract this price from the original price in the result array and stop looking further. If we don't find any suitable discount after checking all subsequent prices, the item's price in the result array will remain unchanged.

After processing all the prices in this manner, the result array will contain the final discounted prices for each item. We can then return this array as our answer.

### Algorithm
- Initialize a variable n to store the length of the input prices array.
- Initialize a result array by creating a copy of the input prices array. This ensures we have a copy of the original prices to work with.
- Start an outer loop that iterates from 0 to n - 1, with loop variable i:
  - Start an inner loop that iterates from index i + 1 to n - 1, with loop variable j.
    - If prices[j] is less than or equal to prices[i]:
      - Calculate the discounted price by subtracting prices[j] from prices[i].
      - Store the calculated discounted price in result[i].
      - Break the inner loop as we have found the first valid discount.
- Return the result array containing all final prices after discounts.

### Implementation
```Typescript
function finalPrices(prices: number[]): number[] {
    if (prices.length < 1 || prices === null) {
        return [];
    }

    let result: number[] = [];
    let i: number = 0;
    while (i < prices.length) {
        let j: number = i + 1;
        while (j > i && j < prices.length) {
            if (prices[j] <= prices[i]) {
                result.push(prices[i] - prices[j]);
                break;
            }
            j++;
        }
        if (j >= prices.length) {
            result.push(prices[i]);
        }
        i++;
    }

    return result;
};
```

### Complexity Analysis
Let n be the length of the input array prices.

Time complexity: O(n^2)

The algorithm uses two nested loops. The outer loop iterates through each element of the array, and for each element, the inner loop can potentially iterate through all remaining elements. In the worst case, where prices are in strictly increasing order, for each element i, we need to check all elements from i + 1 to n - 1. Thus, the time complexity is quadratic, O(n^2).

Space complexity: O(n)

The algorithm creates a new array result of the same size as the input array to store the final prices. Besides this, only a constant amount of extra space is used for loop variables and temporary calculations.

Therefore, the space complexity is O(n).

## Approach 2: `Monotonic Stack`
**Intuition**

Let's focus on a key part of the problem: for any given item, we need to find the first price that is smaller or equal to it and comes after it. This is similar to a classic problem known as finding the "next smaller element," which can be efficiently solved using a stack. But why does a stack work so well here?

Imagine we are processing prices from left to right. At each step, we need to determine if the current price can serve as a discount for any previous prices. The stack helps us keep track of those previous prices that haven't found their discount yet.

The key intuition is that when we find a price that is smaller than some earlier prices, it must be the discount for those earlier prices that are larger than it. We only care about the most recent of these prices because we want the first available discount.

So, for each element, our stack must contain all the most recent prices before that element that are greater than it. This implies that each element present in the stack must be in increasing order of value. This is called a monotonic stack.

When we encounter an element that is smaller than the top of the stack, this means a discount can be applied to the stack element. We continue popping prices from the stack and applying the discount until the stack is empty or the top price is less than the current price. Then, we push the current price to the top of the stack, to wait for a discount which may come further down. This way, we can both apply discounts and also maintain the monotonic property of the stack.

To implement this idea, we'll maintain a stack of indices (not prices, since we need the positions to apply discounts). We iterate over the prices array and check if the current price is less than or equal to the price at the top of the stack. If it is, the current element can be used as a discount to the elements waiting in the stack. We remove each larger price from the stack and apply the discount, then add the current price to the stack. Any prices left on the stack at the end of the main loop had no discount available.

The slideshow below demonstrates this algorithm in action:

### Algorithm
- Initialize:
  - a result array by creating a copy of the input prices array to store the discounted prices.
  - an empty stack that will store indices of prices.
- For each index i of the prices array:
  - Start a while loop that continues as long as:
    1. The stack is not empty, AND
    2. The price at the index stored at the stack's top is greater than or equal to the current price
    - Inside the while loop, pop the top index from the stack.
    - Calculate the discounted price by subtracting the current price from the price at the popped index.
    - Store the result in the result array at the popped index.
  - Add the current index i to the stack.
- Return the result array containing all final prices after discounts.

### Implementation:
```Typescript
function finalPrices(prices: number[]): number[] {
  // Create a copy of the prices array to store discounted prices
  const result = [...prices];
  const stack: number[] = [];

  prices.forEach((price, i) => {
    // Process items that can be discounted by the current price
    while (stack.length > 0 && prices[stack[stack.length - 1]] >= price) {
      // Apply discount to the previous item using the current price
      const idx = stack.pop()!;
      result[idx] -= price;
    }
    // Add the current index to the stack
    stack.push(i);
  });

  return result;
}
```

### Time Complexity
- Let n be the length of the input array prices.

Time complexity: `O(n)`

The algorithm iterates through the array once with a single loop. Although there is a while loop inside, each element can be pushed and popped from the stack exactly once. This means the total number of operations on the stack across all iterations is at most 2⋅n (n pushes and n pops).

Thus, the time complexity is O(2⋅n)=O(n).

Space complexity: O(n)

The algorithm uses a result array of size n to store the final prices. Additionally, in the worst case scenario (when prices are in strictly increasing order), the stack could store all n indices.

Thus, the total space complexity is linear, O(n).
