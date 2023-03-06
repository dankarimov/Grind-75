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

## [8. Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/)

```HTML
var diameterOfBinaryTree = function(root) {
    let diameter = 0;

    function helper(node) {
        if(!node) return 0;

        const left = helper(node.left);
        const right = helper(node.right);

        diameter = Math.max(diameter, left + right);

        return Math.max(left, right) + 1;
    }

    helper(root);

    return diameter;
};
```

_Recursion, O(n)_

## [9. Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/)

```HTML
var middleNode = function(head) {
    let moveByOne = moveByTwo = head;

    while(moveByTwo && moveByTwo.next) {
        moveByOne = moveByOne.next;
        moveByTwo = moveByTwo.next.next;
    }

    return moveByOne;
};
```

_Loop, O(n)_

## [10. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

```HTML
var maxDepth = function(root) {
    return root === null
        ? 0
        : Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
};
```

_Recursion, O(n)_

## [11. Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)

```HTML
var containsDuplicate = function(nums) {
    return new Set(nums).size < nums.length;
};
```

_Set, O(n)_

_Recursion, O(n)_

## [12. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)

```HTML
var maxSubArray = function(nums) {
    let max = nums[0],
        cur = 0;

    for (let n of nums) {
        if(cur < 0) cur = 0;

        cur += n;

        max = Math.max(cur, max);
    }

    return max;
};
```

_Loop, O(n)_

## Week 3

## [1. Insert Interval](https://leetcode.com/problems/insert-interval/)

```HTML
var insert = function(intervals, newInterval) {
    const res = [];

    for (let interval of intervals) {
        const [start, end] = interval,
            [newStart, newEnd] = newInterval,
            min = Math.min(newStart, start),
            max = Math.max(newEnd, end);

    if (newEnd < start) {
        res.push(newInterval);
        newInterval = interval;
    } else if (end < newStart) res.push(interval);
        else newInterval = [min, max];
    }

    res.push(newInterval);

    return res;
};
```

_Loop, O(n)_

## [4. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)

```HTML
var lengthOfLongestSubstring = function(s) {
    const set = new Set();
    let left = right = max = 0;

    while(right < s.length) {
        const rChar = s[right];

        if(!set.has(rChar)) {
            set.add(rChar);
            max = Math.max(max, set.size);
            right++;
        } else {
            const lChar = s[left];
            set.delete(lChar);
            left++;
        }
    }

    return max;
};
```

_2 pointers, O(n)_

## [5. 3Sum](https://leetcode.com/problems/3sum/)

```HTML
var threeSum = function(nums) {
    nums.sort((a,b) => a - b);
    let res = [];

    for (let i = 0; i < nums.length - 2; i++) {
        if(i > 0 && nums[i] === nums[i - 1]) continue;

        let left = i + 1,
            right = nums.length - 1;

        while (left < right) {
            let sum = nums[i] + nums[left] + nums[right];

            if(sum === 0) {
                res.push([nums[i], nums[left], nums[right]]);
                while(nums[left] === nums[left + 1]) left++;
                while(nums[right] === nums[right - 1]) right--;
            }

            if(sum < 0) left++;
            else right--;
        }
    }

    return res;
};
```

_2 pointers, O(n^2)_

## [6. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)

```HTML
var levelOrder = function(root) {
    const res = [],
          level = 0;

     function traverse(node, level) {
        if (node === null) return;
        if (level === res.length) res[level] = [];

        res[level].push(node.val);

        traverse(node.left, level + 1);
        traverse(node.right, level + 1);
     }

    traverse(root, level);

    return res;
};
```

_2 pointers, O(n^2)_

## [8. Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/)

```HTML
var evalRPN = function(tokens) {
    const op = {
        "+": (b, a) => a + b,
        "-": (b, a) => a - b,
        "*": (b, a) => a * b,
        "/": (b, a) => Math.trunc(a / b),
    }, stack = [];

  for (let t of tokens) {
    const exp = op[t];

    if (exp) stack.push(exp(+stack.pop(), +stack.pop()));
    else stack.push(t);
  }

  return stack[0];
};
```

_Loop, O(n)_

## Week 4

## [3. Coin Change](https://leetcode.com/problems/coin-change/)

```HTML
var coinChange = function(coins, amount) {
  let dp = Array(amount + 1).fill(Infinity);
  dp[0] = 0;

  for (let i = 1; i <= amount; i++) {
    for (let coin of coins) {
      const pos = i - coin;

      if (pos >= 0) {
        dp[i] = Math.min(dp[i], dp[pos] + 1);
      }
    }
  }

  return dp[amount] != Infinity ? dp[amount] : -1;
};
```

_DP, O(n \* amount)_
