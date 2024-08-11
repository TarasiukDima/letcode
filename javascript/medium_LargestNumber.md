# Largest Number

[Task link](https://leetcode.com/problems/largest-number/description/)

Given a list of non-negative integers nums, arrange them such that they form the largest number and return it.

Since the result may be very large, so you need to return a string instead of an integer.

Example 1:
Input: nums = [10,2]
Output: "210"

Example 2:
Input: nums = [3,30,34,5,9]
Output: "9534330"

Constraints:

- 1 <= nums.length <= 100
- 0 <= nums[i] <= 109

## Solution

```javascript
const largestNumber = (nums) => {
  const numsStr = nums.sort((a, b) => {
    a = a.toString();
    b = b.toString();

    return b + a - (a + b);
  });
  const result = numsStr.join("");

  return +result === 0 ? "0" : result;
};
```
