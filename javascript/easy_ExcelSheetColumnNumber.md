# Excel Sheet Column Number

[Task link](https://leetcode.com/problems/excel-sheet-column-number/description/)

Given a string columnTitle that represents the column title as appears in an Excel sheet, return its corresponding column number.

For example:

A -> 1
B -> 2
C -> 3
...
Z -> 26
AA -> 27
AB -> 28
...

Example 1:
Input: columnTitle = "A"
Output: 1

Example 2:
Input: columnTitle = "AB"
Output: 28

Example 3:
Input: columnTitle = "ZY"
Output: 701

Constraints:

- 1 <= columnTitle.length <= 7
- columnTitle consists only of uppercase English letters.
- columnTitle is in the range ["A", "FXSHRXW"].

## Solution

```javascript
// variant 1
const titleToNumber = (columnTitle) => {
  const alphabet = [
    "A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M",
    "N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z"
  ];
  const countLetters = alphabet.length;
  const titleLastInd = columnTitle.length;
  let result = 0;

  for (let ind = 0; ind < titleLastInd; ind++) {
    const index = alphabet.indexOf(columnTitle[ind]);
    if (index === -1) continue;

    result *= countLetters;
    result += index + 1;
  }

  return result;
};

// variant 2
const titleToNumber = (columnTitle) => {
  const countLetters = 26;
  const titleLastInd = columnTitle.length;
  let result = 0;

  for (let ind = 0; ind < titleLastInd; ind++) {
    const index = columnTitle.charCodeAt(ind) - 64;
    result *= countLetters;
    result += index;
  }

  return result;
};
```
