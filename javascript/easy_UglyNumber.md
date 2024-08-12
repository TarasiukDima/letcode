# Ugly Number

[Task link](https://leetcode.com/problems/ugly-number/description/)

An ugly number is a positive integer whose prime factors are limited to 2, 3, and 5.

Given an integer n, return true if n is an ugly number.

Example 1:
Input: n = 6
Output: true
Explanation: 6 = 2 × 3

Example 2:
Input: n = 1
Output: true
Explanation: 1 has no prime factors, therefore all of its prime factors are limited to 2, 3, and 5.

Example 3:
Input: n = 14
Output: false
Explanation: 14 is not ugly since it includes the prime factor 7.

Constraints:

- -231 <= n <= 231 - 1

## Solution

```javascript
const isUglyRes = (n, divisible) => {
  const uglyRes = [2, 3, 5];
  if (uglyRes.includes(n)) return true;

  if (n % divisible !== 0) return false;

  return (
    isUglyRes(n / divisible, 2) ||
    isUglyRes(n / divisible, 3) ||
    isUglyRes(n / divisible, 5)
  );
};

const isUgly = (n) => {
  if (n < 1) return false;
  if (n === 1) return true;

  return isUglyRes(n, 2) || isUglyRes(n, 3) || isUglyRes(n, 5);
};
```
