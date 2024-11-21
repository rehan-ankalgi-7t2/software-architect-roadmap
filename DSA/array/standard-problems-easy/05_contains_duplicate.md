# Contains duplicate

<span style="padding: 4px 8px; background-color: green; color: white;">Easy</span>

Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

## Example 1:

**Input**: nums = [1,2,3,1]

**Output**: true

**Explanation**:

The element 1 occurs at the indices 0 and 3.

## Example 2:

**Input**: nums = [1,2,3,4]

**Output**: false

**Explanation**:

All elements are distinct.

## Example 3:

**Input**: nums = [1,1,1,3,3,4,3,2,4,2]

**Output**: true

**Constraints**:

`1 <= nums.length <= 105`
`-109 <= nums[i] <= 109`

```Java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        int n = nums.length;
        HashMap<Integer, Integer> freq = new HashMap<>();
        
        for(int i = 0; i < n; i++){
            if(freq.get(nums[i]) != null && freq.get(nums[i]) > 0){
                return true;
            } else {
                freq.put(nums[i], 1);
            }
        }
        
        return false;
    } 
}
```

## Approach

**Brute solution**:

1. use nested loops and compare each element with every other element in the array

`TC: O(n^2)`

`SC: O(1)`

**Better solution**: 

1. sort the array and compare the adjacent elements

`TC: O(nlogn) + O(n)`

`SC: O(1)`

**Optimal Solution**:

1. use a `HashMap` to store the freq of each element
2. if the element already exists in the map, return true
3. else return false

`TC: O(n)`
`SC: O(n)`
