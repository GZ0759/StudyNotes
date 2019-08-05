# 001 - 两数之和（two-sum）

* 难度：简单
* 涉及知识：数组、哈希表
* 题目地址：https://leetcode-cn.com/problems/two-sum/
* 题目内容：

```
给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

示例:

给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

## 解法-for()

```js
var twoSum = function(nums, target) {
  for (let i = 0; i < nums.length; i++) {
    for (let j = i + 1; j < nums.length; j++) {
      if (nums[j] === target - nums[i]) {
        return [i, j];  // 如果成立就返回两个数字的索引
      }
    }
  }
};
```

## 解法-indexOf()

```js
var twoSum = function(nums, target) {
  let result = [];
  nums.map((item, index) => {
    if (nums.indexOf(target - item) > -1 && nums.indexOf(target - item) != index) {
      result = [index, nums.indexOf(target - item)].sort((a, b) => a > b);
    }
  });
  return result;
};
```

## 解法-Map

```js
var twoSum = function(nums, target) {
  let map = new Map();
  for (let i = 0; i < nums.length; i++) {
    if (map.has(nums[i])) {
      return [map.get(nums[i]), i];
    } else {
      map.set(target - nums[i], i);
    }
  }
};
```