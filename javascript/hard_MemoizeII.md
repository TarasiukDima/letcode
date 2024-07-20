# Memoize II

[Task link](https://leetcode.com/problems/memoize-ii/description/)

Given a function fn, return a memoized version of that function.

A memoized function is a function that will never be called twice with the same inputs. Instead it will return a cached value.

fn can be any function and there are no constraints on what type of values it accepts. Inputs are considered identical if they are === to each other.

Example 1:
Input:
getInputs = () => [[2,2],[2,2],[1,2]]
fn = function (a, b) { return a + b; }
Output: [{"val":4,"calls":1},{"val":4,"calls":1},{"val":3,"calls":2}]
Explanation:
const inputs = getInputs();
const memoized = memoize(fn);
for (const arr of inputs) {
memoized(...arr);
}

For the inputs of (2, 2): 2 + 2 = 4, and it required a call to fn().
For the inputs of (2, 2): 2 + 2 = 4, but those inputs were seen before so no call to fn() was required.
For the inputs of (1, 2): 1 + 2 = 3, and it required another call to fn() for a total of 2.

Example 2:
Input:
getInputs = () => [[{},{}],[{},{}],[{},{}]]
fn = function (a, b) { return ({...a, ...b}); }
Output: [{"val":{},"calls":1},{"val":{},"calls":2},{"val":{},"calls":3}]
Explanation:
Merging two empty objects will always result in an empty object. It may seem like there should only be 1 call to fn() because of cache-hits, however none of those objects are === to each other.

Example 3:
Input:
getInputs = () => { const o = {}; return [[o,o],[o,o],[o,o]]; }
fn = function (a, b) { return ({...a, ...b}); }
Output: [{"val":{},"calls":1},{"val":{},"calls":1},{"val":{},"calls":1}]
Explanation:
Merging two empty objects will always result in an empty object. The 2nd and 3rd third function calls result in a cache-hit. This is because every object passed in is identical.

Constraints:

- 1 <= inputs.length <= 105
- 0 <= inputs.flat().length <= 105
- inputs[i][j] != NaN

## Solution

```javascript
// first variant
const BAD_VALUE = "None";
const EMPTY_OBJ = "Empty_OBJ";

const getFirstKeyFromArgs = (args) =>
  args.length ? getKeyItemArgs(args[0]) : EMPTY_OBJ;

const getKeyItemArgs = (arg) => {
  if (arg === undefined) {
    return "undefined";
  }

  if (arg === null) {
    return "null";
  }

  if (typeof arg === "number" && isNaN(arg)) {
    return "NaN";
  }

  return arg;
};

const getKeyFromCache = (cache, args) => {
  try {
    const keyFirst = getFirstKeyFromArgs(args);
    let elInCache = cache.get(keyFirst);

    if (!elInCache) {
      throw new Error();
    }

    for (let ind = 1; ind < args.length; ind++) {
      const key = getKeyItemArgs(args[ind]);

      if (!elInCache || !elInCache.has(key)) {
        throw new Error();
      }

      elInCache = elInCache.get(key);
    }

    return elInCache && elInCache.has("result")
      ? elInCache.get("result")
      : BAD_VALUE;
  } catch {
    return BAD_VALUE;
  }
};

const setKeyFromCache = (cache, args, result) => {
  const keyFirst = getFirstKeyFromArgs(args);

  if (!cache.has(keyFirst)) {
    cache.set(keyFirst, new Map());
  }

  let curEl = cache.get(keyFirst);

  try {
    for (let ind = 1; ind < args.length; ind++) {
      const key = getKeyItemArgs(args[ind]);

      if (!curEl.has(key)) {
        curEl.set(key, new Map());
      }
      curEl = curEl.get(key);
    }

    curEl.set("result", result);
  } catch {
    return null;
  }
};

const memoize = (fn) => {
  const cache = new Map();

  return function (...args) {
    const cacheResult = getKeyFromCache(cache, args);

    if (cacheResult !== BAD_VALUE) {
      return cacheResult;
    }

    const result = fn(...args);
    setKeyFromCache(cache, args, result);

    return result;
  };
};



// second variant
const memoize = (fn) => {
  const cache = new Map();

  return function (...args) {
    let currentItem = cache;

    for (const arg of args) {
      if (!currentItem.has(arg)) {
        currentItem.set(arg, new Map());
      }

      currentItem = currentItem.get(arg);
    }

    if (currentItem.has("result")) {
      return currentItem.get("result");
    }

    const result = fn(...args);
    currentItem.set("result", result);

    return result;
  };
};
```
