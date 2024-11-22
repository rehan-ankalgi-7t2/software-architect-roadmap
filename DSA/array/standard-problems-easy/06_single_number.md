# single Number

<span style="padding: 4px 8px; background-color: green; color: white;">Easy</span>

Given a non-empty array of integers nums, every element appears twice except for one. Find that single one.

You must implement a solution with a linear runtime complexity and use only constant extra space.

## Example 1

**Input**: nums = [2,2,1]

**Output**: 1

## Example 2

**Input**: nums = [4,1,2,1,2]

**Output**: 4

**Constraints**:

`1 <= nums.length <= 3 *104`

`-3* 104 <= nums[i] <= 3 * 104`

Each element in the array appears twice except for one element which appears only once.

```Java
class Solution {
    public int singleNumber(int[] nums) {
        int result = nums[0];
        
        for(int i = 0; i < nums.length - 1; i++){
            result = result ^ nums[i+1];
        }
        
        return result;
    }
}
```

## Approach

**Brute solution**:

1. use nested loops and compare each element with every other element in the array

`TC: O(n^2)`

`SC: O(1)`

**Better Solution**:

1. use a `HashMap` to store the freq of each element
2. if the element already exists in the map, return true
3. else return false

`TC: O(n)`
`SC: O(n)`

**Optimal Solution**:

1. initialize the result to first element
2. perform bitwise `XOR` operation on the all elements and the result by iterating over the array
3. return the result

`TC: O(n)`
`SC: O(1)`
