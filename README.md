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
*Map, O(n)*
