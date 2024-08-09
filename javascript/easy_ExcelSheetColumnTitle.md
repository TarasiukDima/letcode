# Excel Sheet Column Title

[Task link](https://leetcode.com/problems/excel-sheet-column-title/description/)

Given an integer columnNumber, return its corresponding column title as it appears in an Excel sheet.

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
Input: columnNumber = 1
Output: "A"

Example 2:
Input: columnNumber = 28
Output: "AB"

Example 3:
Input: columnNumber = 701
Output: "ZY"

Constraints:

- 1 <= columnNumber <= 231 - 1

## Solution

```javascript
const convertToTitle = (columnNumber) => {
   const alphabet = [
    "A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M",
    "N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z"
  ];
  const countLetters = alphabet.length;

  let result = '';
  while (columnNumber > 0) {
    const fLetter = ((columnNumber - 1) / countLetters) >> 0;
    let sLetter = (columnNumber % countLetters);
    sLetter = sLetter === 0 ? countLetters : sLetter;
    result = alphabet[sLetter - 1] + result;
    columnNumber = fLetter;
  }
  return result;
};
```
