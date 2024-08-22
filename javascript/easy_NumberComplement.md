# Number Complement

[Task link](https://leetcode.com/problems/number-complement/description/)

The complement of an integer is the integer you get when you flip all the 0's to 1's and all the 1's to 0's in its binary representation.

For example, The integer 5 is "101" in binary and its complement is "010" which is the integer 2.
Given an integer num, return its complement.

Example 1:

Input: num = 5
Output: 2
Explanation: The binary representation of 5 is 101 (no leading zero bits), and its complement is 010. So you need to output 2.
Example 2:

Input: num = 1
Output: 0
Explanation: The binary representation of 1 is 1 (no leading zero bits), and its complement is 0. So you need to output 0.

Constraints:

- 1 <= num < 231

## Solution

```javascript
// var 1
const reverseBinNum = (arr) => arr.map((num) => num === 0 ? 1 : 0);

const findComplement = (num) => {
  return reverseBinNum(num.toString(2).split("")).join("").toString(10);
};


// var 2
const findComplement = (num) => {
  if (num === 0) return 1;

  const res = [];

  while (num) {
    res.push((num & 1) === 0 ? 1 : 0)
    num >>>= 1;
  }

  return res.reduce((acc, n, ind) => acc + (n * 2**ind), 0);
};
```
