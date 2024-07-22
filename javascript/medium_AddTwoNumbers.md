# Add Two Numbers

[Task link]https://leetcode.com/problems/add-two-numbers/description/)

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example 1:
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.

Example 2:
Input: l1 = [0], l2 = [0]
Output: [0]

Example 3:
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]

Constraints:

- The number of nodes in each linked list is in the range [1, 100].
- 0 <= Node.val <= 9
- It is guaranteed that the list represents a number that does not have leading zeros.

## Solution

```javascript
// function ListNode(val, next) {
//   this.val = (val === undefined ? 0 : val)
//   this.next = (next === undefined ? null : next)
// }

const createListFromArray = (arr) => {
  const result = new ListNode(arr[0]);
  let curerntItem = result;

  for (let ind = 1; ind < arr.length; ind++) {
    curerntItem.next = new ListNode(arr[ind]);
    curerntItem = curerntItem.next;
  }

  return result;
};

const getSumVals = (val1, val2, last = 0) => {
  const sum = val1 + val2 + last;
  return {
    num: sum % 10,
    last: parseInt(sum / 10),
  };
};

const addTwoNumbers = (l1, l2) => {
  const numbers = [];
  let l1Node = l1;
  let l2Node = l2;
  let lastSum = 0;

  while (l1Node || l2Node) {
    const val1 = l1Node?.val ?? 0;
    const val2 = l2Node?.val ?? 0;
    const { num, last } = getSumVals(val1, val2, lastSum);

    numbers.push(num);
    lastSum = last;

    l1Node = l1Node?.next ?? null;
    l2Node = l2Node?.next ?? null;
  }

  lastSum && numbers.push(lastSum);

  return createListFromArray(numbers);
};
```
