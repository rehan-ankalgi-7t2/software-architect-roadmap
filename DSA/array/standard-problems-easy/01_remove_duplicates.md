# Remove duplicates from the given sorted array

<span style="padding: 4px 8px; background-color: green; color: white;">Easy</span>

Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same. Then return the number of unique elements in nums.

Consider the number of unique elements of nums to be k, to get accepted, you need to do the following things:

Change the array nums such that the first k elements of nums contain the unique elements in the order they were present in nums initially. The remaining elements of nums are not important as well as the size of nums.
Return k.

## Example 1:

**Input**: nums = [1,1,2]

**Output**: 2, nums = [1,2,_]

**Explanation**: Your function should return k = 2, with the first two elements of nums being 1 and 2 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).

**Constraints**:

1 <= nums.length <= 3 * 104
-100 <= nums[i] <= 100
nums is sorted in non-decreasing order.

```Java
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        
        int i=0;
        for(int j=1; j<nums.length; j++){
            if(nums[j] != nums[i]){
                i++;
                nums[i] = nums[j];   
            }
        }
        
        return i+1;
    }
}
```

## Approach

**Brute solution**: use Set Data structure `O(nlogn) + O(n)`

1. insert all unique items into the Set O(nlogn) i.e. O(logn) for single insertion into the Set
2. retrieve and replace all the unique elements consecutively in the same array
3. return the index value when there are no more elements left in the Set

**Better / @Optimal solution**: 2 pointer method `O(n)`

1. assign the first element to pointer i, we know that first element always remains in first position
2. iterate the second pointer j on the array
3. when the element arr[j] is not equivalent to the arr[i], assign the element arr[j] the next position after pointer i, i.e. arr[i+1]
4, increment i pointer i++
5. return i+1 pointer value
