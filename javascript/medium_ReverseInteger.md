# Reverse Integer


[Task link](https://leetcode.com/problems/reverse-integer/description/)


Given a signed 32-bit integer x, return x with its digits reversed. If reversing x causes the value to go outside the signed 32-bit integer range [-231, 231 - 1], then return 0.

Assume the environment does not allow you to store 64-bit integers (signed or unsigned).


Example 1:
Input: x = 123
Output: 321

Example 2:
Input: x = -123
Output: -321

Example 3:
Input: x = 120
Output: 21


Constraints:

- -231 <= x <= 231 - 1


## Solution
```javascript
// variant 1
const MAX_POSITIVE_INT = (2 ** 31 )- 1;
const MAX_NEGATIVE_INT = Math.pow(-2 , 31);

const reverse = (x) => {
  const numArr = x.toString().split('').reverse();
  const result = x > 0 ? +numArr.join('') : -1 * +numArr.slice(0, numArr.length -1).join('');

  return (result >= MAX_POSITIVE_INT || result <= MAX_NEGATIVE_INT) ? 0 : result;
};

// variant 2
const MAX_POSITIVE_INT = (2 ** 31) - 1;
const MAX_NEGATIVE_INT = Math.pow(-2, 31);

const reverse = (x) => {
  let result = 0;
  let number = Math.abs(x);

  while (number > 0) {
    result = result * 10 + (number % 10);
    number = parseInt(number / 10);
  }
  result = x > 0 ? result : result * -1

  return (result >= MAX_POSITIVE_INT || result <= MAX_NEGATIVE_INT) ? 0 : result;
};

```