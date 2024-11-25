# Plus One

<span style="padding: 4px 8px; background-color: green; color: white;">Easy</span>

You are given a large integer represented as an integer array digits, where each digits[i] is the ith digit of the integer. The digits are ordered from most significant to least significant in left-to-right order. The large integer does not contain any leading 0's.

Increment the large integer by one and return the resulting array of digits.

## Example 1

**Input**: digits = [1,2,3]

**Output**: [1,2,4]

## Example 2

**Input**: digits = [9]

**Output**: [1,0]

**Constraints**:

`1 <= digits.length <= 100`

`0 <= digits[i] <= 9`

`digits does not contain any leading 0's.`

```JavaScript
/**
 * @param {number[]} digits
 * @return {number[]}
 */
var plusOne = function(digits) {
    if(digits.length === 0){
        return 0
    }
    
    let n = digits.length;

    if(digits[n-1] !== 9){
        digits[n-1]++;
        return digits;
    }
    
    for(let i=n-1; i>= 0; i--){
        digits[i]++;
        
        if(digits[i] > 9){
            digits[i] = 0;
        } else {
            return digits;
        }
    }
    
    digits.unshift(1);
    
    return digits;
};
```

## Approach

1. traverse the array backwards
2. check if the digit is greater than 9
3. if true, make the digit 0
4. finally unshift the array by 1 after the iteration

`TC: O(n)`

`SC: O(1)`
