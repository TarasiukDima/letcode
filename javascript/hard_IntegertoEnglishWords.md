# Integer to English Words

[Task link](https://leetcode.com/problems/integer-to-english-words/description/)

Convert a non-negative integer num to its English words representation.

Example 1:
Input: num = 123
Output: "One Hundred Twenty Three"

Example 2:
Input: num = 12345
Output: "Twelve Thousand Three Hundred Forty Five"

Example 3:
Input: num = 1234567
Output: "One Million Two Hundred Thirty Four Thousand Five Hundred Sixty Seven"

Constraints:

-0 <= num <= 231 - 1

## Solution

```javascript
const numberToWords = (num) => {
  if (num === 0) return "Zero";

  const numWords = {
    1: "One",
    2: "Two",
    3: "Three",
    4: "Four",
    5: "Five",
    6: "Six",
    7: "Seven",
    8: "Eight",
    9: "Nine",
    10: "Ten",
    11: "Eleven",
    12: "Twelve",
    13: "Thirteen",
    14: "Fourteen",
    15: "Fifteen",
    16: "Sixteen",
    17: "Seventeen",
    18: "Eighteen",
    19: "Nineteen",
    20: "Twenty",
    30: "Thirty",
    40: "Forty",
    50: "Fifty",
    60: "Sixty",
    70: "Seventy",
    80: "Eighty",
    90: "Ninety",
  };

  const numParts = {
    100: "Hundred",
    1_000: "Thousand",
    1_000_000: "Million",
    1_000_000_000: "Billion",
    // 1_000_000_000_000: "Trillion",
    // 1_000_000_000_000_000: "Quadrillion",
    // 1_000_000_000_000_000_000: "Quintillion",
    // 1_000_000_000_000_000_000_000: "Sextillion",
  };

  const getThousendText = (num) => {
    if (num === 0) return "";

    const numItem = num % 10;
    num = Math.floor(num / 10);
    const ten = (num % 10) * 10;
    const tenForCheck = ten + numItem;
    num = Math.floor(num / 10);
    const hundred = num % 10;

    let numString = " ";

    if (hundred) {
      numString += `${numWords[hundred]} ${numParts[100]} `;
    }

    if (
      ten > 0 &&
      ((tenForCheck > 9 && tenForCheck < 20) || tenForCheck % 10 === 0)
    ) {
      numString += numWords[tenForCheck] + " ";
    } else {
      numString += ten > 0 ? numWords[ten] + " " : "";
      numString += numItem > 0 ? numWords[numItem] + " " : "";
    }

    return numString.trim();
  };

  const STEP_SIZE = 1000;
  let result = "";
  let numberPart = 1;

  while (num > 0) {
    const numStep = num % STEP_SIZE;
    const numResult = getThousendText(numStep);

    num = Math.floor(num / STEP_SIZE);
    numberPart *= STEP_SIZE;

    if (!numResult) continue;

    const partIndex = numberPart / STEP_SIZE;
    const partToAdd = numParts[partIndex] ? ` ${numParts[partIndex]} ` : "";
    result = numResult + partToAdd + result;
  }

  return result.trim();
};
```
