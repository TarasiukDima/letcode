# Remove Nth Node From End of List

[Task link](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/)

Given the head of a linked list, remove the nth node from the end of the list and return its head.

Example 1:

Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
Example 2:

Input: head = [1], n = 1
Output: []
Example 3:

Input: head = [1,2], n = 1
Output: [1]

Constraints:

- The number of nodes in the list is sz.
- 1 <= sz <= 30
- 0 <= Node.val <= 100
- 1 <= n <= sz

## Solution

```javascript
const removeNthFromEnd = (head, n) => {
  if (!head || !head.next) return null;

  const nums = [];
  let cur = head;

  while (cur) {
    nums.push(cur.val);
    cur = cur.next;
  }

  let removeInd = nums.length - n;
  if (removeInd <= 0) {
    return head.next ?? null;
  }

  cur = head;
  while (removeInd > 1) {
    cur = cur.next;
    removeInd--;
  }

  const next = cur.next.next ?? null;
  cur.next = next;

  return head;
};
```
