# Sort Colors

[Task link](https://leetcode.com/problems/sort-colors/description/)

Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.
We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.
You must solve this problem without using the library's sort function.

Example 1:
Input: nums = [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]

Example 2:
Input: nums = [2,0,1]
Output: [0,1,2]

Constraints:

- n == nums.length
- 1 <= n <= 300
- nums[i] is either 0, 1, or 2.

## Solution

```javascript
const sortColors = (nums) => {
  if (nums.length <= 1) {
    return nums;
  }

  let right = nums.length - 1;
  while (right > 0) {
    for (let ind = right - 1; ind >= 0; ind--) {
      const num = nums[ind];

      console.log("num", nums);
      if (num > nums[right]) {
        // without [a,b] = [b,a]
        // I don't like create new array for change two variables
        const tmp = nums[right];
        nums[right] = num;
        nums[ind] = tmp;
      }
    }

    right--;
  }

  return nums;
};
```
