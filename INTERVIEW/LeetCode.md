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

```js
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

# 013 - 罗马数字转整数（roman-to-integer）

* 难度：简单
* 涉及知识：数学、字符串
* 题目地址：https://leetcode-cn.com/problems/roman-to-integer/
* 题目内容：

罗马数字包含以下七种字符: I， V， X， L，C，D 和 M。

| 字符 | 数值 |
| ---- | ---- |
| I    | 1    |
| V    | 5    |
| X    | 10   |
| L    | 50   |
| C    | 100  |
| D    | 500  |
| M    | 1000 |

例如， 罗马数字 2 写做 II ，即为两个并列的 1。12 写做 XII ，即为 X + II 。 27 写做  XXVII, 即为 XX + V + II 。

通常情况下，罗马数字中小的数字在大的数字的右边。但也存在特例，例如 4 不写做 IIII，而是 IV。数字 1 在数字 5 的左边，所表示的数等于大数 5 减小数 1 得到的数值 4 。同样地，数字 9 表示为 IX。这个特殊的规则只适用于以下六种情况：

I 可以放在 V (5) 和 X (10) 的左边，来表示 4 和 9。
X 可以放在 L (50) 和 C (100) 的左边，来表示 40 和 90。 
C 可以放在 D (500) 和 M (1000) 的左边，来表示 400 和 900。
给定一个罗马数字，将其转换成整数。输入确保在 1 到 3999 的范围内。

示例 1:
输入: "III"
输出: 3

示例 2:
输入: "IV"
输出: 4

示例 3:
输入: "IX"
输出: 9

示例 4:
输入: "LVIII"
输出: 58
解释: L = 50, V= 5, III = 3.

示例 5:
输入: "MCMXCIV"
输出: 1994
解释: M = 1000, CM = 900, XC = 90, IV = 4.

## 解法 - for()

```js
var romanToInt = function(s) {
  const arr = s.split('');
  let result = 0;
  
  for (let i = 0; i < arr.length; ) {
    if (arr[i] === 'I' && arr[i+1] === 'V') {
      result += 4;
      i = i + 2;
    } else if(arr[i] === 'I' && arr[i+1] === 'X') {
      result += 9;
      i = i + 2;
    } else if(arr[i] === 'X' && arr[i+1] === 'L') {
      result += 40;
      i = i + 2;
    } else if(arr[i] === 'X' && arr[i+1] === 'C') {
      result += 90;
      i = i + 2;
    } else if(arr[i] === 'C' && arr[i+1] === 'D') {
      result += 400
      i = i + 2;
    } else if(arr[i] === 'C' && arr[i+1] === 'M') {
      result += 900;
      i = i + 2;
    } else if (arr[i] === 'I') {
      result += 1;
      i = i + 1;
    } else if (arr[i] === 'V') {
      result += 5;
      i = i + 1;
    } else if (arr[i] === 'X') {
      result += 10;
      i = i + 1;
    } else if (arr[i] === 'L') {
      result += 50;
      i = i + 1;
    } else if (arr[i] === 'C') {
      result += 100;
      i = i + 1;
    } else if (arr[i] === 'D') {
      result += 500;
      i = i + 1;
    } else if (arr[i] === 'M') {
      result += 1000;
      i = i + 1;
    }
  }

  return result;
};
```

##  解法 - Map

```js
var romanToInt = function(s) {
  let map = new Map();
  map.set('I', 1);
  map.set('V', 5);
  map.set('X', 10);
  map.set('L', 50);
  map.set('C', 100);
  map.set('D', 500);
  map.set('M', 1000)
  
  // let result = 0;
  // for (let i = 0; i < s.length; i++) {
  //   if (s[i] + s[i+1] === 'IV') {
  //     result += 4;
  //     i = i + 1;
  //   } else if(s[i] + s[i+1] === 'IX') {
  //     result += 9;
  //     i = i + 1;
  //   } else if(s[i] + s[i+1] === 'XL') {
  //     result += 40;
  //     i = i + 1;
  //   } else if(s[i] + s[i+1] === 'XC') {
  //     result += 90;
  //     i = i + 1;
  //   } else if(s[i] + s[i+1] === 'CD') {
  //     result += 400
  //     i = i + 1;
  //   } else if(s[i] + s[i+1] === 'CM') {
  //     result += 900;
  //     i = i + 1;
  //   } else {
  //     result += map.get(s[i]);
  //   }
  // }
  
  // return result;

  let re = map.get(s[0]);
  for (let i = 1; i < s.length; i++) {
    if (map.get(s[i-1]) >= map.get(s[i])) {
      re += map.get(s[i]);
    } else {
      re += map.get(s[i]) - 2*map.get(s[i-1]);
    }
  }
  return re;
};
```

# 014 - 最长公共前缀（longest-common-prefix）

* 难度：简单
* 涉及知识：字符串
* 题目地址：https://leetcode-cn.com/problems/longest-common-prefix/
* 题目内容：

```
编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 ""。

示例 1:

输入: ["flower","flow","flight"]
输出: "fl"
示例 2:

输入: ["dog","racecar","car"]
输出: ""
解释: 输入不存在公共前缀。

说明:
所有输入只包含小写字母 a-z 。
```

## 解法 - 暴力破解

```js
var longestCommonPrefix = function(strs) {
  if (!strs.length) {
    return '';
  }
  // 最短字符串的长度
  let shortStrLength = strs[0].length; 
  // 最短字符串的位置
  let shortStrPosition = 0; 
  for (let i = 0; i < strs.length; i++){
    if (strs[i].length < shortStrLength) {
      shortStrLength = strs[i].length;
      shortStrPosition = i;
    }
  }
  let result = [];
  // 字符串中字符的位置
  for (let i = 0; i < shortStrLength; i++) {
    // 字符串的位置
    for (let j = 0; j < strs.length; j++) {
      if (strs[shortStrPosition][i] != strs[j][i]) {
        return result.join('');
      }
      if (j === strs.length - 1) {
        // 遍历字符串找出最短的一个下标
        result[i] = strs[shortStrPosition][i];
      }
    }
  }
  return result.join('');
};
```

## 解法 - 水平扫描

```js
var longestCommonPrefix = function(strs) {
  if (strs.length < 2) {
    return !strs.length ? '' : strs[0];
  }
  
  var result = strs[0];
  
  for(let i = 0; i < result.length; i++) {
    for(let j = 1; j < strs.length; j++) {
      if (result[i] !== strs[j][i]) {
        return result.substring(0, i);
      }
    }
  }
  return result;
};
```

## 解法 - 正则表达式

```js
var longestCommonPrefix = function(strs) {
  if (strs.length < 2) {
    return !strs.length ? '' : strs[0];
  }
  
  let base = strs.shift(),
    joinStrs = '@' + strs.join('@'),
    regx = '@',
    res = '';

  for(let i = 0; i < base.length; i++){
    regx += base.substring(i, i + 1);
    let matchArr = joinStrs.match(new RegExp(`${regx}`,"g")) || [];
    if(matchArr.length === strs.length){
      res += base.substring(i, i+1);
    }
  }
  return res;
};
```

## 解法 - 水平扫描

```js
var longestCommonPrefix = function(strs) {
  if (strs.length < 2) {
    return !strs.length ? '' : strs[0];
  }
  
  return strs.reduce((prev, next) => {
    let i = 0;
    while (prev[i] && next[i] && prev[i] === next[i]) {
      i++;
    };
    return prev.slice(0, i);
  });
};
```

# 020 - 有效的括号（valid-parentheses）

* 难度：简单
* 涉及知识：栈、字符串
* 题目地址：https://leetcode-cn.com/problems/valid-parentheses/
* 题目内容：

```
给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
注意空字符串可被认为是有效字符串。

示例 1:
输入: "()"
输出: true

示例 2:
输入: "()[]{}"
输出: true

示例 3:
输入: "(]"
输出: false

示例 4:
输入: "([)]"
输出: false

示例 5:
输入: "{[]}"
输出: true
```

## 解法 - 栈

```js
var isValid = function(s) {
  let judge = {
    '[': ']',
    '(': ')',
    '{': '}',
  }
  let parameter = s.split('');
  let stack = [];
  for (let i = 0; i < parameter.length; i++) {
    // “左”字符类型的栈的最后一个
    let lastOne = stack[stack.length - 1];
    if (judge[lastOne] === parameter[i]) {
      stack.pop();
    } else {
      stack.push(parameter[i]);
    }
  }
  if (stack.length == 0) {
    return true;
  }
  return false;
};
```

# 021 - 合并两个有序链表（merge-two-sorted-lists）

* 难度：简单
* 涉及知识：链表
* 题目地址：https://leetcode-cn.com/problems/merge-two-sorted-lists/
* 题目内容：

```
将两个有序链表合并为一个新的有序链表并返回。

新链表是通过拼接给定的两个链表的所有节点组成的。 

示例：
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

## 解法 - 链表

```js
// l1 = { val: 1, next: { val: 2, next: { val: 4, next: null } } }
// l2 = { val: 1, next: { val: 3, next: { val: 5, next: null } } }
var mergeTwoLists = function (l1, l2) {
  var mergedHead = { val: -1, next: null },
    crt = mergedHead;
  while (l1 && l2) {
    if (l1.val > l2.val) {
      crt.next = l2;
      l2 = l2.next;
    } else {
      crt.next = l1;
      l1 = l1.next;
    }
    // 跳转下一个节点
    crt = crt.next;
  }
  // 最后一个
  crt.next = l1 || l2;

  return mergedHead.next;
};
```

# 026 - 删除排序数组中的重复项（remove-duplicates-from-sorted-array）

* 难度：简单
* 涉及知识：数组、双指针
* 题目地址：https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/
* 题目内容：

```
给定一个排序数组，你需要在原地删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。

示例 1:

给定数组 nums = [1,1,2], 
函数应该返回新的长度 2, 并且原数组 nums 的前两个元素被修改为 1, 2。 
你不需要考虑数组中超出新长度后面的元素。

示例 2:

给定 nums = [0,0,1,1,1,2,2,3,3,4],
函数应该返回新的长度 5, 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4。
你不需要考虑数组中超出新长度后面的元素。

说明:

为什么返回数值是整数，但输出的答案是数组呢?
请注意，输入数组是以“引用”方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。

你可以想象内部操作如下:

// nums 是以“引用”方式传递的。也就是说，不对实参做任何拷贝
int len = removeDuplicates(nums);

// 在函数里修改输入数组对于调用者是可见的。
// 根据你的函数返回的长度, 它会打印出数组中该长度范围内的所有元素。
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```

## 3.1 解法 - 双指针

```js
var removeDuplicates = function(nums) {
  for (let i = 0; i < nums.length; i++) {
    if (nums[i] === nums[i + 1]) {
      nums.splice(i, 1);
      i--;
    }
  }
};
```

## 3.2 解法 - 违规操作

```js
var removeDuplicates = function(nums) {
  var a = [...new Set(nums)];
  for (var i = 0;i < a.length;i++) nums[i] = a[i];
  return a.length;
};
```