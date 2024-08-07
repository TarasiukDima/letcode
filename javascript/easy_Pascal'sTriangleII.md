# Pascal's Triangle II

[Task link](https://leetcode.com/problems/pascals-triangle-ii/description/)

Given an integer rowIndex, return the rowIndexth (0-indexed) row of the Pascal's triangle.

In Pascal's triangle, each number is the sum of the two numbers directly above it as shown:

Example 1:
Input: rowIndex = 3
Output: [1,3,3,1]

Example 2:
Input: rowIndex = 0
Output: [1]

Example 3:
Input: rowIndex = 1
Output: [1,1]

Constraints:

- 0 <= rowIndex <= 33

## Solution

```javascript
const getRow = (rowIndex) => {
  let prev = [1];

  for (let ind = 1; ind <= rowIndex; ind++) {
    let cur = Array.from({ length: ind + 1 }).fill(1);

    for (let x = 1; x < cur.length - 1; x++) {
      cur[x] = prev[x] + prev[x - 1];
    }

    prev = cur;
  }

  return prev;
};
```
