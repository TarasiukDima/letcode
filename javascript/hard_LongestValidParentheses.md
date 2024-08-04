# Longest Valid Parentheses

[Task link](https://leetcode.com/problems/longest-valid-parentheses/description/)

Given a string containing just the characters '(' and ')', return the length of the longest valid (well-formed) parentheses substring

Example 1:
Input: s = "(()"
Output: 2
Explanation: The longest valid parentheses substring is "()".

Example 2:
Input: s = ")()())"
Output: 4
Explanation: The longest valid parentheses substring is "()()".

Example 3:
Input: s = ""
Output: 0

Constraints:

- 0 <= s.length <= 3 \* 104
- s[i] is '(', or ')'.

## Solution

```javascript
const clearParentheses = (stack) => {
  const openParentheses = "(";
  const closeParentheses = ")";
  let needClose = true;

  while (needClose) {
    needClose = false;

    for (let ind = 1; ind < stack.length; ind++) {
      if (
        stack[ind - 1] === openParentheses &&
        stack[ind] === closeParentheses
      ) {
        stack[ind - 1] = "";
        stack[ind] = 1;
        needClose = true;
      }
    }

    for (let ind = 1; ind < stack.length - 1; ind++) {
      if (
        Number.isInteger(stack[ind]) &&
        stack[ind - 1] === openParentheses &&
        stack[ind + 1] === closeParentheses
      ) {
        stack[ind - 1] = "";
        stack[ind + 1] = "";
        stack[ind] += 1;
        needClose = true;
      }
    }

    for (let ind = 1; ind < stack.length; ind++) {
      if (Number.isInteger(stack[ind]) && Number.isInteger(stack[ind - 1])) {
        stack[ind] = stack[ind] + stack[ind - 1];
        stack[ind - 1] = "";
        needClose = true;
      }
    }

    stack = stack.filter((el) => Boolean(el));
  }

  return stack;
};

const longestValidParentheses = (s) => {
  let stack = s.split("");
  stack = clearParentheses(stack);
  return (
    2 *
    stack.reduce((acc, el) => (Number.isInteger(el) && el > acc ? el : acc), 0)
  );
};
```
