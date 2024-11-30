# Longest Common Prefix

<span style="padding: 4px 8px; background-color: green; color: white;">Easy</span>

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

## Example 1:

**Input**:strs = ["flower","flow","flight"]

**Output**: "fl"

## Example 2:

**Input**: strs = ["dog","racecar","car"]

**Output**: ""

**Constraints**:

- `1 <= strs.length <= 200`
- `0 <= strs[i].length <= 200`
- strs[i] consists of only lowercase English letters.

```JavaScript
/**
 * @param {string[]} strs
 * @return {string}
 */
var longestCommonPrefix = function(strs) {
    // iteration
    if (strs.length === 0) return "";

    let prefix = strs[0];

    for (let i = 1; i < strs.length; i++) {
        while (strs[i].indexOf(prefix) !== 0) {
            prefix = prefix.slice(0, -1);
            if (prefix === "") return "";
        }
    }

    return prefix;
};
```

## Approach

This JavaScript function, `longestCommonPrefix`, finds the longest common prefix string among an array of strings, `strs`. Let's break it down:

### Function Logic:

1. **Base Case**:
   - If the input array `strs` is empty, return an empty string `""` immediately.

2. **Initialization**:
   - Start by assuming the first string in the array (`strs[0]`) is the common prefix.

3. **Iterate Through the Array**:
   - For each subsequent string in the array (`strs[i]`):
     - Check if the current prefix is a prefix of the string.
     - If not, shorten the prefix by removing one character from the end (`prefix.slice(0, -1)`) until it becomes a prefix of `strs[i]`.

4. **Early Exit**:
   - If the prefix becomes an empty string during the iteration, return `""` since no common prefix exists.

5. **Return the Prefix**:
   - After checking all strings, return the prefix, which represents the longest common prefix among all the strings in the array.

### Example Walkthrough:

#### Input: `["flower", "flow", "flight"]`
- Initialize `prefix` = `"flower"`.
- Compare with `"flow"`:
  - `"flower".indexOf("flow") !== 0` → Shorten prefix to `"flow"`.
  - `"flow".indexOf("flow") === 0` → Prefix is valid.
- Compare with `"flight"`:
  - `"flow".indexOf("flight") !== 0` → Shorten prefix to `"flo"`, `"fl"`.
  - `"fl".indexOf("flight") === 0` → Prefix is valid.
- Final prefix: `"fl"`.

#### Output: `"fl"`

### Time Complexity:
- **Worst Case**: \( O(S) \), where \( S \) is the sum of all characters in the array. For each string comparison, the prefix is reduced by one character at most.

### Space Complexity:
- \( O(1) \): Only the `prefix` variable uses additional space.

### Notes:
This approach is efficient for small to medium-sized input arrays. For very large inputs or very long strings, consider optimizing further using divide-and-conquer or binary search.
