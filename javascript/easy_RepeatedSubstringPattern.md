# Repeated Substring Pattern

[Task link](https://leetcode.com/problems/repeated-substring-pattern/description/)

Given a string s, check if it can be constructed by taking a substring of it and appending multiple copies of the substring together.

Example 1:
Input: s = "abab"
Output: true
Explanation: It is the substring "ab" twice.

Example 2:
Input: s = "aba"
Output: false

Example 3:
Input: s = "abcabcabcabc"
Output: true
Explanation: It is the substring "abc" four times or the substring "abcabc" twice.

Constraints:

- 1 <= s.length <= 104
- s consists of lowercase English letters.

## Solution

```javascript
// variant 1
const repeatedSubstringPattern = (s) => {
  if (s.length < 2) return false;

  const patternLengths = [1];
  const sizeStr = s.length;
  const middle = Math.floor(s.length / 2);

  let step = 2;
  while (step <= middle) {
    if (Number.isInteger(sizeStr / step)) {
      patternLengths.push(step);
    }

    step++;
  }

  for (let ind = 0; ind < patternLengths.length; ind++) {
    const patLen = patternLengths[ind];
    const countRepeat = Math.floor(sizeStr / patLen);
    const doubleStr = s.slice(0, patLen).repeat(countRepeat);

    if (doubleStr === s) return true;
  }

  return false;
};

// variant 2
const repeatedSubstringPattern = (s) => {
  if (s.length < 2) return false;
  if (s.length === 2) return s[0] === s[1];

  const sizeStr = s.length;
  let middle = Math.floor(sizeStr / 2);
  let pattern = "";

  for (let ind = 0; ind <= middle; ind++) {
    pattern += s[ind];

    const patLen = pattern.length;
    const countRepeat = Math.floor(sizeStr / patLen);
    const doubleStr = pattern.repeat(countRepeat);

    console.log("doubleStr", s, doubleStr);

    if (doubleStr === s) return true;
  }

  return false;
};
```
