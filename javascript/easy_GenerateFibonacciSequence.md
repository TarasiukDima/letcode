# Generate Fibonacci Sequence

[Task link](https://leetcode.com/problems/generate-fibonacci-sequence/description/)

Write a generator function that returns a generator object which yields the fibonacci sequence.

The fibonacci sequence is defined by the relation Xn = Xn-1 + Xn-2.

The first few numbers of the series are 0, 1, 1, 2, 3, 5, 8, 13.

Example 1:

Input: callCount = 5
Output: [0,1,1,2,3]
Explanation:
const gen = fibGenerator();
gen.next().value; // 0
gen.next().value; // 1
gen.next().value; // 1
gen.next().value; // 2
gen.next().value; // 3
Example 2:

Input: callCount = 0
Output: []
Explanation: gen.next() is never called so nothing is outputted

## Solution

```javascript
const fibGenerator = function* () {
  const figValues = [0, 1];

  yield figValues[0];
  yield figValues[1];

  while (true) {
    figValues.push(
      figValues[figValues.length - 1] + figValues[figValues.length - 2]
    );
    yield figValues[figValues.length - 1];
  }
};


// without array
const fibGenerator = function* () {
    let prevLast = 0;
    let last = 1;

    yield prevLast;
    yield last;

    while (true) {
        const showResult = prevLast + last;
        prevLast = last;
        last = showResult;

        yield showResult;
    }
};
```
