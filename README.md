# Grind 75

Solutions for some problems of [Grind 75](https://www.techinterviewhandbook.org/grind75)

## Week 1

## [1. Two Sum](https://leetcode.com/problems/two-sum/)

```HTML
var twoSum = function(nums, target) {
  const map = {};

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

## [4. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

```HTML
var maxProfit = function(prices) {
  let minPrice = Number.MAX_VALUE,
      profit = 0;

  for (let price of prices) {
    if(price < minPrice) minPrice = price;
    else profit = Math.max(price - minPrice, profit);
  }

  return profit;
};
```

_Loop, O(n)_

## [5. Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)

```HTML
var isPalindrome = function(s) {
  const str = s.toLowerCase().replace(/[^a-z0-9]/g, "");

  let left = 0,
      right = str.length - 1;

  while(left < right) {
    if(str[left] !== str[right]) return false;
    left++;
    right--;
  }

  return true;
};
```

_Loop, O(n)_

## [6. Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/)

```HTML
var invertTree = function(root) {
    if(!root) return root;

    [root.left, root.right] = [root.right, root.left];

    invertTree(root.left);
    invertTree(root.right);

    return root;
};
```

_Recursive dfs, O(n)_

## [7. Valid Anagram](https://leetcode.com/problems/valid-anagram/)

```HTML
var isAnagram = function(s, t) {
    if(s.length !== t.length) return false;

    const map = {};

    for (let c of s) {
        map[c] = map[c] + 1 || 1;
    }

    for (let c of t) {
        if(!map[c] || map[c] < 1) return false;
        map[c]--;
    }

    return true;
};
```

_Map, O(n)_

## [8. Binary Search](https://leetcode.com/problems/binary-search/description/)

```HTML
var search = function(nums, target) {
    let start = 0,
        end = nums.length - 1,
        middle = Math.floor((start + end) / 2);

    while(nums[middle] !== target && start <= end) {
        if(target < nums[middle]) end = middle - 1;
        else start = middle + 1;

        middle = Math.floor((start + end) / 2);
    }

    return nums[middle] === target ? middle : -1;
};
```

_O(log n)_

## [9. Flood Fill](https://leetcode.com/problems/flood-fill/)

```HTML
var floodFill = function(image, sr, sc, color) {
    const initialColor = image[sr][sc],
        rLen = image.length,
        cLen = image[0].length;

    function helper(sr, sc) {
        if(sr < 0 || sc < 0 || sr >= rLen || sc >= cLen || image[sr][sc] !== initialColor || image[sr][sc] === color) return;

        image[sr][sc] = color;

        helper(sr + 1, sc);
        helper(sr - 1, sc);
        helper(sr, sc + 1);
        helper(sr, sc - 1);
    }

    helper(sr, sc);

    return image;
};
```

_DFS, O(n\*m)_

## [9. Flood Fill](https://leetcode.com/problems/flood-fill/)

```HTML
var floodFill = function(image, sr, sc, color) {
    const initialColor = image[sr][sc],
        rLen = image.length,
        cLen = image[0].length;

    function helper(sr, sc) {
        if(sr < 0 || sc < 0 || sr >= rLen || sc >= cLen || image[sr][sc] !== initialColor || image[sr][sc] === color) return;

        image[sr][sc] = color;

        helper(sr + 1, sc);
        helper(sr - 1, sc);
        helper(sr, sc + 1);
        helper(sr, sc - 1);
    }

    helper(sr, sc);

    return image;
};
```

_DFS, O(n\*m)_

## [11. Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/)

```HTML
var isBalanced = function(root) {
    function dfs(node) {
        if (!node) return 0;

        let left = 1 + dfs(node.left),
            right = 1 + dfs(node.right);

        if (Math.abs(left - right) > 1) return Infinity;

        return Math.max(left, right);
    }

    return dfs(root) === Infinity ? false : true;
};
```

_DFS, O(n)_

## [12. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

```HTML
var hasCycle = function(head) {
  let moveByOne = head,
      moveByTwo = head;

  while(moveByTwo !== null) {
    moveByOne = moveByOne?.next;

    if(moveByTwo.next === null) return false;
    moveByTwo = moveByTwo.next.next;

    if(moveByOne === moveByTwo) return true;
  }

  return false
};
```

_Two pointers, O(n)_

## Week 2

## [1. First Bad Version](https://leetcode.com/problems/first-bad-version/)

```HTML
var solution = function(isBadVersion) {
    return function(n) {
        let left = 1,
            right = n;

        while(left <= right) {
            let mid = Math.floor((right + left) / 2);

            if(isBadVersion(mid)) right = mid - 1;
            else left = mid + 1;
        }

        return left;
    };
};
```

_Binary search, O(log n)_

## [2. Ransom Note](https://leetcode.com/problems/ransom-note/)

```HTML
var canConstruct = function(ransomNote, magazine) {
    if(magazine.length < ransomNote.length) return false;
    const map = {};

    for (let c of magazine) map[c] = map[c] + 1 || 1;

    for (let c of ransomNote) {
        if(map[c] > 0) map[c]--;
        else return false;
    }

    return true;
};
```

_Map, O(n)_

## [3. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)

```HTML
var climbStairs = function(n, memo = []) {
    if (n <= 2) return n;

    if (memo[n]) return memo[n];

    memo[n] = climbStairs(n-1, memo) + climbStairs(n-2, memo);
    return memo[n];
};
```

_DP, O(n)_

## [4. Longest Palindrome](https://leetcode.com/problems/longest-palindrome/)

```HTML
var longestPalindrome = function(s) {
    const map = {};
    let max = 0;

    for (let c of s) {
        map[c] = map[c] + 1 || 1;
        if(map[c] % 2 === 0) max += 2;
    }

    return s.length > max ? max + 1 : max;
};
```

_Map, O(n)_

## [5. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)

```HTML
var reverseList = function(head) {
    let prev = null,
        current = head,
        next;

    while(current) {
      next = current.next;
      current.next = prev;
      prev = current;
      current = next;
    }

    head = prev;
    return head;
};
```

_Loop, O(n)_

## [6. Majority Element](https://leetcode.com/problems/majority-element/)

```HTML
var majorityElement = function(nums) {
    const map = {};
    let majorityCount = nums.length / 2;

    for (let num of nums) map[num] = map[num] + 1 || 1;

    for(let count in map) {
      if (map[count] > majorityCount) return count;
    }
};
```

_Map, O(n)_

## [7. Add Binary](https://leetcode.com/problems/add-binary/)

```HTML
let addBinary = (a, b) => {
  let carry = 0,
      res = '',
      lenA = a.length - 1,
      lenB = b.length - 1;

  while (lenA >= 0 || lenB >= 0 || carry > 0) {
    let n1 = +a[lenA],
        n2 = +b[lenB],
        sum = (n1 || 0) + (n2 || 0) + carry;

    if (sum > 1) {
      sum = sum % 2;
      carry = 1;
    } else carry = 0;

    res = sum + res;

    lenA--;
    lenB--;
  }

  return res;
};
```

_Loop, O(n + m)_
