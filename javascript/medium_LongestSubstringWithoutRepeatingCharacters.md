# Longest Substring Without Repeating Characters

[Task link](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)

Given a string s, find the length of the longest
substring
without repeating characters.

Example 1:
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.

Example 2:
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.

Example 3:
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.

Constraints:

- 0 <= s.length <= 5 \* 104
- s consists of English letters, digits, symbols and spaces.

## Solution

```javascript
const lengthOfLongestSubstring = (s) => {
  if (!s.length) return 0;

  let left = 0;
  let right = 1;
  const hash = new Map([[s[left], left]]);
  let maxSize = 0;

  while (right < s.length) {
    const letter = s[right];

    if (hash.has(letter)) {
      const indForUpdate = hash.get(letter) + 1;
      maxSize = Math.max(maxSize, right - left);

      while (left < indForUpdate) {
        hash.delete(letter);
        left++;
      }
    }

    hash.set(letter, right);
    right++;
  }

  return Math.max(maxSize, right - left);
};
```
