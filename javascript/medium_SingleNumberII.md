# Single Number II

[Task link](https://leetcode.com/problems/single-number-ii/description/)

Given an integer array nums where every element appears three times except for one, which appears exactly once. Find the single element and return it.

You must implement a solution with a linear runtime complexity and use only constant extra space.

Example 1:
Input: nums = [2,2,3,2]
Output: 3

Example 2:
Input: nums = [0,1,0,1,0,1,99]
Output: 99

Constraints:

- 1 <= nums.length <= 3 \* 104
- -231 <= nums[i] <= 231 - 1
  Each element in nums appears exactly three times except for one element which appears once.

## Solution

```javascript
// Bad for time O(n log n) + O(n); Need bits operations for solution this task
const singleNumber = (nums) => {
  nums.sort((a, b) => a - b);
  for (let ind = 0; ind < nums.length; ind++) {
    if (nums[ind] !== nums[ind - 1] && nums[ind] !== nums[ind + 1]) {
      return nums[ind];
    }
  }

  return 0;
};

```
