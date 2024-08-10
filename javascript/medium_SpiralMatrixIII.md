# Spiral Matrix III

[Task link](https://leetcode.com/problems/spiral-matrix-iii/description/)

You start at the cell (rStart, cStart) of an rows x cols grid facing east. The northwest corner is at the first row and column in the grid, and the southeast corner is at the last row and column.

You will walk in a clockwise spiral shape to visit every position in this grid. Whenever you move outside the grid's boundary, we continue our walk outside the grid (but may return to the grid boundary later.). Eventually, we reach all rows \* cols spaces of the grid.

Return an array of coordinates representing the positions of the grid in the order you visited them.

Example 1:
Input: rows = 1, cols = 4, rStart = 0, cStart = 0
Output: [[0,0],[0,1],[0,2],[0,3]]

Example 2:
Input: rows = 5, cols = 6, rStart = 1, cStart = 4
Output: [[1,4],[1,5],[2,5],[2,4],[2,3],[1,3],[0,3],[0,4],[0,5],[3,5],[3,4],[3,3],[3,2],[2,2],[1,2],[0,2],[4,5],[4,4],[4,3],[4,2],[4,1],[3,1],[2,1],[1,1],[0,1],[4,0],[3,0],[2,0],[1,0],[0,0]]

Constraints:

- 1 <= rows, cols <= 100
- 0 <= rStart < rows
- 0 <= cStart < cols

## Solution

```javascript
const spiralMatrixIII = (rows, cols, rStart, cStart) => {
  // const matrix = Array.from({ length: rows }, () => Array.from({ length: cols }));
  const answer = [];
  const maxX = cols - 1;
  const maxY = rows - 1;
  let x = cStart;
  let y = rStart;
  let dx = 1;
  let dy = 0;

  let num = 1;
  let needSteps = rows * cols;

  let indexStepsBeforeRotate = 1;
  let numberStepBeforeRotate = 0;
  let countStepsBeforeRotate = indexStepsBeforeRotate * 2;
  let middleIndStepsBeforeRotate = Math.floor(countStepsBeforeRotate / 2);

  const rotateMatrixDirection = () => {
    const tmp = dx;
    dx = -dy;
    dy = tmp;
  };

  while (needSteps > 0) {
    if (x >= 0 && x <= maxX && y >= 0 && y <= maxY) {
      // matrix[y][x] = num;
      answer.push([y, x]);
      num++;
      needSteps--;
    }

    if (numberStepBeforeRotate === middleIndStepsBeforeRotate) {
      rotateMatrixDirection();
    }

    if (numberStepBeforeRotate === countStepsBeforeRotate) {
      rotateMatrixDirection();
      indexStepsBeforeRotate++;
      numberStepBeforeRotate = 0;
      countStepsBeforeRotate = indexStepsBeforeRotate * 2;
      middleIndStepsBeforeRotate = Math.floor(countStepsBeforeRotate / 2);
    }

    x += dx;
    y += dy;
    numberStepBeforeRotate++;
  }

  return answer;
};
```
