# Grind 75

Solutions for some problems of [Grind 75](https://www.techinterviewhandbook.org/grind75)

## [1. Two Sum](https://leetcode.com/problems/two-sum/)

```HTML
var twoSum = function(nums, target) {
  let map = {};

  for (let i = 0; i < nums.length; i++) {
    let n = nums[i],
    part = target - n;

    if(map[part] >= 0) return [map[part], i];
    else map[n] = i;
  }

  return -1;
};
```

_Map, O(n)_

## [2. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

```HTML
var isValid = function(s) {
  const stack = [],
    open = {
      "(" : ")",
      "[" : "]",
      "{" : "}"
    };

  for (let char of s) {
    if(open[char]) {
      stack.push(char)
    } else {
      if(open[stack.pop()] !== char) return false;
    }
  }

  return stack.length === 0;
};
```

_Stack, O(n)_

## [3. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)

```HTML
var mergeTwoLists = function(l1, l2) {
    if(!l1 || !l2) return l1 || l2;

    if(l1.val < l2.val) {
        l1.next = mergeTwoLists(l1.next, l2)
        return l1;
    }
    l2.next = mergeTwoLists(l1, l2.next)
    return l2;
};
```

_Recursion, O(n)_
