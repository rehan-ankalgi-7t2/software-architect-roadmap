# Rotate the array by k times

<span style="padding: 4px 8px; background-color: #ffbb00; color: white;">Medium</span>

Given an integer array nums, rotate the array to the right by k steps, where k is non-negative.

## Example 1:

Input: nums = [1,2,3,4,5,6,7], k = 3

Output: [5,6,7,1,2,3,4]

Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]

## Example 2:

Input: nums = [-1,-100,3,99], k = 2

Output: [3,99,-1,-100]

Explanation:
rotate 1 steps to the right: [99,-1,-100,3]
rotate 2 steps to the right: [3,99,-1,-100]

### Constraints:

- `1 <= nums.length <= 105`
- `-231 <= nums[i] <= 231 - 1`
- `0 <= k <= 105`

## Brute 🤡
- use 2 for loops
- iterate over the array and shift the elements
- O(n^2)

## Better 😎
- shift starting k elements in a temporary array
- shift the rest to the start of the array
- place the elements from the temporary array back in the array at the end positions

```Java
class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        
        if (k == 0 || k == n || n <= 1){
            return;
        }
        
        k = (k % n); // making sure k is in the bound
        
        // maintaining temporary array
        int [] temp;
        temp = new int[k];
        
        for(int i=0; i<k; i++){
            temp[i] = nums[i];
        }
        
        // shifting work
        for(int i = k; i<n; i++){
            nums[i-k] = nums[i];
        }
        
        // load the temp array back
        for(int i = n - k; i < n; i++){
            nums[i] = temp[i - (n - k)];
        }
        
        return;
    }
}
```

## Optimal / Trick shot 🗿
- reverse the entire array
- reverse the first `k` elements
- reverse the remaining `n-k` elements

```Java
class Solution{
    public void rotate(int[]nums,int k){
        int n=nums.length;
        k%=n;
        
        reverse(nums,0,n-1);
        reverse(nums,0,k-1);
        reverse(nums,k,n-1);
    }

    private void reverse(int[]nums,int start,int end){
        while(start < end){
            int temp=nums[start];

            nums[start]=nums[end];
            nums[end]=temp;
            start++;
            end--;
        }
    }
}
```