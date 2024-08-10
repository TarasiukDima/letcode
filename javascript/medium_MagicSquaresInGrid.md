# Magic Squares In Grid

[Task link](https://leetcode.com/problems/magic-squares-in-grid/description/)

A 3 x 3 magic square is a 3 x 3 grid filled with distinct numbers from 1 to 9 such that each row, column, and both diagonals all have the same sum.

Given a row x col grid of integers, how many 3 x 3 contiguous magic square subgrids are there?

Note: while a magic square can only contain numbers from 1 to 9, grid may contain numbers up to 15.

Example 1:
Input: grid = [[4,3,8,4],[9,5,1,9],[2,7,6,2]]
Output: 1
Explanation:
The following subgrid is a 3 x 3 magic square:

while this one is not:

In total, there is only one magic square inside the given grid.

Example 2:
Input: grid = [[8]]
Output: 0

Constraints:

- row == grid.length
- col == grid[i].length
- 1 <= row, col <= 10
- 0 <= grid[i][j] <= 15

## Solution

```javascript
const checkMagicMatrix = (grid, startX, startY) => {
  const MAGIC_SUM = 15;
  const lenDf = 3;

  for (let iDf = 0; iDf < lenDf; iDf++) {
    const rowSum = grid[startY + iDf][startX] + grid[startY + iDf][startX + 1] + grid[startY + iDf][startX + 2];
    if (rowSum !== MAGIC_SUM) return false;

    const colSum = grid[startY][startX + iDf] + grid[startY + 1][startX + iDf] + grid[startY + 2][startX + iDf];
    if (colSum !== MAGIC_SUM) return false;
  }

  // diagonals
  if (
    grid[startY][startX] + grid[startY + 1][startX + 1] + grid[startY + 2][startX + 2] !== MAGIC_SUM
    || grid[startY + 2][startX] + grid[startY + 1][startX + 1] + grid[startY][startX + 2] !== MAGIC_SUM
  )
    return false;

  const needNumbersArr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
  const uniqNums = new Set();
  for (let iDf1 = 0; iDf1 < lenDf; iDf1++) {
    for (let iDf2 = 0; iDf2 < lenDf; iDf2++) {
      uniqNums.add(grid[startY + iDf1][startX + iDf2]);
      if (!needNumbersArr.includes(grid[startY + iDf1][startX + iDf2]))
        return false;
    }
  }

  return uniqNums.size === 9;
};

const numMagicSquaresInside = (grid) => {
  let countMagic = 0;

  if (grid.length < 3 || grid[0].length < 3) return countMagic;

  const maxX = grid[0].length - 1;
  const maxY = grid.length - 1;

  for (let y = 0; y <= maxY - 2; y++) {
    for (let x = 0; x <= maxX - 2; x++) {
      if (checkMagicMatrix(grid, x, y)) countMagic++;
    }
  }

  return countMagic;
};
```
