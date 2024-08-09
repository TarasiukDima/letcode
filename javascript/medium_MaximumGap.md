# Maximum Gap

[Task link](https://leetcode.com/problems/maximum-gap/description/)

Given an integer array nums, return the maximum difference between two successive elements in its sorted form. If the array contains less than two elements, return 0.

You must write an algorithm that runs in linear time and uses linear extra space.

Example 1:
Input: nums = [3,6,9,1]
Output: 3
Explanation: The sorted form of the array is [1,3,6,9], either (3,6) or (6,9) has the maximum difference 3.

Example 2:
Input: nums = [10]
Output: 0
Explanation: The array contains less than 2 elements, therefore return 0.

Constraints:

- 1 <= nums.length <= 105
- 0 <= nums[i] <= 109

## Solution

```javascript
// variant 1
const maximumGap = (nums) => {
  let maxGap = 0;

  if (nums.length < 2) return maxGap;

  nums.sort((a, b) => a - b);

  for (let ind = 1; ind < nums.length; ind++) {
    maxGap = Math.max(maxGap, Math.abs(nums[ind] - nums[ind - 1]));
  }

  return maxGap;
};

// variant 2
const insertionSort = (bucket) => {
  for (let ind = 1; ind < bucket.length; ++ind) {
    const key = bucket[ind];
    let j = ind - 1;

    while (j >= 0 && bucket[j] > key) {
      bucket[j + 1] = bucket[j];
      j--;
    }

    bucket[j + 1] = key;
  }
};

const bucketSort = (arr, countSegments) => {
  const min = Math.min(...arr);
  const bucketCount = countSegments || 200;
  const buckets = [];

  // insert sorting parts to the arr
  for (let ind = 0; ind < arr.length; ind++) {
    const newIndex = Math.floor((arr[ind] - min) / bucketCount);

    if (!buckets[newIndex]) {
      buckets[newIndex] = [];
    }

    buckets[newIndex].push(arr[ind]);
  }

  let idx = 0;
  for (let ind = 0; ind < buckets.length; ind++) {
    if (!buckets[ind]) continue;

    // sort segment
    insertionSort(buckets[ind]);

    // insert sorting segment items to the arr
    for (var j = 0; j < buckets[ind].length; j++) {
      arr[idx++] = buckets[ind][j];
    }
  }
  return arr;
};

const maximumGap = (nums) => {
  const countItems = nums.length;
  let maxGap = 0;
  if (countItems < 2) return maxGap;

  bucketSort(nums, countItems);

  for (let ind = 1; ind < countItems; ind++) {
    maxGap = Math.max(maxGap, Math.abs(nums[ind] - nums[ind - 1]));
  }

  return maxGap;
};
```
