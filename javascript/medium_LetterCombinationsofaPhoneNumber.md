# Letter Combinations of a Phone Number

[Task link](https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/)

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order.

A mapping of digits to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

Example 1:
Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]

Example 2:
Input: digits = ""
Output: []

Example 3:
Input: digits = "2"
Output: ["a","b","c"]

Constraints:

- 0 <= digits.length <= 4
- digits[i] is a digit in the range ['2', '9'].

## Solution

```javascript

!!!!!!BAD SOLUTION!!!!!!

const PHONE_DIGITS_LETTERS = {
  2: ["a", "b", "c"],
  3: ["d", "e", "f"],
  4: ["g", "h", "i"],
  5: ["j", "k", "l"],
  6: ["m", "n", "o"],
  7: ["p", "q", "r", "s"],
  8: ["t", "u", "v"],
  9: ["w", "x", "y", "z"],
};

const letterCombinations = (digits) => {
  const digStr = digits.toString();
  const result = new Set();

  if (digStr.length === 1) {
    return PHONE_DIGITS_LETTERS[digits];
  }

  const key1 = PHONE_DIGITS_LETTERS[digits[0]] ?? [];
  const key2 = PHONE_DIGITS_LETTERS[digits[1]] ?? [];
  const key3 = PHONE_DIGITS_LETTERS[digits[2]] ?? [];
  const key4 = PHONE_DIGITS_LETTERS[digits[3]] ?? [];

  for (let ind1 = 0; ind1 < key1.length; ind1++) {
    const letter1 = key1[ind1];

    for (let ind2 = 0; ind2 < key2.length; ind2++) {
      const letter2 = key2[ind2];
      let result2 = letter2;
      let is2 = true;

      for (let ind3 = 0; ind3 < key3.length; ind3++) {
        const letter3 = key3[ind3];
        let result3 = letter3;
        let is3 = true;
        is2 = false;

        for (let ind4 = 0; ind4 < key4.length; ind4++) {
          const letter4 = key4[ind4];
          let result4 = letter4;
          is3 = false;

          result.add(letter1 + letter2 + letter3 + letter4);
        }

        is3 && result.add(letter1 + letter2 + letter3);
      }

      is2 && result.add(letter1 + letter2);
    }
  }

  return [...result];
};
```
