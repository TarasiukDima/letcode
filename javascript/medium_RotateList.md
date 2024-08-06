# Rotate List

[Task link](https://leetcode.com/problems/rotate-list/description/)

Given the head of a linked list, rotate the list to the right by k places.

Example 1:
Input: head = [1,2,3,4,5], k = 2
Output: [4,5,1,2,3]

Example 2:
Input: head = [0,1,2], k = 4
Output: [2,0,1]

Constraints:

- The number of nodes in the list is in the range [0, 500].
- -100 <= Node.val <= 100
- 0 <= k <= 2 \* 109

## Solution

```javascript
const rotateRight = (head, k) => {
  if (!head || !head.next || !k) return head;

  let lastNode = head;
  let countItems = 1;
  while (lastNode.next) {
    lastNode = lastNode.next;
    countItems++;
  }

  let steps = countItems - (k % countItems);
  let left = head;
  while (steps > 1) {
    left = left.next ? left.next : head;
    steps--;
  }

  if (left === lastNode) return head;

  const newHead = left.next;
  left.next = null;
  lastNode.next = head;

  return newHead;
};
```
