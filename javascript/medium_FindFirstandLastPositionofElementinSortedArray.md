# Find First and Last Position of Element in Sorted Array

[Task link](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/)

Given an array of integers nums sorted in non-decreasing order, find the starting and ending position of a given target value.

If target is not found in the array, return [-1, -1].

You must write an algorithm with O(log n) runtime complexity.

Example 1:
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]

Example 2:
Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]

Example 3:
Input: nums = [], target = 0
Output: [-1,-1]

Constraints:

- 0 <= nums.length <= 105
- -109 <= nums[i] <= 109
- nums is a non-decreasing array.
- -109 <= target <= 109

## Solution

```javascript
const getMiddle = (left, right) => Math.floor((left + right) / 2);
const getResultIndex = (l, r, nums, target) =>
  nums[l] === target ? l : nums[r] === target ? r : -1;

const getFirstLessNumber = (l, r, nums, target) => {
  let left = l;
  let right = r;
  let middle = getMiddle(left, right);

  while (left < right && middle !== right && middle !== left) {
    if (nums[middle] === target) {
      right = middle;
    } else if (nums[middle] < target) {
      left = middle;
    }

    middle = getMiddle(left, right);
  }

  return getResultIndex(left, right, nums, target);
};

const getFirstMoreNumber = (l, r, nums, target) => {
  let left = l;
  let right = r;
  let middle = getMiddle(left, right);

  while (left < right && middle !== right && middle !== left) {
    if (nums[middle] === target) {
      left = middle;
    } else if (nums[middle] > target) {
      right = middle;
    }

    middle = getMiddle(left, right);
  }

  return getResultIndex(right, left, nums, target);
};

const searchRange = (nums, target) => {
  let left = 0;
  let right = nums.length - 1;
  let middle = getMiddle(left, right);

  // get first finded number like target
  while (left < right && middle !== right && middle !== left) {
    if (nums[middle] === target) {
      break;
    }

    if (nums[middle] > target) {
      right = middle - 1;
    } else if (nums[middle] < target) {
      left = middle;
    }

    middle = getMiddle(left, right);
  }

  let newMiddle =
    nums[middle] === target ? middle : nums[left] === target ? left : right;

  return [
    getFirstLessNumber(left, newMiddle, nums, target),
    getFirstMoreNumber(newMiddle, right, nums, target),
  ];
};
```
