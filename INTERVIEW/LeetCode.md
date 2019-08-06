# 001 - 两数之和（two-sum）

* 难度：简单
* 涉及知识：数组、哈希表
* 题目地址：https://leetcode-cn.com/problems/two-sum/
* 题目内容：

给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。  
你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。  
示例:  
给定 nums = [2, 7, 11, 15], target = 9  
因为 nums[0] + nums[1] = 2 + 7 = 9  
所以返回 [0, 1]  

```js
// 例子
var nums=[2, 7, 11, 15], target = 9;
console.log(twoSum(nums, target))  // [0, 1]
```

## 解法 - for()

```js
var twoSum = function(nums, target) {
  for (let i = 0; i < nums.length; i++) {
    for (let j = i + 1; j < nums.length; j++) {
      if (nums[j] === target - nums[i]) {
        // 如果成立就返回两个数字的索引
        return [i, j]; 
      }
    }
  }
};
```

## 解法 - indexOf()

```js
var twoSum = function(nums, target) {
  let result = [];
  nums.map((item, index) => {
    // 另一个符合条件的数的下标
    let theOther = nums.indexOf(target - item);
    if (theOther > -1 && theOther != index) {
      result = [index, theOther].sort((a, b) => a - b);
    }
  });
  return result;
};
```

## 解法 - Map

```js
var twoSum = function(nums, target) {
  let map = new Map();
  for (let i = 0; i < nums.length; i++) {
    // 选中值
    let one = nums[i];
    // 选中值的匹配值
    let theOther = target - nums[i];
    if (map.has(one)) {
      // 找到匹配值
      return [map.get(one), i];
    } else {
      // 存入匹配值
      map.set(theOther, i);
    }
  }
};
```

# 007 - 整数反转（reverse-integer）

* 难度：简单
* 涉及知识：数组、数学
* 题目地址：https://leetcode-cn.com/problems/reverse-integer/
* 题目内容：

给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。 

示例 1:  
输入: 123  
输出: 321  

示例 2:  
输入: -123  
输出: -321  

示例 3:  
输入: 120  
输出: 21  

注意:  
假设我们的环境只能存储得下 32 位的有符号整数，则其数值范围为 [−231,  231 − 1]。请根据这个假设，如果反转后整数溢出那么就返回 0。  

## 解法 - 转字符串

```js
var reverse = function(x) {
  // 转数组
  let numberToArray = String(Math.abs(x)).split('');
  
  // 转字符串
  let result = '';
  for (const i = 0; i < numberToArray.length; ) {
    result += numberToArray.pop();
  }
  // 检测正负
  result = x > 0 ? Number(result) : - Number(result);
  
  // 超 [-Math.pow(2, 31), Math.pow(2, 31) - 1] 判断
  if (result > Math.pow(2, 31) - 1
  || result < - Math.pow(2, 31)) {
    result = 0;
  }
  
  return result;
};
```

## 解法 - 数学算法

```js
var reverse = function(x) {
  let result = 0;
  let y = Math.abs(x);
  while (y != 0) {
    result = result * 10 + y % 10;
    y = Math.floor(y / 10);
    if (result > Math.pow(2, 31) - 1
    || result < -Math.pow(2, 31)) {
      result = 0;
      y = 0;
    }
  }
  return x > 0 ? result : -result;
};
```

# 009 - 回文数（palindrome-number）

* 难度：简单
* 涉及知识：数学
* 题目地址：https://leetcode-cn.com/problems/palindrome-number/
* 题目内容：

判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。  

示例 1:  
输入: 121  
输出: true  

示例 2:  
输入: -121  
输出: false  
解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。  

示例 3:  
输入: 10  
输出: false  
解释: 从右向左读, 为 01 。因此它不是一个回文数。  

```ja
var a = 121, b = -121, c = 10;
console.log(isPalindrome(a), isPalindrome(b), isPalindrome(c))
```

## 解题 - 数组操作

```js
var isPalindrome = function(x) {
  // 整数转数组
  const arr = String(x).split('');
  for (let i = 0; i < arr.length / 2; i++) {
    // i的对称下标
    let j = arr.length - (i + 1);
    if (arr[i] !== arr[j]) {
      return false;
    }
  }
  return true;
};
```

## 解题 - 数学算法

```js
var isPalindrome = function(x) {
  if(x < 0 || (x % 10 == 0 && x != 0)) {
    return false;
  }
  let revertedNumber = 0;
  while(x > revertedNumber) {
    revertedNumber = revertedNumber * 10 + x % 10;
    x = Math.floor(x / 10);
  }
  return x === revertedNumber || x === Math.floor(revertedNumber / 10);
};
```

