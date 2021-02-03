# 1.二维数组查找

## 题目

在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

## 基本思路

二维数组是有序的，比如下面的数据：

```
1 2 3
4 5 6
7 8 9
```

可以直接利用左下角数字开始查找：

- 大于：比较上移
- 小于：比较右移

## 代码思路

将二维数组看作平面坐标系

从左下角（0,arr.length-1）开始比较：

目标值大于坐标值---x 坐标+1

目标值小于坐标值---y 坐标-1

注意：

二维数组 arr[i][j]中

j 代表 x 坐标

i 代表 y 坐标

## 代码

```js
function Find(target, array) {
  let i = array.length - 1; // y坐标
  let j = 0; // x坐标
  return compare(target, array, i, j);
}

function compare(target, array, i, j) {
  if (array[i] === undefined || array[i][j] === undefined) {
    return false;
  }
  const temp = array[i][j];
  if (target === temp) {
    return true;
  } else if (target > temp) {
    return compare(target, array, i, j + 1);
  } else if (target < temp) {
    return compare(target, array, i - 1, j);
  }
}
```

## 拓展：二分查找

二分查找的条件是必须有序。

和线性表的中点值进行比较，如果小就继续在小的序列中查找，如此递归直到找到相同的值。

```js
function binarySearch(data, arr, start, end) {
  if (start > end) {
    return -1;
  }
  var mid = Math.floor((end + start) / 2);
  if (data == arr[mid]) {
    return mid;
  } else if (data < arr[mid]) {
    return binarySearch(data, arr, start, mid - 1);
  } else {
    return binarySearch(data, arr, mid + 1, end);
  }
}
```

## 考察点

- 查找
- 数组

# 5.替换空格

## 题目

请实现一个函数，将一个字符串中的每个空格替换成`“%20”`。例如，当字符串为`We Are Happy`。则经过替换之后的字符串为`We%20Are%20Happy`。

## 代码

1.直接用空格将字符串切割成数组，再用`20%`进行连接。

```js
function replaceSpace(str) {
  return str.split(' ').join('%20');
}
```

2.用正则表达式找到所有空格依次替换

```js
function replaceSpace(str) {
  return str.replace(/\s/g, '%20');
}
```

## 拓展

允许出现多个空格，多个空格用一个`20%`替换：

用正则表达式找到连续空格进行替换

```js
function replaceSpace(str) {
  return str.replace(/\s+/g, '%20');
}
```

## 考察点

- 字符串
- 正则

# 6.从尾到头打印链表

## 题目

输入一个链表，按链表值从尾到头的顺序返回一个`ArrayList`。

## 分析

要了解链表的数据结构：

`val`属性存储当前的值，`next`属性存储下一个节点的引用。

要遍历链表就是不断找到当前节点的`next`节点，当`next`节点是`null`时，说明是最后一个节点，停止遍历。

因为是从尾到头的顺序，使用一个队列来存储打印结果，每次从队列头部插入。

## 代码

```js
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/
function printListFromTailToHead(head) {
  const array = [];
  while (head) {
    array.unshift(head.val);
    head = head.next;
  }
  return array;
}
```

## 考察点

- 链表

# 7.重建二叉树

## 题目 1-二叉树重建

输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

例如输入前序遍历序列`{1,2,4,7,3,5,6,8}`和中序遍历序列`{4,7,2,1,5,3,8,6}`，则重建二叉树并返回。

## 思路

- 前序遍历：根节点 + 左子树前序遍历 + 右子树前序遍历
- 中序遍历：左子树中序遍历 + 根节点 + 右字数中序遍历
- 后序遍历：左子树后序遍历 + 右子树后序遍历 + 根节点

根据上面的规律：

- 前序遍历找到根结点`root`
- 找到`root`在中序遍历的位置 -> 左子树的长度和右子树的长度
- 截取左子树的中序遍历、右子树的中序遍历
- 截取左子树的前序遍历、右子树的前序遍历
- 递归重建二叉树

![](../dist/img/重建二叉树.png)

## 代码

```js
function reConstructBinaryTree(pre, vin) {
  if (pre.length === 0) {
    return null;
  }
  if (pre.length === 1) {
    return new TreeNode(pre[0]);
  }
  const value = pre[0];
  const index = vin.indexOf(value);
  const vinLeft = vin.slice(0, index);
  const vinRight = vin.slice(index + 1);
  const preLeft = pre.slice(1, index + 1);
  const preRight = pre.slice(index + 1);
  const node = new TreeNode(value);
  node.left = reConstructBinaryTree(preLeft, vinLeft);
  node.right = reConstructBinaryTree(preRight, vinRight);
  return node;
}
```

## 题目 2-求二叉树的遍历

给定一棵二叉树的前序遍历和中序遍历，求其后序遍历

输入描述:

两个字符串，其长度 n 均小于等于 26。
第一行为前序遍历，第二行为中序遍历。
二叉树中的结点名称以大写字母表示：A，B，C....最多 26 个结点。

输出描述:

输入样例可能有多组，对于每组测试样例，
输出一行，为后序遍历的字符串。

样例：

```
输入
ABC
BAC
FDXEAG
XDEFAG

输出
BCA
XEDGAF
```

## 思路

和上面题目的思路基本相同

- 前序遍历找到根结点`root`
- 找到`root`在中序遍历的位置 -> 左子树的长度和右子树的长度
- 截取左子树的中序遍历、右子树的中序遍历
- 截取左子树的前序遍历、右子树的前序遍历
- 递归拼接二叉树的后序遍历

## 代码

```js
let pre;
let vin;

while ((pre = readline()) != null) {
  vin = readline();
  print(getHRD(pre, vin));
}

function getHRD(pre, vin) {
  if (!pre) {
    return '';
  }
  if (pre.length === 1) {
    return pre;
  }
  const head = pre[0];
  const splitIndex = vin.indexOf(head);
  const vinLeft = vin.substring(0, splitIndex);
  const vinRight = vin.substring(splitIndex + 1);
  const preLeft = pre.substring(1, splitIndex + 1);
  const preRight = pre.substring(splitIndex + 1);
  return getHRD(preLeft, vinLeft) + getHRD(preRight, vinRight) + head;
}
```

## 考察点

- 二叉树
- 复杂问题拆解
