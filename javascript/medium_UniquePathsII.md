# Unique Paths II

[Task link](https://leetcode.com/problems/unique-paths-ii/description/)

You are given an m x n integer array grid. There is a robot initially located at the top-left corner (i.e., grid[0][0]). The robot tries to move to the bottom-right corner (i.e., grid[m - 1][n - 1]). The robot can only move either down or right at any point in time.

An obstacle and space are marked as 1 or 0 respectively in grid. A path that the robot takes cannot include any square that is an obstacle.

Return the number of possible unique paths that the robot can take to reach the bottom-right corner.

The testcases are generated so that the answer will be less than or equal to 2 \* 109.

Example 1:
Input: obstacleGrid = [[0,0,0],[0,1,0],[0,0,0]]
Output: 2
Explanation: There is one obstacle in the middle of the 3x3 grid above.
There are two ways to reach the bottom-right corner:

1. Right -> Right -> Down -> Down

2. Down -> Down -> Right -> Right
   Example 2:
   Input: obstacleGrid = [[0,1],[0,0]]
   Output: 1

Constraints:

- m == obstacleGrid.length
- n == obstacleGrid[i].length
- 1 <= m, n <= 100
- obstacleGrid[i][j] is 0 or 1.

## Solution

```javascript
const uniquePathsWithObstacles = (obstacleGrid) => {
  if (obstacleGrid.length === 1) return +!obstacleGrid[0].includes(1);

  let prev = Array.from({ length: obstacleGrid[0].length }).fill(0);
  prev[0] = 1;
  for (let x = 0; x < obstacleGrid.length; x++) {
    let cur = Array.from({ length: obstacleGrid[0].length }).fill(0);

    for (let y = 0; y < obstacleGrid[0].length; y++) {
      let up = prev[y];
      let left = y - 1 >= 0 ? cur[y - 1] : 0;
      const isGift = obstacleGrid[x][y] === 1;

      cur[y] = isGift ? 0 : up + left;
    }

    prev = cur;
  }

  return prev[prev.length - 1];
};
```
