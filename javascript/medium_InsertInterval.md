# Insert Interval

[Task link](https://leetcode.com/problems/insert-interval/description/)

You are given an array of non-overlapping intervals intervals where intervals[i] = [starti, endi] represent the start and the end of the ith interval and intervals is sorted in ascending order by starti. You are also given an interval newInterval = [start, end] that represents the start and end of another interval.

Insert newInterval into intervals such that intervals is still sorted in ascending order by starti and intervals still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return intervals after the insertion.

Note that you don't need to modify intervals in-place. You can make a new array and return it.

Example 1:
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]

Example 2:
Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
Output: [[1,2],[3,10],[12,16]]
Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].

Constraints:

- 0 <= intervals.length <= 104
- intervals[i].length == 2
- 0 <= starti <= endi <= 105
- intervals is sorted by starti in ascending order.
- newInterval.length == 2
- 0 <= start <= end <= 105

## Solution

```javascript
// variant 1
const merge = (intervals) => {
  if (!intervals.length) return intervals;

  intervals.sort((a, b) => a[0] - b[0]);

  const result = [[...intervals[0]]];
  for (let ind = 1; ind < intervals.length; ind++) {
    const cur = intervals[ind];
    const endLast = result[result.length - 1][1];

    if (cur[0] > endLast) {
      result.push(cur);
      continue;
    }

    result[result.length - 1][1] = Math.max(endLast, cur[1]);
  }

  return result;
};

const insert = (intervals, newInterval) => {
  return merge([...intervals, newInterval]);
};

// variant 2
const insert = (intervals, newInterval) => {
  if (!intervals.length) return [newInterval];

  const countItems = intervals.length;
  const result = [];
  let ind = 0;

  while (ind < countItems && intervals[ind][1] < newInterval[0]) {
    result.push(intervals[ind]);
    ind++;
  }

  result.push(newInterval);

  for (; ind < countItems; ind++) {
    const prev = result[result.length - 1];
    const next = intervals[ind];

    if (prev && prev[1] >= next[0]) {
      prev[0] = Math.min(prev[0], next[0]);
      prev[1] = Math.max(prev[1], next[1]);
    } else {
      result.push(next);
    }
  }

  return result;
};
```
