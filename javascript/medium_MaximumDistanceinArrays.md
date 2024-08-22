# Maximum Distance in Arrays

[Task link](https://leetcode.com/problems/maximum-distance-in-arrays/description/)

You are given m arrays, where each array is sorted in ascending order.

You can pick up two integers from two different arrays (each array picks one) and calculate the distance. We define the distance between two integers a and b to be their absolute difference |a - b|.

Return the maximum distance.

Example 1:
Input: arrays = [[1,2,3],[4,5],[1,2,3]]
Output: 4
Explanation: One way to reach the maximum distance 4 is to pick 1 in the first or third array and pick 5 in the second array.

Example 2:
Input: arrays = [[1],[1]]
Output: 0

Constraints:

- m == arrays.length
- 2 <= m <= 105
- 1 <= arrays[i].length <= 500
- -104 <= arrays[i][j] <= 104
- arrays[i] is sorted in ascending order.
- There will be at most 105 integers in all the arrays.

## Solution

```javascript
// variant 1
const maxDistance = (arrays) => {
  let maxDistance = 0;
  const max = [];
  const min = [];

  for (let ind = 0; ind < arrays.length; ind++) {
    const min1 = arrays[ind][0];
    const max1 = arrays[ind].at(-1);

    min.push([min1, ind]);
    max.push([max1, ind]);
  }

  min.sort((a, b) => a[0] - b[0]);
  max.sort((a, b) => b[0] - a[0]);

  if (min[0][1] !== max[0][1]) {
    maxDistance = Math.abs(max[0][0] - min[0][0]);
  } else {
    const distance1 = Math.abs(max[0][0] - min[1][0]);
    const distance2 = Math.abs(max[1][0] - min[0][0]);

    maxDistance = Math.max(maxDistance, distance1, distance2);
  }

  return maxDistance;
};

// variant 2
const maxDistance = (arrays) => {
  let min = arrays[0][0];
  let max = arrays[0].at(-1);
  let maxDistance = 0;

  for (let ind = 1; ind < arrays.length; ind++) {
    const nums = arrays[ind];
    const stepMin = nums[0];
    const stepMax = nums.at(-1);

    maxDistance = Math.max(
      maxDistance,
      Math.abs(stepMax - min),
      Math.abs(max - stepMin)
    );

    min = Math.min(min, stepMin);
    max = Math.max(max, stepMax);
  }

  return maxDistance;
};
```
