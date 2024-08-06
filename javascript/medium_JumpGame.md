# Jump Game

[Task link](https://leetcode.com/problems/jump-game/description/)

You are given an integer array nums. You are initially positioned at the array's first index, and each element in the array represents your maximum jump length at that position.

Return true if you can reach the last index, or false otherwise.

Example 1:
Input: nums = [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.

Example 2:
Input: nums = [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.

Constraints:

- 1 <= nums.length <= 104
- 0 <= nums[i] <= 105

## Solution

```javascript
const canJump = (nums) => {
  if (nums.length <= 1) return true;
  if (nums[0] === 0) return false;

  let maxInd = nums.length - 1;
  let left = 0;

  while (left < maxInd) {
    const newIndex = left + nums[left];

    if (newIndex >= maxInd) return true;

    if (nums[newIndex] === 0) {
      let newLeft = newIndex - 1;
      let minNextInd = newIndex + 1;

      while (newLeft >= 0) {
        const stepRes = newLeft + nums[newLeft];

        if (stepRes >= minNextInd) {
          left = stepRes;
          break;
        }

        if (newLeft === 0) return false;

        newLeft--;
      }

      continue;
    }

    left = newIndex;
  }

  return true;
};
```
