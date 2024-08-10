# Factorial Trailing Zeroes

[Task link](https://leetcode.com/problems/factorial-trailing-zeroes/description/)

Given an integer n, return the number of trailing zeroes in n!.

Note that n! = n _ (n - 1) _ (n - 2) _ ... _ 3 _ 2 _ 1.

Example 1:
Input: n = 3
Output: 0
Explanation: 3! = 6, no trailing zero.

Example 2:
Input: n = 5
Output: 1
Explanation: 5! = 120, one trailing zero.

Example 3:
Input: n = 0
Output: 0

Constraints:

- 0 <= n <= 104

Follow up: Could you write a solution that works in logarithmic time complexity?

## Solution

```javascript

const prodTree = (left, right) => {
  if (left > right) return 1n;
  if (left == right) return left;
  if (right - left === 1n) return left * right;

  const middle = left + (right - left) / 2n;
  return prodTree(left, middle) * prodTree(middle + 1n, right);
}

const getFactorialLogTime = (n) => {
  if (n < 0) return 0;
  if (n == 0) return 1;
  if (n == 1 || n == 2) return n;

  return prodTree(2n, n);
};

const getCountTrailingZeros = (n) => {
  const strNum = n.toString();
  let countZeros = 0;
  let right = strNum.length - 1;

  while (right > 0) {
    if (strNum[right] === '0') countZeros++;
    else break;
    right--;
  }

  return countZeros;
};


const trailingZeroes = (n) => getCountTrailingZeros(getFactorialLogTime(BigInt(n)));
```
