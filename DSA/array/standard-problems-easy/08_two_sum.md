# Plus One

<span style="padding: 4px 8px; background-color: green; color: white;">Easy</span>

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

## Example 1

**Input**: nums = [2,7,11,15], target = 9

**Output**: [0,1]

## Example 2

**Input**: nums = [3,2,4], target = 6

**Output**: [1,2]

**Constraints**:

- `2 <= nums.length <= 104`
- `-109 <= nums[i] <= 109`
- `-109 <= target <= 109`
- `Only one valid answer exists.`

```JavaScript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    const map = new Map(); // maping value to index

    for(let i=0; i<nums.length; i++){
        let diff = target - nums[i];

        if(map.has(diff)){
            return [map.get(diff), i]
        }
        map.set(nums[i], i)
    }
};
```

## Approach

1. calulate the difference between the current indexed element and target
2. we have to look whether the difference exists in the array
3. for this searching, we maintain a hashmap of values and index
4. if the map contains the difference value and it's index, we return
5. else we push the current element in the map and continue

`TC: O(n)`

`SC: O(n)`
