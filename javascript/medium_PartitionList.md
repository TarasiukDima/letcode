# Partition List

[Task link](https://leetcode.com/problems/partition-list/description/)

Given the head of a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

You should preserve the original relative order of the nodes in each of the two partitions.

Example 1:
Input: head = [1,4,3,2,5,2], x = 3
Output: [1,2,2,4,3,5]

Example 2:
Input: head = [2,1], x = 2
Output: [1,2]

Constraints:

- The number of nodes in the list is in the range [0, 200].
- -100 <= Node.val <= 100
- -200 <= x <= 200

## Solution

```javascript
// variant 1
const partition = (head, x) => {
  const less = [];
  const greather = [];

  let curItem = head;
  while (curItem) {
    if (curItem.val >= x) {
      greather.push(curItem.val);
    } else {
      less.push(curItem.val);
    }

    curItem = curItem.next;
  }

  let newHead = null;
  let curNewHead = null;
  for (let ind = 0; ind < less.length; ind++) {
    if (!newHead) {
      newHead = new ListNode(less[ind]);
      curNewHead = newHead;
    } else {
      curNewHead.next = new ListNode(less[ind]);
      curNewHead = curNewHead.next;
    }
  }

  for (let ind = 0; ind < greather.length; ind++) {
    if (!newHead) {
      newHead = new ListNode(greather[ind]);
      curNewHead = newHead;
    } else {
      curNewHead.next = new ListNode(greather[ind]);
      curNewHead = curNewHead.next;
    }
  }

  return newHead;
};

// variant 2
const partition = (head, x) => {
  let less = null;
  let curLess = null;
  let greather = null;
  let curGreater = null;
  let curItem = head;

  while (curItem) {
    const num = curItem.val;

    if (num >= x && !greather) {
      greather = new ListNode(num);
      curGreater = greather;
    } else if (num >= x && greather) {
      curGreater.next = new ListNode(num);
      curGreater = curGreater.next;
    } else if (num < x && !less) {
      less = new ListNode(num);
      curLess = less;
    } else {
      curLess.next = new ListNode(num);
      curLess = curLess.next;
    }

    curItem = curItem.next;
  }

  if (!less) return greather;
  curLess.next = greather;

  return less;
};
```
