# 3Sum Closest

[Task link](https://leetcode.com/problems/3sum-closest/description/)

Given an integer array nums of length n and an integer target, find three integers in nums such that the sum is closest to target.
Return the sum of the three integers.
You may assume that each input would have exactly one solution.

Example 1:
Input: nums = [-1,2,1,-4], target = 1
Output: 2
Explanation: The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).

Example 2:
Input: nums = [0,0,0], target = 1
Output: 0
Explanation: The sum that is closest to the target is 0. (0 + 0 + 0 = 0).

Constraints:

- 3 <= nums.length <= 500
- -1000 <= nums[i] <= 1000
- -104 <= target <= 104

## Solution

```javascript
const threeSumClosest = (nums, target) => {
  nums.sort((a, b) => b - a);

  const arrLength = nums.length;
  const maxInd = arrLength - 2;
  let nearSum = nums.slice(0, 3).reduce((acc, el) => acc + el, 0);
  if (nearSum === target) return nearSum;

  for (let ind = 0; ind < maxInd; ind++) {
    let left = ind + 1;
    let right = arrLength - 1;

    while (left < right) {
      const sumStep = nums[ind] + nums[left] + nums[right];

      if (sumStep === target) return sumStep;

      if (sumStep < target) {
        right--;
      } else {
        left++;
      }

      if (Math.abs(sumStep - target) < Math.abs(nearSum - target)) {
        nearSum = sumStep;
      }
    }
  }

  return nearSum;
};
```
