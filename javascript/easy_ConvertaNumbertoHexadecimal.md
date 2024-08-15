# Convert a Number to Hexadecimal

[Task link](https://leetcode.com/problems/convert-a-number-to-hexadecimal/description/)

Given an integer num, return a string representing its hexadecimal representation. For negative integers, two’s complement method is used.

All the letters in the answer string should be lowercase characters, and there should not be any leading zeros in the answer except for the zero itself.

Note: You are not allowed to use any built-in library method to directly solve this problem.

Example 1:
Input: num = 26
Output: "1a"

Example 2:
Input: num = -1
Output: "ffffffff"

Constraints:

- -231 <= num <= 231 - 1

## Solution

```javascript
const getHexFromNum = (num) => {
  const numsHex = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, "a", "b", "c", "d", "e", "f"];
  let res = "";
  let curNum = Math.abs(num);

  while (curNum > 0) {
    res = numsHex[curNum % 16] + res;
    curNum = Math.floor(curNum / 16);
  }

  return !num ? "0" : res;
};

const toHex = (num) => {
  const curNum = num > -1 ? num : num >>> 0;

  return getHexFromNum(curNum);
};
```
