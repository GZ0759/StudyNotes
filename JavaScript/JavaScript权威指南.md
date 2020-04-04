> JavaScript权威指南第6版  
> David Flanagan 著  
> 淘宝前端团队 译  
> 2012 年 4 月第 1 版  
> [试读章节](https://book.2cto.com/201210/7006.html)  
> [博客园](https://www.cnblogs.com/ahthw/category/652668.html)

- [前言](#%e5%89%8d%e8%a8%80)
- [第1章 JavaScript概述](#%e7%ac%ac1%e7%ab%a0-javascript%e6%a6%82%e8%bf%b0)
  - [1.1 JavaScript语言核心](#11-javascript%e8%af%ad%e8%a8%80%e6%a0%b8%e5%bf%83)
  - [1.2 客户端JavaScript](#12-%e5%ae%a2%e6%88%b7%e7%ab%afjavascript)
  - [示例：一个 JavaScript 贷款计算器](#%e7%a4%ba%e4%be%8b%e4%b8%80%e4%b8%aa-javascript-%e8%b4%b7%e6%ac%be%e8%ae%a1%e7%ae%97%e5%99%a8)
- [第一部分 JavaScript语言核心](#%e7%ac%ac%e4%b8%80%e9%83%a8%e5%88%86-javascript%e8%af%ad%e8%a8%80%e6%a0%b8%e5%bf%83)
- [第2章 词法结构](#%e7%ac%ac2%e7%ab%a0-%e8%af%8d%e6%b3%95%e7%bb%93%e6%9e%84)
  - [2.1 字符集](#21-%e5%ad%97%e7%ac%a6%e9%9b%86)
    - [2.1.1 区别大小写](#211-%e5%8c%ba%e5%88%ab%e5%a4%a7%e5%b0%8f%e5%86%99)
    - [2.1.2 空格、换行符和格式控制符](#212-%e7%a9%ba%e6%a0%bc%e6%8d%a2%e8%a1%8c%e7%ac%a6%e5%92%8c%e6%a0%bc%e5%bc%8f%e6%8e%a7%e5%88%b6%e7%ac%a6)
    - [2.1.3 Unicode转义序列](#213-unicode%e8%bd%ac%e4%b9%89%e5%ba%8f%e5%88%97)
    - [2.1.4 标准化](#214-%e6%a0%87%e5%87%86%e5%8c%96)
  - [2.2 注释](#22-%e6%b3%a8%e9%87%8a)
  - [2.3 直接量](#23-%e7%9b%b4%e6%8e%a5%e9%87%8f)
  - [2.4 标识符和保留字](#24-%e6%a0%87%e8%af%86%e7%ac%a6%e5%92%8c%e4%bf%9d%e7%95%99%e5%ad%97)
  - [2.5 可选的分号](#25-%e5%8f%af%e9%80%89%e7%9a%84%e5%88%86%e5%8f%b7)
- [第3章 类型、值和变量](#%e7%ac%ac3%e7%ab%a0-%e7%b1%bb%e5%9e%8b%e5%80%bc%e5%92%8c%e5%8f%98%e9%87%8f)
  - [3.1 数字](#31-%e6%95%b0%e5%ad%97)
    - [3.1.1 整数型直接量](#311-%e6%95%b4%e6%95%b0%e5%9e%8b%e7%9b%b4%e6%8e%a5%e9%87%8f)
    - [3.1.2 浮点型直接量](#312-%e6%b5%ae%e7%82%b9%e5%9e%8b%e7%9b%b4%e6%8e%a5%e9%87%8f)
    - [3.1.3 JavaScript中的算术运算符](#313-javascript%e4%b8%ad%e7%9a%84%e7%ae%97%e6%9c%af%e8%bf%90%e7%ae%97%e7%ac%a6)
    - [3.1.4 二进制浮点数和四舍五入错误](#314-%e4%ba%8c%e8%bf%9b%e5%88%b6%e6%b5%ae%e7%82%b9%e6%95%b0%e5%92%8c%e5%9b%9b%e8%88%8d%e4%ba%94%e5%85%a5%e9%94%99%e8%af%af)
    - [3.1.5 日期和时间](#315-%e6%97%a5%e6%9c%9f%e5%92%8c%e6%97%b6%e9%97%b4)
  - [3.2 文本](#32-%e6%96%87%e6%9c%ac)
    - [3.2.1 字符串直接量](#321-%e5%ad%97%e7%ac%a6%e4%b8%b2%e7%9b%b4%e6%8e%a5%e9%87%8f)
    - [3.2.2 转义字符](#322-%e8%bd%ac%e4%b9%89%e5%ad%97%e7%ac%a6)
    - [3.2.3 字符串的使用](#323-%e5%ad%97%e7%ac%a6%e4%b8%b2%e7%9a%84%e4%bd%bf%e7%94%a8)
    - [3.2.4 模式匹配](#324-%e6%a8%a1%e5%bc%8f%e5%8c%b9%e9%85%8d)
  - [3.3 布尔值](#33-%e5%b8%83%e5%b0%94%e5%80%bc)
  - [3.4 null和undefined](#34-null%e5%92%8cundefined)
  - [3.5 全局对象](#35-%e5%85%a8%e5%b1%80%e5%af%b9%e8%b1%a1)
  - [3.6 包装对象](#36-%e5%8c%85%e8%a3%85%e5%af%b9%e8%b1%a1)
  - [3.7 不可变的原始值和可变的对象引用](#37-%e4%b8%8d%e5%8f%af%e5%8f%98%e7%9a%84%e5%8e%9f%e5%a7%8b%e5%80%bc%e5%92%8c%e5%8f%af%e5%8f%98%e7%9a%84%e5%af%b9%e8%b1%a1%e5%bc%95%e7%94%a8)
  - [3.8 类型转换](#38-%e7%b1%bb%e5%9e%8b%e8%bd%ac%e6%8d%a2)
    - [3.8.1.转换和相等性](#381%e8%bd%ac%e6%8d%a2%e5%92%8c%e7%9b%b8%e7%ad%89%e6%80%a7)
    - [3.8.2.显式类型转换](#382%e6%98%be%e5%bc%8f%e7%b1%bb%e5%9e%8b%e8%bd%ac%e6%8d%a2)
    - [3.8.3.对象转换为原始值](#383%e5%af%b9%e8%b1%a1%e8%bd%ac%e6%8d%a2%e4%b8%ba%e5%8e%9f%e5%a7%8b%e5%80%bc)
  - [3.9 变量声明](#39-%e5%8f%98%e9%87%8f%e5%a3%b0%e6%98%8e)
  - [3.10 变量作用域](#310-%e5%8f%98%e9%87%8f%e4%bd%9c%e7%94%a8%e5%9f%9f)
    - [3.10.1 函数作用域和声明提前](#3101-%e5%87%bd%e6%95%b0%e4%bd%9c%e7%94%a8%e5%9f%9f%e5%92%8c%e5%a3%b0%e6%98%8e%e6%8f%90%e5%89%8d)
    - [3.10.2 作为属性的变量](#3102-%e4%bd%9c%e4%b8%ba%e5%b1%9e%e6%80%a7%e7%9a%84%e5%8f%98%e9%87%8f)
    - [3.10.3 作用域链](#3103-%e4%bd%9c%e7%94%a8%e5%9f%9f%e9%93%be)
- [第4章 表达式和运算符](#%e7%ac%ac4%e7%ab%a0-%e8%a1%a8%e8%be%be%e5%bc%8f%e5%92%8c%e8%bf%90%e7%ae%97%e7%ac%a6)
  - [4.1 原始表达式](#41-%e5%8e%9f%e5%a7%8b%e8%a1%a8%e8%be%be%e5%bc%8f)
  - [4.2 对象和数组的初始化表达式](#42-%e5%af%b9%e8%b1%a1%e5%92%8c%e6%95%b0%e7%bb%84%e7%9a%84%e5%88%9d%e5%a7%8b%e5%8c%96%e8%a1%a8%e8%be%be%e5%bc%8f)
  - [4.3 函数定义表达式](#43-%e5%87%bd%e6%95%b0%e5%ae%9a%e4%b9%89%e8%a1%a8%e8%be%be%e5%bc%8f)
  - [4.4 属性访问表达式](#44-%e5%b1%9e%e6%80%a7%e8%ae%bf%e9%97%ae%e8%a1%a8%e8%be%be%e5%bc%8f)
  - [4.5 调用表达式](#45-%e8%b0%83%e7%94%a8%e8%a1%a8%e8%be%be%e5%bc%8f)
  - [4.6 对象创建表达式](#46-%e5%af%b9%e8%b1%a1%e5%88%9b%e5%bb%ba%e8%a1%a8%e8%be%be%e5%bc%8f)
  - [4.7 运算符概述](#47-%e8%bf%90%e7%ae%97%e7%ac%a6%e6%a6%82%e8%bf%b0)
    - [4.7.1 操作数的个数](#471-%e6%93%8d%e4%bd%9c%e6%95%b0%e7%9a%84%e4%b8%aa%e6%95%b0)
    - [4.7.2 操作数类型和结果类型](#472-%e6%93%8d%e4%bd%9c%e6%95%b0%e7%b1%bb%e5%9e%8b%e5%92%8c%e7%bb%93%e6%9e%9c%e7%b1%bb%e5%9e%8b)
    - [4.7.3 左值](#473-%e5%b7%a6%e5%80%bc)
    - [4.7.4 运算符的副作用](#474-%e8%bf%90%e7%ae%97%e7%ac%a6%e7%9a%84%e5%89%af%e4%bd%9c%e7%94%a8)
    - [4.7.5 运算符优先级](#475-%e8%bf%90%e7%ae%97%e7%ac%a6%e4%bc%98%e5%85%88%e7%ba%a7)
    - [4.7.6 运算符的结合性](#476-%e8%bf%90%e7%ae%97%e7%ac%a6%e7%9a%84%e7%bb%93%e5%90%88%e6%80%a7)
    - [4.7.7 运算顺序](#477-%e8%bf%90%e7%ae%97%e9%a1%ba%e5%ba%8f)
  - [4.8 算术表达式](#48-%e7%ae%97%e6%9c%af%e8%a1%a8%e8%be%be%e5%bc%8f)
    - [4.8.1 “+”运算符](#481-%e8%bf%90%e7%ae%97%e7%ac%a6)
    - [4.8.2 一元算术运算符](#482-%e4%b8%80%e5%85%83%e7%ae%97%e6%9c%af%e8%bf%90%e7%ae%97%e7%ac%a6)
    - [4.8.3 位运算符](#483-%e4%bd%8d%e8%bf%90%e7%ae%97%e7%ac%a6)
  - [4.9 关系表达式](#49-%e5%85%b3%e7%b3%bb%e8%a1%a8%e8%be%be%e5%bc%8f)
    - [4.9.1 相等和不等运算符](#491-%e7%9b%b8%e7%ad%89%e5%92%8c%e4%b8%8d%e7%ad%89%e8%bf%90%e7%ae%97%e7%ac%a6)
    - [4.9.2 比较运算符](#492-%e6%af%94%e8%be%83%e8%bf%90%e7%ae%97%e7%ac%a6)
    - [4.9.3 in运算符](#493-in%e8%bf%90%e7%ae%97%e7%ac%a6)
    - [4.9.4 instanceof运算符](#494-instanceof%e8%bf%90%e7%ae%97%e7%ac%a6)
  - [4.10 逻辑表达式](#410-%e9%80%bb%e8%be%91%e8%a1%a8%e8%be%be%e5%bc%8f)
    - [4.10.1 逻辑与`&&`](#4101-%e9%80%bb%e8%be%91%e4%b8%8e)
    - [4.10.2 逻辑或`||`](#4102-%e9%80%bb%e8%be%91%e6%88%96)
    - [4.10.3 逻辑非`!`](#4103-%e9%80%bb%e8%be%91%e9%9d%9e)
  - [4.11 赋值表达式](#411-%e8%b5%8b%e5%80%bc%e8%a1%a8%e8%be%be%e5%bc%8f)
  - [4.12 表达式计算](#412-%e8%a1%a8%e8%be%be%e5%bc%8f%e8%ae%a1%e7%ae%97)
    - [4.12.1 eval()](#4121-eval)
    - [4.12.2 全局eval()](#4122-%e5%85%a8%e5%b1%80eval)
    - [4.12.3 严格eval()](#4123-%e4%b8%a5%e6%a0%bceval)
  - [4.13 其他运算符](#413-%e5%85%b6%e4%bb%96%e8%bf%90%e7%ae%97%e7%ac%a6)
    - [4.13.1 条件运算符（?:）](#4131-%e6%9d%a1%e4%bb%b6%e8%bf%90%e7%ae%97%e7%ac%a6)
    - [4.13.2 typeof运算符](#4132-typeof%e8%bf%90%e7%ae%97%e7%ac%a6)
    - [4.13.3 delete运算符](#4133-delete%e8%bf%90%e7%ae%97%e7%ac%a6)
    - [4.13.4 void运算符](#4134-void%e8%bf%90%e7%ae%97%e7%ac%a6)
    - [4.13.5 逗号运算符(,)](#4135-%e9%80%97%e5%8f%b7%e8%bf%90%e7%ae%97%e7%ac%a6)
- [第5章 语句](#%e7%ac%ac5%e7%ab%a0-%e8%af%ad%e5%8f%a5)
  - [5.1 表达式语句](#51-%e8%a1%a8%e8%be%be%e5%bc%8f%e8%af%ad%e5%8f%a5)
  - [5.2 复合语句和空语句](#52-%e5%a4%8d%e5%90%88%e8%af%ad%e5%8f%a5%e5%92%8c%e7%a9%ba%e8%af%ad%e5%8f%a5)
  - [5.3 声明语句](#53-%e5%a3%b0%e6%98%8e%e8%af%ad%e5%8f%a5)
    - [5.3.1 var](#531-var)
    - [5.3.2 function](#532-function)
  - [5.4 条件语句](#54-%e6%9d%a1%e4%bb%b6%e8%af%ad%e5%8f%a5)
    - [5.4.1 if](#541-if)
    - [5.4.2 else if](#542-else-if)
    - [5.4.3 switch](#543-switch)
  - [5.5 循环](#55-%e5%be%aa%e7%8e%af)
    - [5.5.1 while](#551-while)
    - [5.5.2 do/while](#552-dowhile)
    - [5.5.3 for](#553-for)
    - [5.5.4 fon/in](#554-fonin)
  - [5.6 跳转](#56-%e8%b7%b3%e8%bd%ac)
    - [5.6.1 标签语句](#561-%e6%a0%87%e7%ad%be%e8%af%ad%e5%8f%a5)
    - [5.6.2 break语句](#562-break%e8%af%ad%e5%8f%a5)
    - [5.6.3 continue语句](#563-continue%e8%af%ad%e5%8f%a5)
    - [5.6.4 return语句](#564-return%e8%af%ad%e5%8f%a5)
    - [5.6.5 throw语句](#565-throw%e8%af%ad%e5%8f%a5)
    - [5.6.5 try/catch/finally语句](#565-trycatchfinally%e8%af%ad%e5%8f%a5)
  - [5.7 其他语句类型](#57-%e5%85%b6%e4%bb%96%e8%af%ad%e5%8f%a5%e7%b1%bb%e5%9e%8b)
    - [5.7.1 with语句](#571-with%e8%af%ad%e5%8f%a5)
    - [5.7.2 debugger语句](#572-debugger%e8%af%ad%e5%8f%a5)
    - [5.7.3 “use strict”](#573-use-strict)
  - [5.8 Javascript语句小结](#58-javascript%e8%af%ad%e5%8f%a5%e5%b0%8f%e7%bb%93)
- [第6章 对象](#%e7%ac%ac6%e7%ab%a0-%e5%af%b9%e8%b1%a1)
  - [6.1 创建对象](#61-%e5%88%9b%e5%bb%ba%e5%af%b9%e8%b1%a1)
    - [6.1.1 对象直接量](#611-%e5%af%b9%e8%b1%a1%e7%9b%b4%e6%8e%a5%e9%87%8f)
    - [6.1.2 通过new创建对象](#612-%e9%80%9a%e8%bf%87new%e5%88%9b%e5%bb%ba%e5%af%b9%e8%b1%a1)
    - [6.1.3 原型](#613-%e5%8e%9f%e5%9e%8b)
    - [6.1.4 Object.create()](#614-objectcreate)
  - [6.2 属性的查询和设置](#62-%e5%b1%9e%e6%80%a7%e7%9a%84%e6%9f%a5%e8%af%a2%e5%92%8c%e8%ae%be%e7%bd%ae)
    - [6.2.1 作为关联数组的对象](#621-%e4%bd%9c%e4%b8%ba%e5%85%b3%e8%81%94%e6%95%b0%e7%bb%84%e7%9a%84%e5%af%b9%e8%b1%a1)
    - [6.2.2 继承](#622-%e7%bb%a7%e6%89%bf)
    - [6.2.3 属性访问错误](#623-%e5%b1%9e%e6%80%a7%e8%ae%bf%e9%97%ae%e9%94%99%e8%af%af)
  - [6.3 删除属性](#63-%e5%88%a0%e9%99%a4%e5%b1%9e%e6%80%a7)
  - [6.4 检测属性](#64-%e6%a3%80%e6%b5%8b%e5%b1%9e%e6%80%a7)
  - [6.5 枚举属性](#65-%e6%9e%9a%e4%b8%be%e5%b1%9e%e6%80%a7)
  - [6.6 属性getter和setter](#66-%e5%b1%9e%e6%80%a7getter%e5%92%8csetter)
  - [6.7 属性的特性](#67-%e5%b1%9e%e6%80%a7%e7%9a%84%e7%89%b9%e6%80%a7)
  - [6.8 对象的三个属性](#68-%e5%af%b9%e8%b1%a1%e7%9a%84%e4%b8%89%e4%b8%aa%e5%b1%9e%e6%80%a7)
    - [6.8.1 原型属性](#681-%e5%8e%9f%e5%9e%8b%e5%b1%9e%e6%80%a7)
    - [6.8.2 类属性](#682-%e7%b1%bb%e5%b1%9e%e6%80%a7)
    - [6.8.3 可扩展性](#683-%e5%8f%af%e6%89%a9%e5%b1%95%e6%80%a7)
  - [6.9 序列化对象](#69-%e5%ba%8f%e5%88%97%e5%8c%96%e5%af%b9%e8%b1%a1)
  - [6.10 对象方法](#610-%e5%af%b9%e8%b1%a1%e6%96%b9%e6%b3%95)
    - [6.10.1 toString()方法](#6101-tostring%e6%96%b9%e6%b3%95)
    - [6.10.2 toLocaleString()方法](#6102-tolocalestring%e6%96%b9%e6%b3%95)
    - [6.10.3 toJSON()方法](#6103-tojson%e6%96%b9%e6%b3%95)
    - [6.10.4 valueOf()方法](#6104-valueof%e6%96%b9%e6%b3%95)
- [第7章 数组](#%e7%ac%ac7%e7%ab%a0-%e6%95%b0%e7%bb%84)
  - [7.1 创建数组](#71-%e5%88%9b%e5%bb%ba%e6%95%b0%e7%bb%84)
  - [7.2 数组元素的读和写](#72-%e6%95%b0%e7%bb%84%e5%85%83%e7%b4%a0%e7%9a%84%e8%af%bb%e5%92%8c%e5%86%99)
  - [7.3 稀疏数组](#73-%e7%a8%80%e7%96%8f%e6%95%b0%e7%bb%84)
  - [7.4 数组长度](#74-%e6%95%b0%e7%bb%84%e9%95%bf%e5%ba%a6)
  - [7.5 数组元素的添加和删除](#75-%e6%95%b0%e7%bb%84%e5%85%83%e7%b4%a0%e7%9a%84%e6%b7%bb%e5%8a%a0%e5%92%8c%e5%88%a0%e9%99%a4)
  - [7.6 数组遍历](#76-%e6%95%b0%e7%bb%84%e9%81%8d%e5%8e%86)
  - [7.7 多维数组](#77-%e5%a4%9a%e7%bb%b4%e6%95%b0%e7%bb%84)
  - [7.8 数组方法](#78-%e6%95%b0%e7%bb%84%e6%96%b9%e6%b3%95)
    - [7.8.1 join()](#781-join)
    - [7.8.2 reverse()](#782-reverse)
    - [7.8.3 sort()](#783-sort)
    - [7.8.4 concat()](#784-concat)
    - [7.8.5 slice()](#785-slice)
    - [7.8.6 splice()](#786-splice)
    - [7.8.7 push()和pop()](#787-push%e5%92%8cpop)
    - [7.8.8 unshift()和shift()](#788-unshift%e5%92%8cshift)
    - [7.8.9 toString()和toLocaleString()](#789-tostring%e5%92%8ctolocalestring)
  - [7.9 ES5中的数组方法](#79-es5%e4%b8%ad%e7%9a%84%e6%95%b0%e7%bb%84%e6%96%b9%e6%b3%95)
    - [7.9.1 forEach()](#791-foreach)
    - [7.9.2 map()](#792-map)
    - [7.9.3 filter()](#793-filter)
    - [7.9.4 every()和some()](#794-every%e5%92%8csome)
    - [7.9.5 reduce()和reduceRight()](#795-reduce%e5%92%8creduceright)
    - [7.9.6 indexOf()和lastIndexOf()](#796-indexof%e5%92%8clastindexof)
  - [7.10 数组类型](#710-%e6%95%b0%e7%bb%84%e7%b1%bb%e5%9e%8b)
  - [7.11 类数组对象](#711-%e7%b1%bb%e6%95%b0%e7%bb%84%e5%af%b9%e8%b1%a1)
  - [7.12 作为数组的字符串](#712-%e4%bd%9c%e4%b8%ba%e6%95%b0%e7%bb%84%e7%9a%84%e5%ad%97%e7%ac%a6%e4%b8%b2)
- [第8章 函数](#%e7%ac%ac8%e7%ab%a0-%e5%87%bd%e6%95%b0)
  - [8.1 函数定义](#81-%e5%87%bd%e6%95%b0%e5%ae%9a%e4%b9%89)
  - [8.2 函数调用](#82-%e5%87%bd%e6%95%b0%e8%b0%83%e7%94%a8)
    - [8.2.1 函数调用](#821-%e5%87%bd%e6%95%b0%e8%b0%83%e7%94%a8)
    - [8.2.2 方法调用](#822-%e6%96%b9%e6%b3%95%e8%b0%83%e7%94%a8)
    - [8.2.3 构造函数调用](#823-%e6%9e%84%e9%80%a0%e5%87%bd%e6%95%b0%e8%b0%83%e7%94%a8)
    - [8.2.4 间接调用](#824-%e9%97%b4%e6%8e%a5%e8%b0%83%e7%94%a8)
  - [8.3 函数的实参和形参](#83-%e5%87%bd%e6%95%b0%e7%9a%84%e5%ae%9e%e5%8f%82%e5%92%8c%e5%bd%a2%e5%8f%82)
    - [8.3.1 可选形参](#831-%e5%8f%af%e9%80%89%e5%bd%a2%e5%8f%82)
    - [8.3.2 可变长的实参列表：实参对象](#832-%e5%8f%af%e5%8f%98%e9%95%bf%e7%9a%84%e5%ae%9e%e5%8f%82%e5%88%97%e8%a1%a8%e5%ae%9e%e5%8f%82%e5%af%b9%e8%b1%a1)
    - [8.3.3 将对象属性用作实参](#833-%e5%b0%86%e5%af%b9%e8%b1%a1%e5%b1%9e%e6%80%a7%e7%94%a8%e4%bd%9c%e5%ae%9e%e5%8f%82)
    - [8.3.4 实参类型](#834-%e5%ae%9e%e5%8f%82%e7%b1%bb%e5%9e%8b)
  - [8.4 作为值的函数](#84-%e4%bd%9c%e4%b8%ba%e5%80%bc%e7%9a%84%e5%87%bd%e6%95%b0)
  - [8.5 作为命名空间的函数](#85-%e4%bd%9c%e4%b8%ba%e5%91%bd%e5%90%8d%e7%a9%ba%e9%97%b4%e7%9a%84%e5%87%bd%e6%95%b0)
  - [8.6 闭包](#86-%e9%97%ad%e5%8c%85)
  - [8.7 函数属性、方法和构造函数](#87-%e5%87%bd%e6%95%b0%e5%b1%9e%e6%80%a7%e6%96%b9%e6%b3%95%e5%92%8c%e6%9e%84%e9%80%a0%e5%87%bd%e6%95%b0)
    - [8.7.1 length属性](#871-length%e5%b1%9e%e6%80%a7)
    - [8.7.2 prototype属性](#872-prototype%e5%b1%9e%e6%80%a7)
    - [8.7.3 call()方法和apply()方法](#873-call%e6%96%b9%e6%b3%95%e5%92%8capply%e6%96%b9%e6%b3%95)
    - [8.7.4 bind()方法](#874-bind%e6%96%b9%e6%b3%95)
    - [8.7.5 toString()方法](#875-tostring%e6%96%b9%e6%b3%95)
    - [8.7.6 Function()构造函数](#876-function%e6%9e%84%e9%80%a0%e5%87%bd%e6%95%b0)
    - [8.7.7 可调用的对象](#877-%e5%8f%af%e8%b0%83%e7%94%a8%e7%9a%84%e5%af%b9%e8%b1%a1)
  - [8.8 函数式编程](#88-%e5%87%bd%e6%95%b0%e5%bc%8f%e7%bc%96%e7%a8%8b)
    - [8.8.1 使用函数处理数组](#881-%e4%bd%bf%e7%94%a8%e5%87%bd%e6%95%b0%e5%a4%84%e7%90%86%e6%95%b0%e7%bb%84)
    - [8.8.2 高阶函数](#882-%e9%ab%98%e9%98%b6%e5%87%bd%e6%95%b0)
    - [8.8.3 不完全函数](#883-%e4%b8%8d%e5%ae%8c%e5%85%a8%e5%87%bd%e6%95%b0)
    - [8.8.4 记忆](#884-%e8%ae%b0%e5%bf%86)
- [第9章 类和模块](#%e7%ac%ac9%e7%ab%a0-%e7%b1%bb%e5%92%8c%e6%a8%a1%e5%9d%97)
  - [9.1 类和对象](#91-%e7%b1%bb%e5%92%8c%e5%af%b9%e8%b1%a1)
  - [9.2 类和构造函数](#92-%e7%b1%bb%e5%92%8c%e6%9e%84%e9%80%a0%e5%87%bd%e6%95%b0)
    - [9.2.1 构造函数和类的标识：](#921-%e6%9e%84%e9%80%a0%e5%87%bd%e6%95%b0%e5%92%8c%e7%b1%bb%e7%9a%84%e6%a0%87%e8%af%86)
    - [9.2.2 constructor属性](#922-constructor%e5%b1%9e%e6%80%a7)
  - [9.3 JavaScript中Java式的类继承](#93-javascript%e4%b8%adjava%e5%bc%8f%e7%9a%84%e7%b1%bb%e7%bb%a7%e6%89%bf)
  - [9.4 类的扩充](#94-%e7%b1%bb%e7%9a%84%e6%89%a9%e5%85%85)
  - [9.5 类和类型](#95-%e7%b1%bb%e5%92%8c%e7%b1%bb%e5%9e%8b)
    - [9.5.1 instanceof运算符](#951-instanceof%e8%bf%90%e7%ae%97%e7%ac%a6)
    - [9.5.2 constructor属性](#952-constructor%e5%b1%9e%e6%80%a7)
    - [9.5.3 构造函数的名称](#953-%e6%9e%84%e9%80%a0%e5%87%bd%e6%95%b0%e7%9a%84%e5%90%8d%e7%a7%b0)
    - [9.5.3 鸭式辨型](#953-%e9%b8%ad%e5%bc%8f%e8%be%a8%e5%9e%8b)
  - [9.6 Javascript中的面向对象技术](#96-javascript%e4%b8%ad%e7%9a%84%e9%9d%a2%e5%90%91%e5%af%b9%e8%b1%a1%e6%8a%80%e6%9c%af)
    - [9.6.1 一个例子：结合类](#961-%e4%b8%80%e4%b8%aa%e4%be%8b%e5%ad%90%e7%bb%93%e5%90%88%e7%b1%bb)
    - [9.6.2 一个例子：枚举类型](#962-%e4%b8%80%e4%b8%aa%e4%be%8b%e5%ad%90%e6%9e%9a%e4%b8%be%e7%b1%bb%e5%9e%8b)
    - [9.6.3 标准转换方法](#963-%e6%a0%87%e5%87%86%e8%bd%ac%e6%8d%a2%e6%96%b9%e6%b3%95)
    - [9.6.4 比较方法](#964-%e6%af%94%e8%be%83%e6%96%b9%e6%b3%95)
    - [9.6.5 方法借用](#965-%e6%96%b9%e6%b3%95%e5%80%9f%e7%94%a8)
    - [9.6.6 私有状态](#966-%e7%a7%81%e6%9c%89%e7%8a%b6%e6%80%81)
    - [9.6.7 构造函数的重载和工厂方法](#967-%e6%9e%84%e9%80%a0%e5%87%bd%e6%95%b0%e7%9a%84%e9%87%8d%e8%bd%bd%e5%92%8c%e5%b7%a5%e5%8e%82%e6%96%b9%e6%b3%95)
  - [9.7 子类](#97-%e5%ad%90%e7%b1%bb)
    - [9.7.1 定义子类](#971-%e5%ae%9a%e4%b9%89%e5%ad%90%e7%b1%bb)
    - [9.7.2 构造函数和方法链](#972-%e6%9e%84%e9%80%a0%e5%87%bd%e6%95%b0%e5%92%8c%e6%96%b9%e6%b3%95%e9%93%be)
    - [9.7.3 组合vs子类](#973-%e7%bb%84%e5%90%88vs%e5%ad%90%e7%b1%bb)
    - [9.7.4 类的层次结构和抽象类](#974-%e7%b1%bb%e7%9a%84%e5%b1%82%e6%ac%a1%e7%bb%93%e6%9e%84%e5%92%8c%e6%8a%bd%e8%b1%a1%e7%b1%bb)
  - [9.8 ECMAScript5中的类](#98-ecmascript5%e4%b8%ad%e7%9a%84%e7%b1%bb)
    - [9.8.1 让属性不可枚举](#981-%e8%ae%a9%e5%b1%9e%e6%80%a7%e4%b8%8d%e5%8f%af%e6%9e%9a%e4%b8%be)
    - [9.8.2 定义不可变的类](#982-%e5%ae%9a%e4%b9%89%e4%b8%8d%e5%8f%af%e5%8f%98%e7%9a%84%e7%b1%bb)
    - [9.8.3 封装对象状态](#983-%e5%b0%81%e8%a3%85%e5%af%b9%e8%b1%a1%e7%8a%b6%e6%80%81)
    - [9.8.4 防止类的扩展](#984-%e9%98%b2%e6%ad%a2%e7%b1%bb%e7%9a%84%e6%89%a9%e5%b1%95)
    - [9.8.5 子类和ECMAScript5](#985-%e5%ad%90%e7%b1%bb%e5%92%8cecmascript5)
    - [9.8.6 属性描述符](#986-%e5%b1%9e%e6%80%a7%e6%8f%8f%e8%bf%b0%e7%ac%a6)
  - [9.9 模块](#99-%e6%a8%a1%e5%9d%97)
    - [9.9.1 用作命名空间的对象](#991-%e7%94%a8%e4%bd%9c%e5%91%bd%e5%90%8d%e7%a9%ba%e9%97%b4%e7%9a%84%e5%af%b9%e8%b1%a1)
    - [9.9.2 作为私有命名空间的函数](#992-%e4%bd%9c%e4%b8%ba%e7%a7%81%e6%9c%89%e5%91%bd%e5%90%8d%e7%a9%ba%e9%97%b4%e7%9a%84%e5%87%bd%e6%95%b0)
- [第10章 正则表达式的模式匹配](#%e7%ac%ac10%e7%ab%a0-%e6%ad%a3%e5%88%99%e8%a1%a8%e8%be%be%e5%bc%8f%e7%9a%84%e6%a8%a1%e5%bc%8f%e5%8c%b9%e9%85%8d)
- [第11章 JavaScript的子集和扩展](#%e7%ac%ac11%e7%ab%a0-javascript%e7%9a%84%e5%ad%90%e9%9b%86%e5%92%8c%e6%89%a9%e5%b1%95)
- [第12章 服务端JavaScript](#%e7%ac%ac12%e7%ab%a0-%e6%9c%8d%e5%8a%a1%e7%ab%afjavascript)
- [第二部分 客户端JavaScript](#%e7%ac%ac%e4%ba%8c%e9%83%a8%e5%88%86-%e5%ae%a2%e6%88%b7%e7%ab%afjavascript)
- [第13章 Web浏览器中的JavaScript](#%e7%ac%ac13%e7%ab%a0-web%e6%b5%8f%e8%a7%88%e5%99%a8%e4%b8%ad%e7%9a%84javascript)
- [第14章 Window对象](#%e7%ac%ac14%e7%ab%a0-window%e5%af%b9%e8%b1%a1)
- [第15章 脚本化文档](#%e7%ac%ac15%e7%ab%a0-%e8%84%9a%e6%9c%ac%e5%8c%96%e6%96%87%e6%a1%a3)
- [第16章 脚本化CSS](#%e7%ac%ac16%e7%ab%a0-%e8%84%9a%e6%9c%ac%e5%8c%96css)
- [第17章 事件处理](#%e7%ac%ac17%e7%ab%a0-%e4%ba%8b%e4%bb%b6%e5%a4%84%e7%90%86)
- [第18章 脚本化HTTP](#%e7%ac%ac18%e7%ab%a0-%e8%84%9a%e6%9c%ac%e5%8c%96http)
- [第19章 jQuery类库](#%e7%ac%ac19%e7%ab%a0-jquery%e7%b1%bb%e5%ba%93)
- [第20章 客户端存储](#%e7%ac%ac20%e7%ab%a0-%e5%ae%a2%e6%88%b7%e7%ab%af%e5%ad%98%e5%82%a8)
- [第21章 多媒体和图形编程](#%e7%ac%ac21%e7%ab%a0-%e5%a4%9a%e5%aa%92%e4%bd%93%e5%92%8c%e5%9b%be%e5%bd%a2%e7%bc%96%e7%a8%8b)
- [第22章 HTML5 API](#%e7%ac%ac22%e7%ab%a0-html5-api)
- [第三部分 JavaScript核心参考](#%e7%ac%ac%e4%b8%89%e9%83%a8%e5%88%86-javascript%e6%a0%b8%e5%bf%83%e5%8f%82%e8%80%83)
- [JavaScript核心参考](#javascript%e6%a0%b8%e5%bf%83%e5%8f%82%e8%80%83)
- [第四部分 客户端JavaScript参考](#%e7%ac%ac%e5%9b%9b%e9%83%a8%e5%88%86-%e5%ae%a2%e6%88%b7%e7%ab%afjavascript%e5%8f%82%e8%80%83)
- [客户端JavaScript参考](#%e5%ae%a2%e6%88%b7%e7%ab%afjavascript%e5%8f%82%e8%80%83)

# 前言
# 第1章 JavaScript概述

JavaScript 是面向 Web 的编程语言。绝大多数网站都适用了 JavaScript ，并且所有的现代 Web 浏览器——基于桌面系统、游戏机、平板电脑和智能手机的浏览器——均包含了 JavaScript 解释器。这使得 JavaScript 能够称得上史上使用最广泛的编程语言。JavaScript 也是前端开发工程师必须掌握的三种技能之一：描述网页内容的 HTML 、描述网页样式的 CSS 以及描述网页行为的 JavaScript 。

## 1.1 JavaScript语言核心

本节是 JavaScript 语言的一个快速概览，也是本书第一部分的快速概览。将关注 JavaScript 的基础知识，第二章讲解 JavaScript 注释、分号和 Unicode 字符集，第三章讲解 JavaScript 变量和赋值。

```js
// 变量是表示值的一个符号名字
// 变量是通过var关键字声明的
var x;    // 声明一个变量x

// 值可以通过等号赋值给变量
x = 0;    // 现在变量x的值为0
x     // => 0:通过变量获取其值

// JavaScript支持多种数据类型
x = 1;    // 数字
x = 0.01;   // 整数和实数共用一种数据类型
x = "hello world";  // 由双引号内的文本构成的字符串
x = 'JavaScript';  // 单引号内的文本同样构成字符串
x = true;   // 布尔值
x = false;   // 另一个布尔值
x = null;   // null是一个特殊的值，意思是"空"
x = undefined;  // undefined和null非常类似
```

JavaScript 中两个非常重要的数据类型是对象和数组。第六章介绍对象，第七章介绍数组，对象和数组在 JavaScript 中是很重要的。

```js
//JavaScript中的最重要的类型就是对象
//对象是名/值对的集合，或字符串到值映射的集合
var book = {    // 对象是由花括号括起来的
    topic: "JavaScript", // 属性"topic"的值是"JavaScript"
    fat: true   // 属性"fat"的值是true
};      // 右花括号标记了对象的结束

// 通过"."或" []"来访问对象属性
book.topic    // => "JavaScript"
book["fat"]    // => true:另外一种获取属性的方式
book.author = "Flanagan";  // 通过赋值创建一个新属性
book.contents = {};   // {} 是一个空对象，它没有属性

// JavaScript同样支持数组（以数字为索引的列表）
var primes = [2, 3, 5, 7];  // 拥有4个值的数组，由"["和"]"划定边界
primes[0]    // => 2: 数组中的第一个元素（索引为0）
primes.length   // => 4: 数组中的元素个数
primes[primes.length - 1]  // => 7:数组的最后一个元素
primes[4] = 9;   // 通过赋值来添加新元素
primes[4] = 11;   // 或通过赋值来改变已有的元素
var empty = [];   // [] 是空数组，它具有0个元素
empty.length    // => 0

// 数组和对象中都可以包含另一个数组或对象:
var points = [   // 具有两个元素的数组
 {x: 0, y: 0},  // 每个元素都是一个对象
 {x: 1, y: 1}
];
var data = {    // 一个包含两个属性的对象
    trial1: [[1, 2],[3, 4]], // 每一个属性都是数组
    trial2: [[2, 3],[4, 5]]  // 数组的元素也是数组
};
```

上段代码中通过方括号定义数组元素和通过花括号定义对象属性名和属性值之间的映射关系的语法称为初始化表达式（initalizer expression），第四章有专门的介绍。表达式是 JavaScript 中的一个短语，这个短语可以通过运算得出一个值。通过 “.” 和 “[]” 来引用对象属性或数组元素的值就构成一个表达式。

JavaScript 中最常见的表达式写法是想下面代码这样使用运算符（operator）。

```js
// 运算符作用于操作数，生成一个新的值
// 最常见的是算术运算符
3 + 2     // => 5: 加法
3 - 2     // => 1: 减法
3 * 2     // => 6: 乘法
3 / 2     // => 1.5: 除法
points[1].x - points[0].x  // => 1: 更复杂的操作数也能照常工作
"3" + "2"    // => "32": + 可以完成加法运算也可以作字符串连接

// JavaScript定义了一些算术运算符的简写形式
var count = 0;   // 定义一个变量
count++;    // 自增1
count--;    // 自减1
count += 2;    // 自增2：和"count = count + 2;"写法一样
count *= 3;    // 自乘3：和"count = count * 3;"写法一样
count     // => 6: 变量名本身也是一个表达式

// 相等关系运算符用来判断两值是否相等
// 不等、大于、小于运算符的运算结果是true或false
var x = 2, y = 3;   // 这里的 = 等号是赋值的意思，不是比较相等
x == y     // => false: 相等
x != y     // => true: 不等
x < y     // => true: 小于
x <= y     // => true: 小于等于
x > y     // => false: 大于等于
x >= y     // => false: 大于等于
"two" == "three"   // => false: 两个字符串不相等
"two" > "three"   // => true: "tw"在字母表中的索引大于"th"
false == (x > y)   // => true: false和false相等

// 逻辑运算符是对布尔值的合并或求反
(x == 2) && (y == 3)   // => true: 两个比较都是true，&&表示"与"
(x > 3) || (y < 3)   // => false: 两个比较不都是true，||表示"或"
!(x == y)    // => true: ! 求反
```

如果 JavaScript 中的“短语”是表达式的话，那么整个句子就称作语句（statement），第五章会详细讲解。在上述代码中，以分号结束的行均是一条语句（下面的代码中，会看到省略分号的多行语句）。实际上，语句和表达式之间有很多共同之处，粗略地将，表达式仅仅计算出一个值但并不作任何操作，它并不改变程序的运行状态。而语句并不包含一个值（或者说它包含的值我们并不关心），但它们改变程序的运算状态。在上文中已经见过变量声明语句和赋值语句。另一类是“控制结构”（control structure），比如条件判断和循环。

函数是带有名称（named）和参数的 JavaScript 代码段，可以一次定义多次调用。第八章会正式详细地讲解函数。

```js
// 函数是一段带有参数的JavaScript代码端，可以多次调用
function plus1(x) {   // 定义了名为plus1的一个函数，带有参数x
    return x+1;   // 返回一个比传入的参数大的值
}      // 函数的代码块是由花括号包裹起来的部分
plus1(y)      // => 4: y为3，调用函数的结果为 3+1

var square = function(x) {    // 函数是一种值，可以赋值给变量
    return x*x;     // 计算函数的值
};        // 分号标识了赋值语句的结束

square(plus1(y))     // => 16: 在一个表达式中调用两个函数
```

当将函数和对象合写在一起时，函数就变成了“方法”（method）：

```js
// 当函数赋值给对象的属性，我们称为
//  "方法"，所有的JavaScript对象都含有方法
var a = [];     // 创建一个空数组
a.push(1, 2, 3);    // push()方法向数组中添加元素
a.reverse();     // 另一个方法：将数组元素的次序反转

// 我们也可以定义自己的方法，"this"关键字是对定义方法
// 的对象的引用：这里的例子是上文中提到的包含两个点位置信息的数组
points.dist = function() {   // 定义一个方法用来计算两点之间的距离
    var p1 = this[0];   // 通过this获得对当前数组的引用
    var p2 = this[1];   // 并取得调用的数组前两个元素
    var a = p2.x - p1.x;   // X坐标轴上的距离
    var b = p2.y - p1.y;   // Y坐标轴上的距离
    return Math.sqrt(a * a +   // 勾股定理
    b * b);    // 用Math.sqrt()来计算平方根
};
points.dist()    // => 1.414: 求得两个点之间的距离
```

现在，给出一些控制语句的例子。

```js
// 这些JavaScript语句使用该语法包含条件判断和循环
// 使用了类似C、C++、Java和其他语言的语法
function abs(x) {    // 求绝对值的函数
    if (x >= 0) {    // if语句...
        return x;    // 如果比较结果为true则执行这里的代码.
    }      // 子句的结束.
    else {     // 当if条件不满足时执行else子句
        return - x;
    }      // 如果分支中只有一条语句，花括号是可以省略的
}       // 注意if/else中嵌套的return语句
function factorial(n) {   // 计算阶乘的函数
    var product = 1;    // 给product赋值为1
    while (n > 1) {    // 当()内的表达式为true时循环执行{}内的代码
        product *= n;   // "product = product * n; "的简写形式
        n--;     //  "n = n - 1; "的简写形式
    }      // 循环结束
    return product;    // 返回product
}
factorial(4)     // => 24: 1*4*3*2
function factorial2(n) {   // 实现循环的另一种写法
    var i, product = 1;   // 给product赋值为1
    for (i = 2; i <= n; i++)   // 将i从2自增至n
      product *= i;   // 循环体，当循环体中只有一句代码，可以省略{}
    return product;    // 返回计算好的阶乘
}
factorial2(5)    // => 120: 1*2*3*4*5
```

JavaScript 是一种面向对象的编程语言，但和传统的面向对象又有很大区别。第九章将详细讲解 JavaScript 中的面向对象编程。下面的代码展示了如何在 JavaScript 中定义一个类来表示 2D 平面几何中的点。这个类实例化的对象拥有一个名为 `r()` 的方法，用来计算点到原点的距离。

```js
// 定义一个构造函数以初始化一个新的Point对象
function Point(x, y) {   // 按照惯例，构造函数均以大写字母开始
    this.x = x;    // 关键字this指代初始化的实例
    this.y = y;    // 将函数参数存储为对象的属性
}       // 不需要return

// 使用new关键字和构造函数来创建一个实例
var p = new Point(1, 1); // 平面几何中的点 (1,1)

// 通过给构造函数的prototye对象赋值
// 来给Point对象定义方法
Point.prototype.r = function() {
    return Math.sqrt(   // 返回 x2 + y2 的平方根
    this.x * this.x +   // this指代调用这个方法的对象
    this.y * this.y);
};

// Point的实例对象p（以及所有的Point实例对象）继承了方法 r()
p.r()      // => 1.414...
```

第九章是第一部分的精华所在，后续的各章做了一些零星的延伸，将我们对 JavaScript 语言核心的探索带向尾声。第十章主要讲解了正则表达式的语法，并演示了如何使用这些“正则表达式”进行文本的模式匹配。第十一章介绍 JavaScript 语言核心的子集和超集。最后，在进入客户端 JavaScript 的内容之前，第十二章介绍两种在 Web 浏览器之外的两种 JavaScript 运行环境。

## 1.2 客户端JavaScript

第十三章是第二部分的第一章，该章介绍如何让 JavaScript 在 Web 浏览器中运行起来。从该章学到的最重要的内容是， JavaScript 代码可以通过`<script>`标签来嵌入到 HTML 文件中。

```html
<html>
<head>
<script src="library.js"></script> <!-- 引入一个JavaScript库-->
</head>
<body>
<p>This is a paragraph of HTML</p>
<script>
// 在这里编写嵌入到HTML文件中的JavaScript代码
</script>
<p>Here is more HTML.</P>
</body>
</html>
```

第十四章讲解 Web 浏览器脚本技术，并涵盖客户端 JavaScript 中的一些重要全局函数。

```html
<script>
function moveon() {
    // 通过弹出一个对话框来询问用户一个问题
    var answer = confirm("准备好了吗?");
    // 单击"确定"按钮，浏览器会加载一个新页面
    if (answer) window.location = "http://taobao.com";
}
// 在1分钟（6万毫秒）后执行定义的这个函数
setTimeout(moveon, 60000);
</script>
```

第十五章的内容更加务实——通过脚本来操纵 HTML 文档内容。它将展示如何选取特定的 HTML 元素、如何给 HTML 元素设置属性、如何修改元素内容，以及如何给文档添加新节点。

```js
// 在document中的一个指定的区域输出调试消息
// 如果document不存在这样一个区域，则创建一个
function debug(msg) {
    // 通过查看HTML元素id属性来查找文档的调试部分
    var log = document.getElementById("debuglog");

    // 如果这个元素不存在，则创建一个
    if (!log) {
        log = document.createElement("div");  // 创建一个新的<div>元素
        log.id = "debuglog";    // 给这个元素的HTML id赋值
        log.innerHTML = "<h1>Debug Log</h1>";  // 定义初始内容
        document.body.appendChild(log);  // 将其添加到文档的末尾
    }

    // 将消息包装在<pre>中，并添加至log中
    var pre = document.createElement("pre");  // 创建<pre>标签
    var text = document.createTextNode(msg);  // 将msg包装在一个文本节点中
    pre.appendChild(text);    // 将文本添加至<pre>
    log.appendChild(pre);    // 将<pre>添加至log
}
```

第十五章讲述 JavaScript 如何操纵 HTML 中定义 Web 内容的元素。第十六章讲诉如何使用 JavaScript 来进行 CSS 样式操作， CSS 样式定义了内容的展示方式。这通常会使用到 HTML 元素的 style 和 class 属性。

```js
function hide(e, reflow) {   // 通过JavaScript操纵样式来隐藏元素e
    if (reflow) {    // 如果第二个参数是true
        e.style.display = "none"  // 隐藏这个元素，其所占的空间也随之消失
    }
    else {     // 否则
        e.style.visibility = "hidden"; // 将e隐藏，但是保留其所占的空间
    }
}
function highlight(e) {   // 通过设置CSS类来高亮显示e
    // 简单地定义或追加HTML类属性
    // 这里假设CSS样式表中已经有"hilite"类的定义
    if (!e.className) e.className = "hilite";
    else e.className += " hilite";
}
```

可以通过 JavaScript 来操控 Web 浏览器中的HTML内容和文档的CSS样式，同样，也可以通过事件处理程序（event handler）来定义文档的行为。事件处理程序是一个在浏览器中注册的 JavaScript 函数，当特定类型的事件发生时浏览器便调用这个函数。通常我们关心的事件类型是鼠标点击事件和键盘按键事件（在智能手机中则是各种触碰事件）。或者说，当浏览器完成了文档的加载，当用户改变窗口大小或当用户向 HTML表单元素中输入数据时便会触发一个事件。第17章详细描述如何定义、注册事件处理程序，以及在事件发生时浏览器是如何调用它们的。

定义事件处理程序最简单的方法是，给 HTML 的以“on”为前缀的属性绑定一个回调。当写一些简单的测试程序时，最实用的方法就是给“onclick”处理程序绑定回调。假定已经将上文中的`debug()`和`hide()`两个函数保存至名为debug.js和hide.js的文件中，那么就可以写一个简单的HTML测试文件，来给`<button>`元素的onclick属性指定一个事件处理程序：

```html
<script src="debug.js"></script>
<script src="hide.js"></script>
<button onclick="hide(this,true); debug('hide button 1');">Hide1</button>
<button onclick="hide(this); debug('hide button 2');">Hide2</button>
```

下面这些客户端 JavaScript 代码用到了事件，它给一个很重要的事件——“load”事件注册了一个事件处理程序。同时，也展示了注册“click”事件处理函数更高级的一种方法。

```js
// "load"事件只有在文档加载完成后才会触发
//通常需要等待load事件发生后才开始执行JavaScript代码
window.onload = function() { // 当文档加载完成时执行这里的代码
    // 找到文档中所有的`<img>`标签
    var images = document.getElementsByTagName("img");

    // 遍历 images，给每个节点的"click"事件添加事件处理程序
    // 在点击图片的时候将图片隐藏
    for(var i = 0; i < images.length; i++) {
        var image = images[i];
        if (image.addEventListener)  // 注册事件处理程序的另一种方法
            image.addEventListener("click", hide, false);
        else     // 兼容IE8及以前的版本
            image.attachEvent("onclick", hide);
    }

    // 这便是上面注册的事件处理函数
    function hide(event) { event.target.style.visibility = "hidden"; }
};
```

第十五章到十七章讲诉了如何使用 JavaScript 来操控网页的内容（HTML）、样式（CSS）以及行为（事件处理）。这些章所讨论得 API 多少有些复杂，且至今仍具有糟糕的浏览器兼容性。也正是由于这个原因，很多客户端 JavaScript 程序员选择使用“库”或“框架”来简化他们的编码工作。最流行的库非 jQuery 莫属。第19章将会详细介绍 jQuery 库。 jQuery 定义了一套灵巧易用的 API ，用来操控文档内容、样式和行为。 jQuery 经过了完整的测试，在所有现代主流浏览器，甚至在 IE6 这种早期浏览器中都可以照常运行。

jQuery代码非常易于识别，因为它充分利用了一个名为`$()`的函数。这里用 jQuery 重写了上文中提到的`debug()`函数：

```js
function debug(msg) {
    var log = $("#debuglog");   // 找到要显示msg的元素.
    if (log.length == 0) {   // 如果不存在则创建之
        log = $("<div id='debuglog'><h1>Debug Log</h1></div>");
        log.appendTo(document.body);  // 并将其追加到body里
    }
    log.append($("<pre/>").text(msg)); // 将msg包装在<pre>中，再追加到log里
}
```

目前我们所提到的第二部分的四章都是围绕网页展开讨论的。后续的四章将着眼点转向 Web 应用。这几章的内容并不是讨论如何通过编写操控内容、样式和行为的脚本使用 Web 浏览器来渲染文档；而是讲解如何将 Web 浏览器当做应用平台，并描述了用以支持更复杂精细的客户端 Web 应用的现代浏览器 API 。第十八掌章讲解如何使用 JavaScript 来发起 HTTP 请求。第二十章描述数据存储的机制以及客户端应用中的会话状态的保持。第二十一章涵盖基于 HTML 的`<canvas>`标签的客户端 API ，用来进行任意形状图形的绘制。

最后，第二十二章讲解 HTML5 所提供的新一代 Web 应用 API 。网络、存储、图形：这些都是 Web 浏览器提供的操作系统级的服务，它们定义了全新的跨平台的应用环境。如果你正在进行基于那些支持这些新 API 的浏览器的开发，这将是你作为客户端 JavaScript 程序员最激动人心的时刻。最后四章并没有太多示例代码，但下面的例子使用了这些新的API。

## 示例：一个 JavaScript 贷款计算器

这里的例子展示了诸多JavaScript语言核心特性，同样展示了重要的客户端JavaScript技术：

- 如何在文档中查找元素
- 如何通过表单 input 元素来获取用户的输入数据
- 如何通过文档元素来设置 HTML 内容
- 如何将数据存储在浏览器中
- 如何使用脚本发起HTTP请求
- 如何利用`<canvas>`元素绘图

# 第一部分 JavaScript语言核心

# 第2章 词法结构

编程语言的词法结构是一套基础性规则，用来描述如何使用这门语言来编写程序。作为语法的基础，它规定了诸如变量名是什么样的，怎么写注释，以及程序语句之间如何分割等规则。

## 2.1 字符集

JavaScript 程序是用 Unicode 字符集编写的。 Unicode 是 ASCALL 和 Latin-1 的超集，并支持地球上几乎所有在用的语言。

### 2.1.1 区别大小写

JavaScript 是区分大小写的语言。也就是说，关键字、变量、函数名和所有的标识符（identifier）都必须采用一致的大小写规则。

但需要注意的是， HTML 并不区分大小写（尽管 XHTML 区分大小写）。许多客户端 JavaScript 对象和属性与它们所表示的 HTML 标签和属性同名。在 HTML中，这些标签和属性名可以使用大写也可以是小写，而在 JavaScript 中则必须是小写。例如，在 HTML 中设置事件处理程序时， onclick 属性可以写成 onClick ，但在 JavaScript 代码（或者 XHTML 文档）中，必须使用小写的 onclick 。 

### 2.1.2 空格、换行符和格式控制符

JavaScript 会忽略程序中的标识（token）之间的空格，多数情况下， JavaScript 同样会忽略换行符。由于可以在代码中随意使用空格和换行符，一次可以采用整齐和一致的缩进来形成统一的编码风格，提高代码的可读性。

JavaScript 除了识别空格符(\u0020)。 JavaScript 还可以识别如下标示空格的字符：水平制表符（\u0009）、垂直制表符(\u000B)、换页符(\u000C)、不中断空白符(\u00A0)、字节序标记(\uFEFF)，以及在Unicode中所有Zs类别的字符。

JavaScript 将如下字符识别为结束符：换行符(\u000A)，回车符号(\u000D)，行分隔符(\u2028)，段分隔符号(\u2029)。回车符加换行符在一起呗解析为一个单行的结束符。

Unicode格式控制字符(Cf类)，比如“从右至左书写标记”(\u200F)和从“从左至右书写标记”(\u200E)，控制着文本的视觉显示。这对一些非英语文本的正确显示来说是至关重要的，这些字符可以在 JavaScript 的注释，字符串直接量和正则表达式直接量中，但不能用在标示符（比如，变量名）中，但有个例外零宽连接符(\u200D)和零宽非连接符(\uFEFF)是可以出现在标示符中，但不能作为标识符的手字符。上文也提到了，字节序标记格式控制符(\uFEFF)被当成了空格来对待。

### 2.1.3 Unicode转义序列

在有些计算机硬件和软件里，无法显示或输入 Unicode 字符全集。为了支持那些使用老旧技术的程序员， JavaScript 定义了一种特殊序列，使用六个 ASCLL 字符来代表任意 16 位 Unicode 内码。这些 Unicode 转义序列均以`\u`为前缀，其后跟随 4 个十六进制数（使用数字以及大写或小写的字符A-F表示）。这种 Unicode转义写法可以用在 JavaScript 字符串直接量、正则表达式直接量和标识符中（关键字除外）。例如，下面两个 JavaScript 字符串是完全一样的。

```js
"café" === "caf\u00e9" => true 
```

Unicode 转义写法也可以出现在注释中，但由于 JavaScript 会将注释忽略，它们只是被当成上下文中的 ASCLL 字符处理，而且不会被解析为其对应的 Unicode 字符。

### 2.1.4 标准化

Unicode 允许使用多种方法对同一个字符进行编码。比如字符é可以使用 Unicode 字符\u00E9,也可以使用普通的 ASCLL 字符e跟随一个语调符号\u0301 ,在文本编辑器中，这两个编码显示的结果是一摸一样的，但是它们的二进制编码表示是不一样的，在计算机里也不相等。 Unicode 标准为索引字符定义了一个首选的代码格式，并给出了一个标准化的处理方式将文本转化为一种适合比较的标准格式，不会再对其它表示、字符串或者正则表达式做标准化处理。

## 2.2 注释

JavaScript 支持两种格式的注释。在行尾`//`之后的文本都会被 JavaScript 当作注释忽略掉的。此外，`/*`和`*/`之间的文本也会当作注释，这种注释可以跨行书写，但不能有嵌套的注释。

```js
// 这里是单行注释
/* 这里是一段注释 */  // 这里是另一段注释
/*
* 这又是一段注释
* 这里的注释可以连续写多行
*/
```

## 2.3 直接量

所谓直接量（literal），就是程序中直接使用的数据值。

```js
12 //数字
1.2 //小数
"Hllo World" //字符串文本
'hi' //另一个字符串
true //布尔值
false //另一个布尔值
/javascript/gi //正则表达式直接量（用做模式匹配）
null //空
```

更多复杂的表达方式可以写成数组或对象直接量。

```js
{ x:1, y:2 } //对象
[ 1,2, 3,4,5 ] //数组
```

## 2.4 标识符和保留字

标识符就是一个名字。在 JavaScript 中，标识符用来对变量和函数进行命名，或者用作 JavaScript 代码中某些循环语句中的跳转位置的标记。 JavaScript 标识符必须以字符、下划线（_）或美元符（$）开始。后续的字符可以是字母、数字、下划线或美元符（数字是不允许作为首字符出现的，以便 JavaScript 可以轻易区分开标识符和数字）。下面是合法的标识符：

- my_variable_name
- b13
- _dummy
- $str

处于可移植性和易于书写的考虑，通常我们只使用 ASCII 字符和数字来书写标识符。然而需要注意的是， JavaScript 允许标识符中出现 Unicode 字符全集中的字母和数字。此外，程序员也可以使用非英语语言或数字符号来书写标识符。

```js
var sá = true;
var π = 3.14;
```

和其他任何编程语言一样，JavaScript 保留了一些标识符为自己所用。这些“保留字”不能用作普通的标识符。

**保留字**

JavaScript 把一些标识符拿出来用作自己的关键字。因此，就不能再在程序中把这些关键字用作标识符了：

- break
- case
- catch
- continue
- default
- delete
- do
- else
- finally
- for
- function
- if
- in
- instanceof
- new
- return
- switch
- this
- throw
- try
- typeof
- var
- void
- while
- with

javascript 同样保留了一些关键字，这些关键字在当前的语言版本并没有使用，但在未来版本中可能会用到。ECMAScript 5 保留了这些关键字。

class const enum export
export extends import super

## 2.5 可选的分号

和很多编程语言一样， JavaScript 使用分号`;`将语句分隔开。这对增强代码的可读性和整洁性是非常重要的。缺少分隔符，一条语句结束就成了下一条语句的开始，反之亦然。

在 JavaScript 中，各自语句独占一行，通常可以省略语句之间的分号（程序结尾处使用`}`花括弧之前的分号也可以省略）。

很多 JavaScript 程序员（包括本书的代码示例）都是使用分号来明确标记语句的结束，即使在并不完全需要分号的时候也是如此，另一种风格是在任何可以省略分号时都将其省略，只有在不得不使用的时候才使用分号，不管哪种编程风格，关于 JavaScript 有几个细节需要注意。

```js
// 如下代码,第一个分号是可以省略的
a=3;
b=4;

// 但如果按照如下格式书写，第一个分号则不能省略。
a=3;b=4;
```

需要注意的是， JavaScript 并不是在所有的换行处都填补分号：只有在缺少了分号就无法正常解析代码的时候， JavaScript 才会填补分号，换句话说（类似下面代码中的两处异常），如果当前的语句和随后的的非空格字符不能当成一个整体解析的话， JavaScript 就在当前语句的结束处来填补分号，看下如下代码

```js
var a
a
=
3
console.log(a)

// javascript将其解析为
var a;a=3;console.log(a); 
```

有些语句的分隔规则会导致一些想不到的情形，这段代码写成了两行，看起来是两条独立的语句。

```js
var y = x + f
(a+b).toString()

// 实际上
var y = x+f(a+b).toString();
```

通常来讲，如果一条语句以 `(`、`[`、`/` `+` 或 `-` 开始，那么它极有可能和前条语句组合在一起解析，以 `/`、`+` 和 `-` 开始的语句不很常见，但以 `(` 和 `[` 开始的语句则非常常见。至少在一些javascript编码符风格中是很常见的。有点程序员喜欢保守的在语句前边加上一个分号，这样，哪怕之前的语句被修稿了，分号被误删了，当前语句还是会正确的解析；

```js
// 这里省略了分号
var x = 0 
// 前面的分号保证了正确地语句解析
;[x, x+1, x+2].forEach(console.log)  
```

如果当前语句和下一行语句无法合并解析。javascript 则在第一行后填补分号，这是通用规则，但有两个例外。第一个例外是涉及到 `returnm`、`birak` 和 `continue` 语句，如果这三个关键字后紧跟着换行。javascript则会在换行处填补分号。例如

```js
return
true;

// 而 javascript解析成
return;ture;

// 而代码的本意是
return ture;
```
也就是说`return`、`break` 和 `contuine` 好的随后的表达式之间不能有换行，如果添加了换行，程序则在极有特殊情况才能报错。而且程序的调试很不方便。

第二个例子是涉及到 `++` 和 `--` 运算符时，这些表达式符号可以代表标识符表达式的前缀和后缀。如果将其又再后表达式，如果的将其用做后缀表达式。它和表达式应该看做一行。否则行尾将填补分号。

```js
x
++
yy

// 以上代码解析为
x;
++y
```

# 第3章 类型、值和变量

计算机程序的运行需要对值（value）进行操作。在编程语言中，能够表示并操作的值的类型称作数据类型（type），编程语言最基本的特性就是能够支持多种数据类型。当程序需要将值保存起来以备将来使用时，便将其复制给（将值“保存”到）一个变量（variable）。变量是一个值的符号名称，可以通过名称来获得对值的引用。变量的工作机制是变成语言的另一个基本特性。

JavaScript 的数据类型分为两类：原始类型(primitive type)和对象类型(object type)。 JavaScript 中的原始类包括数字、字符串和布尔值，

JavaScript 还有两个特殊的原始值，`null`(空)和`Undefined`(未定义)，他们不是数字、字符串、布尔值。它们分别代表了各自特殊类型的唯一成员。

javascript除了数字、字符串、布尔值、`null`、`undefined`之外就是对象了。对象 (object)是属性(property)的集合。每个属性都由"名/值对"(值可以是原始值，比如数字，字符串，也可以是对象)构成。其中一个比较特殊的对象(全局对象(global object)。

普通的 JavaScript 对象是“命名值”的无需集合。 JavaScript 同样定义了一种特殊对象——数组(array)，表示带编号的值的有序集合。 JavaScript 为数组定义了专用的语法。使数组拥有一些和普通对象不同的特有的行为属性。

JavaScript 还定义了一种特殊的对象——函数。函数是具有与它相关联的可执行代码的对象，通过调用函数来运行可执行代码，并返回运算结果。和数组一样，函数行为特征和其它对象都不一样。 JavaScript 为使用函数定义了专用语法。对 JavaScript 函数来讲。最重要的是，他们都是真值，并且 JavaScript 可以将他们当做普通对象来对待。

如果函数初始化（使用`new`运算符）一个新建对象，我们称之为构造函数(constructor)。每个构造函数定义了一类（class）对象——由构造函数初始化对象组成的集合。类可以看做对象类型的子类型。除了数组（Array）类和函数(Function)类之外，JavaScript 还定义了其它三种有用的类。日期（Date）类定义了代表日期的对象。正则（RegExp）类定义了正则表达式的对象。错误（error）类定义了那行表示JavaScript 程序中运行时错误和语法错误对象。可以通过定义自己的构造函数来定义需要的类。

JavaScript 解释器有自己的内存管理机制，可以自动对内存进行垃圾回收（garbage collection）。这意味着程序程序可以按需创建对象，程序员则不必担心这些对象的销毁和内存回收。当不再有任何引用指向一个对象，解释器就知道这个对象没有用了，然后会自动回收它所占用的内存资源。

JavaScript 是一种面向对象的语言。不严格的讲，这意味着我们不用全局的定义函数去操作不同类型的值，数据类型本身可以定义方法(method)来使用值。例如数组的方法可以使用`[].sort()`来排序。

从技术上来将，只有 JavaScript 对象才能拥有方法。然而，数字，字符串，布尔值也拥有自己的方法。在 JavaScript 中，只有`null`和`undefined`是无法拥有方法的值。

JavaScript 的类型可以分为原始类型和对象类型，也可分为可以拥有方法的类型和不能拥有方法的类型。同样可分为可变（mutable）乐行和不可变(immutable)类型。可变类型的值是可以修改的，对象和数组属于可变类型； JavaScript 程序可以改变对象的属性值和数组元素的值。数字、布尔值、`null`和`undefined`属于不可改变的类型。

比如，修改一个数组的内容本身就说不通。字符串可以看做是字符组成的数组，你可以认为它是可以变的。然而在 JavaScript 中，字符串是不可变的。可以访问字符串任意位置的文本，但 JavaScript 并未提供修改已知字符串文本内容的方法。

JavaScript 可以自由地进行数据类型转换。比如，如果在程序期望使用字符串的地方使用了数字，JavaScript 会自动将数字转换为字符串。如果期望在使用布尔值的地方使用了非布尔值，JavaScript 也会相应的转换。JavaScript 中对灵活的类型转换规则对“判断相等”（equality）的定义亦有影响。

JavaScript 的变量是无类型的（untyped），变量可以被赋予任何类型的值，同样一个变量也可以重新赋予不同类型的值。使用`var`关键字来声明（declare）变量。JavaScript 采用语法作用域。不在任何函数内声明的变量称为全局变量（global variable），它在 JavaScript 的程序中任何地方都是可见的。在函数内声明的变量具有函数作用域（function scope），并且只在函数内可见。

## 3.1 数字

和其它编程语言不同， JavaScript 不区分整数值和浮点数数值。 JavaScript 中的数值均用浮点数值来表示。

当一个数字直接出现在 JavaScript 程序中，我们称之为数字直接量（numeric literal）， JavaScript 支持多种格式的数字直接量。注意：在任何数字前直接添加负号（-）可以得到它们的负值。但负号是一元求反运算符，并不是数字直接量语法的组成部分。

### 3.1.1 整数型直接量

在 JavaScript 程序中，用一个数组序列表示一个十进制的整数：

- 0
- 3
- 10000000

除了十进制的整数直接量， JavaScript 同样识别十六进制(以 16 为基数)值。所谓十六进制的直接量是以“0x”或者"0X"为前缀，其后紧跟十六进制数串的直接量。十六进制数值是 0 ~ 9 的数字和 a(A) ~ f(F) 之间的字母构成。 a - f 的字母对应的表示数字 10 ~ 15 。下面是十六进制整型直接量的例子：

```js
0xff // 15*16+15=255(十进制)
0xCAFE911
```

尽管 ECMAScript 标准不支持八进制直接量，但 JavaScript 的某些实现可以允许采用八进制（基数为8）形式表示整数。八进制直接量以数字0开始，其后跟随着一个0-7之间数字组成的序列。

```js
0377 // 3*64 +7*8 +7 =255(十进制)
```

由于某些 JavaScript 的实现支持八进制的之间量，而有些不支持，因此最好不要使用以0为前缀的整数之间量，毕竟我们也无法得知当前 JavaScript 的实现是否支持八进制的解析。在 ECMAScript6 的严格模式下，八进制的直接量是明令禁止的。

### 3.1.2 浮点型直接量

浮点型直接量可以含有小数点，它们采用的是传统的实数写法。一个实数由整数部分，小数点和小数部分组成。

此外，还可以使用指数计数法表示浮点型直接量。即在实数后跟字母 e 或 E ，后面再跟正负号，其后再加一个整型的指数。这种计数方法表示的数值，是有前面的实数乘以10的指数幂。

可以使用更简洁的语法来表示:`[digits][.digits][(E|e)[(+|-)]digits]`

```js
3.14
2345.455
.33333333333333333
6.02e23 // 6.02*10的23次方
1.255454E-23 // 1.255454*10的负23次方
```

### 3.1.3 JavaScript中的算术运算符

JavaScript 程序是使用语言本身提供的算术运算符来进行数字运算的的。这些运算符包含加法运算符`+` 、减法运算符 `-` 、乘法运算符 `*` 、除法运算符 `/` 和求余（整除后的余数）运算符`%`。

除了基本的运算符之外， JavaScript 还支持更加复杂的算术运算，这些复杂运算通过作为 Math 对象的属性定义的函数和常量实现。

```js
Math.pow(2, 53) // => 9007199254740992 2的53次幂
Math.round(.6) // => 1.0 四舍五入
Math.ceil(.6) // => 1.0 向上求整
Math.floor(.6) // => 0.0 向下求整
Math.abs(-5) // => 5 求绝对值
Math.max(x, y, z) // 返回最大值
Math.min(x, y, z) / / 返回最小值
Math.random() // 生成一个大于0小于1的伪随机数
Math.PI // 圆周率π
Math.E // e：自然对数的底数
Math.sqrt(3) // 3的平方根
Math.pow(3, 1 / 3) // 3的立方根
Math.sin(0) // 三角函数，还有Math.cos,Math.atan等
Math.log(10) // 以10为底的自然对数
Math.log(100)/Math.LN10 //以10为底的100的对数
Math.log(512)/Math.LN2 //以2为底的512的对数
Math.exp(3) // e的三次幂
```

JavaScript 中的算术运算在溢出(overflow)、下溢(underflow)或被零整除时不会报错。但数字运算结果超过了 JavaScript 中所能表示的数字上限（溢出），结果为一个特殊的无穷大（infinty）值，在 JavaScript 中以`Infinity`表示。同样地，当负数的值超过了 JavaScript 所能表达的负数范围，结果为负无穷大，在 JavaScript 中以`-Infinty`表示。无穷大值的行为特性和我们所期望的是一致的：基于它们的加减乘除运算结果是无穷大（保留正负号）。

下溢(underflow)是当运算结果无限接近于零并比 JavaScript 能表示的最小值还小的时候发生的一种情形。这种情况下， Javascript 将会返回 0 。当一个负数发生下溢时, JavaScript 返回一个特殊的值“负零”，这个值（负零）几乎和正常的零完全一样， JavaScript 程序员很少用到负零。

被零整除在 JavaScript 并不会报错，它只是简单的返回无穷大（Infinity）或负无穷大（-Infinity）。但有一个例外，零除以零食没有意义的，这种整除运算结果也是一个非数字（not-number）值，用`NaN`表示。无穷大除以无穷大、给任意负数作开平方运算或者算术运算符与不是数字或无法转换为数字的操作数一起使用时都将返回`NaN`。

JavaScript 预定义了全局变量`Infinaty`和`NaN`，用来表达正无穷大和非数字值，在 ECMAScipt3 中，这两个值是可读/写的。 ECMAScript5 修正了这个问题，将他们定义为只读的。在 ECMAScipt3 中的 Number 对象定义的属性值也是只读的，这里有一些例子：

```js
Infinity // 将一个可读/写的变量初始化为infinty
Number.POSITIVE_INFINITY // 同样的值，只读
1 / 0 // 这也是同样的值
Number.MAX_VALUE + 1 // 计算结果还是Infinity
Number.NEGATIVE_INFINITY // 表示了负无穷大
-Infinity
-1/0
-Number.MAX_VALUE -1 
NaN          // 将一个可读/写的变量初始化为NaN
Number.NaN   // 同样的值，但是只读
0/0          // 计算结果还是NaN
Number.MIN_VALUE/2   // 发生下溢。计算结果为0
-Number.MIN_VALUE/2  // 负零
-1/Infinity          // 负零
-0        // 负零
```

JavaScript 中的非数字值有一点特殊，它和任何值都不相等，包括自身。也就是说，没法通过`x==NaN`来判断 x 是否为`NaN`。相反，应当使用`x！=x`来判断，当且仅当 x 为`NaN`的时候，表达式的结果为 true .函数`isNaN()`作用与此相似，如果参数是`NaN`或者是一个非数字值（比如字符串和对象），则返回 true 。 JavaScript 中有一个类似的函数`isFinite()`，在参数不是`NaN`、`Infinty`或`-Infinity`的时候返回 true 。

负零值同样有些特殊，它和正负零是相等的（甚至使用 JavaScript 的严格相等测试来判断）。这意味这两个值几乎是一模一样的，除了作为除数之外：

```js
var zero = 0;
var negz = -0;
zero === negz // => true 正负零值相等
1/zero === 1/negz // false 正无穷大和负无穷大不等
```

### 3.1.4 二进制浮点数和四舍五入错误

实数有无数个，但 JavaScript 通过浮点数的形式只能表示有限的个数（确切的说有18 437 736 874 454 810 627个），也就是说，当在 JavaScript 中使用实数的时候，常常只是真实值的一个近似的表示。

JavaScript 采用了 IEEE-754 浮点数表示法（几乎所有的现代编程语言采用）。这是一种二进制表示法，可以精确的表示分数，比如 1/2 、 1/8 和 1/1024 ，遗憾的是，我们常采用的分数，特别是金融计算方面，都是以十进制分数 1/10 、 1/100 等。二进制表示法并不能表示类似 0.1 这样简单的数字。

JavaScript 中的数字具有足够的精度。并可以接近 0.1 。但事实上，数字不能精确表述带来了一些问题。

```js
var x = .3 - .2;
var y = .2 - .1;
alert(x == y) //=>false 两值不相等
x == .1 //=>false .3-.2 不等于.1 
y == .1 //=>true .2-.1等于1
```

由于舍入误差，0.3和0.2之间的近似差值实际上并不等于0.2和0.1之间的近似差值（在真实模拟环境中，0.3-0.2=0.099 999 999 999 999 98）.这个问题不只在 JavaScript 中存在，理解这一点十分重要：在任何使用二进制浮点数的编程语言中都会有这个问题。同样需要注意的是，上述代码中x和y的值非常接近彼此和最终的正确值。这种计算结果可以胜任大多数的计算任务。这个问题也是只有比较两个值是否相等的时候才才会出现。

JavaScript 的未来版或许支持十进制数字类型以避免这个问题，在这之前你可能更愿意使用大整数进行重要的金融计算。例如，要使用整数“分”，而不要使用小数“元”进行基于货币单位的运算。

### 3.1.5 日期和时间

javascript语言核心包含`Date()`构造函数，用来创建日期和时间的对象，这些日期对象的方法为日期计算提供了简单的 API ，日期对象不能像数字那样是基本数据类型。

```js
var zhen = new Date(2011, 0, 1); // 2011年1月1日
var later = new Date(2011, 0, 1, 17, 10, 30); // 同一天
var now = new Date(); // 当前的日期和时间
var elapsed = now - zhen; // 日期减法。计算时间间隔的毫秒数
later.getFullYear(); // => 2011
later.getMonth(); // => 0 从0开始计数的月份
later.getDate(); // => 1 从1开始计数的天数
later.getDay(); // => 5 得到星期几。 0代表星期日，5代表星期五
later.getHours() // => 当地时间 
later.getUTCHours() // 使用UTC表示小时的时间，基于时区。
```

## 3.2 文本

字符串（string）是一组由 16 位值组成的不可变的有序序列，每个字符通常来自于 Unicode 字符集。 JavaScript 通过字符串类型来表示文本。字符串的长度（length）是其所包含 16 位值的个数。JavaScript 字符串(和其数组)的索引从0开始。空字符串的（empty string）长度为 0 ， JavaScript 中并没有表示单个字符的“字符型”。要表示一个 16 位值，只需要将其赋值给字符串变量即可。这个字符串的长度为 1 。

> 字符集，内码和 JavaScript 字符串  
> JavaScript 采用UTF-16编码的Unicode字符集， JavaScript 字符串是由一组无序号的16位值组成的序列。最常用的Unicode字符都是通过16位的内码表示，并代表字符串中的单个字符，那些不能表示为16位的Unicode字符则遵循UTF-16编码规则——用两个16位值组成一个序列（亦称为“代理项对”）表示。这意味着一个长度为2的 JavaScript 字符串（两个16位值）可能表示一个Unicode字符。  

```js
var p ="π" ;  // π由16位内码表示0x03c0
var e = "𝑒"; // 𝑒由17位内码表示0x1d452
p.length // =>1  p包含一个16位的值
e.length // =>2  𝑒通过UTF-16编码后包含两个值："\ud835\udc52"
```

### 3.2.1 字符串直接量

在 JavaScript 程序中的字符串直接量，是由单引号或双引号括起来的字符序列，由单引号定界的字符串中可以包含双引号，由双引号定界的字符串中也可以包含单引号。这里有几个字符串直接量的例子。

```js
""  // 空字符串，0个字符
'testing'
"3.14"
'name="myform"'
"wouldn't you prefer O'Reily's book?"
```

ECMAScript3中，字符串直接量必须写在一行中，而在ECMAScript5中，字符串的直接量可以拆分为数行，每行必须以反斜线（\）结束，反斜线和行结束符都不是字符串直接量的内容。如果希望在一起，则可以使用`\n`转义字符。

```js
"two\nlines"  // 这里定义了一个显示为两行的字符串
// 用三行代码定义了显示在单行的字符串，只在 ECMAScript 5 中可用
"one\
long\
line"
```

需要注意的是，当使用单引号定界字符串时，需要格外小心英文中的缩写和所有格式写法，比如 can't 和 O'Reilly's 。英文撇号和单引号是同一个字符，所以必须使用反斜线(`\`)来转义所有的撇号。

### 3.2.2 转义字符

在 JavaScript 字符串中，反斜线`\`有着特殊的用途，反斜线符号后加一个字符，就不再表示它们的字面含义了，比如，`\n`就是一个转义字符（escape sequence），它表示的是一个换行符。

另一个例子是上节中提到的转义字符`\'`，表示单引号（或撇号）。当需要在一个单引号定界的字符串内使用撇号的时候，它就显得非常有用。反斜线可以使我们避免使用常规方法解释单引号，当单引号不是用来标记字符串结尾时，它只是一个撇号。

```
'You\'re right, it can\'t be a quote'
```

表格列出了 JavaScript 中的转义字符以及它们所代表的含义。

| 转义字符 | 含义                                 |
|----------|------------------------------------|
| `\0`     | NULL字符 (\u0000)                    |
| `\b`     | 退格符 (\u0008)                      |
| `\t`     | 水平制表符 (\u0009)                  |
| `\n`     | 换行符 (\u000A)                      |
| `\v`     | 垂直制表符 (\u000B)                  |
| `\f`     | 换页符 (\u000C)                      |
| `\r`     | 回车符 (\u000D)                      |
| `\"`     | 双引号 (\u0022)                      |
| `\'`     | 撇号或单引号 (\u0027)                |
| `\\`     | 反斜线 (\u005C)                      |
| `\x`     | 由2位十六进制数XX指定的Lantin-1字符  |
| `\u`     | 由4位十六进制数XXXX指定的Unicode字符 |

### 3.2.3 字符串的使用

JavaScript 的内置功能之一就是字符串连接。如果将加号`+`运算符用于数字，表示两数相加。但将它作用于字符串，则表示字符串连接。将第二个字符串拼接在第一个之后。例如：

```js
var msg = "hello," + "world"; // 生成字符串“hello,world”
```

要确定一个字符串的长度——其所包含的16位值的个数，可以使用 length 属性，比如字符串s的长度`s.length`。

除了 length 属性，字符串还提供很多可以调用的方法。

```js
var s = "hello,world";

s.charAt(0);  // => "h"：第一个字符
s.charAt(s.length - 1)  // => "d"：最后一个字符
s.substring(1, 4)  // => "ell" 第2-4个字符
s.slice(1, 4)  // => “ell” 同上
s.slice(-3)  //  => “rld”：最后出现的3个字符

s.indexOf("l") // => 2：字符l 首次出现的位置
s.lastIndexOf("l")  //  => 10：字符l最后一次出现的位置
s.indexOf("l",3) //  => 3：在位置3及之后，l字符首次出现的位置
s.split(",")  // => ["hello","world"]：分隔成子串
s.replace("h","H") //  => "Hllo,world"：全文字符替换
s.toUpperCase()  // => "HELLO,WORLD"
```

记住，在 JavaScript 中，字符串是固定不变的，类似`replace()`和`toUpperCase()`方法都返回了新的字符串，原来的字符本身没有发生变化。

在 ECMAScript 5 中，字符串可以当做只读数组，除了使用`charAt()`方法，也可以使用方括弧来访问字符串中的单个字符。（16位值）

```js
s = "hello,world"
s[0]  // => "h"
s[s.length-1]  // => "d"
```

基于 Mozilla 的 Web 浏览器（比如Firefox）很久之前就支持这种方式的字符串索引，多数现代浏览器(IE除外)也紧跟 Mozilla 的脚步，在 ECMAScript5 成型之前就支持了这一特性。

### 3.2.4 模式匹配

JavaScript 定义了`RegExp()`构造函数，用来创建表示文本匹配模式的对象。这些模式称为“正则表达式”（regular expression）， JavaScript 采用 Perl 中的正则表达式语法。 String 和 RegExp 对象均定义了利用正则表达式进行模式匹配和查找与替换的函数。

RegExp 并不是 JavaScript 的基本类型。和 Date 一样，它只是一种具有实用 API 的特殊对象。正则表达式的语法很复杂， API 也很丰富。在第10章有详尽的文档介绍。RgeExp是一种强大和常用的文本处理工具。

尽管 RegExp 并不是语言中的基本数据类型，但是它们依然具有直接量写法，可以直接在 JavaScript 程序中使用。在两条斜线之间的文本构成了一个正则表达式直接量。第二条斜线之后也可以跟随一个或多个字母，用来修饰匹配模式的含义，例如：

```js
/^HTML/  // 匹配以HTML开始的字符串
/[1-9][0-9]*/  // 匹配一个非零数字，后面是任意个数字
/\bjavascript\b/i  // 匹配单词javascript，并忽略大小写
```

RegExp 对象定义了很多有用的方法，字符串同样具有可以接受 RegExp 参数的方法。例如：

```js
var text = "testing:1,2,3";  // 文本示例
var pattern = /\d+/g  // 匹配所有包含一个或多个数字的实例
pattern.test(text)  // => true:匹配成功
text.search(pattern)  // => 9 ：首次匹配成功的位置
text.match(pattern)  // => ["1","2","3"]：所有匹配组成数组
text.repeat(pattern,"#");  // => "testing:#,#,#"
text.split(/\D+/);  // => ["","1","2","3"]：用非数字字符截取字符串
```

## 3.3 布尔值

布尔值指代真或假。开或关。是与否。这个类型只有两个值，保留字 true 和 false 。

JavaScript 程序中的比较语句的结果通常都是布尔值`a==4`。

布尔值通常用于 JavaScript 中的控制结构中，例如， JavaScript 中的 if/else 语句，如果布尔值为 true 执行第一段逻辑，如果为 false 执行另一段逻辑。通常将一个创建布尔值的比较直接与使用这个比较的语句结合在一起。结果如下所示：

```js
if (a == 4)
b = b + 1;
else
a = a + 1;
```

任意 JavaScript 的值都可以转换为布尔值。下面的这些值会被转换成 false 。所有其它值，包括所有对象（数组）都会转换成 true 。false 和下面 6 个可以转换成 false 的值有时称作“假值”（falsy value），其他值称做“真值”（truth value）。 JavaScript 期望使用一个布尔值的时候，假值会被当成 false ，真值会被当成 true 。

```js
undefined
null
0
-0
NaN
""//空字符串
```

来看一个例子，假设变量 o 是一个对象或是`null`,可以通过一条 if 语句来检测 o 是否是非`null`值。

```js
if(o !== null)...
```

不等操作符“!==”将 o 和`null`比较，并得出结果为 true 或 false 。可以先忽略这里的比较语句，`null`是一个假值，对象是一个真值。

```js
if(o)...
```

对于第一种情况，只要当 o 不是`null`时才会执行 if 后的代码，第二种情况的限制没有那么严格。只有 o 不是 false 或任何假值（比如null或unfined）时才执行这个if。到底选用哪条语句取决于期望赋给 o 的值是什么。如果需要将`null`与 0 或空字符串区分开来，则需要使用一个显式的比较。

布尔值包含`toString()`方法，因此可以使用这个方法将字符串转换为 “true” 或"false"，但它不包含其他有用的方法，除了这个不重要的API，还有三个重要的布尔值运算符。

`&&`运算符执行了逻辑与（AND）操作。当且仅当两个操作数都是真值时它才返回 true ，否则返回 false 。`||`运算符是布尔或（OR）操作，如果两个操作数其中一之一为真值它就返回 true ，如果两个操作数都是假值则返回 false 。最后，一元操作符`!`执行了布尔非(NOT)操作，如果操作数是真值返回 false ，如果是假值则返回true。比如：

```js
if ((x == 0 && y == 0) || !(z == 0)) {
  //x和y都是零或z是非零
}
```


## 3.4 null和undefined

null 是 JavaScript 语言的关键字，它表示一个特殊值，常用来描述“空值”。对 null 执行 typeof 预算，结果返回字符串“object”，也就是说，可以将 null 认为是一个特殊的对象值，名义是“非对象”。但实际上，通常认为 null 是它自有类型的唯一一个成员，它可以表示数字、字符串和对象是“无值”的。大多数编程语言和 JavaScript 一样含有 null 。

JavaScript 还有第二个值来表示值的空缺。用未定义的值表示更深层次的“空值”。它是变量的一种取值，表明变量没有初始化，如果要查询对象属性或数组元素的值时返回 undefined 则说明这个属性或元素不存在。如果函数没有返回任何值，则返回 undefined。引用没有提供实参的函数形参的值也只会得到 undefined 。 undefined 是预定义的全局变量（它和 null 不一样，它不是关键字），它的值就是“未定义”。在 ECMAScript 3 中，undefined 是可读/写的变量，可以给它赋任何值。这个错误在 ECMAScript 5 中做了修正， undefined 在该版本中是只读的。如果使用 typeof 运算符得到 undefined 的类型，则返回“undefined”，表明这个值是这个类型的唯一成员。

尽管 null 和 undefined 是不通的，但它们都表示“值的空缺”，两者往往可以互换。判断相等运算符“==”认为两者是相等的（要使用严格相等运算符“===”来区分它们）。在希望值是布尔值类型的地方它们的值都是假值，和 false 类似。 null 和 undefined 都不包含任何属性和方法。实际上，使用“.”和“[]”来存取这两个值的成员或方法都会产生一个类型错误。

可以认为 undefined 是表示系统级的、出乎意料的或类似错误的值的空缺，而 null 是表示程序级的、正常的或在意料之中的值的空缺。如果想将它们赋值给变量或者属性，或将它们作为参数传入函数，最佳选择是使用 null 。

## 3.5 全局对象

有一类非常重要的对象，我们不得不现在就把它们讲清楚——全局对象。全局对象（global object）在JavaScript中有着重要的用途：全局对象的属性是全局定义的符号，JavaScript程序可以直接使用。当JavaScript解释器启动时（或者任何Web浏览器加载新页面的时候），它将创建一个新的全局对象，并给它一组定义的初始属性：

- 全局属性，比如`undefined`、`Infinity`和`NaN`
- 全局函数，比如`isNaN()`、`parseInt()`和`eval()`
- 构造函数，比如`Date()`、`RegExp()`、`String()`、`Object()`和`Array()`
- 全局对象，比如`Math`和`JSON`(见6.9节)

全局对象的初始属性并不是保留字，但它们应该当做保留字来对待。可以在第三部分中通过名称查找到，或者通过别名“Global”来找到这些全局对象。对于客户端JavaScript来讲，Window对象定义了一些额外的全局属性，可以在第四部分中查看它们。

在代码的最顶级——不在任何函数内的JavaScript代码——可以使用JavaScript关键字this来引用全局对象：

```js
var global = this;  // 定义一个引用全局对象的全局变量。
```

在客户端JavaScript中，在其表示的浏览器窗口中的所有JavaScript代码中，Window对象充当了全局对象。这个全局Window对象有一个属性window引用其自身，它可以代替this来引用全局对象。Window对象定义了核心全局属性，但它也针对Web浏览器和客户端JavaScript定义了一少部分其他全局属性。

当初次创建的时候，全局对象定义了JavaScript中所有的预定义全局值。这个特殊对象同样包含了为程序定义的全局值。如果代码声明了一个全局变量，这个全局变量就是全局对象的一个属性，3.10.2节有关于此的详尽解释。

## 3.6 包装对象

JavaScript 对象是一种复合值，它是属性或已命名值的集合。通过“.”符号来应用属性值。当属性值是一个函数的时候，称其为方法。通过`o.m()`来调用对象 o 中的方法。

字符串也同样具有属性和方法：

```js
// 一个字符串
var s ="hello world";
// 使用字符串的属性
var word = s.substring(s.indexOf(" ")+1,s.length);
console.log(word)  // "world"
```

只有引用了字符串 s 的属性， JavaScript 就会将字符串值通过调用`new String(s)`的方式转换成对象，这个对象继承了字符串的方法，并被用来处理属性的引用。一旦属性引用结束，这个新创建的对象就会销毁（其实在实现上并不一定创建或者销毁这个临时对象，然而整个过程看起来是这样）。

同字符串一样，数字和布尔值也具有各自的方法：通过`Number()`和`Boolean()`构造函数创建一个临时对象，这些方法的调用均是来自于这个临时对象。`null`和`undefined`没有包装对象，访问它们的属性会造成一个类型错误。

看如下代码，思考它们的执行结果：

```js
var s = "test";  // 创建一个字符串
s.len = 4;  // 给它设置一个属性
var t = s.len  // => undefined 查找这个属性 
```

存取字符串、数字或布尔值的属性时创建的临时对象称做包装对象，它只是偶尔用来区别字符串值和字符串对象、数字和数值对象以及布尔值和布尔对象。通常，包装对象只是被看作是一种实现细节，而不用特别关注。由于字符串、数字和布尔值的属性都是只读的，并且不能给他们定义新属性，因此需要明白它们是有别于对象的。

JavaScript 会在必要时将包装对象转换成原始值，因此下面代码中的对象 S/N/B 常常但不总是表现和值 s/n/b 一样。“==”等于运算符将原始值和其包装对象视为相等，但“===”全等运算符将它们视为不等。通过 typeof 运算符可以看到原始值和其包装对象的不同。

```js
var s = "test",
    n = 1,
    b = true;
var S = new String(s);
var N = new Number(n);
var B = new Boolean(b);
```

## 3.7 不可变的原始值和可变的对象引用

JavaScript 中 的原始值（undefined、null、布尔值、数字和字符串）与对象（包括数组和函数）有着根本区别。原始值是不同更改的；任何方法都无法更改（或“突破”）一个原始值。对数字和布尔值来说显然如此——改变数字的值本身就说不通，而对字符串来说就不那么明显了，因为字符串看起来像由字符串组成的数组，我们期望可以通过指定索引来修改字符串中的字符。实际上， JavaScript 是禁止这样做的。字符串中所有的方法看上去返回了一个修改后的字符串，实际上返回的是一个新的字符串值。例如：

```js
var s = "hello";
s.toUpperCase();  // 返回"HELLO"并没更改s的值
s  // => "hello" 原始的字符串并未改变
```

原始值的比较是值的比较：只有在它们的值相等时它们才相等。这对数字、布尔值、null 和 undefined 来说看起来有点儿难懂，并没有其他办法来比较它们。同样，对于字符串来说则并不明显：如果比较两个单独的字符串，当且仅当它们的长度相等且每个索引的字符都相等时，JavaScript 才认为它们相等。

对象和原始值不同，首先，它们是可变的——它们的值是可修改的：

```js
var o = {x:1}  // 定义一个对象
o.x = 2  // 通过修改对象的属性来改变对象
o.y = 3  // 再次更改这个对象，给它增加一个新属性

var a =[1,2,3]  // 数组也是可以修改的
a[0]=0;  // 更改数组中的一个元素
a[3]=4;  // 给数组增加一个新元素
```

对象的比较并非值的比较：即使两个对象包含同样的属性及相同的值，他们也是不相等的，各个索引元素完全相等的两个数组也不相等。

```js
var o ={x:1}, p={x:1}  // 两个具有相同属性的两个对象
o === p ;  // =>false：两个单独的对象永不相等

var a =[],b=[];  // 两个单独的空数组
a === b ;  // =>false：两个单独的数组永不相等
```

我们通常将对象称为引用类型(reference type)，以此来和 JavaScript 的基本类型区分开来。依照术语的叫法，对象都是引用(reference)，对象的比较均是引用的比较；当且当它们应用同一个基对象时，它们才相等。

```js
var a = [];  // 定义一个引用空数组的变量a
var b = a;  // 变量b引用同一个数组
b[0] = 1;  // 通过变量b来修改引用的数组
a[0]  // =>1：变量a也会修改
a === b  // =>true：a和b引用同一个数组，因此他们相等。
```

就像你刚才看到的如上代码，将对象（或数组）赋值给一个变量，仅仅是赋值的引用值：对象本身并没有复制一次。如果你想得到一个对象或数组的副本，则必须显式复制对象的每个属性或数组的每个元素。下面的这个例子则是通过循环来完成对数组的复制。

```js
var a = ['a', 'b', 'c'];  // 待复制的数组
var b = [];  // 复制到目标的空数组
for (var i = 0; i < a.length; i++) {  // 遍历a[]中的每个元素
    b[i] = a[i];  // 将元素复制到b中。
}
```

同样的，如果我们想比较两个单独或者数组，则必须比较他们的属性或元素。下面这段代码定义了一个比较两个数组的函数。

```js
function equalArrays(a, b) {
  // 两个长度不相同的数组不相等
  if (a.length != b.length) return false; 
  // 循环遍历所有元素
  for (var i = 0; i < a.length; i++) 
    // 如果有任意元素不等，则数组不相等
    if (a[i] !== b[i]) return false; 
  return true; //  否则他们相等
}
```

## 3.8 类型转换

JavaScript 中的取值类型非常灵活，当 JavaScript 期望使用一个布尔值的时候，可以提供任意类型值， JavaScript 将根据需要自行转换类型。一些值（真值）转换为 true，其他值（假值）转换为 false 。这在其他类型中同样适用：如果 JavaScript 期望使用一个字符串，它把给定的值转换为字符串。如果 JavaScript 期望使用一个数字，它把给定的值转换为数字（如果转换结果无意义的话将返回 NaN），一些例子如下：

```js
10 + "object"  // => "10object"：数字10转换成字符串
"7" * "4"  // => 28：两个字符串均转化为数字
var n = 1 - "x"  // => NaN：字符串x无法转换为数字
n + " objects"  // =>"NaN objects"：NaN转换为字符串"NaN"
```

下表简要说明了在 JavaScript 中如何进行类型转换。空单元格表示不必要也没有执行转换。

|            值            |  转换为字符串  |    数字     | 布尔值 |         对象          |
| ------------------------ | -------------- | ----------- | ------ | --------------------- |
| `undefined`              | "undefined"    | NaN         | false  | throws TypeError      |
| `null`                   | "null"         | 0           | false  | throws TypeError      |
| `true`                   | "true"         | 1           |        | new Boolean(true)     |
| `false`                  | "false"        | 0           |        | new Boolean(false)    |
| ""(空字符串)             |                | 0           | false  | new String("")        |
| "1.2"(非空,数字)         |                | 1.2         | true   | new String("1.2")     |
| "one"(非空,非数字)       |                | NaN         | true   | new String("one")     |
| `0`                      | "0"            |             | false  | new Number(0)         |
| `-0`                     | "0"            |             | false  | new Number(-0)        |
| `NaN`                    | "NaN"          |             | false  | new Number(NaN)       |
| `Infinity`               | "Infinity"     |             | true   | new Number(Infinity)  |
| `-Infinity`              | "-Infinity"    |             | true   | new Number(-Infinity) |
| `1`(无穷大,非零)         | "1"            |             | true   | new Number(1)         |
| `{}`(任意对象)           | 参考3.8.3节    | 参考3.8.3节 | true   |                       |
| `[]`(任意数组)           | ""             | 0           | true   |                       |
| `[9]`(1个数字元素)       | "9"            | 9           | true   |                       |
| `['a']`(其他数组)        | 使用join()方法 | NaN         | true   |                       |
| `function(){}`(任意函数) | 参考3.8.3节    | NaN         | true   |                       |

原始值到对象的转换也非常简单，原始值通过调用`String()`、`Number()`或`Boolean`构造函数，转换为它们各自的包装对象。

`null`和`undefined`属于例外，当将它们用在期望是一个对象的地方都会造成一个类型错误（TypeError）异常，而不会执行正常的转换。

对象到原始值的转换多少有些复杂，3.8.3节将以此为专题专门讲诉。

### 3.8.1.转换和相等性 

由于 JavaScript 可以做灵活的类型转换，因此其“==”相等运算符也随相等的含义灵活多变。例如，如下这些比较结果均是`true`：

```js
null == undefined // 这两值被认为相等 
"0" == 0 // 在比较之前字符串转换成数字 
0 == false // 在比较之前布尔值转换成数字  
"0" == false // 在比较之前字符串和布尔值都转换成数字
```

4.9.1节详细讲解了“==”相等运算符在判断两个值是否相等时做了哪些类型转换，并同样介绍了“===”恒等运算符在判断相等时并未做任何类型转换。

需要特别注意的是，一个值转换为另一个值并不意味着两个值相等。比如，如果在期望使用布尔值的地方使用了`undefined`，它将会转换为`false`，但这并不表明`undefined == false`。JavaScript 运算符和语句期望使用多样化的数据类型，并可以相互转换。 if 语句将`undefined`转换为`false`，但“==”运算符从不试图将其操作数转换为布尔值。

### 3.8.2.显式类型转换

尽管JavaScript可以自动做许多类型转换，但有时仍需要做显式转换，或者为了使代码变得清晰易读而做显式转换。

做显式类型转换最简单的方法就是使用`Boolean()`、`Number()`、`String()`或`Object()`函数。当不通过 new 运算符调用这些函数时，它们会作为类型转换函数并按照表3-2所描述的规则做类型转换：

```js
Number("3")  // => 3  
String(false)  // => "false" 或使用 false.toString()
Boolean([])  // => true 
Object(3)  // => new Number(3)
```

需要注意的是，除了`null`或`undefined`之外的任何值都具有`toString()`方法，这个方法的执行结果通常和`String()`方法的返回结果一致。同样需要注意的是，如果试图把`null`或`undefined`转换为对象则会像表3-2所描述的那样抛出一个类型错误（TypeError）。`Object()`函数在这种情况下不会抛出异常：它仅简单地返回一个新创建的空对象。 

JavaScript中的某些运算符会做隐式的类型转换，有时用于类型转换。如果“+”运算符的一个操作数是字符串，它将会把另外一个操作数转换为字符串。一元“+”运算符将其操作数转换为数字。同样，一元“!”运算符将其操作数转换为布尔值并取反。在代码中会经常见到这种类型转换的惯用法：

```js
x + ""  // 等价于String(x)  
+ x  // 等价于 Number(x).也可以写成 x-0
!! x  // 等价于 Boolean(x). 注意是双叹号
```

在计算机程序中数字的解析和格式化是非常普通的工作，JavaScript中提供了专门的函数和方法用来做更加精确的数字到字符串（number-to-string）和字符串到数字（string-to-number）的转换。

Number类定义的`toString()`方法可以接收表示转换基数（radix）的可选参数，如果不指定此参数，转换规则将是基于十进制。同样，亦可以将数字转换为其他进制数（范围在2～36之间），例如：

```js
var n = 17;  
binary_string = n.toString(2);  // 转换为 "10001" 
octal_string = "0" + n.toString(8);  // 转换为 "021" 
hex_string = "0x" + n.toString(16);  // 转换为 "0x11"
```

当处理财务或科学数据的时候，在做数字到字符串的转换过程中，你期望自己控制输出中小数点位置和有效数字位数，或者决定是否需要指数记数法。Number类为这种数字到字符串的类型转换场景定义了三个方法。

- `toFixed()`根据小数点后的指定位数将数字转换为字符串，它从不使用指数记数法。
- `toExponential()`使用指数记数法将数字转换为指数形式的字符串，其中小数点前只有一位，小数点后的位数则由参数指定（也就是说有效数字位数比指定的位数要多一位）。
- `toPrecision()`根据指定的有效数字位数将数字转换成字符串。如果有效数字的位数少于数字整数部分的位数，则转换成指数形式。

我们注意到，所有三个方法都会适当地进行四舍五入或填充0。看一下下面几个例子：

```js
var n = 123456.789; 
n.toFixed(0); // "123457" 
n.toFixed(2); // "123456.79" 
n.toFixed(5); // "123456.78900" 
n.toExponential(1); // "1.2e+5" 
n.toExponential(3); // "1.235e+5" 
n.toPrecision(4); // "1.235e+5" 
n.toPrecision(7); // "123456.8" 
n.toPrecision(10); // "123456.7890" 
```

如果通过`Number()`转换函数传入一个字符串，它会试图将其转换为一个整数或浮点数直接量，这个方法只能基于十进制数进行转换，并且不能出现非法的尾随字符。`parseInt()`函数和`parseFloat()`函数（它们是全局函数，不从属于任何类的方法）更加灵活。`parseInt()`只解析整数，而`parseFloat()`则可以解析整数和浮点数。如果字符串前缀是“0x”或者“0X”，`parseInt()`将其解释为十六进制数，`parseInt()`和`parseFloat()`都会跳过任意数量的前导空格，尽可能解析更多数值字符，并忽略后面的内容。如果第一个非空格字符是非法的数字直接量，将最终返回NaN：

```js
parseInt("3 blind mice") // => 3 
parseFloat(" 3.14 meters") // => 3.14 
parseInt("-12.34") // => -12 
parseInt("0xFF") // => 255 
parseInt("0xff") // => 255 
parseInt("-0XFF") // => -255 
parseFloat(".1") // => 0.1 
parseInt("0.1") // => 0  
parseInt(".1") // => NaN: 整数不能以"."开始 
parseFloat("$72.47"); // => NaN: 数字不能以"$"开始
```

`parseInt()`可以接收第二个可选参数，这个参数指定数字转换的基数，合法的取值范围是2～36，例如： 

```js
parseInt("11", 2); // => 3 (1*2 + 1) 
parseInt("ff", 16); // => 255 (15*16 + 15) 
parseInt("zz", 36); // => 1295 (35*36 + 35) 
parseInt("077", 8); // => 63 (7*8 + 7) 
parseInt("077", 10); // => 77 (7*10 + 7) 
```

### 3.8.3.对象转换为原始值

对象到布尔值：所有的对象（包括数组和函数）都转换为`true`。对于包装对象亦是如此：`new Boolean(false)`是一个对象而不是原始值，它将转换为`true`。

对象到字符串（object-to-string）和对象到数字（object-to-number）的转换是通过调用待转换对象的一个方法来完成的，这样的方法有两个，所有的对象继承了两个转换方法。值得注意的是，这里提到的字符串和数字的转换规则只适用于本地对象（native object）。宿主对象（例如，由Web浏览器定义的对象）根据各自的算法可以转换成字符串和数字。

第一个方法：`toString()`，它的作用是返回一个反映这个对象的字符串。默认的`toString()`方法并不会返回一个有趣的值：

```js
({x:1, y:2}).toString() // => "[object Object]" 
```

很多类定义了更多特定版本的`toString()`方法。例如：数组类(Array class)的`toString()`方法将每个数组元素转换为一个字符串，并在元素之间添加逗号后并合成结果字符串。函数类(Function class)的`toString()`方法返回这个函数的实现定义的表示方式。实际上，这里的实现方式是通常是将用户定义函数转换为javascript源代码字符串。日期类(Date class)定义`toString()`方法返回一个可读的（可被javascript解析的）日期和时间字符串。RegExp 类定义的`toString()`方法将RegExp对象转换为正则表达式直接量字符串。

```js
[1, 2, 3].toString();  // => "1,2,3"
(function(x) { f(x); }).toString(); // => "function(x){\n f(x); \n}"
/\d+/g.toString();  // => /\\d+/g
new Date(2015, 0, 1).toString()  // =>Thu Jan 01 2015 00:00:00 GMT+0800 (中国标准时间)
```

另一个转换对象的函数是`valueOf()`。这个方法的任务并未详细定义：如果存在任意原始值，它就默认将对象转换为表示它的原始值。对象是复合值，而且大多数对象无法真正表示为一个原始值，因此默认的`valueOf()`方法简单地返回对象本身，而不是返回一个原始值。数组、函数和正则表达式简单地继承了这个默认方法，调用这些类型的实例的`valueOf()`方法只是简单返回对象本身。日期类定义的`valueOf()`方法会返回它的一个内部表示：1970年1月1日以来的毫秒数。

```js
var d = new Date(2010, 0, 1); // 2010年1月1日(太平洋时间)
d.valueOf() // => 1262332800000 
```

通常使用刚刚讲解的`toString()`和`valueOf()`方法，就可以做到对象到字符串和对象到数字的转换。但需要注意的是，在某些特殊的场景中， JavaScript 执行了完全不同的对象到原始值的转换。

JavaScript中对象到字符串的转换经过了如下这些步骤：

- 如果对象具有`toString()`方法，则调用这个方法。如果它返回一个原始值，JavaScript将这个值转换为字符串(如果本身不是字符串的话)，并返回这个字符串结果。需要注意的是，原始值到字符串的转换在表3-2中已经有了详尽的说明。
- 如果对象没有`toString()`方法，或者这个方法并不返回一个原始值，那么JavaScript会调用`valueOf()`方法。如果存在这个方法，则JavaScript调用它。如果返回值是原始值，JavaScript将这个值转换为字符串（如果本身不是字符串的话），并返回这个字符串结果。
- 否则，JavaScript无法从`toString()`或`valueOf()`获得一个原始值，因此这时它将抛出一个类型错误异常。

在对象到数字的转换过程中，JavaScript做了同样的事情，只是它会首先尝试使用`valueOf()`方法：

- 如果对象具有`valueOf()`方法，后者返回一个原始值，则JavaScript将这个原始值转换为数字（如果需要的话）并返回这个数字。
- 否则，如果对象具有`toString()`方法，后者返回一个原始值，则JavaScript将其转换并返回。
- 否则，JavaScript抛出一个类型错误异常。

对象转换为数字的细节解释了为什么空数组会被转换为数字0，以及为什么具有单个元素的数组同样会转换成一个数字。数组继承了默认的`valueOf()`方法，这个方法返回一个对象而不是一个原始值，因此，数组到数字的转换则调用`toString()`方法。空数组转换成为空字符串，空字符串转换成为数字0。含有一个元素的数组转换为字符串的结果和这个元素转换字符串的结果一样。如果数组只包含一个数字元素，这个数字转换为字符串，再转换回数字。

JavaScript中的“+”运算符可以进行数学加法和字符串连接操作。如果它的其中一个操作数是对象，则JavaScript将使用特殊的方法将对象转换为原始值，而不是使用其他算术运算符的方法执行对象到数字的转换，“==”相等运算符与此类似。如果将对象和一个原始值比较，则转换将会遵照对象到原始值的转换方式进行。

“+”和“==”应用的对象到原始值的转换包含日期对象的一种特殊情形。日期类是JavaScript语言核心中唯一的预先定义类型，它定义了有意义的向字符串和数字类型的转换。对于所有非日期的对象来说，对象到原始值的转换基本上是对象到数字的转换（首先调用`valueOf()`），日期对象则使用对象到字符串的转换模式，然而，这里的转换和上文讲述的并不完全一致：通过`valueOf()`或`toString()`返回的原始值将被直接使用，而不会被强制转换为数字或字符串。

和“==”一样，“<”运算符以及其他关系运算符也会做对象到原始值的转换，但要除去日期对象的特殊情形：任何对象都会首先尝试调用`valueOf()`，然后调用`toString()`。不管得到的原始值是否直接使用，它都不会进一步被转换为数字或字符串。

“+”、“==”、“!=”和关系运算符是唯一执行这种特殊的字符串到原始值的转换方式的运算符。其他运算符到特定类型的转换都很明确，而且对日期对象来讲也没有特殊情况。例如“-”（减号）运算符把它的两个操作数都转换为数字。下面的代码展示了日期对象和“+”、“-”、“==”以及“>”的运行结果：

```js
var now =new Date();  // 创建一个日期对象
typeof(now+1);  // =>"string"：“+”将日期转换为字符串
typeof(now-1);  // =>"number":"-"使用对象到数字的转换
now== now.toString();  // =>true:隐式的和显示的字符串转换
now>(now-1);  // =>true:">"将日期转换为数字
```

## 3.9 变量声明

在 JavaScript 程序中，使用一个变量之前应该先声明，变量是通过 var 来声明的，如下所示：

```js
var i;
var sum;
```

也可以通过一个 var 关键字声明多个变量

```js
var i,sun;
```

而且还可以将变量的初始值和变量声明和写在一起；

```js
var message = "hello";
var i=0, j=0, k=0;
```

如果在 var 声明语句中给变量指定初始值，那么虽然声明了这个变量，但在给它存入一个值前，它的初始值是`undefined`. 

在 for 和 for/in 循环中同样可以使用 var 语句，这样可以更加简洁地声明在循环体语法中内使用的循环变量。例如：

```js
for (var i = 0; i < 10; i++) log(i);
for (var i = 0, j = 10; i < 10, j = 100; i++, j--) console.log(i * j)
for (var p in o) console.log(p);
```

在 JavaScript 的变量声明中并没有指定变量的数据类型。 JavaScript 变量可以是任意数据类型。例如，在 JavaScript 中首先将数字赋值给一个变量，随后再将字符串赋值给这个变量，这是完全合法的。

```js
var i=10;
i="ten";
```

编程语言分为动态（类型）语言和静态（类型）语言，动态类型语言是指在运行期间才去做数据类型检查的语言，Python、Ruby和JavaScript就是典型的动态类型语言。静态类型语言与动态类型语言刚好相反，它的数据类型实在编译期间检查的，C/C++是静态类型语言的典型代表。

**重复的声明和遗漏声明**

使用 var 语言重复声明变量是合法且无害的。如果重复声明带有初始化器，那么这就和一条简单的赋值语句没什么两样。

如果试图读取一个没有声明的变量的值，JavaScript会报错。在ECMAScript 5严格模式中，给一个没有声明的变量赋值也会报错。然而从历史上讲，在非严格模式下，如果给一个未声明的变量赋值，JavaScript实际上会给全局对象创建一个同名属性，并且它工作起来像一个正确声明的全局变量。这意味着你可以侥幸不声明全局变量。但这是一个不好的习惯并会造成很多bug，因此，你应当始终使用var来声明变量。

## 3.10 变量作用域

一个变量的作用域（scope）是程序源代码中定义这个变量的区域。全局变量拥有全局作用域，在JavaScript代码中的任何地方都是有定义的。然而在函数内声明的变量只在函数体内有定义。它们是局部变量，作用域是局部性的。函数参数也是局部变量，它们只在函数体内有定义。

在函数体内，局部变量的优先级高于同名的全局变量。如果在函数内声明的一个局部变量或者函数参数中带有的变量和全局变量重名，那么全局变量就被局部变量所遮盖。

```js
// 声明一个全局变量
var scope = "global"; 
function checkscope() {
  // 声明一个同名的局部变量
  var scope = "local"; 
  return scope;
}
// => "local"
checkscope(); 
```

尽管在全局作用域编写代码时可以不写var语句，但声明局部变量时则必须使用var语句。

```js
scope = "global"; //声明一个全局变量,甚至不使用var来声明
function checkscope2() {
  scope = "local"; //修改了全局变量
  myscope = "local"; //这里显示式得声明了一个新的全局变量
  return [scope, myscope]; //
}
checkscope2(); //=> ["local","local"]:产生了副作用
scope // =>"local"全局变量修改了
myscope //=> "local"全局命名空间搞乱了。
```

函数定义是可以嵌套的。由于每个函数都有它直接的作用域，因此会出现几个局部作用域嵌套的情况。

```js
var scope = "global scope"; //全局变量
function checkscope() {
  var scope = "local scope"; //局部变量
  function nested() {
    var scope = "sested scope"; //嵌套作用域内的局部变量
    return scope;
  }
  return nested();
}
checkscope() //=> sested scope："嵌套作用域" 
```

### 3.10.1 函数作用域和声明提前

有一些类似 C 语言的编程语言中，花括号内的每一段代码都具有各自的作用域，而且变量在声明它们的代码段之外是不可见的，我们称为块级作用域（block scope），而 JavaScript 中没有块级作用域。 JavaScript 取而代之地使用了函数作用域（function scope），变量在声明它们的函数体以及这个函数体嵌套的任意函数体内都是有定义的。

```js
function test(o) {
  // i在整个函数体内均是定义的
  var i = 0;
  if (typeif o == "object") {  
    // j在函数体内是有定义的，不仅仅是在这个代码段内
    var j = 0; 
    // k在函数体内是有定义的，不仅仅是在循环内
    for (var k = 0; k < 10; k++) { 
      // 输出数字0-9
      console.log(k); 
    }
    // k已经定义，输出10
    console.log(k);  
  }
  // j已经定义了，但可能没有初始化。
  console.log(j);        
}
```

JavaScript 的函数作用域是指在函数内声明的所有变量在函数体内始终可见的。有意思的是，这意味着变量在声明之前甚至已经可用。 JavaScript 的这个特性被非正式地称为声明提前（hoisting），即 JavaScript 函数里声明的所有变量（但不涉及赋值）都被“提前”至函数体的顶部。

```js
var scope = "global";
function f() {
  // 输出"undefined",而不是"global"
  console.log(scope); 
  // 变量在这里赋初始值，但变量本身在函数体内任何地方都是有定义的
  var scope = "local"; 
  // 输出"local"
  console.log(scope); 
}
```

由于函数作用域的特性模具部变量在整个函数体内始终有定义的，也就是说，在函数体内局部变量覆盖了同名全局变量。尽管如此，只有在程序执行到 var 语句的时候，局部变量才能正真的被赋值。因此，上述的过程等价于：将函数内的变量声明"提前"至函数顶部，同时变量初始化留在原来的位置：

```js
function f() {
  var scope; //在函数的顶部声明了局部变量
  console.log(scope); //变量存在，但其值是"undefined"
  scope = "local"; //在这里将其初始化，并赋值
  console.log(scope); //这里它具有了我们所期望的值
}
```

在具有块级作用域的编程语言中，在狭小的作用域里让变量声明和使用变量的代码尽可能靠近彼此，通常来讲，这是一个非常不错的编程习惯。由于JavaScript没有块级作用域，因此一些程序员特意将变量声明放在函数体顶部，而不是将声明靠近放在使用变量之处。这种做法使得他们的源代码非常清晰地反映了真实的变量作用域。

### 3.10.2 作为属性的变量

当声明一个JavaScript全局变量时，实际上是定义了全局对象的一个属性。当使用var声明一个变量时，创建的这个属性是不可配置的，也就是说这个变量无法通过`delete`运算符删除。可能你已经注意到了，如果你没有使用严格模式并给一个未声明的变量赋值的话，JavaScript会自动创建一个全局变量。以这种方式创建的变量是全局对象的正常的可配值属性，并可以删除它们：

```js
var truevar = 1;  // 声明一耳光不可删除的全局变量
fakevar = 2;  // 创建全局对象的一个可删除的属性
this.fakevar2 = 3;  // 同上

delete truevar  // => false   变量并没有删除
delete fakevar  // => true 变量被删除
delete this.fakevar2  // =>true 变量被删除
```

JavaScript 全局变量是全局对象的属性，这是在 ECMAScript 规范中强制规定的。对于局部变量则没有如此规定，但我们可以想象得到，局部变量当做跟函数调用相关的某个对象的属性。ECMAScript 3 规范称该对象为“调用对象”(call object)，ECMAScript 5 规范称为“声明上下文对象”（declarative environment record）。 

JavaScript 可以允许使用this关键字来引用全局对象，却没有方法可以引用局部变量中存放的对象。这种存放局部变量的对象的特有性质，是一种对我们不可见的内部实现。

### 3.10.3 作用域链

JavaScript 是基于词法作用域的语言：通过阅读包含变量定义在内的数行源码就能知道变量的作用域。全局变量在程序中始终都是有定义的。局部变量在声明它的函数体内以及其所嵌套的函数内始终是有定义的。

每一段JavaScript代码（全局代码或函数）都有一个与之关联的作用域链（scope chain）。这个作用域链是一个对象列表或者链表，这组对象定义了这段代码“作用域中”的变量。当JavaScript需要查找变量x的值的时候（这个过程称做“变量解析”（variable resolution）），它会从链中的第一个对象开始查找，如果这个对象有一个名为x的属性，则会直接使用这个属性的值，如果第一个对象中不存在名为x的属性，JavaScript会继续查找链上的下一个对象。如果第二个对象依然没有名为x的属性，则会继续查找下一个对象，以此类推。如果作用域链上没有任何一个对象含有属性x，那么就认为这段代码的作用域链上不存在x，并最终抛出一个引用错误（ReferenceError）异常。

在JavaScript的最顶层代码中（也就是不包含在任何函数定义内的代码），作用域链由一个全局对象组成。在不包含嵌套的函数体内，作用域链上有两个对象，第一个是定义函数参数和局部变量的对象，第二个是全局对象。在一个嵌套的函数体内，作用域链上至少有三个对象。

理解对象链的创建规则是非常重要的。当定义一个函数时，它实际上保存一个作用域链。当调用这个函数时，它创建一个新的对象来存储它的局部变量，并将这个对象添加至保存的那个作用域链上，同时创建一个新的更长的表示函数调用作用域的“链”。对于嵌套函数来讲，事情变得更加有趣，每次调用外部函数时，内部函数又会重新定义一遍。因为每次调用外部函数的时候，作用域链都是不同的。内部函数在每次定义的时候都有微妙的差别——在每次调用外部函数时，内部函数的代码都是相同的，而且关联这段代码的作用域链也不相同。

作用域链的概念对于理解with语句是非常有帮助的，同样对理解闭包的概念也至关重要。

# 第4章 表达式和运算符

表达式（expression）JavaScript中的一个短语，JavaScript解释器会将其计算（evaluate）出一个结果。程序中的常量是最简单的一类表达式。变量名也是一种简单的表达式，它的值就是赋值给变量的值。复杂表达式是由简单表达式组成的。比如，数组访问表达式是由一个表示数组的表达式、左方括号、一个整数表达式和右方括号构成。它们所组成的新的表达式的运算结果是该数组的特定位置的元素值。同样的，函数调用表达式由一个表示函数对象的表达式和0个或多个参数表达式构成。

将简单表达式组合成复杂表达式最常用的方法就是使用运算符（operator）。运算符按照特定的运算规则对操作数（通常是两个）进行运算，并计算出新值。乘法运算符“*”是比较简单的例子。表达式`x*y`是对两个变量表达式`x`和`y`进行运算并得出结果。有时我们更愿意说运算符返回了一个值而不是“计算”出了一个值。

本章将讲解所有的JavaScript运算符，同时也讲解不涉及运算符的表达式（比如访问数组元素和函数调用）。

## 4.1 原始表达式

最简单的表达式是“原始表达式”（primary expression）。原始表达式是表达式的最小单位——它们不再包含其他表达式。JavaScript中的原始表达式包含常量或直接量、关键字和变量。

直接量是直接在程序中出现的常数值。它们看起来像：

```js
1.23 //数字直接量
"hello" //字符串直接量
/pattern/ //正则表达式直接量
```

JavaScript中的一些保留字构成了原始表达式：

```js
true //布尔值：真
false //假
null //返回一个值：空
this //返回"当前"对象
```

最后，第三种原始表达式是变量：

```js
i //返回变量i的值
sum //返回sum的值
undefined //是全局变量，和null不同，它不是一个关键字
```

当JavaScript代码中出现了标识符，JavaScript会将其当做变量而去查找它的值。如果变量名不存在，表达式运算结果为`undefined`。然而，在ECMAScript5的严格模式中，对不存在的变量进行求值会抛出一个引用错误异常。

## 4.2 对象和数组的初始化表达式

对象和数组初始化表达式实际上是一个新创建的对象和数组。这些初始化表达式有时称做“对象直接量”和“数组直接量”。然而和布尔直接量不同，它们不是原始表达式，因为它们所包含的成员或者元素都是子表达式。数组初始化表达式语法非常简单，我们以此开始。

数组初始化表达式是通过一对方括号和其内由逗号隔开的列表构成的。初始化的结果是一个新创建的数组。数组的元素是逗号分隔的表达式的值：

```js
[] //一个空数组；[]内留空即表示该数组没有任何元素
[1+2,3+4] //有两个元素的数组，第一个3，第二个是7
```

数组初始化表达式中的元素初始化表达式也可以是数组初始化表达式。也就是说，这些表达式是可以嵌套的：

```js
var mat = [[1,2,3],[4,5,6],[7,8,9]];
```

JavaScript对数组初始化表达式进行求值的时候，数组初始化表达式中的元素表达式也都会各自计算一次。也就是说，数组初始化表达式每次计算的值有可能是不同的。

数组直接量中的列表逗号之间的元素可以省略，这时省略的空位会填充值`undefined`。例如，下面这个数组包含5个元素，其中三个元素是`undefined`：

```js
var a=[1,,,,5]
```

数组直接量的元素列表结尾处可以留下单个逗号，这时并不会创建一个新的值为`undefined`的元素。

对象初始化表达式和数组初始化表达式非常类似，只是方括号被花括号代替，并且每个子表达式都包含一个属性名和一个冒号作为前缀：

```js
var p = {x: 2.1,y: -3} //一个拥有两个属性成员的对象
var q = {}; //空对象
q.x=2.1;q.y=-3;  //q的属性成员和p的一样
```

对象直接量也可以嵌套，比如：

```js
var anh = {
  left: { x:2, y:3 },
  right: { x:4, y:5 },
}
```

JavaScript求对象初始化表达式的值的时候，对象表达式也都会各自计算一次，并且它们不必包含常数值：它们可以是任意JavaScript表达式。同样，对象直接量中的属性名称可以是字符串而不是标识符（这在那些只能使用保留字或一些非法标识符作为属性名的地方非常有用）：

```js
var side = 1;
var square = {
  "left": { x:p.x, y:p.y },
  'right': { x:p.x+side, y:p.y+side }
}
```

## 4.3 函数定义表达式

函数定义表达式定义一个JavaScript函数。表达式的值是这个新定义的函数。从某种意义上讲，函数定义表达式可称为“函数直接量”，毕竟对象初始化表达式也称为“对象直接量”。一个典型的函数定义表达式包含关键字function，跟随其后的是一对圆括号，括号内是一个以逗号分割的列表，列表含有0个或多个标识符（参数名），然后再跟随一个由花括号包裹的JavaScript代码段（函数体），例如：

```js
// 这个函数返回传入参数值的平方
var square = function(x){ return x*x};
```

函数定义表达式同样包含函数的名字。函数也可以通过函数语句来定义，而不是函数表达式。

## 4.4 属性访问表达式

属性访问表达式运算得到一个对象属性或一个数组元素的值。JavaScript为属性访问定义了两种语法：

```js
expression . indentifier
expression [expression]
```

第一种写法是一个表达式后跟随一个句点和标识符。表达式指定对象，标识符指定需要访问的属性的名称。第二种写法是使用方括号，方括号内是另外一个表达式（这种方法适用于对象和数组）。第二个表达式指定要访问的属性的名称或者代表要访问数组元素的索引。这里有一些具体的例子：

```js
var o = { x: 1, y: {z: 3}};
var a = [0, 4, [5, 6]];
o.x  // =>1：表达式o的x属性
o.y.z  // =>3：表达式o.y的z属性
o.["x"]  // =>1：对象o的x属性
a[1]   // =>4：表达式a索引为1的元素
a[2]["1"] // =>6：表达式a[2]中索引为1的元素
a[0].x  // =>1: 表达式a[0]的x属性
```

不管使用哪种形式的属性访问表达式，在“.”和“[”之前的表达式总是会首先计算。如果计算结果是`null`或者`undefined`，表达式会抛出一个类型错误异常，因为这两个值都不能包含任意属性。如果运算结果不是对象（或者数组）， JavaScript 会将其转换为对象。如果对象表达式后跟随句点和标识符，则会查找由这个标识符所指定的属性的值，并将其作为整个表达式的值返回。如果对象表达式后跟随一对方括号，则会计算方括号内的表达式的值并将它转换为字符串。无论哪种情况，如果命名的属性不存在，那么整个属性访问表达式的值就是`undefined`。

显然`.identifier`的写法更加简单，但需要注意的是，这种方式只适用于要访问的属性名称是合法的标识符，并且需要知道要访问的属性的名字。如果属性名称是一个保留字或者包含空格和标点符号，或是一个数字（对于数组来说），则必须使用方括号的写法。当属性名是通过运算得出的值而不是固定的值的时候，这时必须使用方括号写法。

## 4.5 调用表达式

JavaScript中的调用表达式（invocation expression）是一种调用（或者执行）函数或方法的语法表示。它以一个函数表达式开始，这个函数表达式指代了要调用的函数。函数表达式后跟随一对圆括号，括号内是一个以逗号隔开的参数列表，参数可以有0个也可有多个，例如：

```js
f(0)  // f是一个函数表达式：0是一个参数表达式。
Math.max(x,y,z)  // Math.max是一个函数；x,y和z是参数
a.sort()  // a.sort是一个函数，它没有参数。
```

当对调用表达式进行求值的时候，首先计算函数表达式，然后计算参数表达式，得到一组参数值。如果函数表达式的值不是一个可调用的对象，则抛出一个类型错误异常（所有的函数都是可调用的，即使宿主对象不是函数它也有可能被调用。然后，实参的值被依次赋值给形参，这些形参是定义函数时指定的，接下来开始执行函数体。如果函数使用`return`语句给出一个返回值，那么这个返回值就是整个调用表达式的值。否则，调用表达式的值就是`undefined`。

任何一个调用表达式都包含一对圆括号和左圆括号之前的表达式。如果这个表达式是一个属性访问表达式，那么这个调用称做“方法调用”（method invocation）。在方法调用中，执行函数体的时候，作为属性访问主题的对象和数组便是其调用方法内`this`的指向。这种特性使得在面向对象编程范例中，函数（其OO名称为“方法”）可以调用其宿主对象。

并不是方法调用的调用表达式通常使用全局对象作为`this`关键字的值。然而在ECMAScript 5中，那些通过严格模式定义的函数在调用时将使用`undefined`作为`this`的值，`this`不会指向全局对象。

## 4.6 对象创建表达式

对象创建表达式（object creation expression）创建一个对象并调用一个函数（这个函数称做构造函数）初始化新对象的属性。对象创建表达式和函数调用表达式非常类似，只是对象创建表达式之前多了一个关键字new：

```js
new Object()
new Point(2,3)
```

如果一个对象创建表达式不需要传入任何参数给构造函数的话，那么这对空圆括号是可以省略掉的：

```js
new Object
new Point
```

当计算一个对象创建表达式的值时，和对象初始化表达式通过`{}`创建对象的做法一样，JavaScript首先创建一个新的空对象，然后，JavaScript通过传入指定的参数并将这个新对象当做`this`的值来调用一个指定的函数。这个函数可以使用`this`来初始化这个新创建对象的属性。那些被当成构造函数的函数不会返回一个值，并且这个新创建并被初始化后的对象就是整个对象创建表达式的值。如果一个构造函数确实返回了一个对象值，那么这个对象就作为整个对象创建表达式的值，而新创建的对象就废弃了。

## 4.7 运算符概述

JavaScript中的运算符用于算术表达式、比较表达式、逻辑表达式、赋值表达式等。表4-1简单列出了JavaScript中的运算符，作为一个方便的参照。

需要注意的是，大多数运算符都是由标点符号表示的，比如“+”和“=”。而另外一些运算符则是由关键字表示的，比如`delete`和`instanceof`。关键字运算符和标点符号所表示的运算符一样都是正规的运算符，它们的语法都非常言简意赅。

表4-1是按照运算符的优先级排序的，前面的运算符优先级要高于后面的运算符优先级。被水平分割线分隔开来的运算符具有不同的优先级。标题为A的列表示运算符的结合性，L（从左至右）或R（从右至左），标题为N的列表示操作数的个数。标题为“类型”的列表示期望的操作数类型，以及运算符的结果类型（在“→”符号之后）。

### 4.7.1 操作数的个数

运算符可以根据其操作数的个数进行分类。JavaScript中的大多数运算符（比如“*”乘法运算符）是一个二元运算符（binary operator），将两个表达式合并成一个稍复杂的表达式。换言之，它们的操作数均是两个。

JavaScript同样支持一些一元运算符（unary operator），它们将一个表达式转换为另一个稍复杂的表达式。表达式`-x`中的“-”运算符就是一个一元运算符，是将操作数x求负值。最后，JavaScript支持一个三元运算符（ternary operator），条件判断运算符“?:”，它将三个表达式合并成一个表达式。

### 4.7.2 操作数类型和结果类型

一些运算符可以作用于任何数据类型，但仍然希望它们的操作数是指定类型的数据，并且大多数运算符返回（或计算出）一个特定类型的值。

JavaScript运算符通常会根据需要对操作数进行类型转换。乘法运算符`*`希望操作数为数字，但表达式`"3"*"5"`却是合法的，因为JavaScript会将操作数转换为数字。这个表达式的值是数字15，而不是字符串“15”。之前也提到过，JavaScript中的所有值不是真值就是假值，因此对于那些希望操作数是布尔类型的操作符来说，它们的操作数可以是任意类型。

有一些运算符对操作数类型有着不同程度的依赖。最明显的例子是加法运算符，“+”运算符可以对数字进行加法运算，也可以对字符串作连接。同样，比如“<”比较运算符可以根据操作数类型的不同对数字进行大小值的比较，也可以比较字符在字母表中的次序先后。单个运算符的描述充分解释了它们对类型有着怎样的依赖以及对操作数进行怎样的类型转换。

### 4.7.3 左值

左值（lvalue）是一个古老的术语，它是指“表达式只能出现在赋值运算符的左侧”。在JavaScript中，变量、对象属性和数组元素均是左值。ECMAScript规范允许内置函数返回一个左值，但自定义的函数则不能返回左值。

### 4.7.4 运算符的副作用

计算一个简单的表达式（比如`2*3`）不会对程序的运行状态造成任何影响，程序后续执行的计算也不会受到该计算的影响。而有一些表达式则具有很多副作用，前后的表达式运算会相互影响。赋值运算符是最明显的一个例子：如果给一个变量或属性赋值，那么那些使用这个变量或属性的表达式的值都会发生改变。“++”和“--”递增和递减运算符与此类似，因为它们包含隐式的赋值。`delete`运算符同样有副作用：删除一个属性就像（但不完全一样）给这个属性赋值`undefined`。

其他的JavaScript运算符都没有副作用，但函数调用表达式和对象创建表达式有些特别，在函数体或者构造函数内部运用了这些运算符并产生了副作用的时候，我们说函数调用表达式和对象创建表达式是有副作用的。

### 4.7.5 运算符优先级

表4-1中所示的运算符是按照优先级从高到低排序的，每个水平分割线内的一组运算符具有相同的优先级。运算符优先级控制着运算符的执行顺序。优先级高的运算符（表格的顶部）的执行总是先于优先级低（表格的底部）的运算符。

看一下下面这个表达式：

```js
w = x + y * z;
```

乘法运算符“*”比加法运算符“+”具有更高的优先级，所以乘法先执行，加法后执行。然后，由于赋值运算符“=”具有最低的优先级，因此赋值操作是在右侧的表达式计算出结果后进行的。运算符的优先级可以通过显式使用圆括号来重写。

为了让加法先执行，乘法后执行，可以这样写：

```js
w = (x + y) * z;
```

需要注意的是，属性访问表达式和调用表达式的优先级要比表中的所有运算符都要高。

```js
typeof my.Function[x](y)
```

尽管`typeof`是优先级最高的运算符之一，但`typeof`也是在两次属性访问和函数调用之后执行的。

实际上，如果真的不确定你所使用的运算符的优先级，最简单的方法就是使用圆括号来强行指定运算次序。有些重要规则需要熟记：乘法和除法的优先级高于加法和减法，赋值运算的优先级非常低，通常总是最后执行的。

### 4.7.6 运算符的结合性

在表4-1中标题为A的列说明了运算符的结合性。L指从左至右结合，R指从右至左结合。结合性指定了在多个具有同样优先级的运算符表达式中的运算顺序。从左至右是指运算的执行是按照由左到右的顺序进行。例如，减法运算符具有从左至右的结合性，因此：

```js
w = x - y - z
// 和这段代码一样：
w = ((x - y) - z)

// 反过来讲，下面这个表达式：
x = ~-y;
w = x = y = z;
q = a ? b : c ? d : e ? f : g;
// 和这段代码一模一样
x =~ (-y);
w = ( x = ( y = z ));
q = a ? b : (c ? d : (e ? f : g))
```

因为一元操作符、赋值和三元运算符都具有从右至左的结合性。

### 4.7.7 运算顺序

运算符的优先级和结合性规定了它们在复杂的表达式中的运算顺序，但并没有规定子表达式的计算过程中的运算顺序。JavaScript总是严格按照从左至右的顺序来计算表达式。例如，在表达式`w=x+y*z`中，将首先计算子表达式w，然后计算x、y和z，然后，y的值和z的值相乘，再加上x的值，最后将其赋值给表达式w所指代的变量或属性。给表达式添加圆括号将会改变乘法、加法和赋值运算的关系，但从左至右的顺序是不会改变的。

只有在任何一个表达式具有副作用而影响到其他表达式的时候，其求值顺序才会和看上去有所不同。如果表达式x中的一个变量自增1，这个变量在表达式z中使用，那么实际上是先计算出了x的值再计算z的值，这一点非常重要。

## 4.8 算术表达式

基本的算术运算符是`*`（乘法）、`/`（除法）、`%`（求余）、`+`（加法）和`-`（减法）。我们会在随后有专门一节讲述“+”运算符。剩下的4个运算符非常简单，只是在必要的时候将操作数转换为数字而已，然后求积、商、余数和差。所有那些无法转换为数字的操作数都转换为`NaN`值。如果操作数（或者转换结果）是`NaN`值，算术运算的结果也是`NaN`。

运算符“/”用第二个操作数来除第一个操作数，如果你使用过那些区分整型和浮点型数字的编程语言，那么当用一个整数除以另一个整数时，则希望得到的结果也是整数。但在JavaScript中，所有的数字都是浮点型的，除法运算的结果也是浮点型，比如，`5/2`的结果是2.5，而不是2。除数为0的运算结果为正无穷大或负无穷大，而`0/0`的结果是`NaN`，所有这些运算均不会报错。

运算符“%”计算的是第一个操作数对第二个操作数的模。换句话说，就是第一个操作数除以第二个操作数的余数。结果的符号和第一个操作数（被除数）的符号保持一致。例如，`5%2`结果是1，`-5%2`的结果是-1。

求余运算符的操作数通常都是整数，但也适用于浮点数，比如，`6.5%2.1`结果是0.2。

### 4.8.1 “+”运算符

二元加法运算符“+”可以对两个数字做加法，也可以做字符串连接操作：

```js
1+2  // => 3
"hello" + "" + "there"  // =>"hello there"
"1"+"2"  // =>"12"
```

当两个操作数都是数字或都是字符串的时候，计算结果是显而易见的。然而对于其他情况来说，则要进行一些必要的类型转换，并且运算符的行为依赖于类型转换的结果。加号的转换规则优先考虑字符串连接，如果其中一个操作数是字符串或者转换为字符串的对象，另外一个操作数将会转换为字符串，加法将进行字符串的连接操作。如果两个操作数都不是类字符串（string-like）的，那么都将进行算术加法运算。

从技术上讲，加法操作符的行为表现为：

- 如果其中一个操作数是对象，则对象会遵循对象到原始值的转换规则转换为原始类值：日期对象通过`toString()`方法执行转换，其他对象则通过`valueOf()`方法执行转换（如果`valueOf()`方法返回一个原始值的话）。由于多数对象都不具备可用的`valueOf()`方法，因此它们会通过`toString()`方法来执行转换。

- 在进行了对象到原始值的转换后，如果其中一个操作数是字符串的话，另一个操作数也会转换为字符串，然后进行字符串连接。

- 否则，两个操作数都将转换为数字（或者NaN），然后进行加法操作。

这里有一些例子：

```js
1 + 2  // =>3：加法
"1" + "2"  // =>"12"：字符串连接
"1" + 2  // =>"12"：数字转换为字符串后进行字符串连接
1 + {}  // =>"1[object object]":对象转换为字符串后进行字符串连接
true + true  // =>2：布尔值转换为数字后做加法
2 + null  // =>2：null转换为0后做加法
2 + undefined  // =>NaN：undefined转换为NaN做加法
```

最后，需要特别注意的是，当加号运算符和字符串和数字一起使用时，需要考虑加法的结合性的对运算顺序的影响。也就是说，运算结果是依赖于运算符的运算顺序的，比如：

```js
1 + 2 + " blind mice"  // => "3 blind mice"
1 + (2 + " blind mice")  // => "12 blind mice"
```

### 4.8.2 一元算术运算符

一元运算符作用于一个单独的操作数，并产生一个新值。在JavaScript中，一元运算符具有很高的优先级，而且都是右结合（right-associative）。本节将讲述一元算术运算符（+、-、++和--），必要时，它们会将操作数转换为数字。需要注意的是，“+”和“-”是一元运算符，也是二元运算符。

下面介绍一元算术运算符：

**一元加法(+)**

一元加法运算符把操作数转换为数字（或者`NaN`），并返回这个转换后的数字。如果操作数本身就是数字，则直接返回这个数字。

**一元减法（-）**

当“-”用做一元运算符时，它会根据需要把操作数转换为数字，然后改变运算结果的符号。

**递增（++）**

递增“++”运算符对其操作数进行增量（加一）操作，操作数是一个左值（lvalue）（变量、数组元素或对象属性）。运算符将操作数转换为数字，然后给数字加1，并将加1后的数值重新赋值给变量、数组元素或者对象属性。递增“++”运算符的返回值依赖于它相对于操作数的位置。当运算符在操作数之前，称为“前增量”（pre-increment）运算符，它对操作数进行增量计算，并返回计算后的值。当运算符在操作数之后，称为“后增量”（post-increment）运算符，它对操作数进行增量计算，但返回未做增量计算的（unincremented）值。思考一下如下两行代码之间的区别：

```js
var i = 1, j = ++i  // i和j的值都是2
var i = 1, j = i++;  // i是2，j是1
```

需要注意的是，表达式`++x`并不总和`x=x+1`完全一样，“++”运算符从不进行字符串连接操作，它总是会将操作数转换为数字并增1。如果x是字符串“1”，`++x`的结果就是数字2，而`x+1`是字符串“11”。

同样需要注意的是，由于JavaScript会自动进行分号补全，因此不能在后增量运算符和操作数之间插入换行符。如果插入了换行符，JavaScript将会把操作数当做一条单独的语句，并在其之前补上一个分号。

不管是前增量还是后增量，这个运算符通常用在for循环中，用于控制循环内的计数器。

**递减（--）**

递减“-”运算符的操作数也是一个左值。它把操作数转换为数字，然后减1，并将计算后的值重新赋值给操作数。和“++”运算符一样，递减“--”运算符的返回值依赖于它相对操作数的位置，当递减运算符在操作数之前，操作数减1并返回减1之后的值。当递减运算符在操作数之后，操作数减1并返回减1之前的值。当递减运算符在操作符的右侧时，运算符和操作数之间不能有换行符。

### 4.8.3 位运算符

位运算符可以对由数字表示的二进制数据进行更低层级的按位运算。尽管它们并不是传统的数学运算，但这里也将其归类为算术运算符，因为它们作用于数值类型的操作数并返回数字。这些运算符在JavaScript编程中并不常用。这里的4个运算符都是对操作数的每个位进行布尔运算，这里将操作数的每个位当做布尔值（1=true，0=false），其他三个位运算符用来进行左移位和右移位。

位运算符要求它的操作数是整数，这些整数表示为32位整型而不是64位浮点型。必要时，位运算符首先将操作数转换为数字，并将数字强制表示为32位整型，这会忽略原格式中的小数部分和任何超过32位的二进制位。移位运算符要求右操作数在0～31之间。在将其操作数转换为无符号32位整数后，它们将舍弃第5位之后的二进制位，以便生成一个位数正确的数字。需要注意的是，位运算符会将`NaN`、`Infinity`和`-Infinity`都转换为0。

**按位与（&）**

位运算符“&”对它的整型操作数逐位执行布尔与（AND）操作。只有两个操作数中相对应的位都是1，结果中的这一位才是1。例如，0x1234 & 0x00FF = 0x0034。

**按位或（|）**

位运算符“|”对它的整型操作数逐位执行布尔或（OR）操作。如果其中一个操作数相应的位为1，或者两个操作数相应位都是1，那么结果中的这一位就为1。例如：0x1234 | 0x00FF = 0x12FF。

**按位异或（^）**

位运算符“|”对它的整型操作数逐位执行布尔异或（XOR）操作。异或是指第一个操作数为true或第二个操作数为true，但两者不能同时为true。如果两个操作数中只有一个相应位为1（不能同时为1），那么结果中的这一位就是1。例如，0xFF00 ^ 0xF0F0 = 0x0FF0。

**按位非（～）**

运算符“～”是一元运算符，位于一个整型参数之前，它将操作数的所有位取反。根据JavaScript中带符号的整数的表示方法，对一个值使用“～”运算符相当于改变它的符号并减1。例如，～0x0F = 0xFFFFFFF0或-16。

**左移（<<）**

将第一个操作数的所有二进制位进行左移操作，移动的位数由第二个操作数指定，移动的位数是0～31之间的一个整数。例如，在表达式a<<1中，a的第一位变成了第二位，a的第二位变成了它的第三位，以此类推。新的第一位用0来补充，舍弃第32位。将一个值左移1位相当于它乘以2，左移两位相当于乘以4，以此类推。例如，7<<2=28。

**带符号右移（>>）**

运算符“>>”将第一个操作数的所有位进行右移操作，移动的位数由第二个操作数指定，移动的位数是0～31之间的一个整数。右边溢出的位将忽略。填补在左边的位由原操作数的符号决定，以便保持结果的符号与原操作数一致。如果第一个操作数是正数，移位后用0填补最高位；如果第一个操作数是负的，移位后就用1填补高位。将一个值右移1位，相当于用它除以2（忽略余数），右移两位，相当于它除以4，以此类推，例如，7>>1=3，-7>>1=-4。

**无符号右移（>>>）**

运算符“>>>”和运算符“>>”一样，只是左边的高位总是填补0，与原来的操作数符号无关，例如，-1>>4=-1，但是-1>>>4=0x0FFFFFFF。

## 4.9 关系表达式

关系运算符用于测试两个值之间的关系（比如“相等”、“小于”，或“是...的属性”），根据关系是否存在而返回 true 或 false。关系表达式总是返回一个布尔值，通常在 if 、 while 或者 for 语句中使用关系表达式，用以控制程序的执行流程。

### 4.9.1 相等和不等运算符

“==”和“===”运算符用于比较两个值是否相等，当然它们对相等的定义不尽相同。两个运算符允许任意类型的操作数，如果操作数相等则返回true，否则返回false。“===”也称为严格相等运算符（strict equality）（有时也称做恒等运算符（identity operator）），它用来检测两个操作数是否严格相等。“==”运算符称做相等运算符（equality operator），它用来检测两个操作数是否相等，这里“相等”的定义非常宽松，可以允许进行类型转换。

JavaScript支持“=”、“==”和“===”运算符。应该把“=”称做“得到或赋值”，把“==”称做“相等”，把“===”称做“严格相等”。

“!=”和“!==”运算符的检测规则是“==”和“===”运算符的求反。如果两个值通过“==”的比较结果为true，那么通过“!=”的比较结果则为false。如果两值通过“===”的比较结果为true，那么通过“!==”的比较结果则为false。“！”运算符是布尔非运算符。我们只要记住“!=”称做“不相等”、“!==”称做“不严格相等”就可以了。

JavaScript对象的比较是引用的比较，而不是值的比较。对象和其本身是相等的，但和其他任何对象都不相等。如果两个不同的对象具有相同数量的属性，相同的属性名和值，它们依然是不相等的。相应位置的数组元素是相等的两个数组也是不相等的。

严格相等运算符“===”首先计算其操作数的值，然后比较这两个值，比较过程没有任何类型转换：

- 如果两个值类型不相同，则它们不相等。
- 如果两个值都是`null`或者都是`undefined`，则它们相等。
- 如果两个值都是布尔值true或都是布尔值false，则它们相等。
- 如果其中一个值是`NaN`，或者两个值都是`NaN`，则它们不相等。`NaN`和其他任何值都是不相等的，包括它本身！
- 如果两个值为数字且数值相等，则它们相等。如果一个值为0，另一个值为-0，则它们同样相等。
- 如果两个值为字符串，且所含的对应位上的16位数完全相等，则它们相等。如果它们的长度或内容不同，则它们不等。两个字符串可能含义完全一样且所显示出的字符也一样，但具有不同编码的16位值。JavaScript并不对Unicode进行标准化的转换，因此像这样的字符串通过“===”和“==”运算符的比较结果也不相等。第三部分的`String.localeCompare()`提供了另外一种比较字符串的方法。
- 如果两个引用值指向同一个对象、数组或函数，则它们是相等的。如果指向不同的对象，则它们是不等的，尽管两个对象具有完全一样的属性。

相等运算符"=="和恒等运算符相似，但相等运算符比较并不严格。如果两个数不是同一类型，那么相等运算符会尝试进行一些类型转换，然后进行比较:

- 如果两个操作类型相同，则和上文相等运算符的比较规则一样。如果严格相等，那么比较结果相等。如果他们不严格相等，则比较结果不相等。
- 如果两个操作类型不同，“==”相等操作符也会认为它们相等。检测相等会遵循如下的规则和类型转换：

  - 如果一个类型是`null`，令一个是`undefined`,则它们相等。
  - 如果一个值是数字，另一个是字符串，先将字符串转换为数字，然后使用转换后的值进行比较。
  - 如果一个值是true,则将其转换为1再进行比较，如果一个值是false,则转换为0比较。
  - 如果一个值是对象，另一个值是数字或字符串，则使用3章8节3小节的方法的转换规则将对象转换为原始值，然后进行比较。对象通过`toString()`方法或者`valueOf()`方法转换为原始值。javascript语言核心的内置类首先尝试使用`valueOf()`再尝试使用`toString()`，除了日期类，日期类只能通过`toString()`转换。那些不是 JavaScript语言核心中的对象则通过实现中定义的方法转换为原始值。
  - 其它不同类型之间的比较均不相等

### 4.9.2 比较运算符

比较运算符用来检测两个操作数的大小关系（数值大小或者字母表的顺序）：

小于（<）  
如果第一个操作数小于第二个操作数，则“<”运算符的计算结果为true；否则为false。

大于（>）  
如果第一个操作数大于第二个操作数，则“>”运算符的计算结果为true；否则为false。

小于等于(<=)  
如果第一个操作数小于或者等于第二个操作数，则“<=”运算符的计算结果为true；否则为false。

大于等于(>=)   
如果第一个操作数大于或者等于第二个操作数，则“>=”运算符的计算结果为false；否则为false。

比较操作符的操作数可能是任意类型。然而，只有数字和字符串才能真正执行比较操作，因此那些不是数字和字符串的操作数都将进行类型转换，类型转换规则如下：

- 如果操作数为对象，那么这个对象将依照3.8.3节结尾处所描述的转换规则转换为原始值：如果`valueOf()`返回一个原始值，那么直接使用这个原始值。否则，使用`toString()`的转换结果进行比较操作。

- 在对象转换为原始值之后，如果两个操作数都是字符串，那么将依照字母表的顺序对两个字符串进行比较，这里提到的“字母表顺序”是指组成这个字符串的16位Unicode字符的索引顺序。

- 在对象转换为原始值之后，如果至少有一个操作数不是字符串，那么两个操作数都将转换为数字进行数值比较。0和-0是相等的。`Infinity`比其他任何数字都大（除了`Infinity`本身），`-Infinity`比其他任何数字都小（除了它自身）。如果其中一个操作数是（或转换后是）`NaN`，那么比较操作符总是返回`false`。

需要注意的是，JavaScript字符串是一个由16位整数值组成的序列，字符串的比较也只是两个字符串中的字符的数值比较。由Unicode定义的字符编码顺序和任何特定语言或者本地语言字符集中的传统字符编码顺序不尽相同。注意，字符串比较是区分大小写的，所有的大写的ASCII字母都“小于”小写的ASCII字母。如果不注意这条不起眼的规则的话会造成一些小麻烦。比如，使用“<”小于运算符比较“Zoo”和“aardvark”，结果为true。

参照`String.localCompare()`方法来获取更多字符串比较的相关信息，`String.localCompare()`方法更加健壮可靠，这个方法参照本地语言的字母表定义的字符次序。对于那些不区分字母大小写的比较来说，则需要首先将字符串转全部换为小写字母或者大写字母，通过`String.toLowerCase()`和`String.toUpperCase()`做大小写的转换。

对于数字和字符串操作符来说，加号运算符和比较运算符的行为都有所不同，前者更偏爱字符串，如果它的其中一个操作数是字符串的话，则进行字符串连接操作。而比较运算符则更偏爱数字，只有在两个操作数都是字符串的时候，才会进行字符串的比较：

```js
1 + 2  // =>3 加法，结果为3
"1" + "2"  // 字符串连接，结果为"12"
"1" + 2  // 字符串连接，2转换为"2",结果"12"
11 < 3  // 数字比较，结果true
"11" < "3"  // 字符串比较，结果为true
"11" < 3  // 数字的比较，“11”转换为11，结果为false
"one" < 3  // 数字比较，"one"转换为NaN，结果为false
```

最后，需要注意的是，“<=”（小于等于）和“>=”（大于等于）运算符在判断相等的时候，并不依赖于相等运算符和严格相等运算符的比较规则。相反，小于等于运算符只是简单的“不大于”，大于等于运算符也只是“不小于”。只有一个例外，那就是当其一个操作数是（或者转换后是）`NaN`的时候，所有4个比较运算符均返回false。

### 4.9.3 in运算符

in运算符希望它的左操作数是一个字符串或可以转换为字符串，希望它的右操作数是一个对象。如果右侧的对象拥有一个名为左操作数值的属性名，那么表达式返回true，例如：

```js
var point = {
  x: 1,
  y: 1
}  // 定义一个对象
"x" in point  // =>true 对象有一个名为x的属性
"z" in point  // =>false 对象无名为z的属性
"toString" in point  // =>true 对象继承了toString方法

var data = [7, 8, 8]
"0" in data  // =>true 数组包含0
1 in data  // =>true 数字转换为字符串
3 in data  // =>fase 没有索引为3的元素
```
### 4.9.4 instanceof运算符

instanceof运算符希望左操作数是一个对象，右操作数标识对象的类。如果左侧的对象是右侧类的实例，则表达式返回true；否则返回false。第9章将会讲到，JavaScript中对象的类是通过初始化它们的构造函数来定义的。这样的话，instanceof的右操作数应当是一个函数。比如：

```js
var d = new Date();  // 构造一个新对象
d instanceof Date;  // 计算结果为true：d是Date()创建的
d instanceof Object  // 计算结果为true：所有的对象都是Object的实例
d instanceof Number  // 计算结果为false：d不是一个Number对象

var a = [1,2,3]  // 数组直接量创建数组
a instanceof Array  // 计算结果为true：a为数组
a instanceof Object  // 计算结果为true：所有的数组都是对象
a instanceof RegExp  // 计算结果为fasle：数组不是正则表达式
```

需要注意的是，所有的对象都是Object的实例。当通过instanceof判断一个对象是否是一个类的实例的时候，这个判断也会包含对“父类”（superclass）的检测。如果instanceof的左操作数不是对象的话，instanceof返回false。如果右操作数不是函数，则抛出一个类型错误异常。

为了理解instanceof运算符是如何工作的，必须首先理解“原型链”（prototype chain）。原型链作为JavaScript的继承机制。

## 4.10 逻辑表达式

逻辑运算符“&&”、“||”和“!”是对操作数进行布尔算术运算，经常和关系运算符一起配合使用，逻辑运算符将多个关系表达式组合起来组成一个更复杂的表达式。

### 4.10.1 逻辑与`&&`

“&&”运算符可以从三个不同的层次进行理解。最简单的第一层理解是，当操作数都是布尔值的时候，“&&”对两个值执行布尔与（AND）操作，只有在第一个操作数和第二个操作数都是true的时候，它才返回true。如果其中一个操作数是false，它返回false。

“&&”常用来连接两个关系表达式：

```js
x == 0 && y == 0; //只有在x和y都是0时，才返回true
```

关系表达式的运算结果总是为true或false，因此当这样使用的时候，“&&”运算符本身也返回true或false。关系运算符的优先级比“&&”（和“||”）要高，因此类似这种表达式可以放心地书写，而不用补充圆括号。

但是“&&”的操作数并不一定是布尔值。（假值是false、null、undefined、0、-0、NaN和""，所有其他的值包括所有对象都是真值）。对“&&”的第二层理解是，“&&”可以对真值和假值进行布尔与（AND）操作。如果两个操作数都是真值，那么返回一个真值；否则，至少一个操作数是假值的话，则返回一个假值。在JavaScript中任何希望使用布尔值的地方，表达式和语句都会将其当做真值或假值来对待，因此实际上“&&”并不总是返回true和false，但也并无大碍。

需要注意的是，上文提到了运算符返回一个“真值”或者“假值”，但并没有说明这个“真值”或者“假值”到底是什么值。为此，我们深入讨论对“&&”的第三层（也是最后一层）理解。运算符首先计算左操作数的值，即首先计算“&&”左侧的表达式。如果计算结果是假值，那么整个表达式的结果一定也是假值，因此“&&”这时简单地返回左操作数的值，而并不会对右操作数进行计算。

```js
var o = {
  x: 1
};
var p = null;
o && o.x;  // =>1 : 1:0是真值，因此返回值是o.x
p && p.x  // => null : p是假值，因此将其返回，而并不计算p.x
```

“&&”的行为有时称做“短路”（short circuiting），我们也会经常看到很多代码利用了这一特性来有条件地执行代码。例如，下面两行JavaScript代码是完全等价的：

```js
if (a == b) stop();  // 只有a==b时才能调运stop()
(a == b) && stop();  // 同上
```

尽管“&&”可以按照第二层和第三层的理解进行一些复杂表达式运算，但大多数情况下，“&&”仅用来对真值和假值做布尔计算。

### 4.10.2 逻辑或`||`

“||”运算符对两个操作数做布尔或（OR）运算。如果其中一个或者两个操作数是真值，它返回一个真值。如果两个操作数都是假值，它返回一个假值。

尽管“||”运算符大多数情况下只是做简单布尔或（OR）运算，和“&&”一样，它也具有一些更复杂的行为。它会首先计算第一个操作数的值，也就是说会首先计算左侧的表达式。如果计算结果为真值，那么返回这个真值。否则，再计算第二个操作数的值，即计算右侧的表达式，并返回这个表达式的计算结果。

和“&&”运算符一样，同样应当避免右操作数包含一些具有副作用的表达式，除非你目地明确地在右侧使用带副作用的表达式，而有可能不会计算右侧的表达式。

这个运算符最常用的方式是用来从一组备选表达式中选出第一个真值表达式：

```js
// 如果max_width已经定义了，直接使用它。
// 否则在preferences对象中查找max_width
// 如果没有定义它，则使用一个写死的常量。
var max =max_width || preferences.max_windth || 500;
```

这种贯用法通常在函数体内，用来给参数提供默认值。

```js
//将o成功的属性复制到p中，并返回p
function copy(o, p) {
  p = p || {}; //如果向参数p没有传入任何对象，则使用一个新创建对象。
  //函数体内的主逻辑
}
```

### 4.10.3 逻辑非`!`

“!”运算符是一元运算符。它放置在一个单独的操作数之前。它的目的是将操作数的布尔值进行求反。例如，如果x是真值，则!x返回false；如果x是假值，则!x返回true。

和“&&”与“||”运算符不同，“!”运算符首先将其操作数转换为布尔值，然后再对布尔值求反。也就是说“!”总是返回true或者false，并且，可以通过使用两次逻辑非运算来得到一个值的等价布尔值：`!!x`。

作为一个一元运算符，“!”具有很高的优先级，并且和操作数紧密绑定在一起。如果希望对类似`p && q`的表达式做求反操作，则需要使用圆括号：`!(p && q)`。

```js
// 对于p和q取任意值，这两个等式都永远成立
!(p && q) === !p || !q  
!(p || q) === !p && !q  
```

## 4.11 赋值表达式

JavaScript 使用“=”运算符来给变量或者属性赋值。例如：

```js
i = 0  // 将变量i设置为0
o.x = 1  // 将对象o的属性x 设置为1
```

“=”运算符希望它的左操作数是一个左值：一个变量或者对象属性（或数组元素）。它的右操作数可以是任意类型的任意值。赋值表达式的值就是右操作数的值。赋值表达式的副作用是，右操作数的值赋值给左侧的变量或对象属性，这样的话，后续对这个变量和对象属性的引用都将得到这个值。

尽管赋值表达式通常非常简单，但有时仍会看到一些复杂表达式包含赋值表达式的情况。例如，可以将赋值和检测操作放在一个表达式中，就像这样：

```js
(a = b) == 0
```

需要注意的是，“=”具有非常低的优先级，通常在一个较长的表达式中用到了一条赋值语句的值的时候，需要补充圆括号以保证正确的运算顺序。

赋值操作符的结合性是从右至左，也就是说，如果一个表达式中出现了多个赋值运算符，运算顺序是从右到左。因此，可以通过如下的方式来对多个变量赋值：

```js
i=j=k=0; //把三个变量初始化为0
```

**带操作的赋值运算**

除了常规的赋值运算“=”之外，JavaScript还支持许多其他的赋值运算符，这些运算符将赋值运算符和其他运算符连接起来，提供一种更为快捷的运算方式。例如，运算符“+=”执行的是加法运算和赋值操作，下面的表达式：

```js
total += salaes_tax;

// 和下面的表达式等价的
total = total + salaes_tax
```

运算符“+=”可以作用于数字或字符串，如果其操作数是数字，它将执行加法运算和赋值操作；如果操作数是字符串，它就执行字符串连接操作和赋值操作。

这类运算符还包括“-=”、“*=”、“&=”等。表4-2列出了这一类的所有运算符。


| 运算符 | 示例  | 等价于  |
|--------|--------|---------|
| `+=`   | a+=b   | a=a+b   |
| `-=`   | a-=b   | a=a-b   |
| `*=`   | a*=b   | a=a*b   |
| `/=`   | a/=b   | a=a/b   |
| `%=`   | a%=b   | a=a%b   |
| `<<=`  | a<<=b  | a=a<<b  |
| `>>=`  | a>>=b  | a=a>>b  |
| `>>>=` | a>>>=b | a=a>>>b |
| `&=`   | a&=b   | a=a&b   |
| \|=    | a\|=b  | a=a\|b  |
| `^= `  | a^=b   | a=a^b   |


大多数情况下，表达式为`a op =b`。这里的op代表一个运算符，这个表达式等价于
`a =a op b`。

在第一行中，表达式a计算了一次，在第二行中，表达式a计算了两次。

只有 a 包含具有副作用的表达式（比如函数调用和赋值操作）的时候，两者才不等价。如下两个表达式不等价

```js
data[i++] *= 2;
data[i++] = data[i++] * 2
```

## 4.12 表达式计算

和其他很多解释性语言一样，JavaScript同样可以解释运行由JavaScript源代码组成的字符串，并产生一个值。JavaScript通过全局函数eval()来完成这个工作：

```js
eval("3+2")  // =>5
```

动态判断源代码中的字符串是一种强大的语言特性，几乎没有必要在实际中应用。如果你使用了`eval()`，你应当仔细考虑是否真的需要使用它。

下面讲解`eval()`的基础用法，并且介绍严格使用它的两种方法，从代码优化的角度讲，这两种方法对于原有代码造成的影响是最小的。

`eval()`是一个函数，但由于它已经被当成运算符来对待了，因此将它放在本章来讲述。一般来讲，如果一个函数调用了`eval()`，那么解释器将无法对这个函数做进一步优化。而将`eval()`定义为函数的另一个问题是，它可以被赋予其他的名字。如果允许这种情况的话，那么解释器将无法放心地优化任何调用的函数。而当eval是一个运算符（并作为一个保留字）的时候，这种问题就可以避免掉。

### 4.12.1 eval()

`eval()`只有一个参数，如果传入的参数不是字符串，它直接返回这个参数。如果参数是字符串，它会把字符串当成 JavaScript t进行编译(parse)，如果编译失败则抛出一个语法错误(SyntaxError)。如果编译成功，则开始执行这段代码，并返回字符串中最后一个表达式或语句的值，如果最后一个表达式没有语句或者值，则最终返回`undefined`。如果字符串抛出一个异常，这个异常把该调用的传给`eval()`。

关于`eval()`最重要的是，它使用了调用它的变量作用域环境，也就是说，它查找变量的值和定义新变量和函数的操作和局部的代码作用域中的代码一样。如果一个函数定义了一个局部变量x,然后调用了eval("x"),它会返回局部变量的值。如果它调用eval("x=1"),它会改变局部变量的值。如果函数调用了eval("var y=3;")它声明一个新的局部变量y。同样的，一个函数可以通过如下代码声明一个局部函数：

```js
eval("function f(){return x+1;}");
```

如果最顶层的代码中调用了`eval()`。当然它会作用于全局变量和全局函数。

需要注意的是，传递给`eval()`的字符串必须在语法上讲得通——不能通过`eval()`往函数中任意粘贴代码片段，比如，`eval("return; ")`是没有意义的，因为 return 只有在函数中才起作用，并且事实上，eval 的字符串执行时的上下文环境和调用函数的上下文环境是一样的，这不能使其作为函数的一部分来运行。如果字符串作为一个单独的脚本是由语义的，那么将其传递给`eval()`作参数是完全没有问题的，否则，`eval()`将抛出语法错误异常。

### 4.12.2 全局eval()

`eval()`具有改变局部变量的能力，这对javascript优化器来说，是一个很大的问题，然而作为一种权宜之计，javascript征对那行调用了`eval()`函数所做的优化并不多。但当脚本定义了一个别名，并且用令一个名称来调用它，javascript解释器又如何工作呢，为了javascript解释器更加简化。ECMAScipt3标准规定了任何解释器都不允许对`eval()`赋予别名。如果`eval()`使用别的别名来调用的话，则会抛出EvalError异常。

实际上，大多数的实现并不是这样做的。当通过别名调用时，`eval()`会将其字符串当成顶层的全局代码来执行。执行代码可能会定义新的全局变量和全局函数。执行的代码可能会定义新的全局变量和全局函数，或者给全局变量赋值。但却不能修改或修改主调函数中的局部变量，因此这不会影响到函数内的代码优化。

ECMAScript5是反对使用EvalError的，并且规范了`eval()`的行为。“直接的eval”，当直接使用非限定的“eval”名称，来调用`eval()`函数时，它总共是在它的上下文作用域内执行。其它间接调用则使用全局函数为其上下文作用域。并且无法读、写、定义局部变量和函数。下面有一段代码实例：

```js
var geval = eval; //使用别名调用eval将是全局eval
var x = "global",
  y = "global"; //两个全局变量
function f() { //函数内执行的局部eval
  var x = "local" //定于局部变量
  eval("x += 'changed';"); //直接eval更改了局部变量的
  return x; //返回更改后的局部变量
}

function g() { //这个函数执行了全局eval
  var y = "local" //定义了局部变量
  geval("y += 'changed';"); //间接改变了局部变量的值
  return y; //返回未更改的局部变量
}
console.log(f(), x); //更改了局部变量，输出local changed global
console.log(g(), y); //更改了全局变量，输出local globalchanged
```

我们注意到，全局eval的这些行为不仅仅是出于代码优化器的需要而做出的一种折中方案，它实际上是一种非常有用的特性，它允许我们执行那些对上下文没有任何依赖的全局脚本代码段。我们在本节开始处也提到，真正需要eval来执行代码段的场景并不多见。但当你真的意识到它的必要性时，你更可能会使用全局eval而不是局部eval。

IE 9之前的早期版本IE和其他浏览器有所不同，当通过别名调用`eval()`时并不是全局`eval()`（它也不会抛出一个EvalError异常，仅仅将其当做局部eval来调用）。但IE的确定义了一个名叫`execScript()`的全局函数来完成全局eval的功能（但和`eval()`稍有不同，`execScript()`总是会返回null）。

### 4.12.3 严格eval()

ECMAScript 5严格模式对`eval()`函数的行为施加了更多的限制，甚至对标识符eval的使用也施加了限制。当在严格模式下调用`eval()`时，或者`eval()`执行的代码段以“use strict”指令开始，这里的`eval()`是私有上下文环境中的局部eval。也就是说，在严格模式下，eval执行的代码段可以查询或更改局部变量，但不能在局部作用域中定义新的变量或函数。此外，严格模式将“eval”列为保留字，这让`eval()`更像一个运算符。不能用一个别名覆盖`eval()`函数。并且变量名、函数名、函数参数或者异常捕获的参数都不能取名为“eval”。

## 4.13 其他运算符

JavaScript 支持很多其他各种各样的运算符。

### 4.13.1 条件运算符（?:）

条件运算符是JavaScript中唯一的一个三元运算符（三个操作数），有时直接称做“三元运算符”。通常这个运算符写成“?:”，当然在代码中往往不会这么简写，因为这个运算符拥有三个操作数，第一个操作数在“?”之前，第二个操作数在“?”和“:”之间，第三个操作数在“:”之后，例如：

```js
x > 0 ? x : -x;  // 求x的绝对值
```

条件运算符的操作数可以是任意类型。第一个操作数当成布尔值，如果它是真值，那么将计算第二个操作数，并返回其计算结果。否则，如果第一个操作数是假值，那么将计算第三个操作数，并返回其计算结果。第二个和第三个操作数总是会计算其中之一，不可能两者同时执行。

其实使用 if 语句也会带来同样的效果，“?:”运算符只是提供了一种简写形式。这里是一个“?:”的典型应用场景，判断一个变量是否有定义（并拥有一个有意义的真值），如果有定义则使用它，如果无定义则使用一个默认值：

```js
grett = "hello" + (username ? username : "there");
```

和以下的代码是等价的，但上面的更加简洁

```js
grett = "hello";
if (username)
  grett += username;
else
  grett += "there";
```

### 4.13.2 typeof运算符

typeof是一元运算符，放在单个操作数前面，操作数可以是任何类型，返回值表示操作类型的一个字符串。

| x | typeof x |
|---|---|
| undefined | "undefined" |
| null | "object" |
| ture或false | "boolean" |
| 任意数字或NaN | "number" |
| 任意字符串 | "String" |
| 任意函数 | "function" |
| 任意内置对象（非函数） | "object" |
| 任意宿主对象 | 由编译器各自实现的字符串，但不是"undefined" "boolean" "number" "string" |

typeof最常用的用法写在表达式中们就像这样

```js
(typeof value == "string") ? "'" + value + "'" : value;
```

typeof运算符同样在swith语句中非常有用，需要注意的是，typeof运算可以带上园括号。这样让typeof看起来像一个函数名，而不是一个运算关键字：

```js
typeof(i)
```

我们注意到，当操作数是null的时候，typeof将返回"object"。如果想将null和对象区分开，则必须针对特殊值显式检测。对于宿主对象来说，typeof有可能并不返回“object”，而返回字符串。但实际上客户端JavaScript中的大多数宿主对象都是“object”类型。

由于所有对象和数组的typeof运算结果是“object”而不是“function”，因此它对于区分对象和其他原始值来说是很有帮助的。如果想区分对象的类，则需要使用其他的手段，比如使用instanceof运算符、class特性以及constructor属性。

尽管JavaScript中的函数是对象的一种，但typeof运算符还是将函数特殊对待，对函数做typeof运算有着特殊的返回值。在JavaScript中，函数和“可执行的对象”（callable object）有着微妙的区别。所有的函数都是可执行的（callable），但是对象也有可能是可执行的，可以像调用函数一样调用它，但它并不是一个真正的函数。

根据ECMAScript 3规范，对于所有内置可执行对象，typeof运算符一律返回“function”。ECMAScript 5规范则扩充至所有可执行对象，包括内置对象（native object）和宿主对象（host object），所有可执行对象进行typeof运算都将返回“function”。大多数浏览器厂商也将JavaScript的原生函数对象（native function object）当成它们的宿主对象的方法来使用。但微软却一直将非原生可执行对象（non-native callable object）当成其客户端的方法来使用，在IE 9之前的版本中，非原生可执行对象的typeof运算将返回“object”，尽管它们的行为和函数非常相似。而在IE 9中，这些客户端方法是真正的内置函数对象（native function object）。

### 4.13.3 delete运算符

delete是一元操作符，它用来删除对象的属性或者数组的元素。就像赋值、递增、递减运算符一样。delete也是具有副作用的。它是用来做删除操作的。不是用来返回一个值的。

```js
var o = {
    x: 1,
    y: 2
}
delete o.x;
"x" in o;  // => false

var a = [1, 2, 3];
delete a[2]; 
2 in a;  // => false
a.length;  // =>3
```

注意，数组长度并没有改变，尽管上一行删除了这个元素，但删除操作留下了一个洞。实际上并没有修改数组的长度，因此a的长度仍然为3。

需要注意的是，删除属性或删除数组元素不仅仅设置了一个undefined值，当删除一个属性时，这个属性不复存在。读取一个不存在的值将会返回undefined，但是可以通过 in 运算符来检测这个属性是否在对象中存在。

delete希望他的操作数是一个左值，如果它不是左值，那么delete将不进行任何操作同时返回true。否则，delete将试图删除这个指定的左值。如果删除成功，delete将返回true。然而并不是所有的属性都可删除，一些内置核心和客户端属性是不能删除的，用户通过var语句声明的变量不能删除。同样，通过function语句定义的函数和函数参数也不能删除。

在ECMAScript 5严格模式中，如果delete的操作数是非法的，比如变量、函数或函数参数，delete操作将抛出一个语法错误（SyntaxError）异常，只有操作数是一个属性访问表达式的时候它才会正常工作。在严格模式下，delete删除不可配置的属性时会抛出一个类型错误异常。在非严格模式下，这些delete操作都不会报错，只是简单地返回false，以表明操作数不能执行删除操作。

这里有一些关于delete运算符的例子：

```js
var o = {x: 1,y: 2};
delete o.x;  // 删除一个对象属性，返回true
typeof o.x;  // 属性不存在，返回"undefined"
delete o.x;  // 删除不存在的属性，返回true;
delete o;  // 不能删除通过var关键字声明的变量，返回false
delete 1;  // 参数不是一个左值。
this.x = 1;  // 给全局定义一个属性，这里没有使用var
delete x ;  // 试图删除它，在非严格模式下返回true
            // 在严格模式下回抛出异常，这时使用"delete this.x"来代替
x;        // 运行时出错，没有定义x
```

### 4.13.4 void运算符

void是一元运算符，它出现在操作数之前，操作数可以是任意类型。这个运算符并不是经常使用：操作数会照常计算，但忽略计算结果并返回undefined。由于void会忽略操作数的值，因此在操作数具有副作用的时候使用void来让程序更具语义。

这个运算符最常用在客户端的URL——javascript:URL中，在URL中可以写带有副作用的表达式，而void则让浏览器不必显示这个表达式的计算结果。例如，经常在HTML代码中的``<a>``标签里使用void运算符：

```js
<a href="javascript:void window.open();">new</a>
```

通过给`<a>`的onclick绑定一个事件处理程序要比在href中写“javascript:URL”要更加清晰，当然，这样的话void操作符就可有可无了。

### 4.13.5 逗号运算符(,)

逗号运算符是二元运算符，它的操作数可以是任意类型。它首先计算左操作数，然后计算右操作数，最后返回右操作数的值，看下面的示例代码：

```js
i = 0, j = 1, k = 2;
```

它和下面的代码基本上等价的

```js
i = 0; j = 1; k = 2;
```

总是会计算左侧的表达式，但计算结果忽略掉，也就是说，只有左侧表达式具有副作用，才会使用逗号运算让代码变得更通畅。逗号运算符最常用的场景是for循环中，这个for循环通常有多个循环变量。

```js
// for循环中的第一个逗号是var语句的一部分
// 第二个逗号是逗号运算符
// 它将两个表达式(i++和j--)放在一条(for循环中)语句中
for (var i = 0, j = 10; i < j; i++, j--);
console.log(i + j);
```

# 第5章 语句

表达式在 JavaScript 中是短语，那么语句（statement）就是 JavaScript 整句或没那个令。正如英文是用句号作结尾来分割语句， JavaScript 语句是以分号结束。表达式计算出一个值，但语句用来执行以使某件事发生。

“使某件事发生”的一个方法是计算带有副作用的表达式。诸如赋值和函数调用这些有副作用的表达式，是可以作为单独的语句的，这种把表达式当作语句的用法也称作表达式语句（expression statement）。类似的语句还有声明语句（declaration statement），声明语句用来声明新变量或定义新函数。

JavaScript 程序无非就是一系列可执行语句的集合。默认情况下， JavaScript 解释器依照语句的编写顺序依次执行。另一种“使某件事发生”的方法是改变语句的默认执行顺序。 JavaScript 中有很多语句和控制结构（control structure）来改变语句的默认执行顺序：

- 条件（conditional）语句，JavaScript解释器可以根据一个表达式的值来判断是执行还是跳过这些语句，如if语句和switch语句。
- 循环（loop）语句，可以重复执行语句，如while和for语句。
- 跳转（jump）语句，可以让解释器跳转至程序的其他部分继续执行，如break、return和throw语句。

## 5.1 表达式语句

具有副作用的表达式是 JavaScript 中最简单的语句。这类语句已经在第四章讲诉了。赋值语句是一类比较重要的表达式语句，例如：

```js
greet = "hello" + name;
i *= 3;
```

增值运算符`++`和递减运算符`--`和赋值语句有关。它们的作用是改变一个变量的值，就像执行一条赋值语句一样：

```js
counter++;    
```

delete运算符的重要作用就是删除一个对象的属性（或数组的元素），所有它一般作为语句使用，而不是作为复杂表达式的一部分。

```js
delete o.x;
```

函数调用是表达式语句的另外一个大类，例如

```js
alert(greet);
window.close();
```

虽然这些客户端函数都是表达式，但它们对web浏览器造成了一定的影响。所以我们认为也是语句，调用一个没有副作用的函数是没有意义的，除非它是复杂的表达式或赋值语句的一部分，例如。不可能随便把一个余弦值丢弃；

```js
Math.cos(x);
```

相反，得出余弦值就得把它赋值给一个变量，以便将来使用这个值：

```js
var cx = Math.cos(x);
```

再次提醒，每行代码就是以分号结束的。

## 5.2 复合语句和空语句

可以用逗号运算符将几个表达式连接在一起，形成一个表达式。同样，javascript还可以讲多条语句联合在一起，形成一个复合语句（compound statement）。只需花括号将多条语句括起来即可。因此，下面几行代码可以当成一条单独的语句，使用在javascript任何希望使用一条语句的地方。

```js
{
  x = Math.PI;
  cx = Math.cos(x);
  console.log("cos(π)=" + cx);
}
```

关于语句块有几点需要注意：
- 第一，语句块不需要分号。块中的元素语句必须以分号结尾，但语句块不需要。
- 第二，语句块中的行都有缩进，这不是必须的，但整齐的缩进能使代码可读性更强，更容易理解。
- 第三，javascript没有块级作用域，在语句块中声明的变量并不是语句块所私有的。

将很多条语句合并成一个大语句块的做法在javascript编程中非常常见。类似的表达式通常包含子表达式一样，很多javascript包含其它子语句，从形式来讲，javascript通常允许一个语句块包含一条子语句。例如：while循环的循环体就可以只包含一条语句。使用语句块，可以将任意数量的语句放到这个块中，这个语句块可以当做一条语句来使用。

在javascript中，当希望多条语句被当做一条语句使用时，使用符合语句来替代。空语句(empty statement)则恰好相反，它允许包含0条语句。空语句如下所示：

```js
;//分号
```

javascript解释器在执行空语句时显然不执行任何动作，但实践证明：当创建一个具有空循环体的循环时，空语句有时是很有用的，例如下面的for循环

```js
//初始化一个数组a
for (i = 0; i < a.length; a[i++] = 0);
```

在这个循环中，所有的操作都在表达`式a[i++]=0`中完成，这里并不需要任何循环体。然而javascript需要循环体中至少包含一条语句，因此这里只使用了一个单独的分号来表示一条空语句。

注意，在for循环、while循环或if语句的右边园括号的分号很不起眼，这很可能造成 一些致命的bug，而这些bug很难定位到。例如下面的代码的执行结果很可能就是作者不想要的效果：

```js
if((a==0)||(b==0)); //这一行代码什么也没做....
o = null; //这一行代码总会执行
```

如果有特殊目的使用空语句，最好在代码中添加注释，这样能更清楚的说明这条空语句是有用的

```js
for (i = 0; i < a.length; a[i++] = 0) /*empty*/;
```

## 5.3 声明语句

var 和 function 都是声明语句，它们声明或定义变量或函数。这些语句定义标识符（变量名和函数名）并给其复制，这些标识符可以在程序中任意地方使用。声明语句本身什么也不做，但它有一个重要的意义，通过创建变量和函数，可以更好地组织代码的语义。

### 5.3.1 var

var 语句用来声明一个或多个变量，它的语法如下：

```js
var name_1[ = value_1][, ..., name_n[ = value_n]]
```

关键字 var 之后跟随的是要声明的变量列表，列表中的每一个变量都可以带有初始化表达式，用于指定它的初始值，例如：

```js
var i;  // 一个简单的变量
var j = 0;  // 一个带有初始值的变量
var p, q;  // 两个变量
var greet = "hello" + name;  // 更复杂的初始化表达式
var x = 2.34,y = Math.cos(0.75),r, theta;  // 很多变量
var x = 2,y = x * x;  // 第二个变量使用了第一个变量
var x = 2,
    f = function(x) {return x * x},  // 每个变量都独占一行
    y = f(x)
```

如果var语句出现在函数体内，那么它定义的是一个局部变量，其作用域就是这个函数。如果在顶层代码中使用var语句，它声明的是全局变量，在整个JavaScript程序中都是可见的。正如在3.10.2节提到的，全局变量是全局对象的属性。然而和其他全局对象属性不同的是，var声明的变量是无法通过delete删除的。

如果var语句中的变量没有指定初始化表达式，那么这个变量的值初始为undefined。变量在声明它们的脚本或函数中都是有定义的，变量声明语句会被“提前”至脚本或者函数的顶部。但是初始化的操作则还在原来var语句的位置执行，在声明语句之前变量的值是undefined。

需要注意的是，var语句同样可以作为for循环或者for/in循环的组成部分（和在循环之外声明的变量声明一样，这里声明的变量也会“提前”）。

```js
for (var i = 0; i < 10; i++) console.log(i);
for (var i = 0, j = 10; i < 10; i++, j--) console.log(i * j);
for (var i in o) console.log(i);
```

注意，多次声明同一个变量是无所谓的。

### 5.3.2 function

关键字function用来定义函数。在4.3节中我们已经见过函数定义表达式。函数定义也可以写成语句的形式。例如，下面示例代码中的两种定义写法：

```js
// 将表达式赋值给一个变量
var f = function f(x) { 
  return x + 1; 
} 
// 含有变量名的语句 
function f(x){ 
  return x + 1; 
} 
```

函数声明的语法如下：

```js
function funcname([arg1[, arg2[..., argn]]]) {
  statements
}
```

funcname是要声明的函数的名称的标识符。函数名之后的圆括号中是参数列表，参数之间使用逗号分隔。当调用函数时，这些标识符则指代传入函数的实参。

函数体是由JavaScript语句组成的，语句的数量不限，且用花括号括起来。在定义函数时，并不执行函数体内的语句，它和调用函数时待执行的新函数对象相关联。注意，function语句里的花括号是必需的，这和while循环和其他一些语句所使用的语句块是不同的，即使函数体只包含一条语句，仍然必须使用花括号将其括起来。

```js
function hyteus(x, y) {
    return Math.sqrt(x * x + y * y);
}

// 一个递归函数
function facial(n) { 
    if (n <= 1) return 1;
    return n * facial(n - 1);
}
```

函数声明语句通常出现在JavaScript代码的最顶层，也可以嵌套在其他函数体内。但在嵌套时，函数声明只能出现在所嵌套函数的顶部。也就是说，函数定义不能出现在if语句、while循环或其他任何语句中，正是由于函数声明位置的这种限制，ECMAScript标准规范并没有将函数声明归类为真正的语句。有一些JavaScript实现的确允许在出现语句的地方都可以进行函数声明，但是不同的实现在细节处理方式上有很大差别，因此将函数声明放在其他的语句内的做法并不具备可移植性。

尽管函数声明语句和函数定义表达式包含相同的函数名，但二者仍然不同。两种方式都创建了新的函数对象，但函数声明语句中的函数名是一个变量名，变量指向函数对象。

和通过var声明变量一样，函数定义语句中的函数被显式地“提前”到了脚本或函数的顶部。因此它们在整个脚本和函数内都是可见的。使用var的话，只有变量声明提前了——变量的初始化代码仍然在原来的位置。然而使用函数声明语句的话，函数名称和函数体均提前：脚本中的所有函数和函数中所有嵌套的函数都会在当前上下文中其他代码之前声明。也就是说，可以在声明一个JavaScript函数之前调用它。

和var语句一样，函数声明语句创建的变量也是无法删除的。但是这些变量不是只读的，变量值可以重写。

## 5.4 条件语句

条件语句是通过判断指定表达式的值来决定执行还是跳转某些语句。这些语句是代码的“决策点”，有时称为“分支”。如果说 JavaScript 解释器是按照代码的“路径”执行的，条件语句就是这条路径上的分叉点，程序执行到这里时必须选择其中一条路径继续执行。

### 5.4.1 if

if语句是一种基本的控制语句，它让JavaScript程序可以选择执行路径，更准确地说，就是有条件地执行语句，这种语句有两种形式，第一种是：

```js
if (expression)
  statement
```

在这种形式中，需要计算expression的值，如果计算结果是真值，那么就执行statement。如果expression的值是假值，那么就不执行statement。例如：

```js
if (username == null)  // 如果username是null或undefined
  username = "jack wong";  // 对其进行定义
```

同样地：

```js
// 如果username是null/undefined/false/0/""/NaN
// 那么给它赋一个新值
if (!username)  
  username = "jack wong";
```

需要注意的是，if语句中括住expression的圆括号在语法上是必需的。

JavaScript语法规定，if关键字和带圆括号的表达式之后必须跟随一条语句，但可以使用语句块将多条语句合并成一条。因此，if语句的形式如下所示：

```js
if (!address) {
  address = "";
  message = "please mailing address";
}
```

if语句的第二种形式引入了else从句，当expression的值是false的时候执行else中的逻辑。其语法如下：

```js
if (expression)
  statement1
else
  statement2
```

在这段代码中，当expression为真值时执行statement1，当expression为假值时执行statement2，例如：

```js
if (n == 1)
  console.log("You have 1 new message");
else
  console.log("You have" + n + "new message");
```

当在if/else语句中嵌套使用if语句时，必须注意确保else语句匹配正确的if语句。考虑如下代码：

```js
i = j = 1;
k = 2;
if (i == j)
  if (j == k)
    console.log("i equs k");
else
  console.log("i dosent equal j");  // 错误！！
```

在这个示例中，内层if语句构成了外层if语句所需要的子句。但是，if和else的匹配关系并不清晰（只有缩进给出了一些暗示），而且在这个例子中，缩进给出的暗示是错误的，因为JavaScript解释器将上述代码实际解释为：

```js
if (i == j) {
  if (j == k)
    console.log("i equs k");
  else
    console.log("i dosent equal j");
}
```

和大多数编程语言一样，JavaScript中的if、else匹配规则是，else总是和就近的if语句匹配。为了让这个例子可读性更强、更易理解、更方便维护和调试，应当适当地使用花括号：

```js
if (i == j) {
  if (j == k) {
    console.log("i equs k");
  } else {  // 花括号使代码的结果更清晰
    console.log("i dosent equal j");
  }
}
```

虽然这并不是本书中所使用的编码风格，但许多程序员都有将if和else语句主体用花括号括起来的习惯（就像在类似while循环这样的复合语句中一样），即便每条分支只有一条语句，但坚持这样做可以避免刚才这种程序歧义的问题。

### 5.4.2 else if

if/else语句通过判断一个表达式的计算结果来选择执行两条分支中的一条。但当代码中有多条分支的时候该怎么办呢？一种解决办法是使用else if语句。else if语句并不是真正的JavaScript语句，它只不过是多条if/else语句连在一起时的一种惯用写法。

```js
if (n == 1) {
  // 执行代码块 1
} else if (n == 2) {
  // 执行代码块2
} else if (n == 3) {
  // 执行代码块3
} else {
  // 之前的条件都为false，则执行代码块4
}
```

这种代码并没有什么特别之处，它由多条if语句组成，每条if语句的else从句又包含另外一条if语句。可以用if语句的嵌套形式来完成在语法上等价的代码，但与之相比，显然使用else if写法更清晰也更可取。

### 5.4.3 switch

if语句在程序执行过程中创建一条分支，并且可以使用else if来处理多条分支。然而，当所有的分支都依赖于同一个表达式的值时，else if并不是最佳解决方案。在这种情况下，重复计算多条if语句中的条件表达式是非常浪费的做法。switch语句正适合处理这种情况。关键字switch之后紧跟着圆括号括起来的一个表达式，随后是一对花括号括起来的代码块：

```js
switch (expression) {
  statements
}
```

然而，switch语句的完整语法要比这复杂一些。代码块中可以使用多个由case关键字标识的代码片段，case之后是一个表达式和一个冒号，case和标记语句很类似，只是这个标记语句并没有名字，它只和它后面的表达式关联在一起。当执行这条switch语句的时候，它首先计算expression的值，然后查找case子句中的表达式是否和expression的值相同（这里的“相同”是按照“===”运算符进行比较的）。如果找到匹配的case，那么将会执行这个case对应的代码块。如果找不到匹配的case，那么将会执行“default:”标签中的代码块。如果没有“default:”标签，switch语句将跳过它的所有代码块。

switch语句是非常容易引起混淆的。用例子来解释会比较清晰一些，下面的switch语句和方才展示的if/else语句是等价的：

```js
switch (n) {
  case 1:  // 如果n === 1，从这里开始
    // 执行代码块1
    break;
  case 2:
    // 执行代码块2
    break;
  case 3:
    // 执行代码块3
    break;
  default:
    // 执行代码块4
    break;
}
```

需要注意的是，在上面的代码中，在每一个case语句块的结尾处都使用了关键字break。break语句可以使解释器跳出switch语句或循环语句。在switch语句中，case只是指明了要执行的代码起点，但并没有指明终点。如果没有break语句，那么switch语句就会从与expression的值相匹配的case标签处的代码块开始执行，依次执行后续的语句，一直到整个switch代码块的结尾。这种由一个case标签执行到下一个case标签的代码逻辑是很少使用的，在大多数情况下，应该使用break语句来终止每个case语句块。当然，如果在函数中使用switch语句，可以使用return来代替break，return和break都用于终止switch语句，也会防止一个case语句块执行完后继续执行下一个case语句块。

下面的switch语句的例子更加贴近实战，它根据值的类型将该值转换为字符串：

```js
function convert(x) {
  switch (typeof x) {
    case 'number':  // 将数字转换为十六进制
      return x.toString(16);
    case 'string':
      return '"' + x + '"';  // 返回两段带双引号的字符串。
    default:  // 使用普通方法转换其它类型
      return String(x);
  }
}
```

注意，在上面两个例子中，case关键字后跟随的是数字和字符串直接量，在实际中这是switch语句最常见的用法，但是ECMAScript标准允许每个case关键字跟随任意的表达式。

switch语句首先计算switch关键字后的表达式，然后按照从上到下的顺序计算每个case后的表达式，直到执行到case的表达式的值与switch的表达式的值相等时为止。由于对每个case的匹配操作实际上是“===”恒等运算符比较，而不是“==”相等运算符比较，因此，表达式和case的匹配并不会做任何类型转换。

由于每次执行switch语句的时候，并不是所有的case表达式都能执行到，因此，应当避免使用带有副作用的case表达式，比如函数调用表达式和赋值表达式。最安全的做法就是在case表达式中使用常量表达式。

前面提到过，如果switch表达式与所有case表达式都不匹配，则执行标记为“default:”的语句块；如果没有“default:”标签，则switch的整个语句块都将跳过。我们注意到，在之前的例子中，“default:”标签都出现在switch的末尾，位于所有case标签之后。当然这是最合理也是最常用的写法，实际上，“default:”标签可以放置在switch语句内的任何地方。

## 5.5 循环

为了理解条件语句，可以在 JavaScript 中的代码想象成一条条的分支路径。循环语句（looping statement）就是程序路径的一个回路，可以让一部分代码重复执行。 JavaScript 中有四种循环语句：while、do/while、for 和 for/in。其中最常用的就是对数组元素的遍历。

### 5.5.1 while

if语句是一种基本的控制语句，用来选择执行程序的分支语句。和if一样，while语句也是一个基本循环语句，它的语法如下：

```js
while (expression)
  statement
```

在执行while语句之前，JavaScript解释器首先计算expression的值，如果它的值是假值，那么程序将跳过循环体中的逻辑statement转而执行程序中的下一条语句。反之，如果表达式expression是真值，JavaScript解释器将执行循环体内的逻辑，然后再次计算表达式expression的值，这种循环会一直继续下去，直到expression的值为假值为止。换一种说法就是当表达式expression是真值时则循环执行statement，注意，使用while（true）则会创建一个死循环。

通常来说，我们并不想让JavaScript反复执行同一操作。在几乎每一次循环中，都会有一个或多个变量随着循环的迭代而改变。正是由于改变了这些变量，因此每次循环执行的statement的操作也不尽相同。而且，如果改变的变量在expression中用到，那么每次循环表达式的值也不同。这一点非常重要，否则一个初始值为真值的表达式的值永远都是真值，循环也不会结束，下面这个示例所示的while循环输出0～9之间的值：

```js
var count = 0;
while (count < 10) {
  console.log(count);
  count++;
}
```

### 5.5.2 do/while

do/while循环和while循环非常相似，只不过它是在循环的尾部而不是顶部检测循环表达式，这就意味着循环体至少会执行一次。do/while循环的语法如下：

```js
do 
  statement 
while(expression);
```

do/while循环并不像while循环那么常用。这是因为在实践中那种想要循环至少一次的情况并不常见，下面是一个do/while循环的例子：

```js
function printArray(a) {
  var len = a.length,
    i = 0;
  if (len == 0)
    console.log("空数组");
  else
    do {
      console.log(a[i]);
    } while (++i < len);
}
```

在do/while循环和普通的while循环之间有两点语法方面的不同之处。首先，do循环要求必须使用关键字do来标识循环的开始，用while来标识循环的结尾并进入循环条件判断；其次，和while循环不同，do循环是用分号结尾的。如果while的循环体使用花括号括起来的话，则while循环也不用使用分号做结尾。

### 5.5.3 for

for语句提供了一种比while语句更加方便的循环控制结构。for语句对常用的循环模式做了一些简化。大部分的循环都具有特定的计数器变量。在循环开始之前要初始化这个变量，然后在每次循环执行之前都检测一下它的值。最后，计数器变量做自增操作，否则就在循环结束后、下一次判断循环条件前做修改。在这一类循环中，计数器的三个关键操作是初始化、检测和更新。for语句就将这三步操作明确声明为循环语法的一部分，各自使用一个表达式来表示。for语句的语法如下：

```js
for (initialize; test; increment)
  statement
```

initialize、test和increment三个表达式之间用分号分隔，它们分别负责初始化操作、循环条件判断和计数器变量的更新。将它们放在循环的第一行会更容易理解for循环正在做什么，而且也可以防止忘记初始化或者递增计数器变量。要解释for循环是如何工作的，最简单的方法莫过于列出一个与之等价的while循环

```js
initialize
while (test) {
  statement
  increment;
}
```

换句话说，initialize表达式只在循环开始之前执行一次。初始化表达式应当具有副作用（通常是一条赋值语句）。JavaScript同样允许初始化表达式中带有var变量声明语句，这样的话就可以同时声明并初始化一个计数变量。每次循环执行之前会执行test表达式，并判断表达式的结果来决定是否执行循环体，如果test计算结果为真值，则执行循环体中的statement。最后，执行increment表达式。同样，为了有用起见，这里的increment表达式也必须具有副作用。通常来讲，它不是一个赋值表达式就是一个由“++”或“--”运算符构成的表达式。在上文中的while循环的例子可以使用for循环来重写，这个循环同样输出数字0～9：

```js
for (var count = 0; count < 10; count++)
console.log(count)
```

当然，有些循环会比这些例子更加复杂，而且循环中的一次迭代会改变多个变量。在JavaScript中，这种情况则必须用到逗号运算符，它将初始化表达式和自增表达式合并入一个表达式中以用于for循环：

```js
var i, j;
for (i = 0, j = 10; i < 10; i++, j--)
  console.log(i * j);
```
到目前为止，在示例代码中的循环变量都是数字。当然数字是最常用的，但不是必需的。下面这段代码就使用for循环来遍历链表数据结构，并返回链表中的最后一个对象（也就是第一个不包含next属性的对象）：

```js
// 返回链表的最后一个节点对象
function tail(o) {  
  // 根据判断o.next是不是真值来执行遍历
  for (; o.next; o = o.next) /*empty*/  
    return o;
}
```

需要注意的是，这段代码不包含initialize表达式，for循环中那三个表达式中的任何一个都可以忽略，但是两个分号必不可少。如果省略test表达式，那么这将是一个死循环，同样，和while（true）类似，死循环的另外一种写法是for（;;）。

### 5.5.4 fon/in

for/in语句也使用for关键字，但它是和常规的for循环完全不同的一类循环。for/in循环语句的语法如下：

```js
for (variable in object)
  statement
```

variable通常是一个变量名，也可以是一个可以产生左值的表达式或者一个通过var语句声明的变量，总之必须是一个适用于赋值表达式左侧的值。object是一个表达式，这个表达式的计算结果是一个对象。同样，statement是一个语句或语句块，它构成了循环的主体。

使用for循环来遍历数组元素是非常简单的：

```js
var a = [1, 3, 5, "44"];
for (var i = 0; i < a.length; i++)  // i代表了数组元素的索引
  console.log(a[i])  // 输出每个数组的元素
```

而for/in循环则是用来更方便地遍历对象属性成员：

```js
for (var p in o)  // 将属性的名字赋值给变量p
  console.log(o[p]);  // 输出每一个属性的值
```

在执行for/in语句的过程中，JavaScript解释器首先计算object表达式。如果表达式为null或者undefined，JavaScirpt解释器将会跳过循环并执行后续的代码。如果表达式等于一个原始值，这个原始值将会转换为与之对应的包装对象（wrapper object）(见3.6节)。否则，expression本身已经是对象了。JavaScript会依次枚举对象的属性来执行循环。然而在每次循环之前，JavaScript都会先计算variable表达式的值，并将属性名（一个字符串）赋值给它。

需要注意的是，只要for/in循环中variable的值可以当做赋值表达式的左值，它可以是任意表达式。每次循环都会计算这个表达式，也就是说每次循环它计算的值有可能不同。例如，可以使用下面这段代码将所有对象属性复制至一个数组中：

```js
var o = {x: 1, y: 2, z: 3};
var a = [], i = 0;
for (a[i++] in o) /*empty*/;
console.log(a)  // => [ 'x', 'y', 'z' ]
```

JavaScript数组不过是一种特殊的对象，因此，for/in循环可以像枚举对象属性一样枚举数组索引。例如，在上面的代码之后加上这段代码就可以枚举数组的索引0、1、2：

```js
for(i in a)
  console.log(i)
```

其实，for/in循环并不会遍历对象的所有属性，只有“可枚举”（enumerable）的属性才会遍历到。由JavaScript语言核心所定义的内置方法就不是“可枚举的”。比如，所有的对象都有方法`toString()`，但for/in循环并不枚举toString这个属性。除了内置方法之外，还有很多内置对象的属性也是“不可枚举的”（nonenumerable）。而代码中定义的所有属性和方法都是可枚举的。对象可以继承其他对象的属性，那些继承的自定义属性也可以使用for/in枚举出来。

如果for/in的循环体删除了还未枚举的属性，那么这个属性将不会再枚举到。如果循环体定义了对象的新属性，这些属性通常也不会枚举到（然而，JavaScript的有些实现是可以枚举那些在循环体中增加的继承属性的）。

**属性枚举的顺序**

ECMAScript规范并没有指定for/in循环按照何种顺序来枚举对象属性。但实际上，主流浏览器厂商的JavaScript实现是按照属性定义的先后顺序来枚举简单对象的属性，先定义的属性先枚举。如果使用对象直接量的形式创建对象，则将按照直接量中属性的出现顺序枚举。有一些网站和JavaScript库是依赖于这种枚举顺序的，浏览器厂商不大可能会修改这个顺序。

上一段讨论了JavaScript解释器枚举“简单”对象一种交互的属性枚举顺序。在下列情况下，枚举的顺序取决于具体的实现（并且是非交互的）：

- 对象继承了可枚举属性；
- 对象具有整数数组索引的属性；
- 使用delete删除了对象已有的属性；
- 使用`Object.defineProperty()`或者类似的方法改变了对象的属性。

除了所有非继承的“自有”属性以外的继承属性都往往（但并不是所有的JavaScript实现都是如此）都是可枚举的，而且可以按照它们定义的顺序进行枚举。如果对象属性继承自多个“原型”（prototype），也就是说它的原型链上有多个对象，那么链上面的每一个原型对象的属性的遍历也是依照特定顺序执行的。JavaScript的一些（但不是全部）实现依照数字顺序来枚举数组属性，而不是某种特定的顺序。但当数组元素的索引是非数字或数组是稀疏数组（数组索引是不连续的）时它们则按照特定顺序枚举。

## 5.6 跳转

JavaScript 中另一类语句是跳转语句（jump statement）。从名称就可以看出，它使得 JavaScript 的执行可以从一个位置跳转到另一个位置。break 语句是跳转到循环或者其他语句的结束。continue 语句是终止本次循环的执行并开始下一次循环的执行。 JavaScript 中的语句可以命名或带有标签， break 和 continue 可以标识目标循环或者其他语句标签。

return 语句让解释器跳转函数体的执行，并提供本次调用的返回值。 throw 语句触发或者“抛出”一个异常，它是 try/catch/finally 语句一同使用的，这些语句指定了处理异常的代码逻辑。这是一种复杂的跳转语句，当抛出一个异常的时候，程序将跳转至最近的闭合异常处理程序，这个异常处理程序可以是在同一个函数中或者在更高层的调用栈中。

### 5.6.1 标签语句

语句是可以添加标签的，标签是由语句前的标识符和冒号组成：

```js
identifier: statement
```

通过给语句定义标签，就可以在程序的任何地方通过标签名引用这条语句。可以对任意语句定义标签，但是只有在标签语句里面才有用。通过给循环定义一个标签名，可以在循环体内部使用break和continue来退出循环或者直接跳转到下一个循环的开始。break和continue是JavaScript中唯一可以使用语句标签的语句。这里有一个例子，其中while循环定义了一个标签，continue语句使用了这个标签:

```js
mainloop: while (token != null) {
  // 忽略这里代码...
  continue mainloop;  // 跳转到下一次循环
  // 忽略这里的代码...
}
```

这里用做标签的identifier必须是一个合法的JavaScript标识符，而不能是一个保留字。标签的命名空间和变量或函数的命名空间是不同的，因此可以使用同一个标识符作为语句标签和作为变量名或函数名。语句标签只有在它所起作用的语句（当然也可以在它的子句中）内是有定义的。一个语句标签不能和它内部的语句标签重名，但在两个代码段不相互嵌套的情况下是可以出现同名的语句标签的。带有标签的语句还可以带有标签，也就是说，任何语句可以有很多个标签。

### 5.6.2 break语句

单独使用break语句的作用是立即退出最内层的循环或switch语句。它的语法如下：

```js
break;
```

由于它能够使循环和switch语句退出，因此这种形式的break只有出现在这类语句中才是合法的。

我们在switch语句的例子中已经见到过break语句。在循环中，不论出于什么原因，只要不想继续执行整个循环，就可以用break来提前退出。当循环终止条件非常复杂时，在函数体内使用break语句实现这些条件判断的做法要比直接在循环表达式中写出这个复杂终止条件的做法简单很多。下面的例子中的循环遍历整个数组元素来查找某个特定的值，当整个数组遍历完成后会正常退出循环，如果找到了需要查找的数组元素，则使用break语句退出循环：

```js
for (var i = 0; i < a.length; i++) {
  if (a[i] == target) break;
}
```

JavaScript中同样允许break关键字后面跟随一个语句标签（只有标识符，没有冒号）：

```js
break labelname;
```

当break和标签一块使用时，程序将跳转到这个标签所标识的语句块的结束，或者直接终止这个闭合语句块的执行。当没有任何闭合语句块指定了break所用的标签，这时会产生一个语法错误。当使用这种形式的break语句时，带标签的语句不需要是循环或者switch语句，因为break可以“跳出”任何闭合的语句块。这里的语句可以是由花括号括起来的一组语句，使用同一个标签来标识这一组语句。

在break关键字和labelname之间不能换行。因为JavaScript可以给语句自动补全省略掉的分号，如果break关键字和标签之间有换行，JavaScript解释器会认为你在使用break不带标签的最简形式，因此会在break后补充分号。

当你希望通过break来跳出非就近的循环体或者switch语句时，就会用到带标签的break语句。下面是示例代码：

```js
// 从某处获得一个二维数组
var matrix = getData(); 
// 将矩阵中所有元素进行求和
var sum = 0,
  success = false;
// 从签名处开始，以便在报错时推出程序。
compure_sum: if (matrix) {
  for (var x = 0; x < matrix.length; x++) {
    var row = matrix[x];
    if (!row) break compure_sum;
    for (var y = 0; y < row.length; y++) {
      var cell = row[y];
      if (isNaN(cell)) break compure_sum;
      sum += cell;
    }
  }
  success = true;
}
// break语句跳转至此
// 如果success =false条件到达这里，说明我们给出的矩阵中有错误
// 否则对矩阵中所有的元素进行求和
```

最后，需要注意的是，不管break语句带不带标签，它的控制权都无法越过函数的边界。比如，对于一条带标签的函数定义语句来说，不能从函数内部通过这个标签来跳转到函数外部。

### 5.6.3 continue语句

continue语句和break语句非常类似，但它不是退出循环，而是转而执行下一次循环。continue语句的语法和break语句语法一样简单：

```js
continue;
```

continue语句同样可以带有标签：

```js
continue lebname;
```

不管continue语句带不带标签，它只能在循环体内使用。在其他地方使用将会报语法错误。

当执行到continue语句的时候，当前的循环逻辑就终止了，随即执行下一次循环，在不同类型的循环中，continue的行为也有所区别：

- 在while循环中，在循环开始处指定的expression会重复检测，如果检测结果为true，循环体会从头开始执行。
- 在do/while循环中，程序的执行直接跳到循环结尾处，这时会重新判断循环条件，之后才会继续下一次循环。
- 在for循环中，首先计算自增表达式，然后再次检测test表达式，用以判断是否执行循环体。
- 在for/in循环中，循环开始遍历下一个属性名，这个属性名赋给了指定的变量。

需要注意continue语句在while和for循环中的区别，while循环直接进入下一轮的循环条件判断，但for循环首先计算其increment表达式，然后判断循环条件。之前的章节讨论了和while循环“等价”的for循环的行为。但由于continue在这两种循环中的行为表现不同，因此使用while循环不可能完美地模拟等价的for循环。

下面这段代码展示了不带标签的continue语句，当产生一个错误的时候跳过当前循环的后续逻辑：

```js
for (i = 0; i < data.length; i++) {
  if (!data[i]) continue;  // 不能处理undefined数据
  total += data[i];
}
```

和break语句类似，带标签的continue语句可以用在嵌套的循环中，用以跳出多层次嵌套的循环体逻辑。同样和break语句类似，在continue语句和labelname之间不能有换行。

### 5.6.4 return语句

回想一下，函数调用是一种表达式，而所有表达式都有值。函数中的return语句既是指定函数调用后的返回值。这里是return语句的语法：

```js
return expression;
```

return语句只能在函数体内出现，如果不是的话会报语法错误。当执行到return语句的时候，函数终止执行，并返回expression的值给调用程序。例如：

```js
// 一个包含return的语句函数
function square(x) {
  return x * x
} 
// 执行为16
square(4) 
```

如果没有return语句，则函数调用仅依次执行函数体内的每一条语句直到函数结束，最后返回调用程序。这种情况下，调用表达式的结果是undefined。return语句经常作为函数内的最后一条语句出现，但并不是说要一定放在函数最后，即使在执行return语句的时候还有很多后续代码没有执行到，这时函数也还会返回调用程序。

return语句可以单独使用而不必带有expression，这样的话函数也会向调用程序返回undefined。例如：

```js
function display_object(o) {
  //如果参数是null或者undefined则立即返回
  if (!o) return;
  //其它逻辑        
}
```

由于JavaScript可以自动插入分号，因此在return关键字和它后面的表达式之间不能有换行。

### 5.6.5 throw语句

所谓异常（exception）是当发生了某种异常情况或错误时产生的一个信号。抛出异常，就是用信号通知发生了错误或异常状况。捕获异常是指处理这个信号，即采取必要的手段从异常中恢复。在JavaScript中，当产生运行时错误或者程序使用throw语句时就会显式地抛出异常。使用try/catch/finally语句可以捕获异常，下一节会对它作详细介绍。

throw语句的语法如下：

```js
throw expression
```

expression的值可以是任意类型的。可以抛出一个代表错误码的数字，或者包含可读的错误消息的字符串。当JavaScript解释器抛出异常的时候通常采用Error类型和其子类型，当然也可以使用它们。一个Error对象有一个name属性表示错误类型，一个message属性用来存放传递给构造函数的字符串，在下面的例子中，当使用非法参数调用函数时就抛出一个Error对象：

```js
function factorial(x) {
  // 如果输入的参数是非法的，则抛出一个异常
  if (x < 0) throw new Error("x不能是负数");
  // 否则，计算出一个值，正常地返回它
  for (var f = 1; x > 1; f *= x, x--) /*empty*/;
  return f;
}
```

当抛出异常时，JavaScript解释器会立即停止当前正在执行的逻辑，并跳转至就近的异常处理程序。异常处理程序是用try/catch/finally语句的catch从句编写的，下一节会介绍它。如果抛出异常的代码块没有一条相关联的catch从句，解释器会检查更高层的闭合代码块，看它是否有相关联的异常处理程序。以此类推，直到找到一个异常处理程序为止。如果抛出异常的函数没有处理它的try/catch/finally语句，异常将向上传播到调用该函数的代码。这样的话，异常就会沿着JavaScript方法的词法结构和调用栈向上传播。如果没有找到任何异常处理程序，JavaScript将把异常当成程序错误来处理，并报告给用户。

### 5.6.5 try/catch/finally语句

try/catch/finally语句是JavaScript的异常处理机制。其中try从句定义了需要处理的异常所在的代码块。catch从句跟随在try从句之后，当try块内某处发生了异常时，调用catch内的代码逻辑。catch从句后跟随finally块，后者中放置清理代码，不管try块中是否产生异常，finally块内的逻辑总是会执行。尽管catch和finally都是可选的，但try从句需要至少二者之一与之组成完整的语句。try、catch和finally语句块都需要使用花括号括起来，这里的花括号是必需的，即使从句中只有一条语句也不能省略花括号。

下面的代码说明了try/catch/finally的语法和使用目的：

```js
try{
  // 通常来讲，这里的代码会从头执行到尾而不会产生任何问题，
  // 但有时会抛出一个异常，要么是由throw语句直接抛出异常
  // 要么通过调用一个方法间接抛出异常
}
catch(e){
  // 当且仅当try抛出了异常，才会执行这里的代码
  // 这里可以通过局部变量e来获得对Error对象或者抛出的其它值的引用
  // 这里的代码可以基于某种原因处理这个异常 ，也可以忽略这个异常。
  // 还可以通过throw语句重新抛出异常
}
finally{
  // 不管try语句块是否抛出看异常，这里的逻辑总会执行，终止try的语句块方式有：
  // 1）正常终止，执行完语句块的最后一条语句
  // 2）通过break，continue或return语句终止
  // 3）抛出一个异常，异常被catch从句捕获
  // 4）抛出一个异常，异常未被捕获，继续向上传播
}
```

我们注意到，关键字catch后跟随了一对圆括号，圆括号内是一个标识符。这个标识符和函数参数很像。当捕获一个异常时，把和这个异常相关的值（比如Error对象）赋值给这个参数。和普通的变量不同，这条catch子句中的标识符具有块级作用域，它只在catch语句块内有定义。

这里有一个关于try/catch语句更实际的例子，这里使用了前面章节中提到的`factorial()`方法，并使用客户端JavaScript方法`prompt()`和`alert()`来输入和输出：

```js
try {
  // 要求用户输入一个数字
  var n = Number(prompt("请输入一个正整数", ""));
  // 假设输入是合法的，计算这个阶乘
  var f = factorial(n);
  // 显示结果
  alert(n + "!=" + f);
} catch (ex) {
  // 如果输入不合法，将执行这里的逻辑
  document.write(ex);  // 告诉用户发送了什么。
}
```

这里的try/catch语句并不包含finally从句。尽管finally不像catch那样经常使用，但有时候它还是非常有用。然而，我们需要更详尽地解释它的行为。不管try语句块中的代码执行完成了多少，只要try语句中有一部分代码执行了，finally从句就会执行。它通常在try从句的代码后用于清理工作。

通常状况下，解释器执行到try块的尾部，然后开始执行finally中的逻辑，以便进行必要的清理工作。当由于return、continue或break语句使得解释器跳出try语句块时，解释器在执行新的目标代码之前先执行finally块中的逻辑。

如果在try中产生了异常，而且存在一条与之相关的catch从句来处理这个异常，解释器会首先执行catch中的逻辑，然后执行finally中的逻辑。如果不存在处理异常的局部catch从句，解释器会首先执行finally中的逻辑，然后向上传播这个异常，直到找到能处理这个异常的catch从句。

如果finally块使用了return、continue、break或者throw语句使程序发生跳转，或者通过调用了抛出异常的方法改变了程序执行流程，不管这个跳转使程序挂起还是继续执行，解释器都会将其忽略。例如，如果finally从句抛出一个异常，这个异常将替代正在抛出的异常。如果finally从句运行到了return语句，尽管已经抛出了异常且这个抛出的异常还没有处理，这个方法依然会正常返回。

```js
var foo = function() {
  try {
    // 抛出一个异常
  } finally {
    // 未处理异常直接返回，这里将正常返回
    return 1;  
  }
}
```

在没有catch从句的情况下try从句可以和finally从句一起使用。在这种情况下，finally块只包含清理代码，不管try块中是否有break、continue或return语句，这里的代码一定会执行，回想一下，我们无法完全精确地使用while循环来模拟for循环，因为continue语句在两个循环中的行为表现不一致。如果使用try/finally语句，就能使用while循环来正确模拟包含continue的for循环：

```js
// 模拟for(initialize; test; increment) body;
initialize;
while(test) {
  try { body; }
  finally { increment; }
}
```

然而需要注意的是，当body包含break语句时，while循环和for循环便有了更微妙的区别（造成了一次额外的自增运算），因此即便是用了finally从句，使用while来完全模拟for循环依然是不可能的。

## 5.7 其他语句类型

本节讨论剩余的三种 JavaScript 语句—— with、debugger 和 use strict。

### 5.7.1 with语句

3.10.3节讨论了作用域链（scope chain），一个可以按序检索的对象列表，通过它可以进行变量名解析。with语句用于临时扩展作用域链，它具有如下的语法：

```js
with (object)
statement
```

这条语句将object添加到作用域链的头部，然后执行statement，最后把作用域链恢复到原始状态。

在严格模式中（参照5.7.3节）是禁止使用with语句的，并且在非严格模式里也是不推荐使用with语句的，尽可能避免使用with语句。那些使用with语句的JavaScript代码非常难于优化，并且同没有使用with语句的代码相比，它运行得更慢。

在对象嵌套层次很深的时候通常会使用with语句来简化代码编写。例如，在客户端JavaScript中，可能会使用类似下面这种表达式来访问一个HTML表单中的元素：

```js
document.forms[0].address.value
```

如果这种表达式在代码中多次出现，则可以使用with语句将form对象添加至作用域链的顶层：

```js
with(document.forms[0]){
  // 直接访问表单元素
  name.value="";
  address.value="";
  email.value ="";
}
```

这种方法减少了大量的输入，不用再为每个属性名添加`document.forms[0]`前缀。这个对象临时挂载在作用域链上，当JavaScript需要解析诸如address的标识符时，就会自动在这个对象中查找。当然，不使用with语句的等价代码可以写成这样：

```js
var f = document.forms[0];
f.name.value = "";
f.adress.value = "";
f.email.value = "";
```

不要忘记，只有在查找标识符的时候才会用到作用域链，创建新的变量的时候不使用它，看一下下面这行代码：

```js
with(o) x = 1;
```

如果对象o有一个属性x，那么这行代码给这个属性赋值为1。但如果o中没有定义属性x，这段代码和不使用with语句的代码`x=1`是一模一样的。它给一个局部变量或者全局变量x赋值，或者创建全局对象的一个新属性。with语句提供了一种读取o的属性的快捷方式，但它并不能创建o的属性。

### 5.7.2 debugger语句

debugger语句通常什么也不做。然而，当调试程序可用并运行的时候，JavaScript解释器将会（非必需）以调式模式运行。实际上，这条语句用来产生一个断点（breakpoint），JavaScript代码的执行会停止在断点的位置，这时可以使用调试器输出变量的值、检查调用栈等。例如，假设由于调用函数`f()`的时候使用了未定义的参数，因此`f()`抛出一个异常，但无法定位到底是哪里抛出了异常。为了有助于调试这个问题，需要修改函数`f()`：

```js
function f(o){
  if (o === undefined) debugger;  // 这段代码用来临时调试
  console.log(1)   // 函数的其它部分
}
f();
```

这时，当调用`f()`的时候没有传入参数，程序将停止执行，这时可以通过调试器检测调用栈并找出错误产生的原因。

在ECMAScript 5中，debugger语句正式加入到这门语言里。但在相当长的一段时间里，主流浏览器厂商已经将其实现了。注意，可用的调试器是远远不够的，debugger语句不会启动调试器。但如果调试器已经在运行中，这条语句才会真正产生一个断点。例如，如果使用Firefox的调试扩展插件Firebug，则必须首先为待调试的网页启用Friebug，这样debugger语句才能正常工作。

### 5.7.3 “use strict”

“use strict”是ECMAScript 5引入的一条指令。指令不是语句（但非常接近于语句）。“use strict”指令和普通的语句之间有两个重要的区别：

- 它不包含任何语言的关键字，指令仅仅是一个包含一个特殊字符串直接量的表达式（可以是使用单引号也可以使用双引号），对于那些没有实现ECMAScript 5的JavaScript解释器来说，它只是一条没有副作用的表达式语句，它什么也没做。将来的ECMAScript标准希望将use用做关键字，这样就可以省略引号了。
- 它只能出现在脚本代码的开始或者函数体的开始、任何实体语句之前。但它不必一定出现在脚本的首行或函数体内的首行，因为“use strict”指令之后或之前都可能有其他字符串直接量表达式语句，并且JavaScript的具体实现可能将它们解析为解释器自有的指令。在脚本或者函数体内第一条常规语句之后字符串直接量表达式语句只当做普通的表达式语句对待；它们不会当做指令解析，它们也没有任何副作用。

使用“use strict”指令的目的是说明（脚本或函数中）后续的代码将会解析为严格代码（strict code）。如果顶层（不在任何函数内的）代码使用了“use strict”指令，那么它们就是严格代码。如果函数体定义所处的代码是严格代码或者函数体使用了“use strict”指令，那么函数体的代码也是严格代码。如果`eval()`调用时所处的代码是严格代码或者`eval()`要执行的字符串中使用了“scrict code”指令，则`eval()`内的代码是严格代码。

严格代码以严格模式执行。ECMAScript 5中的严格模式是该语言的一个受限制的子集，它修正了语言的重要缺陷，并提供健壮的查错功能和增强的安全机制。严格模式和非严格模式之间的区别如下（前三条尤为重要）：

- 在严格模式中禁止使用with语句。在严格模式中，所有的变量都要先声明，如果给一个未声明的变量、函数、函数数、catch从句参数或全局对象的属性赋值，将会抛出一个引用错误异常（在非严格模式中，这种隐式声明的全局变量的方法是给全局对象新添加一个新属性）。
- 在严格模式中，调用的函数（不是方法）中的一个this值是undefined。（在非严格模式中，调用的函数中的this值总是全局对象）。可以利用这种特性来判断JavaScript实现是否支持严格模式：`var hasStrictMode = (function() { "use strict"; return this === undefined }());`
- 同样，在严格模式中，当通过`call()`或`apply()`来调用函数时，其中的this值就是通过`call()`或`apply()`传入的第一个参数（在非严格模式中，null和undefined值被全局对象和转换为对象的非对象值所代替）。
- 在严格模式中，给只读属性赋值和给不可扩展的对象创建新成员都将抛出一个类型错误异常（在非严格模式中，这些操作只是简单地操作失败，不会报错）。
- 在严格模式中，传入`eval()`的代码不能在调用程序所在的上下文中声明变量或定义函数，而在非严格模式中是可以这样做的。相反，变量和函数的定义是在`eval()`创建的新作用域中，这个作用域在`eval()`返回时就弃用了。
- 在严格模式中，函数里的arguments对象拥有传入函数值的静态副本。在非严格模式中，arguments对象具有“魔术般”的行为，arguments里的数组元素和函数参数都是指向同一个值的引用。
- 在严格模式中，当delete运算符后跟随非法的标识符（比如变量、函数、函数参数）时，将会抛出一个语法错误异常（在非严格模式中，这种delete表达式什么也没做，并返回false）。
- 在严格模式中，试图删除一个不可配置的属性将抛出一个类型错误异常（在非严格模式中，delete表达式操作失败，并返回false）。
- 在严格模式中，在一个对象直接量中定义两个或多个同名属性将产生一个语法错误（在非严格模式中不会报错）。
- 在严格模式中，函数声明中存在两个或多个同名的参数将产生一个语法错误（在非严格模式中不会报错）。
- 在严格模式中是不允许使用八进制整数直接量（以0为前缀，而不是0x为前缀）的（在非严格模式中某些实现是允许八进制整数直接量的）。
- 在严格模式中，标识符eval和arguments当做关键字，它们的值是不能更改的。不能给这些标识符赋值，也不能把它们声明为变量、用做函数名、用做函数参数或用做catch块的标识符。
- 在严格模式中限制了对调用栈的检测能力，在严格模式的函数中，arguments. caller和arguments.callee都会抛出一个类型错误异常。严格模式的函数同样具有caller和arguments属性，当访问这两个属性时将抛出类型错误异常（有一些JavaScript的实现在非严格模式里定义了这些非标准的属性）。

## 5.8 Javascript语句小结

| 语句 | 语法 | 用途 |
|---|---|---|
| break | break[label]; | 退出最内侧循环或者退出switch语句，又或退出label指定的语句 |
| case | case expression： | 在switch语句标记一条语句 |
| continue | continue [label]; | 重新开始最内层的循环或从新开始label指定的循环 |
| debugger | debugger; | 断点器调试 |
| default | default; | 在switch标记默认语句 |
| do/while | do statement while(expression); | while循环的一种替代形式 |
| empty | ; | 什么都不做 |
| for | for(init;test;incr)statement | 一种简写的循环 |
| for/in | for(var in object)statement | 遍历一个对象属性 |
| function | function name([param[],...]){body} | 声明一个函数 |
| if/else | if (expr)statement1[else statement2] | 执行statement1或者statement2 |
| label | label:statement | 给statement指定一个名字：label |
| return | return [expression]; | 从函数返回一个值 |
| switch | switch(expression){statements} | 用case或者“default：”语句标记多个分支语句 |
| throw | throw expression | 抛出异常 |
| try | try {statements} [catch {hander satements}] [finally {cleanup satements}] | 捕获异常 |
| use strict  | "use strict" | 对脚本和函数使用严格模式 |
| var | avr name=[=expr][,...] | 声明并初始化一个或多个变量 |
| while | while (expression) statement | 基本的循环结构 |
| with | with(object) statement | 扩展作用域链（不赞成使用） |

# 第6章 对象

对象是 JavaScript 的基本数据类型。对象是一种复合值：它将很多值（原始值或者其他对象）聚合在一起，可通过名字访问这些值。对象也可看作是属性的无序集合，每个属性都是一个名/值对。属性名是字符串，因此可以把对象看成是从字符串到值的映射。这种基本数据类型还有很多种叫法，有些我们已然非常熟悉，比如“散列”（hash）、“散列表”（hashtable）、“字典”（dictionary）、“关联数组”（associative array）。然而对象不仅仅是字符串到值的映射，除了可以保持自有的属性， JavaScript 对象还可以从一个称为原型的对象继承属性。对象的方法通常是继承的属性。这种“原型式继承”（prototypal inheritance）是JavaScript的核心特征。

JavaScript 对象是动态的——可以新增属性也可以删除属性——但它们常用来模拟静态对象以及静态类型语言中的“结构体”（struct）。有时他们也用作字符串的集合（忽略名/值对中的值）。

除了字符串、数字、true、false、null 和 undefined 之外， JavaScript 中的值都是对象，尽管字符串、数字和布尔值不是对象，但它们的行为和不可变对象非常类似。

对象是可变的，通过引用而非值来操作对象。如果变量 x 是指向一个对象的引用，那么执行代码`var y = x;`变量y也是指向同一个对象的引用，而非这个对象的副本。通过变量 y 修改这个对象也会对变量 x 造成影响。

对象最常见的用法是创建（create）、设置（set）、查找（query）、删除（delete）、检测（test）和枚举（enumerate）它的属性。

属性包括名字和值。属性名可以是包含空字符串在内的任意字符串，但对象中不能存在两个同名的属性。值可以是任意JavaScript值，或者（在ECMAScript 5中）可以是一个getter或setter函数（或两者都有）。6.6节会有关于getter和setter函数的讲解。除了名字和值之外，每个属性还有一些与之相关的值，称为“属性特性”（property attribute）：

- 可写（writable attribute），表明是否可以设置该属性的值。
- 可枚举（enumerable attribute），表明是否可以通过for/in循环返回该属性。
- 可配置（configurable attribute），表明是否可以删除或修改该属性。

在ECMAScript 5之前，通过代码给对象创建的所有属性都是可写的、可枚举的和可配置的。在ECMAScript5中则可以对这些特性加以配置。6.7节讲述如何操作。

除了包含属性之外，每个对象还拥有三个相关的对象特性（object attribute）：

- 对象的原型（prototype）指向另外一个对象，本对象的属性继承自它的原型对象。
- 对象的类（class）是一个标识对象类型的字符串。
- 对象的扩展标记（extensible flag）指明了（在ECMAScript 5中）是否可以向该对象添加新属性。

6.1.3节和6.2.2节会有关于原型和属性继承的讲述，6.8节会进一步详细讲述这三个特性。

最后，我们用下面这些术语来对三类JavaScript对象和两类属性作区分：

- 内置对象（native object）是由ECMAScript规范定义的对象或类。例如，数组、函数、日期和正则表达式都是内置对象。
- 宿主对象（host object）是由JavaScript解释器所嵌入的宿主环境（比如Web浏览器）定义的。客户端JavaScript中表示网页结构的HTMLElement对象均是宿主对象。既然宿主环境定义的方法可以当成普通的JavaScript函数对象，那么宿主对象也可以当成内置对象。
- 自定义对象（user-defined object）是由运行中的JavaScript代码创建的对象。
- 自有属性（own property）是直接在对象中定义的属性。
- 继承属性（inherited property）是在对象的原型对象中定义的属性。

## 6.1 创建对象 

### 6.1.1 对象直接量

创建对象最简单的方式就是在JavaScript代码中使用对象直接量。对象直接量是由若干名/值对组成的映射表，名/值对中间用冒号分隔，名/值对之间用逗号分隔，整个映射表用花括号括起来。属性名可以是JavaScript标识符也可以是字符串直接量（包括空字符串）。属性的值可以是任意类型的JavaScript表达式，表达式的值（可以是原始值也可以是对象值）就是这个属性的值。下面有一些例子：

```js
var empty ={};  // 一个空对象
var point ={x:0, y:0};  // 两个属性
var point2 ={x:point.x, y:point.y+1};
var book ={
  "main title": "javascript",  // 属性名字里有空格，必须用字符串表示
  'sub-title': "the defintive guide",  // 属性里有连接字符，因此需要使用字符串
  "for": "all adiences",  // for是保留字，因此需要引号。
  author: {  // 这个属性的值是一个对象
    firstName: "dabid",  // 这里属性的值也是一个对象
    surname: "flangan"  // 这里的属性名都没有引号
  }
};
```

在ECMAScript 5（以及ECMAScript 3的一些实现）中，保留字可以用做不带引号的属性名。然而对于ECMAScript 3来说，使用保留字作为属性名必须使用引号引起来。在ECMAScript 5中，对象直接量中的最后一个属性后的逗号将忽略，且在ECMAScript 3的大部分实现中也可以忽略这个逗号，但在IE中则报错。

对象直接量是一个表达式，这个表达式的每次运算都创建并初始化一个新的对象。每次计算对象直接量的时候，也都会计算它的每个属性的值。也就是说，如果在一个重复调用的函数中的循环体内使用了对象直接量，它将创建很多新对象，并且每次创建的对象的属性值也有可能不同。

### 6.1.2 通过new创建对象

new运算符创建并初始化一个新对象。关键字new后跟随一个函数调用。这里的函数称做构造函数（constructor），构造函数用以初始化一个新创建的对象。JavaScript语言核心中的原始类型都包含内置构造函数。例如：

```js
var o = new Object();  // 创建一个空对象，和{}一样
var a = new Array();
var d = new Date();
var r = new RegExp("js");
```

除了这些内置构造函数，用自定义构造函数来初始化新对象也是非常常见的。

### 6.1.3 原型

在讲述第三种对象创建技术之前，我们应当首先解释一下原型。每一个JavaScript对象（null除外）都和另一个对象相关联。“另一个”对象就是我们熟知的原型，每一个对象都从原型继承属性。

所有通过对象直接量创建的对象都具有同一个原型对象，并可以通过JavaScript代码`Object.prototype`获得对原型对象的引用。通过关键字new和构造函数调用创建的对象的原型就是构造函数的prototype属性的值。因此，同使用`{}`创建对象一样，通过`new Object()`创建的对象也继承自`Object.prototype`。同样，通过`new Array()`创建的对象的原型就是`Array.prototype`，通过`new Date()`创建的对象的原型就是`Date.prototype`。

没有原型的对象为数不多，`Object.prototype`就是其中之一。它不继承任何属性。其他原型对象都是普通对象，普通对象都具有原型。所有的内置构造函数（以及大部分自定义的构造函数）都具有一个继承自`Object.prototype`的原型。例如，`Date.prototype`的属性继承自`Object.prototype`，因此由`new Date()`创建的Date对象的属性同时继承自`Date.prototype`和`Object.prototype`。这一系列链接的原型对象就是所谓的“原型链”（prototype chain）。

6.2.2节讲述属性继承的工作机制。6.8.1节将会讲到如何获取对象的原型。第9章将会更详细地讨论原型和构造函数，包括如何通过编写构造函数定义对象的“类”，以及给构造函数的 prototype 属性赋值可以让其“实例”直接使用这个原型上的属性和方法。

### 6.1.4 Object.create()

ECMAScript 5定义了一个名为`Object.create()`的方法，它创建一个新对象，其中第一个参数是这个对象的原型。`Object.create()`提供第二个可选参数，用以对对象的属性进行进一步描述。

`Object.create()`是一个静态函数，而不是提供给某个对象调用的方法。使用它的方法很简单，只须传入所需的原型对象即可：

```js
var o1 = Object.create({
  x: 1,
  y: 2
});  // o1继承了属性x和y
```

可以通过传入参数 null 来创建一个没有原型的新对象，但通过这种方式创建的对象不会继承任何东西，甚至不包括基础方法，比如`toString()`，也就是说，它将不能和“+”运算符一起正常工作：

```js
var o2 = Object.create(null);  // o2不继承任何属性和方法
```

如果想创建一个普通的空对象（比如通过`{}`或`new Object()`创建的对象），需要传入`Object.prototype`：

```js
var o3 =Object.create(Object.prototype);  // o3和{}和new Object一样
```

可以通过任意原型创建新对象（换句话说，可以使任意对象可继承），这是一个强大的特性。在 ECMAScript3 中可以用类似的代码来模拟原型继承：

```js
// 例 6.1
// inherit()返回了一个继承自原型对象p属性的新对象
// 这里是有ECMAScript5中的Object.create()函数（如果存在的话）
// 如果不存在Object.create,则使用其他方法
function inherit(p) {
  if (p == null) throw TypeError(); // p是一个对象，不能是null
  if (Object.create) // 如果Object.create存在
    return Object.create(p); // 直接使用它
  var t = typeof p; // 否则进一步检测
  if (t !== "object" && t !== "function") throw TypeError;
  function f() {}; // 定义一个空构造函数
  f.prototype = p; // 将其原型属性设置p
  return new f(); // 将f()创建p的继承对象
}
```

现在只要知道`inherit()`返回的新对象继承了参数对象的属性就可以了。注意，`inherit()`并不能完全代替`Object.create()`，它不能通过传入null原型来创建对象，而且不能接收可选的第二个参数。不过我们仍会在本章和第9章的示例代码中多次用到`inherit()`。

`inherit()`函数的其中一个用途就是防止库函数无意间（非恶意地）修改那些不受你控制的对象。不是将对象直接作为参数传入函数，而是将它的继承对象传入函数。当函数读取继承对象的属性时，实际上读取的是继承来的值。如果给继承对象的属性赋值，则这些属性只会影响这个继承对象自身，而不是原始对象：

```js
var o = {
  x: "donot change this balue"
};
library_function(inherit(o));  // 防止对o的意外修改
```

## 6.2 属性的查询和设置 

可以通过点`.`或方括号`[]`运算符来获取属性的值。运算符左侧应当是一个表达式，它返回一个对象。对于点`.`来说，右侧必须是一个以属性名称命名的简单标识符。对于方括号`[]`来说，方括号内必须是一个计算结果为字符串的表达式，这个字符串就是属性的名字。

```js
var author = book.author;  // 得到book的“author”属性
var name = oAuthor.surname  // 得到author的“surname”的属性
var title = book["main title"]  // 得到book的main title属性
```

和查询属性值的写法一样，通过点和方括号也可以创建属性或给属性赋值，但需要将它们放在赋值表达式的左侧：

```js
book.edition = 6;  // 给book添加一个名为edition的属性
book["main title"] = "ECMAscript";  // 给"main title"属性赋值
```

在 ECMAScript 3 中，点运算符后的标识符不能是保留字，比如，`o.for`或`o.class`是非法的，因为for是JavaScript的关键字，class是保留字。如果一个对象的属性名是保留字，则必须使用方括号的形式访问它们，比如`o["for"]`和`o["class"]`。ECMAScript 5对此放宽了限制（包括ECMAScript3的某些实现），可以在点运算符后直接使用保留字。

当使用方括号时，我们说方括号内的表达式必须返回字符串。其实更严格地讲，表达式必须返回字符串或返回一个可以转换为字符串的值。在第7章里有一些例子中的方括号内使用了数字，这情况象是非常常见的。

### 6.2.1 作为关联数组的对象

上文提到，下面两个JavaScript表达式的值相同：

```js
object.property
object["property"]
```

第一种语法使用点运算符和一个标识符，这和C和Java中访问一个结构体或对象的静态字段非常类似。第二种语法使用方括号和一个字符串，看起来更像数组，只是这个数组元素是通过字符串索引而不是数字索引。这种数组就是我们所说的关联数组（associative array），也称做散列、映射或字典（dictionary）。JavaScript对象都是关联数组，本节将讨论它的重要性。

在C、C++和Java和一些强类型（strong typed）语言中，对象只能拥有固定数目的属性，并且这些属性名称必须提前定义好。由于JavaScript是弱类型语言，因此不必遵循这条规定，在任何对象中程序都可以创建任意数量的属性。但当通过点运算符`.`访问对象的属性时，属性名用一个标识符来表示。标识符必须直接出现在JavaScript程序中，它们不是数据类型，因此程序无法修改它们。

反过来讲，当通过`[]`来访问对象的属性时，属性名通过字符串来表示。字符串是 JavaScript 的数据类型，在程序运行时可以修改和创建它们。因此，可以在 JavaScript 中使用下面这种代码：

```js
var addr = "";
// 读取custom对象的address0、address1、address2和address3属性
for (i = 0; i < 4; i++) {
  addr += customer["address" + i] + '\n';
};
```

这个例子主要说明了使用数组写法和用字符串表达式来访问对象属性的灵活性。这段代码也可以通过点运算符来重写，但是很多场景只能使用数组写法来完成。假设你正在写一个程序，这个程序利用网络资源计算当前用户股票市场投资的金额。程序允许用户输入每只股票的名称和购股份额。该程序使用名为portfolio的对象来存储这些信息。每只股票在这个对象中都有对应的属性，属性名称就是股票名称，属性值就是购股数量，例如，如果用户持有 IBM 的50股，那么 portfolio.ibm 属性的值就为50。

下面是程序的部分代码，这个函数用来给 portifolio 添加新的股票：

```js
function addstock (portfolio,stockname,shares){
portfolio[stockname] = shares;
```

由于用户是在程序运行时输入股票名称，因此在之前无法得知这些股票的名称是什么。而由于在写程序的时候不知道属性名称，因此无法通过点运算符`.`来访问对象portfolio的属性。但可以使用`[]`运算符，因为它使用字符串值（字符串值是动态的，可以在运行时更改）而不是标识符（标识符是静态的，必须写死在程序中）作为索引对属性进行访问。

当使用for/in循环遍历关联数组时，就可以清晰地体会到for/in的强大之处。下面的例子就是利用for/in计算portfolio的总计值：

```js
function getvalue(protfolio) {
  var total = 0.0;
  for (stock in protfolio) {  // 遍历protfolio中的每只股票
    var shares = protfolio[stock];  // 得到每只股票的份额
    var price = getquote(stock);  // 查找股票的价格
    total += shares * price;  // 将结果累加到total中
  }
  return total;
}
```

### 6.2.2 继承

JavaScript对象具有“自有属性”（own property），也有一些属性是从原型对象继承而来的。为了更好地理解这种继承，必须更深入地了解属性访问的细节。本节中的许多示例代码借用了例 6.1 中的`inherit()`函数，通过给它传入指定原型对象来创建实例。

假设要查询对象o的属性x，如果o中不存在x，那么将会继续在o的原型对象中查询属性x。如果原型对象中也没有x，但这个原型对象也有原型，那么继续在这个原型对象的原型上执行查询，直到找到x或者查找到一个原型是 null 的对象为止。可以看到，对象的原型属性构成了一个“链”，通过这个“链”可以实现属性的继承。

```js
var o = {};  // 从Object.prototype继承对象方法
o.x = 1;  // 给o定义一个属性x

var p = inherit(o);  // p继承o和Object.prototype
p.y = 2;  // 给p定义一个属性y

var q = inherit(p);  // q继承p、o和Object.prototype
q.z = 3;  // 给q定义一个属性z

var s = q.toString();  // toString继承自Object.prototype
q.x + q.y  // =>3：xhey分别继承自o和p
```

现在假设给对象o的属性x赋值，如果o中已经有属性x（这个属性不是继承来的），那么这个赋值操作只改变这个已有属性x的值。如果o中不存在属性x，那么赋值操作给o添加一个新属性x。如果之前o继承自属性x，那么这个继承的属性就被新创建的同名属性覆盖了。

属性赋值操作首先检查原型链，以此判定是否允许赋值操作。例如，如果o继承自一个只读属性x，那么赋值操作是不允许的。如果允许属性赋值操作，它也总是在原始对象上创建属性或对已有的属性赋值，而不会去修改原型链。在JavaScript中，只有在查询属性时才会体会到继承的存在，而设置属性则和继承无关，这是JavaScript的一个重要特性，该特性让程序员可以有选择地覆盖（override）继承的属性。

```js
var unitcircle = {r: 1}  // 一个用来继承的的对象
var c = inherit(unitcircle);  // c继承r
c.x = 1; c.y = 1;  // c定义两个属性
c.r = 2;  // c覆盖继承来的属性
console.log(unitcircle.r)  // =>1 对象原型没有被修改
```

属性赋值要么失败，要么创建一个属性，要么在原始对象中设置属性，但有一个例外，如果o继承自属性x，而这个属性是一个具有setter方法的accessor属性，那么这时将调用setter方法而不是给o创建一个属性x。需要注意的是，setter方法是由对象o调用的，而不是定义这个属性的原型对象调用的。因此如果setter方法定义任意属性，这个操作只是针对o本身，并不会修改原型链。

### 6.2.3 属性访问错误

属性访问并不总是返回或设置一个值。本节讲述查询或设置属性时的一些出错情况。

查询一个不存在的属性并不会报错，如果在对象o自身的属性或继承的属性中均未找到属性x，属性访问表达式`o.x`返回 undefined 。

```js
// book对象有属性“sub-title”，而没有属性“subtitle”
book.subtitle;  // =>undefined：属性不存在
```

但是，如果对象不存在，那么试图查询这个不存在的对象的属性就会报错。 null 和 undefined 值都没有属性，因此查询这些值的属性会报错，接上例：

```js
// 抛出一个类型错误异常，undefined没有length属性
var len = book.subtitle.length;
// Uncaught TypeError: Cannot read property 'length' of undefined
```

除非确定 book 和 book.subtitle 都是（或在行为上）对象，否则不能这样写表达式`book.subtitle.length`，因为这样会报错，下面提供了两种避免出错的方法：

```js
// 一种很冗余但很容易懂的方法
var len = undefined;
if (book){
  if(book.subtitle) len = book.subtitle.length;
}

// 一种更简练的常用的方法，获取subtitle的length属性undefined
var len = book && book.subtitle && book.subtitle.length;
```

当然，给 null 和 undefined 设置属性也会报类型错误。给其他值设置属性也不总是成功，有一些属性是只读的，不能重新赋值，有一些对象不允许新增属性，但让人颇感意外的是，这些设置属性的失败操作不会报错：

```js
// 内置构造函数的原型是只读的
Object.prototype = 0;  // 赋值失败，但没报错，Object.prototype没有修改
```

这是一个历史遗留问题，这个bug在ECMAScript 5的严格模式中已经修复。在严格模式中，任何失败的属性设置操作都会抛出一个类型错误异常。

尽管属性赋值成功或失败的规律看起来很简单，但要描述清楚并不容易。在这些场景下给对象 o 设置属性 p 会失败：

- o中的属性p是只读的：不能给只读属性重新赋值（`defineProperty()`方法中有一个例外，可以对可配置的只读属性重新赋值）。
- o中的属性p是继承属性，且它是只读的：不能通过同名自有属性覆盖只读的继承属性。
- o中不存在自有属性p：o没有使用setter方法继承属性p，并且o的可扩展性（extensible attribute）是false。如果o中不存在p，而且没有setter方法可供调用，则p一定会添加至o中。但如果o不是可扩展的，那么在o中不能定义新属性。

## 6.3 删除属性 

delete 运算符可以删除对象的属性。它的操作数应当是一个属性访问表达式。让人感到意外的是， delete 只是断开属性和宿主对象的联系，而不会去操作属性中的属性：

```js
delete book.author;  // book不再有属性author
delete book["main title"]  // book不再有属性"main title"
```

delete运算符只能删除自有属性，不能删除继承属性（要删除继承属性必须从定义这个属性的原型对象上删除它，而且这会影响到所有继承自这个原型的对象）。

当delete表达式删除成功或没有任何副作用（比如删除不存在的属性）时，它返回true。如果delete后不是一个属性访问表达式，delete同样返回true：

```js
o = { x: 1 };  // o有一个属性x，并继承属性toString
delete o.x;  // 删除x，返回true
delete o.x;  // 什么都没做，（x已经不存在），返回true
delete o.toString();  // 什么也没有做（toString是继承来的），返回true
delete o.toString();  // 返回true
delete 1;  // 无意义，返回true
```

delete 不能删除那些可配置性为false的属性（尽管可以删除不可扩展对象的可配置属性）。某些内置对象的属性是不可配置的，比如通过变量声明和函数声明创建的全局对象的属性。在严格模式中，删除一个不可配置属性会报一个类型错误。在非严格模式中（以及ECMAScript3中），在这些情况下的delete操作会返回false：

```js
delete Object.prototype;  // 不能删除，属性是不可配置的
var x = 1;  // 声明一个全局变量
console.log(delete this.x);  // 不能删除这个属性
function f() {}  //  声明一个全局函数
console.log(delete this.f);  // 也不能删除全局函数
```

当在非严格模式中删除全局对象的可配值属性时，可以省略对全局对象的引用，直接在delete操作符后跟随要删除的属性名即可：

```js
this.x = 1;  // 创建一个可配置的全局属性(没有用var)
delete x;  // 将它删除
```

然而在严格模式中，delete后跟随一个非法的操作数（比如x），则会报一个语法错误，因此必须显式指定对象及其属性：

```js
delete x;  // 在严格模式下报语法错误
delete.this.x  // 正常工作
```

## 6.4 检测属性 

JavaScript对象可以看做属性的集合，我们经常会检测集合中成员的所属关系——判断某个属性是否存在于某个对象中。可以通过 in 运算符、`hasOwnPreperty()`和`propertyIsEnumerable()`方法来完成这个工作，甚至仅通过属性查询也可以做到这一点。

in运算符的左侧是属性名（字符串），右侧是对象。如果对象的自有属性或继承属性中包含这个属性则返回true：

```js
var o = {x: 1}
"x" in o;  // =>true：x是o的属性
"y" in o;  // =>false：y不是o的属性
"toString" in o;  // =>true：o继承toString属性
```

对象的`hasOwnProperty()`方法用来检测给定的名字是否是对象的自有属性。对于继承属性它将返回false：

```js
var o = {x: 1};
o.hasOwnProperty("x");  // =>true：o中有一个自有属性x
o.hasOwnProperty("y");  // =>false：o中不存在属性y
o.hasOwnProperty("toString");  // false：toString是继承属性
```

`propertyIsEnumerable()`是`hasOwnProperty()`的增强版，只有检测到是自有属性且这个属性的可枚举性（enumerable attribute）为true时它才返回true。某些内置属性是不可枚举的。通常由JavaScript代码创建的属性都是可枚举的，除非在ECMAScript 5中使用一个特殊的方法来改变属性的可枚举性，随后会提到：

```js
var o = inherit({ y: 2 });
o.x = 1;
o.propertyIsEnumerable("x");  // true：o是一个可枚举的自有属性
o.propertyIsEnumerable("y");  // false：y是继承来的
Object.prototype.propertyIsEnumerable("toString");  // false：不可枚举
```

除了使用in运算符之外，另一种更简便的方法是使用`!==`判断一个属性是否是undefined：

```js
var o = {x: 1}
o.x !== undefined;  // true：o有属性x
o.y !== undefined;  // fakse：o没有属性y
o.toString() !== undefined;  // true：o继承了toString属性
```

然而有一种场景只能使用in运算符而不能使用上述属性访问的方式。in可以区分不存在的属性和存在但值为undefined的属性。例如下面的代码：

```js
var o = {
  x: undefined
}  // 属性被显式赋值为undefined
o.x !== undefined;  // false：属性存在，但值为undefined
o.y !== undefined;  // false：属性不存在
"x" in o;  // true
"y" in o;  // false
delete o.x;  // 删除了属性x
"x" in o  // false  属性不存在
```

注意，上述代码中使用的是`!==`运算符，而不是`!=`。`!==`可以区分undefined和null。有时则不必作这种区分：

```js
// 如果o中有属性x，且x的值不是null undefined ,o.x乘以2
if (o.x != null) o.x *= 2;

// 如果o中还有属性x, 且x的值不能转换false, o.x乘以2
// 如果x是undefined、null、false、""、0、NaN、则它保持不变
if (o.x) o.x *= 2;
```

## 6.5 枚举属性 

除了检测对象的属性是否存在，我们还会经常遍历对象的属性。通常使用for/in循环遍历，ECMAScript5提供了两个更好用的替代方案。

5.5.4节讨论过for/in循环，for/in循环可以在循环体中遍历对象中所有可枚举的属性（包括自有属性和继承的属性），把属性名称赋值给循环变量。对象继承的内置方法不可枚举的，但在代码中给对象添加的属性都是可枚举的（除非用下文中提到的一个方法将它们转换为不可枚举的）。例如：

```js
var o = {x: 1, y: 2, z: 3};  // 三个可枚举的属性
o.propertyIsEnumerable("toString");  // =>false，不可枚举
for(p in o)  // 遍历属性
console.log(p);   // 输出x、y和z 不会输出toString
```

有许多实用工具库给`Object.prototype`添加了新的方法或属性，这些方法和属性可以被所有对象继承并使用。然而在ECMAScript 5标准之前，这些新添加的方法是不能定义为不可枚举的，因此它们都可以在for/in循环中枚举出来。为了避免这种情况，需要过滤for/in循环返回的属性，下面两种方式是最常见的：

```js
 for(p in o){
  if(!o.hasOwnProperty(p)) continue;  // 跳过继承的属性
}
for(p in o){
  if (typeof o[p]==="function") continue;  // 跳过方法
}
```

例6-2定义了一些有用的工具函数来操控对象的属性，这些函数用到了for/in循环。实际上`extend()`函数经常出现在JavaScript实用工具库中。

```js
/*
*把p中可枚举的属性复制到o中，并返回o
*如果o和p中含有同名属性，则覆盖o中的属性
*这个函数并不处理getter和setter以及复制属性
*/
function extend(o, p) {
  for (prop in p) { //遍历p中所有的属性
    o[prop] = p[prop]; //将遍历属性添加至o中
  }
  return o;
}

/*将p中可枚举的属性复制至o中，并返回o
* 如果o和p有同名属性，o中的属性将不受影响
* 这个函数并不处理getter和setter以及复制属性
*/
function merge(o, p) {
  for (prop in p) { //遍历p中所有的元素
    if (o.hasOwnProperty[prop]) continue; //过滤掉已在o中存在的属性
    o[prop] = p[prop]; //将属性添加至o中
  }
  return o;
}

/*
* 如果o中的属性在p中没有同名属性，则从o中删除这个属性
* 返回o
*/
function restrict(o, p) {
  for (prop in o) { //遍历o的所有属性
    if (!(prop in p)) delete o[prop]; //如果在p中不存在，则删除之
  }
  return o;
}

/*
* 如果o中的属性在p中存在属性，则从o中删除这个属性
* 返回o
*/
function subtarck(o, p) {
  for (prop in p) { //遍历p中所有的属性
    delete o[prop]; //从o中删除（删除一个不存在的属性一般不报错）
  }
  return o;
}

/*
* 返回一个新对象，这个对象同时拥有o的属性和p的属性
* 如果o和p中有同名属性，使用p中的属性
*/
function union(o, p) {
  return extend(extend({}, o), p);
}

/*
* 返回一个新对象，这个对象同时拥有o的属性和p中出现的属性
* 很像求o和p的交集，但p中的属性值被忽略
*/
function intersection(o, p) {
  return restrict(extend({}, o), p);
}

/*
* 返回一个数组，这个数组包含的是o中可枚举的自由属性的名字
*/
function keys(o) {
  if (typeof o !== "object") throw TypeError(); //参数必须是对象
  var result = []; //将要返回的对象
  for (var prop in o) { //遍历所有可枚举的属性
    if (o.hasOwnProperty(prop)) //判断是否自有属性
      result.push(prop); //将属性名添加至数组中
  }
  return result; //返回这个数组
}
```

除了for/in循环之外，ECMAScript 5定义了两个用以枚举属性名称的函数。第一个是`Object.keys()`，它返回一个数组，这个数组由对象中可枚举的自有属性的名称组成，它的工作原理和例6-2中的工具函数`keys()`类似。ECMAScript 5中第二个枚举属性的函数是`Object.getOwnPropertyNames()`，它和`Ojbect.keys()`类似，只是它返回对象的所有自有属性的名称，而不仅仅是可枚举的属性。在ECMAScript 3中是无法实现的类似的函数的，因为 ECMAScript 3 中没有提供任何方法来获取对象不可枚举的属性。

## 6.6 属性getter和setter 

对象属性是由名字、值和一组特性（attribute）构成的。在ECMAScript 5中，属性值可以用一个或两个方法替代，这两个方法就是getter和setter。由getter和setter定义的属性称做“存取器属性”（accessorproperty），它不同于“数据属性”（data property），数据属性只有一个简单的值。

当程序查询存取器属性的值时，JavaScript调用getter方法（无参数）。这个方法的返回值就是属性存取表达式的值。当程序设置一个存取器属性的值时，JavaScript调用setter方法，将赋值表达式右侧的值当做参数传入setter。从某种意义上讲，这个方法负责“设置”属性值。可以忽略setter方法的返回值。

和数据属性不同，存取器属性不具有可写性（writable attribute）。如果属性同时具有getter和setter方法，那么它是一个读/写属性。如果它只有getter方法，那么它是一个只读属性。如果它只有setter方法，那么它是一个只写属性（数据属性中有一些例外），读取只写属性总是返回undefined。

定义存取器属性最简单的方法是使用对象直接量语法的一种扩展写法：

```js
var o = { 
  // 普通数据属性
  data_prop: value,

  // 存取器属性都是成对定义的函数
  get accessor_prop() { /*这里是函数体*/ },
  set accessor_prop(value) { /*这里是函数体*/ }
};
```

存取器属性定义为一个或两个和属性同名的函数，这个函数定义没有使用function关键字，而是使用get和（或）set。注意，这里没有使用冒号将属性名和函数体分隔开，但在函数体的结束和下一个方法或数据属性之间有逗号分隔。例如，思考下面这个表示2D笛卡尔点坐标的对象。它有两个普通的属性x和y分别表示对应点的X坐标和Y坐标，它还有两个等价的存取器属性用来表示点的极坐标：

```js
var p = {
  // x和y是普通的可读写数据属性
  x: 1.0,
  y: 1.0,
  // r是可读写的存取器属性，它带有getter和setter。
  // 函数体结束后不要忘记带上逗号
  get r() {
    return Math.sqrt(this.x * this.x + this.y * this.y);
  },
  set r(newvalue) {
    var oldvalue = Math.sqrt(this.x * this.x + this.y * this.y);
    var ratio = newvalue / oldvalue;
    this.x *= ratio;
    this.y *= ratio;
  },
  // theta是只读存取器属性，它只有getter方法
  get theta() {
    return Math.atan2(this.y, this.x);
  }
};
```

注意在这段代码中getter和setter里this关键字的用法。JavaScript把这些函数当做对象的方法来调用，也就是说，在函数体内的this指向表示这个点的对象，因此，r属性的getter方法可以通过this.x和this.y引用x和y属性。

和数据属性一样，存取器属性是可以继承的，因此可以将上述代码中的对象p当做另一个“点”的原型。可以给新对象定义它的x和y属性，但r和theta属性是继承来的：

```js
var q = inherit(p);  // 创建一个继承getter和setter的新对象
q.x = 1, q.y = 1;  // 给q添加两个属性
console.log(q.r)  // 可以使用存储器的存取属性
console.log(q.theta);
```

这段代码使用存取器属性定义API，API提供了表示同一组数据的两种方法（笛卡尔坐标系表示法和极坐标系表示法）。还有很多场景可以用到存取器属性，比如智能检测属性的写入值以及在每次属性读取时返回不同值：

```js
// 这个对象产生严格的自增序列号
var serialnum = {
  // 这个属性包含下一个序列号
  // $符号暗示这个属性是一个私有属性
  $n: 0,

  // 返回当前的值，然后自增
  get next() {
    return this.$n++;
  },

  // 返回当前新的值，大只有当它比当前值大时才设置成功
  set next(n) {
    if (n >= this.$n) this.$n = n;
    else throw "序列号的值不能比当前值小";
  }
};
```

最后我们再来看一个例子，这个例子使用getter方法实现一种“神奇”的属性：

```js
//这个对象表示有一个可以返回随机数的存取器属性
//例如，"random.octet"产生一个随机数
//每次产生的随机数都在0-255之间
var random = {
  get octet() {
    return Math.floor(Math.random() * 256);
  },
  get uint16() {
    return Math.floor(Math.random() * 65536);
  },
  get int16() {
    return Math.floor(Math.random() * 65536) - 32768;
  }
}
```

## 6.7 属性的特性 

除了包含名字和值之外，属性还包含一些标识它们可写、可枚举和可配置的特性。在 ECMAScript 3 中无法设置这些特性，所有通过 ECMAScript 3 的程序创建的属性都是可写的、可枚举的和可配置的，且无法对这些特性做修改。本节将讲述 ECMAScript 5 中查询和设置这些属性特性的API。这些API对于库的开发者来说非常重要，因为：

- 可以通过这些API给原型对象添加方法，并将它们设置成不可枚举的，这让它们看起来更像内置方法。
- 可以通过这些API给对象定义不能修改或删除的属性，借此“锁定”这个对象。

在本节里，我们将存取器属性的 getter 和 setter 方法看成是属性的特性。按照这个逻辑，我们也可以把数据属性的值同样看做属性的特性。因此，可以认为一个属性包含一个名字和4个特性。数据属性的4个特性分别是它的值（value）、可写性（writable）、可枚举性（enumerable）和可配置性（configurable）。存取器属性不具有值（value）特性和可写性，它们的可写性是由 setter 方法存在与否决定的。因此存取器属性的4个特性是读取（get）、写入（set）、可枚举性和可配置性。

为了实现属性特性的查询和设置操作，ECMAScript 5中定义了一个名为“属性描述符”（property descriptor）的对象，这个对象代表那4个特性。描述符对象的属性和它们所描述的属性特性是同名的。因此，数据属性的描述符对象的属性有 value 、 writable 、 enumerable 和 configurable 。存取器属性的描述符对象则用 get 属性和 set 属性代替 value 和 writable 。其中writable、enumerable和configurable都是布尔值，当然，get属性和set属性是函数值。

通过调用`Object.getOwnPropertyDescriptor()`可以获得某个对象特定属性的属性描述符：

```js
//返回{value: 1, writable: true, enumerable: true, configurable: true}
Object.getOwnPropertyDescriptor({x: 1}, "x");

//查询上例子中的randam对象的octet属性
//返回 {get: /*function octet(){...*/ , set: undefined, enumerable: true, configurable: true}
Object.getOwnPropertyDescriptor(random, "octet");

//对于继承属性和不存在的属性，返回undefined
Object.getOwnPropertyDescriptor({}, "x"); //undefined 没有这个属性
Object.getOwnPropertyDescriptor({}, "toString"); //undefined 继承属性
```

从函数名字就可以看出，`Object.getOwnPropertyDescriptor()`只能得到自有属性的描述符。要想获得继承属性的特性，需要遍历原型链（参照6.8.1节的`Object.getPrototypeOf()`）。

要想设置属性的特性，或者想让新建属性具有某种特性，则需要调用`Object.definePeoperty()`，传入要修改的对象、要创建或修改的属性的名称以及属性描述符对象：

```js
// 空对象
var o = {}; 
// 添加一个不可枚举的数据属性x，并赋值1
Object.defineProperty(o, "x", {
  value:1,
  writable:true,
  enumerable:false,
  configurable:true
});
// {value: 1, writable: true, enumerable: false, configurable: true}
Object.getOwnPropertyDescriptor(o, "x");

// 属性是存在的，但不可枚举
o.x; // => 1
Object.keys(o) // => [];

// 现在对属性x修改，让它只变为只读
Object.defineProperty(o, "x", {
  writable:false
});

// 试图改变这个属性的值
// 操作失败但不报错，严格模式中会抛出类型错误的异常
o.x = 2; 
o.x // => 1

// 属性依然是可配置的，因此可以通过这样的方式进行修改：
Object.defineProperty(o, "x", {
  value:2
});
o.x // =>2

// 现在讲x从数据属性修改为存取器属性
Object.defineProperty(o, "x", {
  get: function(){
    return 9;
  } 
});
o.x // =>9
```

传入`Object.defineProperty()`的属性描述符对象不必包含所有4个特性。对于新创建的属性来说，默认的特性值是false或undefined。对于修改的已有属性来说，默认的特性值没有做任何修改。注意，这个方法要么修改已有属性要么新建自有属性，但不能修改继承属性。

如果要同时修改或创建多个属性，则需要使用`Object.defineProperties()`。第一个参数是要修改的对象，第二个参数是一个映射表，它包含要新建或修改的属性的名称，以及它们的属性描述符，例如：

```js
var p = Object.defineProperties({},{
  x: {value:1, writable:true, enumerable:true, configurable:true},
  y: {value:1, writable:true, enumerable:true, configurable:true},
  r: {
    get: function(){
      return Math.sqrt(this.x*this.x + this.y*this.y)},enumerable:true,configurable:true
  }
});
```

这段代码从一个空对象开始，然后给它添加两个数据属性和一个只读存取器属性。最终`Object.defineProperties()`返回修改后的对象（和`Object.defineProperty()`一样）。

对于那些不允许创建或修改的属性来说，如果用`Object.defineProperty()`和`Object.defineProperties()`对其操作（新建或修改）就会抛出类型错误异常，比如，给一个不可扩展的对象新增属性就会抛出类型错误异常。造成这些方法抛出类型错误异常的其他原因则和特性本身相关。可写性控制着对值特性的修改。可配置性控制着对其他特性（包括属性是否可以删除）的修改。然而规则远不止这么简单，例如，如果属性是可配置的话，则可以修改不可写属性的值。同样，如果属性是不可配置的，仍然可以将可写属性修改为不可写属性。下面是完整的规则，任何对`Object. defineProperty()`或`Object.defineProperties()`违反规则的使用都会抛出类型错误异常：

- 如果对象是不可扩展的，则可以编辑已有的自有属性，但不能给它添加新属性。
- 如果属性是不可配置的，则不能修改它的可配置性和可枚举性。
- 如果存取器属性是不可配置的，则不能修改其getter和setter方法，也不能将它转换为数据属性。
- 如果数据属性是不可配置的，则不能将它转换为存取器属性。
- 如果数据属性是不可配置的，则不能将它的可写性从false修改为true，但可以从true修改为false。
- 如果数据属性是不可配置且不可写的，则不能修改它的值。然而可配置但不可写属性的值是可以修改的（实际上是先将它标记为可写的，然后修改它的值，最后转换为不可写的）。

例6-2中实现了`extend()`函数，这个函数把一个对象的属性复制到另一个对象中。这个函数只是简单地复制属性名和值，没有复制属性的特性，而且也没有复制存取器属性的getter和setter方法，只是将它们简单地转换为静态的数据属性。例6-3给出了改进的`extend()`，它使用`Object.getOwnPropertyDescriptor()`和`Object.defineProperty()`对属性的所有特性进行复制。新的`extend()`作为不可枚举属性添加到Object.prototype中，因此它是Object上定义的新方法，而不是一个独立的函数。

```js
/*
* 复制属性的特性
* Object.prototype添加一个不可枚举的extend()方法
* 这个方法继承自调用它的对象，将作为参数传入的对象的属性一一复制
* 除了值之外，也复制属性的所有特性，除非在目标对象中有同名的属性
* 参数对象的所有自有对象（包括不可枚举的属性）也会一一复制
* */
Object.defineProperty(Object.prototype,
  "extend", //定义Object.prototype.extend
  {
    writable: true,
    enumerable: false, //将其定义为不可枚举的
    configurable: true,
    value: function(o) { //值就是这个函数
      // 得到所有的自由属性，包括不可枚举属性
      var names = Object.getOwnPropertyNames(o);
      // 遍历他们
      for (var i = 0; i < names.length; i++) {
        // 如果属性已经存在，则跳过
        if (names[i] in this) continue;
        // 获得o中的属性描述符
        var desc = Object.getOwnPropertyDescriptor(o, names[i]);
        // 用它给this创建一个属性
        Object.defineProperty(this, names[i], desc);
      }
    }
  }
);
```

**getter和setter的老式API**

可以通过6.6节描述的对象直接量语法给新对象定义存取器属性，但不能查询属性的getter和setter方法或给已有的对象添加新的存取器属性。在ECMAScript 5中，可以通过`Object.getOwnPropertyDescriptor()`和`Object.defineProperty()`来完成这些工作。

在ECMAScript 5标准被采纳之前，大多数JavaScript的实现（IE浏览器除外）已经可以支持对象直接量语法中的get和set写法。这些实现提供了非标准的老式API用来查询和设置getter和setter。这些API由4个方法组成，所有对象都拥有这些方法。`__lookupGetter__()`和`__lookupSetter__()`用以返回一个命名属性的getter和setter方法。`__defineGetter__()`和 `__defineSetter__()`用以定义getter和setter，这两个函数的第一个参数是属性名字，第二个参数是getter和setter方法。这4个方法都是以两条下划线作前缀，两条下划线作后缀，以表明它们是非标准的方法。本书第三部分没有对非标准的方法做介绍。

## 6.8 对象的三个属性 

每一个对象都有与之相关的原型（prototype）、类（class）和可扩展性（extensible attribute）。

### 6.8.1 原型属性

对象的原型属性时用来继承属性的。这个属性如此重要，以至于我们经常把“o的原型属性”直接叫做“o的原型”。

原型属性时在实例对象创建之初就设置好的，通过对象直接量创建的对象使用`Object.prototype`作为它们的原型。通过new创建的对象使用构造函数的prototype属性作为它们的原型。通过`Object.create()`创建的对象使用第一个参数（也可以是null）作为它们的原型。

在ECMAScript 5中，将对象作为参数传入`Object.getPrototypeOf()`可以查询它的原型。在ECMAScript 3中，则没有与之等价的函数，但经常使用表达式`o.constructor.prototype`来检测一个对象的原型。通过 new 表达式创建的对象，通常继承一个 constructor 属性，这个属性指代创建这个对象的构造函数。注意，通过对象直接量或`Object.create()`创建的对象包含一个名为 constructor 的属性，这个属性指代`Object()`构造函数。因此，`constructor.prototype`才是对象直接量的真正的原型，但对于通过`Object.create()`创建的对象则往往不是这样。

要想检测一个对象是否是另一个对象的原型（或处于原型链中），请使用`isPrototypeOf()`方法。例如，可以通过`p.isPrototypeOf(o)`来检测p是否是o的原型：

```js
var p = {x: 1};  // 一个原型对象
var o = Object.create(p);  // 使用这个原型创建一个对象
p.isPrototypeOf(o);  // =>true o继承自p
Object.prototype.isPrototypeOf(p);  // =>true p继承自Object.prototype
```

需要注意的是，`isPrototypeOf()`函数实现的功能和 instanceof 运算符非常类似。

Mozilla实现的JavaScript（包括早些年的Netscape）对外暴露了一个专门命名为`__proto__`的属性，用以直接查询/设置对象的原型。但并不推荐使用`__proto__`，因为尽管Safari和Chrome的当前版本都支持它，但IE和Opera还未实现它（可能以后也不会实现）。实现了ECMAScript 5的Firefox版本依然支持`__proto__`，但对修改不可扩展对象的原型做了限制。

### 6.8.2 类属性

对象的类属性（class attribute）是一个字符串，用以表示对象的类型信息。ECMAScript 3和ECMAScript 5都未提供设置这个属性的方法，并只有一种间接的方法可以查询它。默认的`toString()`方法（继承自Object.prototype）返回了如下这种格式的字符串：

```js
[object class]
```

因此，要想获得对象的类，可以调用对象的`toString()`方法，然后提取已返回字符串的第8个到倒数第二个位置之间的字符。不过让人感觉棘手的是，很多对象继承的`toString()`方法重写了，为了能调用正确的`toString()`版本，必须间接地调用`Function.call()`方法。例6-4中的`classof()`函数可以返回传递给它的任意对象的类：

```js
function classOf(o) {
  if (o === null) return "Null";
  if (o === undefined) return "Undefined";
  return Object.prototype.toString.call(o).slice(8, -1);
}
```

`classof()`函数可以传入任何类型的参数。数字、字符串和布尔值可以直接调用`toString()`方法，就和对象调用`toString()`方法一样，并且这个函数包含了对null和undefined的特殊处理（在ECMAScript5中不需要对这些特殊情况做处理）。通过内置构造函数（比如Array和Date）创建的对象包含“类属性”（classattribute），它与构造函数名称相匹配。宿主对象也包含有意义的“类属性”，但这和具体的JavaScript实现有关。通过对象直接量和Object.create创建的对象的类属性是“Object”，那些自定义构造函数创建的对象也是一样，类属性也是“Object”，因此对于自定义的类来说，没办法通过类属性来区分对象的类：

```js
classOf(null)  // =>"Null"
classOf(1)  // =>"Number"
classOf("")  // =>"String"
classOf(false)  // =>"Blooean"
classOf({})  // =>"Object"
classOf([])  // =>"Array"
classOf(/./)  // =>"RegExp"
classOf(new Date())  // =>"Date"
classOf(window)  // => "window"(这是客户端宿主对象)
function f() {}  // 定义一个自定义构造函数
classOf(new f())  // => "Object"
```

### 6.8.3 可扩展性

对象的可扩展性用以表示是否可以给对象添加新属性。所有内置对象和自定义对象都是显式可扩展的，宿主对象的可扩展性是由 JavaScript 引擎定义的。在ECMAScript 5中，所有的内置对象和自定义对象都是可扩展的，除非将它们转换为不可扩展的，同样，宿主对象的可扩展性也是由实现 ECMAScript 5 的 JavaScript 引擎定义的。

ECMAScript 5 定义了用来查询和设置对象可扩展性的函数。通过将对象传入`Object.isExtensible()`，来判断该对象是否是可扩展的。如果想将对象转换为不可扩展的，需要调用`Object.preventExtensions()`，将待转换的对象作为参数传进去。注意，一旦将对象转换为不可扩展的，就无法再将其转换回可扩展的了。同样需要注意的是，`preventExtensions()`只影响到对象本身的可扩展性。如果给一个不可扩展的对象的原型添加属性，这个不可扩展的对象同样会继承这些新属性。

可扩展属性的目的是将对象“锁定”，以避免外界的干扰。对象的可扩展性通常和属性的可配值性与可写性配合使用，ECMAScript 5定义的一些函数可以更方便地设置多种属性。

`Object.seal()`和`Object.preventExtensions()`类似，除了能够将对象设置为不可扩展的，还可以将对象的所有自有属性都设置为不可配置的。也就是说，不能给这个对象添加新属性，而且它已有的属性也不能删除或配置，不过它已有的可写属性依然可以设置。对于那些已经封闭（sealed）起来的对象是不能解封的。可以使用`Object.isSealed()`来检测对象是否封闭。

`Object.freeze()`将更严格地锁定对象——“冻结”（frozen）。除了将对象设置为不可扩展的和将其属性设置为不可配置的之外，还可以将它自有的所有数据属性设置为只读（如果对象的存取器属性具有setter方法，存取器属性将不受影响，仍可以通过给属性赋值调用它们）。使用`Object.isFrozen()`来检测对象是否冻结。`Object.preventExtensions()`、`Object.seal()`和`Object.freeze()`都返回传入的对象，也就是说，可以通过函数嵌套的方式调用它们：

```js
// 创建一个封闭对象，包括一个冻结的原型和一个不可枚举的属性
var o = Object.seal(Object.create(Object.freeze({x: 1}), {
  y: {value: 2, writable: true}
}));

Object.isSealed(o)  // =>true
Object.isFrozen(o)  // =>false
```

## 6.9 序列化对象

对象序列化（serialization）是指将对象的状态转换为字符串，也可将字符串还原为对象。ECMAScript 5提供了内置函数`JSON.stringify()`和`JSON.parse()`用来序列化和还原JavaScript对象。这些方法都使用JSON作为数据交换格式，JSON的全称是“JavaScript Object Notation”——JavaScript对象表示法，它的语法和JavaScript对象与数组直接量的语法非常相近：

```js
// 定义一个测试对象
o = {x: 1,y: {z: [false, null, ""]}}; 
// s是'{"x":1,"y":{"z":[false,null,""]}}'
s = JSON.stringify(o); 
// p是o的深拷贝
p = JSON.parse(s) 
```

JSON的语法是JavaScript语法的子集，它并不能表示JavaScript里的所有值。支持对象、数组、字符串、无穷大数字、true、false和null，并且它们可以序列化和还原。NaN、Infinity和-Infinity序列化的结果是null，日期对象序列化的结果是ISO格式的日期字符串（参照`Date.toJSON()`函数），但`JSON.parse()`依然保留它们的字符串形态，而不会将它们还原为原始日期对象。函数、RegExp、Error对象和undefined值不能序列化和还原。`JSON.stringify()`只能序列化对象可枚举的自有属性。对于一个不能序列化的属性来说，在序列化后的输出字符串中会将这个属性省略掉。`JSON.stringify()`和`JSON.parse()`都可以接收第二个可选参数，通过传入需要序列化或还原的属性列表来定制自定义的序列化或还原操作。

## 6.10 对象方法 

所有的JavaScript对象都从Object.prototype继承属性（除了那些不通过原型显式创建的对象）。这些继承属性主要是方法，因为JavaScript程序员普遍对继承方法更感兴趣。我们已经讨论过`hasOwnProperty()`、`propertyIsEnumerable()`和`isPrototypeOf()`这三个方法，以及在Object构造函数里定义的静态函数`Object.create()`和`Object.getPrototypeOf()`等。本节将对定义在Object.prototype里的对象方法展开讲解，这些方法非常好用而且使用广泛，但一些特定的类会重写这些方法。

### 6.10.1 toString()方法

`toString()`方法没有参数，它将返回一个表示调用这个方法的对象值的字符串。在需要将对象转换为字符串的时候，JavaScript都会调用这个方法。比如，当使用“+”运算符连接一个字符串和一个对象时或者在希望使用字符串的方法中使用了对象时都会调用`toString()`。

默认的`toString()`方法的返回值带有的信息量很少（尽管它在检测对象的类型时非常有用），例如，下面这行代码的计算结果为字符串“[object Object]”：

```js
var s = { x:1, y:1 }.toString(); //=>[object Object]
```

由于默认的`toString()`方法并不会输出很多有用的信息，因此很多类都带有自定义的`toString()`。例如，当数组转换为字符串的时候，结果是一个数组元素列表，只是每个元素都转换成了字符串，再比如，当函数转换为字符串的时候，得到函数的源代码。第三部分有关于`toString()`的详细文档说明，比如`Array.toString()`、`Date.toString()`以及`Function.toString()`。

### 6.10.2 toLocaleString()方法

除了基本的`toString()`方法之外，对象都包含`toLocaleString()`方法，这个方法返回一个表示这个对象的本地化字符串。Object中默认的`toLocaleString()`方法并不做任何本地化自身的操作，它仅调用`toString()`方法并返回对应值。Date和Number类对`toLocaleString()`方法做了定制，可以用它对数字、日期和时间做本地化的转换。Array类的`toLocaleString()`方法和`toString()`方法很像，唯一的不同是每个数组元素会调用`toLocaleString()`方法转换为字符串，而不是调用各自的`toString()`方法。

### 6.10.3 toJSON()方法

Object.prototype实际上没有定义`toJSON()`方法，但对于需要执行序列化的对象来说，`JSON.stringify()`方法会调用`toJSON()`方法。如果在待序列化的对象中存在这个方法，则调用它，返回值即是序列化的结果，而不是原始的对象。具体示例参见`Date.toJSON()`。

### 6.10.4 valueOf()方法

`valueOf()`方法和`toString()`方法非常类似，但往往当JavaScript需要将对象转换为某种原始值而非字符串的时候才会调用它，尤其是转换为数字的时候。如果在需要使用原始值的上下文中使用了对象，JavaScript就会自动调用这个方法。默认的`valueOf()`方法不足为奇，但有些内置类自定义了`valueOf()`方法（比如`Date.valueOf()`）。

# 第7章 数组

数组是值的有序集合。每个值叫做一个元素，而每个元素在数组中有一个位置，以数字表示，称为索引。JavaScript数组是无类型的：数组元素可以是任意类型，并且同一个数组中的不同元素也可能有不同的类型。数组的元素甚至也可能是对象或其他数组，这允许创建复杂的数据结构，如对象的数组和数组的数组。JavaScript数组的索引是基于零的32位数值：第一个元素的索引为0，最大可能的索引为4 294 967 294（2^32-2），数组最大能容纳4 294 967 295个元素。JavaScript数组是动态的：根据需要它们会增长或缩减，并且在创建数组时无须声明一个固定的大小或者在数组大小变化时无须重新分配空间。JavaScript数组可能是稀疏的：数组元素的索引不一定要连续的，它们之间可以有空缺。每个JavaScript数组都有一个length属性。针对非稀疏数组，该属性就是数组元素的个数。针对稀疏数组，length比所有元素的索引要大。

JavaScript数组是JavaScript对象的特殊形式，数组索引实际上和碰巧是整数的属性名差不多。我们将在本章的其他地方更多地讨论特殊化的数组。通常，数组的实现是经过优化的，用数字索引来访问数组元素一般来说比访问常规的对象属性要快很多。

数组继承自Array.prototype中的属性，它定义了一套丰富的数组操作方法。

## 7.1 创建数组

使用数组直接量是创建数组最简单的方法，在方括号中将数组元素用逗号隔开即可。例如：

```js
var empty = [];  // 没有元素的数组
var primes = [2, 3, 5, 7, 11];  // 有五个数值的数组
var misc = [ 1.1, true, "a", ];  // 三个不同类型的元素和结尾的逗号
```

数组直接量中的值不一定要是常量；它们可以是任意的表达式：

```js
var base = 1024;
var table = [base, base + 1, base + 2, base + 3]
```

它可以包含对象直接量或其他数组直接量：

```js
var b = [ [1,{x:1,y:2}], [2,{x:3,y:4}] ];
```

如果省略数组直接量中的某个值，省略的元素将被赋予undefined值：

```js
var count = [1, , 3];  // 数组中有三个元素，第二个值为undefined
var undefs = [, , ];  // 两个元素，都是undefined
```

数组直接量的语法允许有可选的结尾的逗号，故[,,]只有两个元素而非三个。调用构造函数`Array()`是创建数组的另一种方法。可以用三种方式调用构造函数。

- 调用时没有参数。该方法创建一个没有任何元素的空数组，等同于数组直接量[]。

```js
var a = new Array();
```

- 调用时有一个数值参数，它指定长度。该技术创建指定长度的数组。当预先知道所需元素个数时，这种形式的`Array()`构造函数可以用来预分配一个数组空间。注意，数组中没有存储值，甚至数组的索引属性“0”、“1”等还未定义。

```js
var a = new Array(10);
```

- 显式指定两个或多个数组元素或者数组的一个非数值元素。以这种形式，构造函数的参数将会成为新数组的元素。使用数组字面量比这样使用`Array()`构造函数要简单多了。

```js
var a = new Array(5, 4, 3, 2, 1, "testing,testing")
```

## 7.2 数组元素的读和写

使用`[]`操作符来访问数组中的一个元素。数组的引用位于方括号的左边。方括号中是一个返回非负整数值的任意表达式。使用该语法既可以读又可以写数组的一个元素。因此，如下代码都是合法的JavaScript语句：

```js
var a = ["world"];  // 从一个元素的数组开始
var value = a[0];  // 读取第0个元素
a[1] = 3.14;  // 写第1个元素
i = 2;
a[i] = 3;  // 写第2个元素
a[i + 1] = "hello";  // 写第3个元素
a[a[i]] = a[0]  // 读取第0和第2个元素，写第3个元素
```

请记住，数组是对象的特殊形式。使用方括号访问数组元素就像用方括号访问对象的属性一样。JavaScript将指定的数字索引值转换成字符串——索引值1变成“1”——然后将其作为属性名来使用。关于索引值从数字转换为字符串没什么特别之处：对常规对象也可以这么做：

```js
o = {};  // 创建一个普通的对象
o[1] = "none" ;  // 用一个整数来索引它
```

数组的特别之处在于，当使用小于2^32的非负整数作为属性名时数组会自动维护其length属性值。如上，创建仅有一个元素的数组。然后在索引1、2和3处分别进行赋值。当我们这么做时数组的length属性值变为4。

清晰地区分数组的索引和对象的属性名是非常有用的。所有的索引都是属性名，但只有在0～2^32-2之间的整数属性名才是索引。所有的数组都是对象，可以为其创建任意名字的属性。但如果使用的属性是数组的索引，数组的特殊行为就是将根据需要更新它们的length属性值。

注意，可以使用负数或非整数来索引数组。这种情况下，数值转换为字符串，字符串作为属性名来用。既然名字不是非负整数，它就只能当做常规的对象属性，而非数组的索引。同样，如果凑巧使用了是非负整数的字符串，它就当做数组索引，而非对象属性。当使用的一个浮点数和一个整数相等时情况也是一样的：

```js
a[-1.23] = true;  // 这将创建一个名为"-1.23"的属性
a["1000"] = 0;  // 这是数组的第1001个元素
a[1.000]  // 和a[1]相等
```

事实上数组索引仅仅是对象属性名的一种特殊类型，这意味着JavaScript数组没有“越界”错误的概念。当试图查询任何对象中不存在的属性时，不会报错，只会得到undefined值。类似于对象，对于对象同样存在这种情况。

既然数组是对象，那么它们可以从原型中继承元素。在ECMAScript 5中，数组可以定义元素的getter和setter方法。如果一个数组确实继承了元素或使用了元素的getter和setter方法，你应该期望它使用非优化的代码路径：访问这种数组的元素的时间会与常规对象属性的查找时间相近。

## 7.3 稀疏数组

稀疏数组就是包含从0开始的不连续索引的数组。通常，数组的length属性值代表数组中元素的个数。如果数组是稀疏的，length属性值大于元素的个数。可以用`Array()`构造函数或简单地指定数组的索引值大于当前的数组长度来创建稀疏数组。

```js
a = new Array(5);  // 数组中没有元素，但a.length值是5
a = [];  // 创建一个空数组，length的值为0
a[1000] = 0;  // 赋值添加一个元素，但设置的length值为1001
```

后面会看到你也可以用delete操作符来生产稀疏数组。

足够稀疏的数组通常在实现上比稠密的数组更慢、内存利用率更高，在这样的数组中查找元素的时间与常规对象属性的查找时间一样长。

注意，当在数组直接量中省略值时不会创建稀疏数组。省略的元素在数组中是存在的，其值为undefined。这和数组元素根本不存在是有一些微妙的区别的。可以用in操作符检测两者之间的区别：

```js
var a1 = [, , , ];  // 数组是[undefined,undefined,undefined]
var a2 = new Array(3);  // 该数组根本没有元素
0 in a1;  // =>true a1在索引0处有一个元素;
0 in a2;  // =>false a2在索引0处没有元素
```

当使用for/in循环时，a1和a2之间的区别也很明显。

需要注意的是，当省略数组直接量中的值时（使用连续的逗号，比如[1,,3]），这时所得到的数组也是稀疏数组，省略掉的值是不存在的：

```js
var a1 = [, ];  // 此时数组没有元素，长度为1
var a2 = [undefined];  // 此时数组包含一个值为undefined的元素
0 in a1;  // =>false: a1在索引0处没有元素
0 in a2;  // =>true: a2在0处有一个值为undefined的元素
```

在一些旧版本的实现中（比如Firefox 3），在存在连续逗号的情况下，插入undefined值的操作则与此不同，在这些实现中，`[1,,3]`和`[1,undefined,3]`是一模一样的。

了解稀疏数组是了解JavaScript数组的真实本质的一部分。尽管如此，实际上你所碰到的绝大多数JavaScript数组不是稀疏数组。并且，如果你确实碰到了稀疏数组，你的代码很可能像对待非稀疏数组一样来对待它们，只不过它们包含一些undefined值。

## 7.4 数组长度

每个数组有一个length属性，就是这个属性使其区别于常规的JavaScript对象。针对稠密（也就是非稀疏）数组，length属性值代表数组中元素的个数。其值比数组中最大的索引大1：

```js
[].length  // =>0:数组没有元素
['a', 'b', 'c'].length  // =>3 最大是索引为2，length为3
```

当数组是稀疏的时，length属性值大于元素的个数。而且关于此我们可以说的一切也就是数组长度保证大于它每个元素的索引值。或者，换一种说法，在数组中（无论稀疏与否）肯定找不到一个元素的索引值大于或等于它的长度。为了维持此规则不变化，数组有两个特殊的行为。第一个如同上面的描述：如果为一个数组元素赋值，它的索引i大于或等于现有数组的长度时，length属性的值将设置为i+1。

第二个特殊的行为就是设置length属性为一个小于当前长度的非负整数n时，当前数组中那些索引值大于或等于n的元素将从中删除：

```js
var a = [1, 2, 3, 4, 5];  // 从5个元素的数组开始
a.length = 3;  // 现在a为 [1, 2, 3]
a.length = 0;  // 删除所有的元素a为[]
a.length = 5;  // 长度为5，但是没有元素，就像new Array(5)
```

还可以将数组的length属性值设置为大于其当前的长度。实际上这不会向数组中添加新的元素，它只是在数组尾部创建一个空的区域。

在ECMAScript 5中，可以用`Object.defineProperty()`让数组的length属性变成只读的：

```js
var a = [1, 2, 3];
Object.defineProperty(a, "length", {writable: false});
a.length = 0;
console.log(a);  // => [1, 2, 3]
```

类似地，如果让一个数组元素不能配置，就不能删除它。如果不能删除它，length属性不能设置为小于不可配置元素的索引值。（见6.7节和6.8.3节的`Object.seal()`和`Object. freeze()`方法。）

## 7.5 数组元素的添加和删除

我们已经见过添加数组元素最简单的方法：为新索引赋值：

```js
a = [];  // 开始是一个空数组
a[0] = "zero";  // 想其中添加元素
a[1] = "one";
```

也可以使用`push()`方法在数组末尾增加一个或多个元素：

```js
a = []; //开始是空数组
a.push("zero"); //在末尾添加一个元素。 a = ["zero"]
a.push("one","two"); //再添加两个元素
```

在数组尾部压入一个元素与给数组`a[a.length]`赋值是一样的。可以使用`unshift()`方法在数组的首部插入一个元素，并且将其他元素依次移到更高的索引处。

可以像删除对象属性一样使用delete运算符来删除数组元素：

```js
a = [1, 2, 3];
delete a[1];  // a在索引1的位置不再有元素
1 in a;  // =>false：数组索引1并未在数组中定义
a.length;  // =>3: delete操作并不影响数组的长度
```

删除数组元素与为其赋undefined值是类似的（但有一些微妙的区别）。注意，对一个数组元素使用delete不会修改数组的length属性，也不会将元素从高索引处移下来填充已删除属性留下的空白。如果从数组中删除（delete）一个元素，它就变成稀疏数组。

上面我们看到，也可以简单地设置length属性为一个新的期望长度来删除数组尾部的元素。数组有`pop()`方法（它和`push()`一起使用），后者一次使减少长度1并返回被删除元素的值。还有一个`shift()`方法（它和`unshift()`一起使用），从数组头部删除一个元素。和delete不同的是`shift()`方法将所有元素下移到比当前索引低1的地方。7.8节和第三部分涵盖`pop()`和`shift()`的内容。最后，`splice()`是一个通用的方法来插入、删除或替换数组元素。它会根据需要修改length属性并移动元素到更高或较低的索引处。

## 7.6 数组遍历

使用for循环是遍历数组元素最常见的方法：

```js
var keys = Object.keys(o); //获得o对象属性名组成的数组
var values = []; //在数组中存储匹配属性的值
for (var i = 0; i < keys.length; i++) { //对于数组中的每个索引
    var key = keys[i]; //获得索引处的键值
    values[i] = o[key]; //在values数组中保存属性值
}
```

在嵌套循环或其他性能非常重要的上下文中，可以看到这种基本的数组遍历需要优化，数组的长度应该只查询一次而非每次循环都要查询：

```js
for (var i = 0, len = keys.length; i < len; i++) {
  //循环体仍然不变
}
```

这些例子假设数组是稠密的，并且所有的元素都是合法数据。否则，使用数组元素之前应该先检测它们。如果想要排除null、undefined和不存在的元素，代码如下：

```js
for (var i = 0; i < keys.length; i++) {
  if (!keys[i]) continue;  // 跳过null、undefined和不存在的元素
}
```

如果只想跳过undefined和不存在的元素，代码如下：

```js
for (var i = 0; i < keys.length; i++) {
  if (!keys[i] === undefined) continue; // 跳过undefined和不存在的元素
  // 循环体    
}
```

最后，如果只想跳过不存在的元素而仍然要处理存在的undefined元素，代码如下：

```js
for (var i = 0; i < keys.length; i++) {
  if (!(i in keys)) continue; // 跳过不存在的元素
}
```

还可以使用for/in循环（见5.5.4节）处理稀疏数组。循环每次将一个可枚举的属性名（包括数组索引）赋值给循环变量。不存在的索引将不会遍历到：

```js
for (var index in sparseArray) {
  var value = sparseArray[index];
  // 此处可使用索引和值做一些事情
}
```

在6.5节已经注意到for/in循环能够枚举继承的属性名，如添加到Array.prototype中的方法。由于这个原因，在数组上不应该使用for/in循环，除非使用额外的检测方法来过滤不想要的属性。如下检测代码取其一即可：

```js
for (var i in a) {
  if (!a.hasOwnProperty(i)) continue; // 跳过继承的属性
  // 循环体
}

for (var i in a) {
  // 跳过不是非负整数的i
  if (String(Math.floor(Math.abs(Number(i)))) !== i) continue;
}

```

ECMAScript规范允许for/in循环以不同的顺序遍历对象的属性。通常数组元素的遍历实现是升序的，但不能保证一定是这样的。特别地，如果数组同时拥有对象属性和数组元素，返回的属性名很可能是按照创建的顺序而非数值的大小顺序。如何处理这个问题的实现各不相同，如果算法依赖于遍历的顺序，那么最好不要使用for/in而用常规的for循环。

ECMAScript 5定义了一些遍历数组元素的新方法，按照索引的顺序按个传递给定义的一个函数。这些方法中最常用的就是`forEach()`方法：

```js
var data = [1, 2, 3, 4, 5];
var sumOfSquares = 0; // 得到数据的平方和
data.forEach(function(x) { // 把每个元素传递给此函数
    sumOfSquares += x * x; // 平方相加
});
sumOfSquares; // =>55: 1+4+9+16+25
```

`forEach()`和相关的遍历方法使得数组拥有简单而强大的函数式编程风格。

## 7.7 多维数组

JavaScript不支持真正的多维数组，但可以用数组的数组来近似。访问数组的数组中的元素，只要简单地使用两次`[]`操作符即可。例如，假设变量matrix是一个数组的数组，它的基本元素是数值，那么`matrix[x]`的每个元素是包含一个数值数组，访问数组中特定数值的代码为`matrix[x][y]`。这里有一个具体的例子，它使用二维数组作为一个九九乘法表：

```js
//创建一个多维数组
var table = new Array(10); //表格10行
for (var i = 0; i < table.length; i++)
  table[i] = new Array(10); //每行10列
//初始化数组
for (var row = 0; row < table.length; row++) {
  for (col = 0; col < table[row].length; col++) {
      table[row][col] = row * col;
  }
}
//使用多维数组来计算(查询)8*9
table[8][9]; //=>72
```

## 7.8 数组方法

ECMAScript3 在 Array.prototype 中定义了一些很有用的操作数组的函数，这意味着这些函数作为任何数组的方法都是可用的。

### 7.8.1 join()

`Array.join()`方法将数组中所有元素都转化为字符串并连接在一起，返回最后生成的字符串。可以指定一个可选的字符串在生成的字符串中来分隔数组的各个元素。如果不指定分隔符，默认使用逗号。如以下代码所示：

```js
var a = [1, 2, 3];
a.join(); // => "1,2,3"
a.join(" "); // => "1 2 3"  
a.join(""); // => "123"
var b = new Array(10);
b.join('-'); // => '---------'：9个连字号组成的字符串
```

`Array.join()`方法是`String.split()`方法的逆向操作，后者是将字符串分割成若干块来创建一个数组。

### 7.8.2 reverse()

`Array.reverse()`方法将数组中的元素颠倒顺序，返回逆序的数组。它采取了替换；换句话说，它不通过重新排列的元素创建新的数组，而是在原先的数组中重新排列它们。例如，下面的代码使用`reverse()`和`join()`方法生成字符串“3，2，1”：

```js
var a = [1, 2, 3];
a.reverse().join(); // => "3,2,1"，并且现在的a是[3,2,1]
```

### 7.8.3 sort()

`Array.sort()`方法将数组中的元素排序并返回排序后的数组。当不带参数调用`sort()`时，数组元素以字母表顺序排序（如有必要将临时转化为字符串进行比较）：

```js
var a = new Array("banana", "cheery", "apple");
a.sort(); // => ["apple", "banana", "cheery"]
var s = a.join("-"); // => "apple-banana-cheery"
```

如果数组包含undefined元素，它们会被排到数组的尾部。

为了按照其他方式而非字母表顺序进行数组排序，必须给`sort()`方法传递一个比较函数。该函数决定了它的两个参数在排好序的数组中的先后顺序。假设第一个参数应该在前，比较函数应该返回一个小于0的数值。反之，假设第一个参数应该在后，函数应该返回一个大于0的数值。并且，假设两个值相等（也就是说，它们的顺序无关紧要），函数应该返回0。因此，例如，用数值大小而非字母表顺序进行数组排序，代码如下：

```js
var a = [33, 4, 1111, 222, 45555];
a.sort(); // 字母表顺序：1111, 222, 33, 4, 45555
a.sort(function(a, b) { // 数值顺序：4, 33, 222, 1111, 45555
    return a - b; // 根据数据，返回负数，0，正数
});
a.sort(function(a, b) {return b - a}); // 数值大小相反的顺序
```

注意，这里使用匿名函数表达式非常方便。既然比较函数只使用一次，就没必要给它们命名了。

另外一个数组元素排序的例子，也许需要对一个字符串数组执行不区分大小写的字母表排序，比较函数首先将参数都转化为小写字符串（使用`toLowerCase()`方法），再开始比较：

```js
a = ['ant', 'Bug', 'cat', 'Dog']
a.sort(); // 区分大小写的排序 ["Bug", "Dog", "ant", "cat"]
a.sort(function(s, t) { // 不区分大小写排序
    var a = s.toLowerCase();
    var b = t.toLowerCase();
    if (a < b) return -1;
    if (a > b) return 1;
    return 0;
}); // => ["ant", "Bug", "cat", "Dog"]
```

### 7.8.4 concat()

`Array.concat()`方法创建并返回一个新数组，它的元素包括调用`concat()`的原始数组的元素和`concat()`的每个参数。如果这些参数中的任何一个自身是数组，则连接的是数组的元素，而非数组本身。但要注意，`concat()`不会递归扁平化数组的数组。`concat()`也不会修改调用的数组。下面有一些示例：

```js
var a = [1, 2, 3];
a.concat(4, 5); // => [1, 2, 3, 4, 5]
a.concat([4, 5]); // => [1, 2, 3, 4, 5]
a.concat([4, 5], [6, 7]); // => [1, 2, 3, 4, 5, 6, 7]
a.concat(4, [5, [6, 7]]); // => [1, 2, 3, 4, 5, [6,7]]
```

### 7.8.5 slice()

`Array.slice()`方法返回指定数组的一个片段或子数组。它的两个参数分别指定了片段的开始和结束的位置。返回的数组包含第一个参数指定的位置和所有到但不含第二个参数指定的位置之间的所有数组元素。如果只指定一个参数，返回的数组将包含从开始位置到数组结尾的所有元素。如参数中出现负数，它表示相对于数组中最后一个元素的位置。例如，参数-1指定了最后一个元素，而-3指定了倒数第三个元素。注意，`slice()`不会修改调用的数组。下面有一些示例：

```js
var a = [1, 2, 3, 4, 5];
a.slice(0, 3); // => [1, 2, 3]
a.slice(3); // => [4, 5]
a.slice(1, -1); // => [2, 3, 4]
a.slice(-3, -2); // => [3]
```

### 7.8.6 splice()

`Array.splice()`方法是在数组中插入或删除元素的通用方法。不同于`slice()`和`concat()`，`splice()`会修改调用的数组。注意，`splice()`和`slice()`拥有非常相似的名字，但它们的功能却有本质的区别。

`splice()`能够从数组中删除元素、插入元素到数组中或者同时完成这两种操作。在插入或删除点之后的数组元素会根据需要增加或减小它们的索引值，因此数组的其他部分仍然保持连续的。`splice()`的第一个参数指定了插入和（或）删除的起始位置。第二个参数指定了应该从数组中删除的元素的个数。如果省略第二个参数，从起始点开始到数组结尾的所有元素都将被删除。`splice()`返回一个由删除元素组成的数组，或者如果没有删除元素就返回一个空数组。例如：

```js
var a = [1, 2, 3, 4, 5, 6, 7, 8];
a.splice(4); // 返回[5, 6, 7, 8] ,a是 [1, 2, 3, 4]
a.splice(1,2) // 返回[2, 3] ,a是 [1, 4]
a.splice(1,1) // 返回[4],a是[1]
```

`splice()`的前两个参数指定了需要删除的数组元素。紧随其后的任意个数的参数指定了需要插入到数组中的元素，从第一个参数指定的位置开始插入。例如：

```js
var a = [1, 2, 3, 4, 5];
a.splice(2, 0, 'a', 'b') // 返回[]；a的值是[1, 2, "a", "b", 3, 4, 5]
a.splice(2, 2, [1, 2], 3) // 返回 ["a", "b"]
// a是[1, 2, [1,2], 3, 3, 4, 5]
```

注意，区别于`concat()`，`splice()`会插入数组本身而非数组的元素。

### 7.8.7 push()和pop()

`push()`和`pop()`方法允许将数组当做栈来使用。`push()`方法在数组的尾部添加一个或多个元素，并返回数组新的长度。`pop()`方法则相反：它删除数组的最后一个元素，减小数组长度并返回它删除的值。注意，两个方法都修改并替换原始数组而非生成一个修改版的新数组。组合使用`push()`和`pop()`能够用JavaScript数组实现先进后出的栈。例如：

```js
var stack = []; // stack:[]
stack.push(1, 2); // stack:[1,2] 返回2
stack.pop(); // stack:[1] 返回2
stack.push(3); // stack:[1,3] 返回2
stack.pop(); // stack:[1] 返回3
stack.push([4, 5]); // stack:[1,[4,5]] 返回2
stack.pop() // stack:[1] 返回[4,5]
stack.pop() // stcck:[] 返回1
```

### 7.8.8 unshift()和shift()

`unshift()`和`shift()`方法的行为非常类似于`push()`和`pop()`，不一样的是前者是在数组的头部而非尾部进行元素的插入和删除操作。`unshift()`在数组的头部添加一个或多个元素，并将已存在的元素移动到更高索引的位置来获得足够的空间，最后返回数组新的长度。`shift()`删除数组的第一个元素并将其返回，然后把所有随后的元素下移一个位置来填补数组头部的空缺。例如：

```js
var a = []; // a:[]
a.unshift(1); // a:[1] 返回1
a.unshift(22); // a:[22,1] 返回2
a.shift(); // a:[1] 返回22
a.unshift(3, [4, 5]); // a:[3,[4,5],1] 返回3
a.shift(); // a:[[4,5],1] 返回3
a.shift(); // a:[1] 返回[4,5]
a.shift(); // a:[] 返回1
```

注意，当使用多个参数调用`unshift()`时它的行为令人惊讶。参数是一次性插入的（就像splice()方法）而非一次一个地插入。这意味着最终的数组中插入的元素的顺序和它们在参数列表中的顺序一致。而假如元素是一次一个地插入，它们的顺序应该是反过来的。

### 7.8.9 toString()和toLocaleString()

数组和其他JavaScript对象一样拥有`toString()`方法。针对数组，该方法将其每个元素转化为字符串（如有必要将调用元素的`toString()`方法）并且输出用逗号分隔的字符串列表。注意，输出不包括方括号或其他任何形式的包裹数组值的分隔符。例如：

```js
[1, 2, 3].toString(); // => '1,2,3'
["a", "b", "c"].toString(); // => 'a,b,c'
[1, [2, 'c']].toString()  // => '1,2,c'
```

注意，这里与不使用任何参数调用`join()`方法返回的字符串是一样的。

`toLocaleString()`是`toString()`方法的本地化版本。它调用元素的`toLocaleString()`方法将每个数组元素转化为字符串，并且使用本地化（和自定义实现的）分隔符将这些字符串连接起来生成最终的字符串。

## 7.9 ES5中的数组方法

ECMAScript 5 定义了九个新的数组方法来遍历、映射、过滤、检测、简化和搜索数组。下面几节描述了这些方法。

但在开始详细介绍之前，很有必要对ECMAScript 5中的数组方法做一个概述。首先，大多数方法的第一个参数接收一个函数，并且对数组的每个元素（或一些元素）调用一次该函数。如果是稀疏数组，对不存在的元素不调用传递的函数。在大多数情况下，调用提供的函数使用三个参数：数组元素、元素的索引和数组本身。通常，只需要第一个参数值，可以忽略后两个参数。大多数ECMAScript 5数组方法的第一个参数是一个函数，第二个参数是可选的。如果有第二个参数，则调用的函数被看做是第二个参数的方法。也就是说，在调用函数时传递进去的第二个参数作为它的this关键字的值来使用。被调用的函数的返回值非常重要，但是不同的方法处理返回值的方式也不一样。ECMAScript 5中的数组方法都不会修改它们调用的原始数组。当然，传递给这些方法的函数是可以修改这些数组的。

### 7.9.1 forEach()

`forEach()`方法从头至尾遍历数组，为每个元素调用指定的函数。如上所述，传递的函数作为`forEach()`的第一个参数。然后`forEach()`使用三个参数调用该函数：数组元素、元素的索引和数组本身。如果只关心数组元素的值，可以编写只有一个参数的函数——额外的参数将忽略：

```js
var data = [1, 2, 3, 4, 5]; // 要求和的数组
// 计算数组的和
var sum = 0; // 初始值0
data.forEach(function(value) {
  sum += value; // 将每个值累加到sum上
});
sum; // =>15
// 给每个数组元素自加1
data.forEach(function(v, i, a) {
  a[i] = v + 1;
});
data; // => [2, 3, 4, 5, 6]
```

注意，`forEach()`无法在所有元素都传递给调用的函数之前终止遍历。也就是说，没有像for循环中使用的相应的break语句。如果要提前终止，必须把`forEach()`方法放在一个try块中，并能抛出一个异常。如果`forEach()`调用的函数抛出foreach.break异常，循环会提前终止：

```js
function foreach(a, f, t) {
  try {
    a.forEach(f, t);
  } catch (e) {
    if (e === foreach.break) return;
    else throw e;
  }
}
foreach.break = new Error("StopIteration");
```

### 7.9.2 map()

`map()`方法将调用的数组的每个元素传递给指定的函数，并返回一个数组，它包含该函数的返回值。例如：

```js
a = [1, 2, 3]
b = a.map(function(x) {
  return x * x;
});
b; //=> [1, 4, 9]
```

传递给`map()`的函数的调用方式和传递给`forEach()`的函数的调用方式一样。但传递给`map()`的函数应该有返回值。注意，`map()`返回的是新数组：它不修改调用的数组。如果是稀疏数组，返回的也是相同方式的稀疏数组：它具有相同的长度，相同的缺失元素。

### 7.9.3 filter()

`fliter()`方法返回的数组元素是调用的数组的一个子集。传递的函数是用来逻辑判定的：该函数返回true或false。调用判定函数就像调用`forEach()`和`map()`一样。如果返回值为true或能转化为true的值，那么传递给判定函数的元素就是这个子集的成员，它将被添加到一个作为返回值的数组中。例如：

```js
a = [5, 4, 3, 2, 1];
smallvalues = a.filter(function(x) {
  return x < 3
}); // => [2, 1]
everyother = a.filter(function(x, i) {
  return i % 2 == 0
}); // => [5, 3, 1]
```

注意，`filter()`会跳过稀疏数组中缺少的元素，它的返回数组总是稠密的。为了压缩稀疏数组的空缺，代码如下：

```js
var dense = sparse.filter(function() {
  return true;
});
```

甚至，压缩空缺并删除undefined和null元素，可以这样使用`filter()`：

```js
a = a.filter(function(x) {
  return x !== undefined && x != null;
});
```

### 7.9.4 every()和some()

`every()`和`some()`方法是数组的逻辑判定：它们对数组元素应用指定的函数进行判定，返回true或false。

`every()`方法就像数学中的“针对所有”的量词：当且仅当针对数组中的所有元素调用判定函数都返回true，它才返回true：

```js
var a = [1, 2, 3, 4, 5];
a.every(function(x) {return x < 10;}); // => true：所有的值都小于10
a.every(function(x) {return x % 2 === 0;}); // => fasle：不是所有的值都是偶数
```

`some()`方法就像数学中的“存在”的量词：当数组中至少有一个元素调用判定函数返回true，它就返回true；并且当且仅当数值中的所有元素调用判定函数都返回false，它才返回false：

```js
var a = [1, 2, 3, 4, 5];
a.some(function(x) {return x % 2 === 0;}); // => true：a含有偶数值
a.some(isNaN) // => false：a不包含非数值元素
```

注意，一旦`every()`和`some()`确认该返回什么值它们就会停止遍历数组元素。`some()`在判定函数第一次返回true后就返回true，但如果判定函数一直返回false，它将会遍历整个数组。`every()`恰好相反：它在判定函数第一次返回false后就返回false，但如果判定函数一直返回true，它将会遍历整个数组。注意，根据数学上的惯例，在空数组上调用时，`every()`返回true，`some()`返回false。

### 7.9.5 reduce()和reduceRight()

`reduce()`和`reduceRight()`方法使用指定的函数将数组元素进行组合，生成单个值。这在函数式编程中是常见的操作，也可以称为“注入”和“折叠”。举例说明它是如何工作的：

```js
var a = [1, 2, 3, 4, 5];
var sum = a.reduce(function(x, y) {return x + y}, 0); // 数组求和
var produce = a.reduce(function(x, y) {return x * y}, 1); // 数组求积
var max = a.reduce(function(x,y){return (x>y)?x:y;}); // 求最大值
```

`reduce()`需要两个参数。第一个是执行化简操作的函数。化简函数的任务就是用某种方法把两个值组合或化简为一个值，并返回化简后的值。在上述例子中，函数通过加法、乘法或取最大值的方法组合两个值。第二个（可选）的参数是一个传递给函数的初始值。

`reduce()`使用的函数与`forEach()`和`map()`使用的函数不同。比较熟悉的是，数组元素、元素的索引和数组本身将作为第2～4个参数传递给函数。第一个参数是到目前为止的化简操作累积的结果。第一次调用函数时，第一个参数是一个初始值，它就是传递给`reduce()`的第二个参数。在接下来的调用中，这个值就是上一次化简函数的返回值。在上面的第一个例子中，第一次调用化简函数时的参数是0和1。将两者相加并返回1。再次调用时的参数是1和2，它返回3。然后它计算3+3=6、6+4=10，最后计算10+5=15。最后的值是15，`reduce()`返回这个值。

可能已经注意到了，上面第三次调用`reduce()`时只有一个参数：没有指定初始值。当不指定初始值调用`reduce()`时，它将使用数组的第一个元素作为其初始值。这意味着第一次调用化简函数就使用了第一个和第二个数组元素作为其第一个和第二个参数。在上面求和与求积的例子中，可以省略初始值参数。

在空数组上，不带初始值参数调用`reduce()`将导致类型错误异常。如果调用它的时候只有一个值——数组只有一个元素并且没有指定初始值，或者有一个空数组并且指定一个初始值——`reduce()`只是简单地返回那个值而不会调用化简函数。

`reduceRight()`的工作原理和`reduce()`一样，不同的是它按照数组索引从高到低（从右到左）处理数组，而不是从低到高。如果化简操作的优先顺序是从右到左，你可能想使用它，例如：

```js
var a = [2, 3, 4];
// 计算2^(3^4)。乘方操作的优先顺序是从右到左
var big = a.reduceRight(function(accumlator, value) {
  return Math.pow(value, accumlator);
});
```

注意，`reduce()`和`reduceRight()`都能接收一个可选的参数，它指定了化简函数调用时的this关键字的值。可选的初始值参数仍然需要占一个位置。如果想让化简函数作为一个特殊对象的方法调用，请参看`Function.bind()`方法。

值得注意的是，上面描述的`every()`和`some()`方法是一种类型的数组化简操作。但是不同的是，它们会尽早终止遍历而不总是访问每一个数组元素。

为了简单起见，到目前位置所展示的例子都是数值的，但数学计算不是`reduce()`和`reduceRight()`的唯一意图。考虑一下例6-2中的`union()`函数。它计算两个对象的“并集”，并返回另一个新对象，新对象具有二者的属性。该函数期待两个对象并返回另一个对象，所以它的工作原理和一个化简函数一样，并且可以使用`reduce()`来把它一般化，计算任意数目的对象的“并集”。

```js
function extend(o, p) {
  for (prop in p) { // 遍历p中所有的属性
    o[prop] = p[prop]; // 将遍历属性添加至o中
  }
  return o;
}

function union(o, p) {
  return extend(extend({}, o), p);
}

var objects =[{x:1},{y:2},{z:3}];
var merged = objects.reduce(union); // => {x:1,y:2,z:3}
```

回想一下，当两个对象拥有同名的属性时，`union()`函数使用第一个参数的属性值。这样，`reduce()`和`reduceRight()`在使用`union()`时给出了不同的结果：

```js
var objects =[{x:1,a:1}, {y:2,a:2}, {z:3,a:3}]; 
var leftunion = objects.reduce(union); // => {x:1, a:3, y:2, z:3}
var rightunion = objects.reduceRight(union); // => {z:3, a:1, y:2, x:1}
```

### 7.9.6 indexOf()和lastIndexOf()

`indexOf()`和`lastIndexOf()`搜索整个数组中具有给定值的元素，返回找到的第一个元素的索引或者如果没有找到就返回-1。`indexOf()`从头至尾搜索，而`lastIndexOf()`则反向搜索。

```js
a = [0, 1, 2, 1, 0];
a.indexOf(1); // =>1：a[1]是1
a.lastIndexOf(1); // =>3：a[3]是1
a.indexOf(3) // =>-1：没有找到值为3的元素
```

不同于本节描述的其他方法，`indexOf()`和`lastIndexOf()`方法不接收一个函数作为其参数。第一个参数是需要搜索的值，第二个参数是可选的：它指定数组中的一个索引，从那里开始搜索。如果省略该参数，`indexOf()`从头开始搜索，而`lastIndexOf()`从末尾开始搜索。第二个参数也可以是负数，它代表相对数组末尾的偏移量，对于`splice()`方法：例如，-1指定数组的最后一个元素。

如下函数在一个数组中搜索指定的值并返回包含所有匹配的数组索引的一个数组。它展示了如何运用`indexOf()`的第二个参数来查找除了第一个以外匹配的值。

```js
// 在数组中查找所有出现的x，并返回一个包含匹配索引的数组
function findall(a, x) {
  var results = [], // 将会返回的数组
    len = a.length, // 待搜索数组的长度
    pos = 0; // 开始搜索的位置
  while (pos < len) { // 循环搜素多个元素...
    pos = a.indexOf(x, pos); // 搜素
    if (pos === -1) break; // 未找到，就完成搜素
    results.push(pos); // 否则，在数组中存储索引
    pos = pos + 1; // 并从下一个位置开始搜索
  }
  return results; // 返回包含索引的数组
};
```

注意，字符串也有`indexOf()`和`lastIndexOf()`方法，它们和数组方法的功能类似。

## 7.10 数组类型

我们在本章中到处都可以看见数组是具有特殊行为的对象。给定一个未知的对象，判定它是否为数组通常非常有用。在ECMAScript 5中，可以使用`Array.isArray()`函数来做这件事情：

```js
Array.isArray([]); // true
Array.isArray({}); // false
```

但是，在ECMAScript 5以前，要区分数组和非数组对象却令人惊讶地困难。typeof操作符在这里帮不上忙：对数组它返回“对象”（并且对于除了函数以外的所有对象都是如此）。instanceof操作符只能用于简单的情形：

```js
[] instanceof Array; // => true
({}) instanceof Array; // => false
```

使用instanceof的问题是在Web浏览器中有可能有多个窗口或窗体（frame）存在。每个窗口都有自己的JavaScript环境，有自己的全局对象。并且，每个全局对象有自己的一组构造函数。因此一个窗体中的对象将不可能是另外窗体中的构造函数的实例。窗体之间的混淆不常发生，但这个问题足已证明instanceof操作符不能视为一个可靠的数组检测方法。

解决方案是检查对象的类属性。对数组而言该属性的值总是“Array”，因此在ECMAScript3中`isArray()`函数的代码可以这样书写：

```js
var isArray = Function.isArray || function(o) {
  return typeof o === "object" && 
  Object.prototype.toString.call(o) === "[object Array]";
};
```

实际上，此处类属性的检测就是ECMAScript 5中`Array.isArray()`函数所做的事情。获得对象类属性的技术使用了6.8.2节和例6-4中展示的Object.prototype.toString()方法。

## 7.11 类数组对象

我们已经看到，JavaScript数组的有一些特性是其他对象所没有的：

- 当有新的元素添加到列表中时，自动更新length属性。
- 设置length为一个较小值将截断数组。
- 从Array.prototype中继承一些有用的方法。
- 其类属性为“Array”。

这些特性让JavaScript数组和常规的对象有明显的区别。但是它们不是定义数组的本质特性。一种常常完全合理的看法把拥有一个数值length属性和对应非负整数属性的对象看做一种类型的数组。

实践中这些“类数组”对象实际上偶尔出现，虽然不能在它们之上直接调用数组方法或者期望length属性有什么特殊的行为，但是仍然可以用针对真正数组遍历的代码来遍历它们。结论就是很多数组算法针对类数组对象工作得很好，就像针对真正的数组一样。如果算法把数组看成只读的或者如果它们至少保持数组长度不变，也尤其是这种情况。以下代码为一个常规对象增加了一些属性使其变成类数组对象，然后遍历生成的伪数组的“元素”：

```js
var a = {}; // 从一个常规空对象开始
// 添加一组属性，称为“类数组”
var i = 0;
while (i < 10) {
  a[i] = i * i;
  i++;
}
a.length = i;

// 现在当真正的数组遍历它
var total = 0;
for (var j = 0; j < a.length; j++)
  total += a[j];
console.log(total)
```

8.3.2节描述的Arguments对象就是一个类数组对象。在客户端JavaScript中，一些DOM方法（如`document.getElementsByTagName()`）也返回类数组对象。下面有一个函数可以用来检测类数组对象：

```js
//判定o是否是一个类数组对象
//字符串和函数都length属性，但是他们可以有typeOf检测将其排除
//在客户端javascript中，DOM文本节点也有length属性，需要用额外的o.nodetype != 3将其排除
function isArrayLike(o) {
  if (o && //o非null、undefined等
    typeof o === "object" && //o是对象
    isFinite(o.length) && //o.length是有限数
    o.length >= o && //o.length是非负数
    o.length === Math.floor(o.length) && //o.length是整数
    o.length < 4294967296) //o.length < 2^32
    return true;
  else
    return fasle; //否则它不是
}
```

将在7.12节中看到在ECMAScript 5中字符串的行为与数组类似（并且有些浏览器在ECMAScript 5之前已经让字符串变成可索引的了）。然而，类似上述的类数组对象的检测方法针对字符串常常返回false——它们通常最好当做字符串处理，而非数组。

JavaScript数组方法是特意定义为通用的，因此它们不仅应用在真正的数组而且在类数组对象上都能正确工作。在ECMAScript 5中，所有的数组方法都是通用的。在ECMAScript 3中，除了`toString()`和`toLocaleString()`以外的所有方法也是通用的。（`concat()`方法是一个特例：虽然可以用在类数组对象上，但它没有将那个对象扩充进返回的数组中。）既然类数组对象没有继承自Array.prototype，那就不能在它们上面直接调用数组方法。尽管如此，可以间接地使用Function.call方法调用：

```js
var a ={"0":"a","1":"b","2":"c",length:3}
Array.prototype.join.call(a,"+") // => "a+b+c"
Array.prototype.slice.call(a,0) // => ["a","b","c"]：真正的数组副本
Array.prototype.map.call(a.Function(x){
  return x.toUpperCase();
}) // => ["A","B","C"] 
```

在7.10节的`isArray()`方法之前我们就已经见过`call()`技术。8.7.3节涵盖关于Function对象的`call()`方法的更多内容。ECMAScript 5数组方法是在Firefox 1.5中引入的。由于它们的写法的一般性，Firefox还将这些方法的版本在Array构造函数上直接定义为函数。使用这些方法定义的版本，上述例子就可以这样重写：

```js
var a = {"0": "a","1": "b","2": "c",length: 3};
Array.join(a, "+");
Array.slice(a, 0);
Array.map(a, function(x) {
  return x.toUpperCase();
})
```

当用在类数组对象上时，数组方法的静态函数版本非常有用。但既然它们不是标准的，不能期望它们在所有的浏览器中都有定义。可以这样书写代码来保证使用它们之前是存在的：

```js
Array.join = Array.join || function(a, serp) {
  return Array.prototype.join.call(a, serp);
};
Array.slice = Array.slice || function(a, form, to) {
  return Array.prototype.slice.call(a, form, to);
};
Array.map = Array.map || function(a, f, thisArg) {
  return Array.prototype.map.call(a, f, thisArg);
};
```

## 7.12 作为数组的字符串

在ECMAScript 5（在众多最近的浏览器实现——包括IE8——早于ECMAScript5）中，字符串的行为类似于只读的数组。除了用`charAt()`方法来访问单个的字符以外，还可以使用方括号：

```js
var s = "test";
s.charAt(0); // => "t"
s[1 ;  // => "e"
```

当然，针对字符串的typeof操作符仍然返回“string”，但是如果给Array.isArray()传递字符串，它将返回false。

可索引的字符串的最大的好处就是简单，用方括号代替了`charAt()`调用，这样更加简洁、可读并且可能更高效。不仅如此，字符串的行为类似于数组的事实使得通用的数组方法可以应用到字符串上。例如：

```js
var s = "javascript"
Array.prototype.join.call(s, " "); //=>' j a v a s c r i p t'
Array.prototype.filter.call(s, function(x) { //过滤字符串中的字符
  return x.match(/[^aeiou]/); //匹配非元音字符
}).join("") //=>jvscrpt
```

请记住，字符串是不可变值，故当把它们作为数组看待时，它们是只读的。如`push()`、`sort()`、`reverse()`和`splice()`等数组方法会修改数组，它们在字符串上是无效的。不仅如此，使用数组方法来修改字符串会导致错误：出错的时候没有提示。

# 第8章 函数

函数是这样的一段 JavaScript 代码，它只定义一次，但可能被执行或调用任意次。 JavaScript 函数是参数化的：函数的定义会包括一个称为形参（parameter）的标识符列表，这些参数在函数体中像局部变量一样工作。函数调用会为形参提供实参的值。函数使用它们实参的值来计算返回值，成为该函数调用表达式的值。除了实参之外，每次调用还会拥有另一个值——本次调用的上下文——这就是 this 关键字的值。

如果函数挂载在一个对象上，作为对象的一个属性，就称它为对象的方法。当通过这个对象来调用函数时，该对象就是此次调用的上下文（context），也就是该函数的 this 的值。用于初始化一个新创建的对象的函数称为构造函数（constructor）。

在 JavaScript 里，函数即对象，程序可以随意操控它们。比如， JavaScript 可以把函数赋值给变量，或者作为参数传递给其他函数。因为函数就是对象，所以可以给它们设置属性，甚至调用它们的方法。

JavaScript 的函数可以嵌套在其他函数中定义，这样它们就可以访问它们被定义时所处的作用域中的任何变量。这意味着 JavaScript 函数构成了一个闭包（closure），它给 JavaScript 带来了非常强劲的编程能力。

> 参数有形参和实参的区别，形参相当于函数中定义的变量，实参是在运行时的函数调用时传入的参数。

## 8.1 函数定义 

函数使用 function 关键字来定义，它可以用在函数定义表达式或者函数声明语句里。在两种形式中，函数定义都从 function 关键字开始，其后跟随这些组成部分：

- 函数名称标识符。函数名称是函数声明语句必需的部分。它的用途就像变量的名字，新定义的函数对象会赋值给这个变量。对函数定义表达式来说，这个名字是可选的：如果存在，该名字只存在于函数体中，并指代该函数对象本身。
- 一对圆括号，其中包含由0个或者多个用逗号隔开的标识符组成的列表。这些标识符是函数的参数名称，它们就像函数体中的局部变量一样。
- 一对花括号，其中包含0条或多条 JavaScript 语句。这些语句构成了函数体：一旦调用函数，就会执行这些语句。

注意，以表达式来定义函数只适用于它作为一个大的表达式的一部分，比如在赋值和调用过程中定义函数：

```js
//定义javascript函数
//输出o的每个属性的名称和值，返回undefined
function printprops(o) {
  for (p in o)
    console.log(p + ":" + o[p] + "\n")
}

//计算两个迪卡尔坐标（x1,y1）和(x2,y2)之间的距离
function distance(x1, y1, x2, y2) {
  var dx = x2 - x1;
  var dy = y2 - y1;
  return Math.sqrt(dx * dx + dy * dy)
}

//计算递归函数（调用自身的函数）
//x!的值是从x到x递减（步长为1）的值的累乘
function factorial(x) {
  if (x <= 1) return 1;
  return x * factorial(x - 1);
}

//这个函数表达式定义了一个函数用来求传入参数的平方
//注意我们把它赋值了给一个变量
var square = function(x) {
  return x * x
}

//函数表达式可以包含名称，这在递归时很有用
var f = function fact(x) {
  if (x <= 1) return 1;
  else return x * fact(x - 1);
};

//函数表达式也可以作为参数传给其它函数
data.sort(function(a, b) {
  return a - b;
});

//函数表达式有时定义后立即使用
var tensquared = (function(x) {
  return x * x;
}(10))
```

注意：以表达式方式定义的函数，函数的名称是可选的。一条函数声明语句实际上声明了一个变量，并把一个函数对象赋值给它。相对而言，定义函数表达式时并没有声明一个变量。函数可以命名，就像上面的阶乘函数，它需要一个名称来指代自己。如果一个函数定义表达式包含名称，函数的局部作用域将会包含一个绑定到函数对象的名称。实际上，函数的名称将成为函数内部的一个局部变量。通常而言，以表达式方式定义函数时都不需要名称，这会让定义它们的代码更为紧凑。函数定义表达式特别适合用来定义那些只会用到一次的函数，比如上面展示的最后两个例子。

> 函数名称通常是动词或以动词为前缀的词组。通常函数名的第一个字符为小写，这是一种编程约定。当函数名包含多个单词时，一种约定是将单词以下划线分隔，就像`like_this()`。还有另外一种约定，就是除了第一个单词之外的单词首字母使用大写字母，就像`likeThis()`。有一些函数是用做内部函数或私有函数（不是作为公用API的一部分），这种函数名通常以一条下划线为前缀。

> 在一些编程风格中，或者编程框架里，通常为那些经常调用的函数指定短名称，比如客户端JavaScript框架jQuery就将最常用的方法重命名为`$()`（一个美元符号）（美元符号和下划线是除了字母和数字之外的两个合法的JavaScript标识符）。

函数声明语句“被提前”到外部脚本或外部函数作用域的顶部，所以以这种方式声明的函数，可以被在它定义之前出现的代码所调用。不过，以表达式定义的函数就另当别论了，为了调用一个函数，必须要能引用它，而要使用一个以表达式方式定义的函数之前，必须把它赋值给一个变量。变量的声明提前了，但给变量赋值是不会提前的，所以，以表达式方式定义的函数在定义之前无法调用）。

大多数函数（但不是全部）包含一条 return 语句。 return 语句导致函数停止执行，并返回它的表达式（如果有的话）的值给调用者。如果 return 语句没有一个与之相关的表达式，则它返回 undefined 值。如果一个函数不包含 return 语句，那它就只执行函数体中的每条语句，并返回 undefined 值给调用者。

**嵌套函数**

在 JavaScript 里，函数可以嵌套在其他函数里。

```js
function hyuse(a, b) {
  function square(x) {
    return x * x
  }
  return Math.sqrt(square(a) + square(b));
}
```

嵌套函数的有趣之处在于它的变量作用域规则，它们可以访问嵌套它们（或多重嵌套）的函数的参数和变量。

函数声明语句并非真正的语句， ECMAScript 规范只是允许它们作为顶级语句。它们可以出现在全局代码里，或者内嵌在其他函数中，但它们不能出现在循环、条件判断，或者`try/catch/finally`以及`with`语句中。注意，此限制仅用于以语句声明形式定义的函数。函数定义表达式可以出现在 JavaScript 代码的任何地方。

## 8.2 函数调用 

构成函数主体的 JavaScript 代码在定义之时并不会执行，只有调用该函数时，它们才会执行。有4种方式来调用 JavaScript 函数：

1. 作为函数
2. 作为方法
3. 作为构造函数
4. 通过它们的`call()`和`apply()`方法间接调用

### 8.2.1 函数调用

使用调用表达式可以进行普通的函数调用也可进行方法调用。一个调用表达式由多个函数表达式组成，每个函数表达式都是由一个函数对象和左圆括号、参数列表和右圆括号组成，参数列表是由逗号分隔的零个或多个参数表达式组成。如果函数表达式是一个属性访问表达式，即该函数是一个对象的属性或数组中的一个元素，那么它就是一个方法调用表达式。

```js
printprops({x: 1});
var total = distance(0,0,2,1) + distance(2,2,3,5);
var probality = factorial(5) / factorial(13);
```

在一个调用中，每个参数表达式（圆括号之间的部分）都会计算出一个值，计算的结果作为参数传递给另外一个函数。这些值作为实参传递给声明函数时定义的形参。

对于普通的函数调用，函数的返回值称为调用表达式的值。如果该函数返回时因为解释器达到结尾，返回值就是 undefined 。如果函数返回时因为解释器执行到一条 return 语句，返回值就是 return 之后的表达式的值。如果 return 语句没有值，则返回 undefined 。

根据 ECMAScript3 和非严格的 ECMAScript5 对函数调用的规定，调用上下文（this的值）是全局对象。然而，在严格模式下，调用上下文则是 undefined 。以函数形式调用的函数通常不使用 this 关键字。不过，“this”可以用来判断当前是否是严格模式。

```js
var strict= (function(){return !this;}());
```

### 8.2.2 方法调用

一个方法无非是个保存在一个对象的属性里的 JavaScript 函数。如果有一个函数 f 和一个对象 o ，则可以用下面的代码给 o 定义一个名为`m()`的方法。

```js
o.m = f;
```

给对象 o 定义了方法`m()`调用它时就像这样：

```js
o.m();

// 需要实参的调用
o.m(x, y);
```

上面的代码是一个调用表达式：它包括一个函数表达式 o.m ，以及两个实参表达式 x 和 y ，函数表达式本身就是一个属性访问表达式，这意味着该函数被当作一个方法，而不是作为一个普通函数来调用。

对方法调用的参数和返回值的处理，和上面所描述的普通函数调用完全一致。但是，方法调用和函数调用有一个重要的区别，就是调用上下文。属性访问表达式由两部分组成，一个对象（本例中的 o ）和属性名称（m）。在像这样的方法调用表达式里，对象 o 成为调用上下文，函数体可以使用关键字 this 引用该对象。

```js
var calcul = { //对象直接量
  oprand1: 1,
  oprand2: 1,
  add: function() {
    //注意this关键字的用法，this指带当前对象
    return this.result = this.oprand1 + this.oprand2;
  }
};
calcul.add(); //这个方法调用计算1+1的结果
calcul.result; //=>2
```

大多数方法调用使用点符号来访问属性，使用方括号也可以进行属性访问操作。

```js
o["m"](x, y) //o.m(x,y)的另外一种写法
a[0](z)//同样是一个方法调用(这里假设a[0]是一个函数)
```

方法调用可能包括更复杂的属性访问表达式

```js
customer.surname.toUpperCase(); //调用customer.surname方法
f().m(); //在f()调用结束后继续调用返回值中的方法m()
```

方法和 this 关键字是面向对象编程范例的核心。任何函数只要作为方法调用实际上都会传入一个隐式的实参——这个实参是一个对象，方法调用的母体就是这个对象。通常来讲，基于那个对象的方法可以执行多种操作，方法调用的语法已经很清晰地表明了函数将基于一个对象进行操作

```js
rect.setSize(windth, height);
setrectSize(rect, width, heigth);
```

当方法的返回值是一个对象，这个对象还可以再调用它的方法。这种方法调用序列中（通常称为“链”或者“级联”）每次的调用结果都是另外一个表达式的组成部分。比如，基于jQuery库，我们常常会这样写代码：

```js
//找到所有的header，取得他们的id的映射，转换为数组并给它们进行排序
$(":header").map(function(){return this.id}).get().sort();
```

需要注意的是， this 是一个关键字，不是变量，也不是属性名。 JavaScript 的语法不允许给 this 赋值。

和变量不同，关键字 this 没有作用域的限制，嵌套的函数不会从调用它的函数中继承 this 。如果嵌套函数作为方法调用，其 this 的值指向调用它的对象。如果嵌套函数作为函数调用，其 this 值不是全局对象（非严格模式下）就是undefined（严格模式下）。很多人误以为调用嵌套函数时 this 会指向调用外层函数的上下文。如果你想访问这个外部函数的 this 值，需要将 this 的值保存在一个变量里，这个变量和内部函数都同在一个作用域内。通常使用变量 self 来保存 this ，比如：

```js
var o = { //对象o
  m: function() { //对象中的方法m()
    var self = this; //将this的值保存在一个变量中
    console.log(this === o); //输出true，this就是这个对象o
    f(); //调用辅助函数f()

    function f() { //定义一个嵌套函数f()
      console.log(this === o); //"false":this的值是全局对象undefied
      console.log(self === o); //"true": slef指外部函数this的值
    }
  }
};
o.m();//调用对象o的方法m
```

### 8.2.3 构造函数调用

如果函数或者方法调用之前带有关键字 new ，它就构成构造函数调用。构造函数调用和普通的函数调用以及方法调用在实参处理、调用上下文和返回值方面有所不同。

如果构造函数调用在圆括号内包含一组实参列表，先计算这些实参表达式，然后传入函数内，这和函数调用和方法调用是一致的。但如果构造函数没有形参， JavaScript 构造函数的语法是允许省略实参列表和圆括号的。凡事没有形参的构造函数调用都可以省略括号。

```js
var o = Object();
// 等价
var o = Object;
```

构造函数调用创建一个新的空对象，这个对象继承来自构造函数的 prototype 属性。构造函数视图初始化这个新创建的对象，并将这个对象用作其调用上下文，因此构造函数可以使用 this 关键字来引用这个新创建的对象。注意，尽管构造函数看起来像一个方法调用，它仍然会使用这个新对象作为调用上下文，也就是说，在表达式`new o.m()`中，调用上下文并不是 o 。

构造函数通常不使用 return 关键字，它们通常初始化新对象，当构造函数的函数体执行完毕时，它会显式返回。在这种情况下，构造函数调用表达式的计算结果就是这个新对象的值。然而如果构造函数显式地使用 return 语句返回一个对象，那么调用表达式的值就是这个对象。如果构造函数使用 return 语句但没有指定返回值，或者返回一个原始值，那么这时将忽略返回值，同时使用这个新对象作为调用结果。

### 8.2.4 间接调用

JavaScript 中的函数也是对象，和其他 JavaScript 对象没什么两样，函数对象也可以包含方法。其中的两个方法`call()`和`apply()`可以用来间接地调用函数。两个方法都允许显式指定调用所需的 this 值，也就是说，任何函数可以作为任何对象的方法来调用，哪怕这个函数不是那个对象的方法。两个方法都可以指定调用的实参。`call()`方法使用它自有的实参列表作为函数的实参，`apply()`方法则要求以数组的形式传入参数。

## 8.3 函数的实参和形参 

JavaScript 中的函数定义并未指定函数形参的类型，函数调用也未对传入的实参值做任何类型检查。实际上， JavaScript 函数调用甚至不检查形参的个数。

### 8.3.1 可选形参

当调用函数的时候传入的实参比函数声明指定的形参个数要少，剩下的形参都将设置为 undefined 值。因此在调用函数时形参是否可选以及是否可以省略应当保持好的适应性。为了做到这一点，应当给省略的参数赋一个合理的默认值。

```js
//将对象o中的可枚举属性名追加到数组a中，并返回这个数组a
//如果省略a，则创建一个新数组并返回这个新数组
function getPropertyNames(o, /*optional*/ a) {
    if (a === undefined) a = []; //如果a未定义，则使用新数组
    for (var property in o) a.push(property);
    return a;
}

//这个函数调用时可以使用两个实参
getPropertyNames(xx); //将o的属性存储到一个新的数组中
getPropertyNames(xx, zz); //将p的属性追加到数组a中
```

如果在第一行代码中不使用 if 语句，可以使用“||”运算符，这是一个钟习惯用法。

```js
a = a || [];
```

需要注意的是，当用这种可选实参来实现函数时，需要将可选实参放在实参列表的最后，那些调用你的函数的程序员是没办法省略第一个实参并传入第二个实参的，它必须将 undefined 作为第一个实参显式传入。

### 8.3.2 可变长的实参列表：实参对象

当调用函数的时候传入的实参个数超过函数定义时，没有办法直接获得未命名值的引用。参数对象解决了这个问题。在函数体内，标识符 arguments 是指向实参对象的引用，实参对象是一个类数组对象，这样可以通过数字下标就能访问传入函数的实参值，而不用非要通过名字来得到实参。

此外，和真正的数组一样， arguments 也包含一个 length 属性，用以标识其所包含元素的个数。

实参对象在很多地方都非常有用，下面的例子展示了使用它来验证实参的个数。需要注意的是，通常不必像这样检查实参个数。大多数情况下 JavaScript 的默认行为是可以满足需要的：省略的实参都是 undefined ，多出的参数会自动省略。

```js
function f(x, y, z) {
    //首先验证传入实参的个数是否正确
    if (arguments.leng != 3) {
        throw new Error("function f() called with" + arguments.length + "arguments,but it ecxpects 3 arguments");
    }
    //再执行函数的其它逻辑
}
```

实参对象有一个重要的用处，就是让函数可以操作任意数量的实参。下面的函数就可以接收任意数量的实参，并返回传入实参的最大值（内置函数`Math.max()`的功能与之类似）。类似这种函数可以接收任意个数的实参，这种函数也称为“不定实参函数”（varargs function）。

```js
function max( /*...*/ ) {
    var max = Number.NEGATIVE_INFINITY;
    //遍历实参，查找并记住最大值
    for (var i = 0; i < arguments.length; i++)
        if (arguments[i] > max) max = arguments[i];
        //返回最大值
    return max;
}
max(1, 10, 222, 100); //=>222
```

注意，不定实参函数的实参个数不能为零，`arguments[]`对象最适合的应用场景是在这样一类函数中，这种函数包含固定个数的命名和必须参数，以及随后个数不定的可选实参。

数组对象包含一个非同寻常的特性。在非严格模式下，当一个函数包含若干形参，实参对象的数组元素时函数形参所对应实参的别名，实参对象中以数字索引，并且形参名称可以认为是相同变量的不同命名。通过实参名字来修改参数值的话，通过`arguments[]`数组也可以获取到更改后的值。

```js
function f(x) {
    console.log(x); //输出实参的初始值
    arguments[0] = null; //修改实参组的元素同样会修改x的内容
    console.log(x); //输“null”
}
f(11);
```

在 ECMAScript 5 中移除了实参对象的这个特殊特性。再严格模式中，它变成了一个保留字。严格模式中的函数无法使用 arguments 作为形参名或局部变量名，也不能给 arguments 赋值。

**callee和caller属性**

除了数组元素，实参对象还定义了 callee 和 caller 属性。在 ECMAScript 5 严格模式中，对这两个属性的读写操作都会产生一个类型错误。而在非严格模式下， ECMAScript标准规定 callee 属性指代当前正在执行的函数。 caller是非标准的，但大多数浏览器实现了这个属性，它指代调用当前正在执行的函数的函数。通过 caller 属性可以访问调用栈。callee 属性在某些时候会非常有用，比如在匿名函数中通过 callee 来递归地调用自身。

```js
var factorial = function(x) {
    if (x <= 1) return 1;
    return x * arguments.callee(x - 1);
}
```

### 8.3.3 将对象属性用作实参

当一个函数包含超过三个形参时，要记住调用函数中实参的正确顺序比较困难，最好通过名/值对的形式来传入参数。为了实现这种风格的方法调用，定义函数的时候，传入的实参都写入一个单独的对象之中，在调用的时候传入一个对象，对象中的名/值是真正需要的实参数据。

```js
//将原始值数组的length元素复制至目标数组
//开始复制原始数组的from_start元素
//并且将其复制到目标数组to_start中
//要记住实现的顺序并不容易
function arrayCopy( /*array*/ from, /*index*/ from_start, 
                    /*array*/ to, /*index*/ to_start, 
                    /*integer*/ length) {
  //逻辑代码
}
//这个版本的实现效率有些低，但你不必再记住实参的顺序
//并且from_start和to_start都默认为0
function easyCopy(args) {
  arrayCopy(args.form,
    args.form_start || 0, //注意，这里设置了默认值
    args.to,
    args.to_start || 0, args.length);
}
//来看如何调用easyCopy
var a = [1, 2, 3, 4],
    b = [];
easyCopy({
  from: a,
  to: b,
  length: 4
});
```

### 8.3.4 实参类型

JavaScript 方法的形参并未声明类型，在形参传入函数体之前也未做任何类型检查。

应当添加类似的实参类型检查逻辑，宁愿程序在传入非法值时报错，也不愿非法值导致程序在执行时报错。

```js
//判定o是否是一个类数组对象
//字符串和函数都length属性，但是他们可以有typeOf检测将其排除
//在客户端javascript中，DOM文本节点也有length属性，需要用额外的o.nodetype != 3将其排除
function isArrayLike(o) {
  if (o && //o非null、undefined等
    typeof o === "object" && //o是对象
    isFinite(o.length) && //o.length是有限数
    o.length >= o && //o.length是非负数
    o.length === Math.floor(o.length) && //o.length是整数
    o.length < 4294967296) //o.length < 2^32
    return true;
  else
    return fasle; //否则它不是
}

//返回数组（或类数组对象）a的元素累加和
//数组a中必须为数字/ null undefined的元素都将忽略
function sum(a) {
  if (isArrayLike(a)) {
    var total = 0;
    for (var i = 0; i < a.length; i++) { //遍历所有元素
      var element = a[i];
      if (element == null) continue; //跳过null和undefiend
      if (isFinite(element)) total += element;
      else throw new Error("sum():elements must be a finte numbers");
    }
    return total;
  } else throw new Error("sun():arguments mustbe array-like")
};

a = [1,2,4,5,3,6,7];
sum(a)
```

JavaScript 是一种非常灵活的弱类型语言，有时适合编写实参类型和实参个数的不确定性的函数。接下来的`flexisum()`方法就是这样。它可以接收任意数量的实参，并可以递归地处理实参是数组的情况。

```js
function flexisum(a) {
  var total = 0;
  for (var i = 0; i < arguments.length; i++) {
    var element = arguments[i],
        n;
    if (element == null) continue; //忽略null和undefined
    if (isArray(element)) //如果实参是数组
      n = flexisum.apply(this, element); //递归的计算累加和
    else if (typeof element === "function") //否则，如果是函数...
      n = Number(element()); //调用它并做类型抓换
    else
      n = Number(element); //直接做类型抓换
    if (isNaN(n)) //如果无法转换为数字，则抛出异常
      throw Error("flexisum():can nont convent" + element + "to number");
    total += n; //否则，将n累加到total
  }
  return total;
}
```

## 8.4 作为值的函数 

函数可以定义，也可以调用，这是函数最重要的特性。在 JavaScript 中，函数不仅是一种语法，也是值，也就是说，可以将函数赋值给变量，存储在对象的属性或数组的元素中，作为参数传入另外一个函数等。

```js
function square(x) {
  return x * x
}
var s = square; //现在s和sqare指代同一个函数
square(4); //=>16
s(4); //=>16
```

除了可以将函数赋值给变量，同样可以将函数赋值给对象的属性。当函数作为对象的属性调用时，函数就成为方法。

```js
var o = {
  square: function(x) {
    return x * x
  }
}; //对象直接量
var y = o.square(16);
```

函数甚至不需要名字，当把它们赋值给数组元素时。

```js
var a = [
  function(x) {return x * x},
  20
];
console.log(a[0](a[1])) //=>400
```

**自定义函数属性**

JavaScript 中的函数并不是原始值，而是一种特殊的对象，也就是说，函数可以拥有属性。

比如，想写一个返回一个唯一整数的函数，不管在哪里调用函数都会返回这个整数。而函数不能两次返回同一个值。因为这个信息仅仅是函数本身用到的。最好将这个信息保存到函数对象的一个属性中。

```js
//初始化函数对象的计数器属性
//由于函数声明被提前了，因此这个是可以在函数声明
//之前给它的成员赋值的
unInterger.counter = 0;

//每次调用这个函数都会返回一个不同的整数
//它使用一个属性来记住下一次将要返回的值
function unInterger() {
  unInterger.counter++  ; //先返回计数器的值，然后计数器自增1
}
```

下面这个函数`factorrial()`使用了自身的属性（将自身当作数组来对象）来缓存上一次的计算结果。

```js
//计算阶乘，并将结果缓存在函数的属性中
function factorrial(n) {
  if (isFinite(n) && n > 0 && n == Math.round(n)) { //有限的正整数
    if (!(n in factorrial)) //如果没有缓存结果
      factorrial[n] = n * factorrial(n - 1); //计算并缓存之
    return factorrial[n];
  } else return NaN; //如果输入有误
}
factorrial[1] = 1; //初始化缓存以保存这种基本情况
console.log(factorrial())
```

## 8.5 作为命名空间的函数 

在函数中声明的变量在整个函数体内都是可见的（包括在嵌套的函数中），在函数的外部是不可见的。不再任何函数内声明的变量是全局变量，在整个 JavaScript 程序中都是可见的。在 JavaScript 中是无法声明在一个代码块内可见的变量的，基于这个原因，可以简单地定义一个函数用作临时的命名空间，在这个命名空间内定义的变量都不会污染到全局命名空间。

```js
function mymodule() {
  // 模块代码
  // 这个模块所有使用的所有变量是局部变量
  // 而不是污染全局命名空间
}
mymodule(); // 不要忘了还要调用的这个函数
```

这段代码仅仅定义了一个单独的全局变量：名为“mymodule”的函数。这样还是太麻烦，可以直接定义一个匿名函数，并在某个表达式中调用它。

```js
(function() { //mymodule函数重写为匿名函数表达式
  //模块代码
}()); //结束函数定义并立即调用它
```

## 8.6 闭包 

和其他大多数现代编程语言一样， JavaScript 也采用词法作用域（lexical scoping），也就是说，函数的执行依赖于变量作用域，这个作用域是在函数定义时决定的，而不是函数调用时决定的。为了实现这种词语作用域， JavaScript 函数对象的内部状态不仅包含函数的代码逻辑，还必须引用当前的作用域链。函数对象可以通过作用域链相互关联起来，函数体内部的变量都可以保存在函数作用域内，这种特性在计算机科学文献中被称为“闭包”。

从技术的角度讲，所有的 JavaScript 函数都是闭包，它们都是对象，它们都关联到作用域链。定义大多数函数时的作用域链在调用函数时依然有效，但这并不影响闭包。当一个函数嵌套了另一个函数，外部函数将嵌套的函数对象作为返回值返回的时候，往往会发生这种事情：调用函数时闭包所指向的作用域链和定义函数时的作用域链不是同一个作用域链。有很多强大的编程技术都利用到了这类嵌套的函数闭包，以至于这种编程模式在 JavaScript 中非常常见。

理解闭包首先要了解嵌套函数的词法作用域规则。

```js
var scope = "global scope"; //全局变量
function checkscope() {
  var scope = "local scope"; //局部变量
  function f() {
    return console.log(scope);
  } //在作用域中返回这个值
  return f();
}
checkscope(); // => local scope
```

将函数体内的一对圆括号移动到了`checkscope()`之后。`checkscope()`现在仅仅返回函数体内嵌套的一个函数对象，而不是直接返回结果。在定义函数的作用域外面，调用这个嵌套的函数（包含最后一行代码的最后一对圆括号）会发生什么事情呢？

```js
var scope = "global scope"; //全局变量
function checkscope() {
  var scope = "local scope"; //局部变量
  function f() {
    return console.log(scope);
  } //在作用域中返回这个值
  return f;
}
checkscope()(); // 返回值是什么？
```

回顾一下词法作用域链的基本规则： JavaScript 函数的执行涉及到作用域链，这个作用域链是函数定义的时候创建的。嵌套的函数`f()`定义在这个作用域链里，其中的变量 scope 一定是局部变量，不管在何时何地执行函数`f()`，这种绑定在执行`f()`时依然有效，因此最后一行代码返回“local scope”。简言之，闭包的这个特性强大到让人吃惊：它们可以捕捉到局部变量（和参数），并一直保存下来，看起来像这些变量绑定到了在其中定义它们的外部函数。

> 实现闭包。函数定义时的作用域链到函数执行时依然有效。往往我们觉得在外部函数中定义的局部变量在函数返回后就不存在了，那么嵌套的函数如何能调用不存在的作用域链呢？但其实这是错的。  
我们将作用域链描述为一个对象列表，不是绑定的栈。每次调用 JavaScript 函数的时候，都会为之创建一个新的对象用来保存局部变量，把这个对象添加至作用域链中。当函数返回的时候，就从作用域链中将这个绑定变量的对象删除。如果不存在嵌套的函数，也没有其他引用指向这个绑定对象，它就会被当作垃圾回收掉。如果定义了嵌套的函数，每个嵌套函数都各自对应一个作用域链，并且这个作用域链指向一个变量绑定对象。如果这些嵌套的函数对象在外部函数中保存下来，那么它们也会和所指向的变量绑定对象一样当作垃圾回收。但是，如果这个函数定义了嵌套的函数，并将它作为返回值返回或者存储在某处的属性里，这时就会有一个外部引用指向这个嵌套的函数。它就不会被当作垃圾回收，并且它所指向的变量绑定对象也不会被当作垃圾回收。

在 8.4.1 节中定义了`uniqueInteger()`函数，这个函数使用自身的一个属性来保存每次返回的值，以便每次调用都能跟踪上次的返回值。但这种做法有一个问题，就是恶意代码可能将计数器重置或者把一个非整数赋值给它，导致该函数不一定能产生唯一的整数。而闭包可以捕捉到单个函数调用的局部变量，并将这些局部变量用作私有状态。

```js
var uniqueInteger = (function() { //定义函数并立即调用
    var counter = 0; //函数的私有状态
    return function() {
      return counter++;
    };
}());
```

实际上，这段代码定义了一个立即调用的函数（函数的开始带有左圆括号），因此是这个函数的返回值赋值给变量 uniqueInteger 。现在，我们来看函数体，这个函数返回另外一个函数，这是一个嵌套的函数，我们将它赋值给变量 uniqueInteger ，嵌套的函数是可以访问作用域内的变量的，而且可以访问外部函数中定义的 counter 变量。当外部函数返回之后，其他任何代码都无法访问 counter 变量，只有内部的函数才能访问到它。

像 counter 一样的私有变量不是只能用在一个单独的闭包内，在同一个外部函数内定义的多个嵌套函数也可以访问它，这多个嵌套函数都共享一个作用域链。

```js
function counter(){
  var n =0;
  return{
    count: function(){ return n++; },
    reset: function(){ n = 0; }
  };
}
var c = counter(), d = counter(); // 创建两个计数器
console.log(c.count())  // =>0
console.log(d.count())  // =>0：它们互不干扰
c.reset()  // reset()和count方法共享状态
console.log(c.count())  // =>0：因为我们重置了c
console.log(d.count())  // =>1：我们没有重置d
```

从技术角度看，其实可以将这个闭包合并为属性存取器方法 getter 和 seter 。下面这段代码所示的`counter()`函数的版本是6.6节中代码的变种，所不同的是，这里私有状态的实现是利用了闭包，而不是利用普通的对象属性来实现：

```js
function counter(n) { // 函数参数n是一个私有变量
  return {
    // 属性getter方法返回并给私有计数器var递增1
    get count() {
      return n++;
    },
    // 属性setter方法不允许n递减
    set count(m) {
      if (m >= n) n = m;
      else throw Error("count can only be set to a larger value");
    }
  };
}
var c = counter(1000);
console.log(c.count) //=>1000
console.log(c.count) //=>1001

c.count = 2000
console.log(c.count) //=>2000
console.log(c.count) //=>2001

c.count = 2000 //Error
```

需要注意的是，这个版本的`counter()`函数并未声明局部变量，而只是使用参数n来保存私有状态，属性存取器方法可以访问n。这样的话，调用`counter()`的函数就可以指定私有变量的初始值了。

在同一个作用域链中定义两个闭包，这两个闭包共享同样的私有变量或变量。这是一种非常重要的技术，但还是要特别小心那些不希望共享的变量往往不经意间共享给了其他的闭包。

```js
// 这个函数返回一个总是返回v的函数
function constfunc(v) {
  return function() { 
    return v; 
  }
};

// 创建一个数组用来常数函数
var funcs = [];
for (var i = 0; i < 10; i++) {
  funcs[i] = constfunc(i);
}

// 在第5个位置的元素所表示的函数返回值为5
funcs[5]() // => 5
```

这段代码利用循环创建了很多个闭包，当写类似这种代码的时候往往会犯一个错误，那就是试图将循环代码移入定义这个闭包的函数之内。

```js
// 返回一个函数组成的数组，它们的返回值是0-9
function constfuncs() {
  var funcs = [];
  for (var i = 0; i < 10; i++)
    funcs[i] = function() {
      return i;
    };
  return funcs;
}

var funcs = constfuncs();
console.log(funcs[5]()) // 10
```

上面这段代码创建了10个闭包，并将它们存储到一个数组中。这些闭包都是在同一个函数调用中定义的，因此它们可以共享变量i。当`constfuncs()`返回时，变量i的值是10，所有的闭包都共享这一个值，因此，数组中的函数的返回值都是同一个值，这不是我们想要的结果。关联到闭包的作用域链都是“活动的”，记住这一点非常重要。嵌套的函数不会将作用域内的私有成员复制一份，也不会对所绑定的变量生成静态快照（static snapshot）。

书写闭包的时候还需要注意一件事情， this 是 JavaScript 的关键字，而不是变量。正如之前讨论得，每个函数调用都包含一个 this 值，闭包是不可以访问在外部函数里的 this 值的，除非外部函数将 this 转存为一个变量。

```js
// 将this保存到一个变量中，以便嵌套的函数能够访问它
var self = this; 
```

绑定 arguments 的问题与之类似， arguments 并不是一个关键字，但在调用每个函数时都会自动声明它，由于闭包具有自己所绑定的 arguments ，因此闭包内无法直接访问外部函数的参数数组，除非外部函数将参数数组保存到另外一个变量中。

```js
// 保存起来以便嵌套的函数能使用它
var outerArguments = arguments; 
```

在本章接下来讲到的例8-5中就利用了这种编程技巧来定义闭包，以便在闭包中可以访问外部函数的this和arguments值。

## 8.7 函数属性、方法和构造函数 

在 JavaScript 程序中，函数是一些值。对函数执行 typeof 运算会返回字符串“function”，但是函数其实是 JavaScript 中特殊的对象。因为函数也是对象，它们也可以拥有属性和方法，就像普通的对象可以拥有属性和方法一样。甚至可以用`Function()`构造函数来创建新的函数对象。

### 8.7.1 length属性

在函数体里，`arguments.length`表示传入函数的实参的个数。而函数本身的 length 属性则有着不同含义。函数的 length 属性时只读属性，它代表函数参数的数量，这里的参数指的是“形参”而非“实参”，也就是在函数定义时给出的参数个数，通常也是在函数调用时期望传入函数的参数个数。

```js
// 这个函数使用arguments.callee,因此它不能再严格模式下工作
function check(args) {
  var actual = args.length; // 实参个数
  var expected = args.callee.length; // 形参个数
  if (actual !== expected) // 如果不同则抛出异常
    throw Error("Expected" + expected + "args; got" + actual)
}

function f(x, y, z) {
  check(arguments); // 检查实参个数和形参个数是否一致
  return x + y + z; // 再执行函数的后续逻辑
}
```

### 8.7.2 prototype属性

每一个函数都包含一个 prototype 属性，这个属性是指向一个对象的引用。这个对象称作“原型对象”（prototype object）。每一个函数都包含不同的原型对象。当将函数用作构造函数的时候，新创建的对象会从原型对象上继承属性。6.1.3节讨论了原型和prototype属性，在第9章里会有进一步讨论。

### 8.7.3 call()方法和apply()方法

可以将`call()`和`apply()`看作是某个对象的方法，通过调用方法的形式来间接调用函数。`call()`和`apply()`的第一个实参是要调用函数的母对象，它是调用上下文，在函数体内通过 this 来获得对它的引用。要想以对象 o 的方法来调用函数`f()`，可以这样使用。

```js
f.call(o);
f.apply(o);
```

上面的例子每行代码和下面代码的功能类型（假设对象o中预先不存在名为m的属性）

```js
o.m = f; //将f存储为o的临时方法
o.m(); //调用它不传入参数
delete o.m; //将临时方法删除
```

在 ECMAScript 5 的严格模式中，`call()`和`apply()`的第一个实参都会变成 this 的值，哪怕传入的实参是原始值甚至是 null 或 undefined 。在 ECMAScript 3 和非严格模式中，传入的 null 和 undefined 都会被全局对象代替，而其他原始值则会被相应的包装对象（wrapper object）所替代。

对于`call()`来说，第一个调用上下文实参之后的所有参数就是要传入待调用函数的值。`apply()`方法与之类似，但传入实参的形式和`call()`有所不同，它的实参都放入一个数组当中。

```js
f.call(o, 1, 2);

f.apply(o, [1, 2]);
```

如果一个函数的实参可以是任意数量，给`apply()`传入的参数数组可以是任意长度的。比如，为了找出数组中最大的数值元素，调用`Math.max()`方法的时候可以给`apply()`传入一个包含任意个元素的数组：

```js
var biggest = Math.max.apply(Math, array_of_numbers);
```

需要注意的是，传入`apply()`的参数数组可以是类数组对象也可以是真实数组。实际上，可以将当前函数的 arguments 数组直接传入（另一个函数的）`apply()`来调用另一个函数。

```js
// 将对象o中名为m()的方法替换为另一个方法
// 可以在调用原始的方法之前和之后记录日志消息
function trace(o, m) {
  var original = o[m]; // 在闭包中保存原始方法
  o[m] = function() { // 定义新的方法
    console.log(new Date(), "entering:", m); // 输出消息
    var result = original.apply(this, arguments); // 调用原始函数
    console.log(new Date(), "exiting:", m);
    return result;
  };
}
```

`trace()`函数接收两个参数，一个对象和一个方法名，它将指定的方法替换为一个新方法，这个新方法是“包裹”原始方法的另一个泛函数。这种动态修改已有方法的做法有时称作“monkey-patching”。

### 8.7.4 bind()方法

`bind()`实在 ECMAScript 5 中新增的方法，但在 ECMAScript 3 中可以轻易模拟`bind()`。从名字就可以看出，这个方法的主要作用就是将函数绑定至某个对象。当在函数`f()`上调用`bind()`方法并传入一个对象 o 作为参数，这个方法将返回一个新的函数。（以函数调用的方式）调用新的函数将会把原始的函数`f()`当作 o 的方法来调用。传入新函数的任何实参都将传入原始函数。

```js
// 这个是待绑定的函数
function f(y) {
  return this.x + y;
} 
// 将要绑定的函数
var o = { x: 1 }; 
// 通过g(x)来调用o.f(x)
var g = f.bind(o); 
g(2) // => 3
```

也可以通过以下代码实现轻松绑定：

```js
// 返回一个函数，通过它来调用o中的方法f(),传递它所有的实参
function bind(f, o){    
  // 如果bind()方法存在的话，使用bind()方法
  if(f.bind) {
    return f.bind(o);
  } else {
    // 否则这样绑定
    return function(){
      return f.apply(o, arguments);
    }
  }
}
```

ECMAScript 5 中的`bind()`方法不仅仅是将函数绑定至一个对象，它还附带一些其他应用：除了第一个实参之外，传入`bind()`的实参也会绑定至 this ，这个附带的应用是一种常见的函数式编程技术，有时也被称为“柯里化”（currying）。

```js
// 返回两个实参的值
var sum = function(x, y){
  return x + y
};
// 创建一个类似sum的新函数，但this的值绑定到null
// 并且第一个参数绑定到1，这个新的参数期望只传入一个实参
var succ = sum.bind(null, 1);
// => 3：x绑定到1，并传入2作为实参y
succ(2)     

// 另外一个左累加计算的函数
function f(y, z) {
  return this.x + y + z
}; 
// 绑定this和y
var g = f.bind({x: 1}, 2);  
// => 6：this.x绑定到1，y绑定到2，z绑定到3
g(3) 
```

也可以绑定 this 的值并在 ECMScript 3 中实现这个附带的应用。下面的代码就模拟了实现标准的`bind()`方法。注意，我们将这个方法另存为`Function.prototype.bind`，以便所有的函数对象都继承它。

```js
 if(!Function.prototype.bind){
  Function.prototype.bind = function(o /*,args*/){
    // 将this和arguments的值保存至变量中
    // 以便在后面的嵌套函数中可以使用他们
    var self = this, boundArgs = arguments;
    
    // bind()返回值是一个函数
    return function(){
      // 创建一个实参列表
      // 将传入bind()的第二个及后续的实参都传入这个函数
      var arg = [], i;
      for(i = 1; i < boundArgs.length; i++) 
        args.push(boundArgs[i]);
      for(i = 0; i < arguments.length; i++) 
        args.push(arguments[i]);
      // 现在将self作为o的方法来调用，传入这些实参
      return self.apply(o, args);
    };
  };
}
```

`bind()`方法返回的函数是一个闭包，在这个闭包的外部函数中声明了 self 和 boundArgs 变量，这两个变量在闭包里用到。尽管定义闭包的内部函数已经从外部函数中返回，而且调用这个闭包逻辑的时刻要在外部函数返回之后（在闭包中照样可以正确访问这两个变量）。

ECMAScript 5 定义的`bind()`方法也有一些特性是上述 ECMAScript 3 代码无法模拟的。首先，真正的`bind()`方法返回一个函数对象，这个函数对象的 length 属性时绑定函数的形参个数减去绑定的实参的个数（length 的值不能小于零）。再者，ECMAscript 5 的`bind()`方法可以顺带用作构造函数。如果`bind()`返回的函数用作构造函数，将忽略传入`bind()`的 this ，原始函数就会以构造函数的形式调用，其实参已经绑定。由`bind()`方法所返回的函数并不包含 prototype 属性（普通函数固有的 prototype 属性是不能删除的），并且将这些绑定的函数用作构造函数时所创建的对象从原始的未绑定的构造函数中继承 prototype 。同样，在使用 instanceof 运算符时，绑定构造函数和未绑定构造函数并无两样。

### 8.7.5 toString()方法

和所有的 JavaScript 对象一样，函数也有`toString()`方法，ECMAScript 规范规定这个方法返回一个字符串，这个字符串和函数声明语句的语法相关。实际上，大多数（非全部）的`toString()`方法的实现都返回函数的完整源码。内置函数往往返回一个类似“[native code]”的字符串作为函数体。

### 8.7.6 Function()构造函数

不管是通过函数定义语句还是函数直接量表达式，函数的定义都要使用 function 关键字，但函数还可以通过`Function()`构造函数来定义。

```js
var f = new Function("x", "y", "return x*y");

// 等价于
var f = function(x, y) {
  return x * y;
}
```

`Function()`构造函数可以传入任意数量的字符串实参，最后一个实参所表示的文本就是函数体，它可以包含任意的 JavaScript 语句，每两条语句之间用分号分隔。传入构造函数的其他所有的实参字符串是指定函数的形参名字的字符串。如果定义的函数不包含任何参数，只须给构造函数简单地传入一个字符串（函数体）即可。

注意，`Function()`构造函数并不需要通过传入实参以指定函数名，就像函数直接量一样，`Function()`构造函数创建一个匿名函数。

关于`Function()`构造函数有几点需要特别注意：

1. `Function()`构造函数允许 JavaScript 在运行时动态地创建并编译函数。
2. 每次调用`Function()`构造函数都会解析函数体，并创建新的函数对象。如果是在一个循环或者多次调用的函数中执行这个构造函数，执行效率会受影响。相比之下，循环中的嵌套函数和函数定义表达式则不会每次执行时都重新编译。
3. 最后一点，就是它创建的函数并不是使用词法作用域，相反，函数体代码的编译总是会在顶层函数执行。

```js
var scope = "global";

function constructFunction() {
  var scope = "local";
  return new Function("return scope"); // 无法捕捉局部作用域
}
// 这行代码返回global
// 因为通过Function()构造函数所返回的函数使用的不是局部作用域
constructFunction()(); // => "global"
```

可以将`Function()`构造函数认为是在全局作用域中执行的`eval()`，`eval()`可以在自己的私有作用域内定义新变量和函数，`Function()`构造函数在实际编程过程中很少会用到。

### 8.7.7 可调用的对象

在 7.11 节中提到“类数组对象”并不是真正的数组，但大部分场景下可以将其当作数组来对待。对于函数也存在类似的情况。“可调用的对象”（callable object）是一个对象，可以在函数调用表达式中调用这个对象。所有的函数都是可调用的，但并非所有的可调用对象都是函数。

截止目前，可调用对象在两个 JavaScript 实现中不能算作函数。首先， IE Web 浏览器（IE8及之前的版本）实现了客户端方法（诸如`Window.alert()`和`Document.getElementsById()`），使用了可调用的宿主对象，而不是内置函数对象。 IE 中的这些方法在其他浏览器中也都存在，但它们本质上不是 Function 对象。 IE 9 将它们实现为真正的函数，因此这类可调用的对象将越来越罕见。

另外一个常见的可调用对象是 RegExp 对象（在众多浏览器中均有实现），可以直接调用 RegExp 对象，这比调用它的`exec()`方法更快捷一些。在 JavaScript 中这是一个彻头彻尾的非标准特性。

如果想检测一个对象是否是真正的函数对象（并且具有函数方法），可以检测它的 class 属性。

```js
function isFunction(x) {
  return Object.prototype.toString.call(x) === "[object Function]"
}
```

## 8.8 函数式编程 

和 Lisp 、 Haskell 不同， JavaScript 并非函数式编程语言，但在 JavaScript 中可以像操控对象一样操控函数，也就是说可以在 JavaScript 中应用函数式编程技术。ECMAScript 5 中的数组方法（诸如`map()`和`reduce()`）就可以非常适合用于函数式编程风格。

### 8.8.1 使用函数处理数组

假设有一个数组，数组元素都是数字，我们想要计算这些元素的平均值和标准差。若使用非函数式编程风格的话，代码会是这样：

```js
var data = [1, 1, 3, 5, 5]; // 这里待处理的数组
// 平均数是所有元素的累加值和除以元素的个数
var total = 0;
for (var i = 0; i < data.length; i++) {
  total += data[i]
}
var mean = total / data.length; // => 3

// 计算标准差，首先计算每个数减去平均数减去平均数之后偏差的平方然后求和
total = 0;
for (var i = 0; i < data.length; i++) {
  var deviation = data[i] - mean;
  total += deviation * deviation;
}
var stddev = Math.sqrt(total / (data.length - 1)); // 标准差的值是2
```

可以使用数组方法`map()`和`reduce()`来实现同样的计算，这种实现极其简洁。

```js
// 首先先简单定义两个简单函数
var sum = function(x,y){
  return x+y;
};
var square = function(x) {
  return x*x;
};

// 然后将这些函数和数组方法配合使用计算出平均数和标准差
var data = [1, 1, 3, 5, 5]; 
var mean = data.reduce(sum)/data.length;
var deviations = data.map(function(x){
  return x-mean;
});
var stddev = Math.sqrt(deviations.map(square).reduce(sum)/(data.length-1));
```

如果基于 ECMAScript 3 来如何实现呢？因为 ECMAScript 3 并不包含这些数组方法，如果不存在内置方法的话可以自定义`map()`和`reduce()`函数。

```js
// 对于每个数组元素调用函数f()，并返回一个结果数组
// 如果Array.prototype.map定义了的话，就使用这个方法
var map = Array.prototype.map 
  ? function(a, f) {
      // 如果已经存在map()方法，就直接使用它
      return a.map(f);
    } 
  : function(a, f) { 
    // 否则就自己实现一个
    var result = [];
    for (var i = 0, len = a.length; i < len; i++) {
      if (i in a) {
        result[i] = f.call(null, a[i], i, a);
      }
      return result;
    }
  };

// 使用函数f()和可选的初始值将数组a减至一个值
// 如果Array.prototype.reduce存在的话，就使用这个方法
var reduce = Array.prototype.reduce 
? function(a, f, initial) { 
  // 如果reduce()方法存在的话
  if (arguments.length > 2)
    // 如果成功的传入了一个值
    return a.reduce(f, initial); 
  else {
    //否则没有初始值
    return a.reduce(f);
  } 
}
: function(a,f,initial){
  // 这个算法来自ECMAScript5规范
  var i =0,len =a.length,accumulator;
  // 以特定的初始值开始，否则第一个值取自a
  if(arguments.length>2) accumulator = initial;
  else {
    // 找到数组中第一个已经定义的索引
    if(len == 0) throw TypeError();
    while(i<len){
      if(i in a){
        accumulator = a[i++];
        break;
      }else i++;
    }if(i == len) throw TypeError();
  }
  // 对于数组中剩下的元素一次调用f()
  while(i<len){
    if(i in a)
    accumulator = f.call(undefined,accumulator,a[i],i,a);
  }
  return accumulator;
};
```

使用定义的`map()`和`reduce()`函数，计算平均值和标准差的代码看起来像这样：

```js
var data = [1, 2, 35, 6, 3, 2];
var sum =function(x,y){
  return x+y;
};
var square = function(x){
  return x*x;
};
var mean = reduce(data,sum)/data.length;
var deviations = map(data,function(x){
  return x-mean;
});
var stddev = Math.sqrt(reduce(map(deviations,square),sum)/(data.length-1));
```

### 8.8.2 高阶函数

所谓高阶函数（higher-order function）就是操作函数的函数，它接收一个或多个函数作为参数，并返回一个新函数，来看这个例子：

```js
// 这个高阶函数返回一个新的函数，这个新函数将它的实参传入f()
// 并返回f的返回值逻辑非
function not(f){
  return function(){  // 返回一个新的函数
    var result = f.apply(this, arguments);  // 调用f()
    return !result;  // 对结果求反
  };
}
var even = function (x){  // 判断a是否为偶数的函数
  return x % 2 === 0;
};

var odd = not(even);  // 判断一个新函数，和even()相反
[1, 1, 3, 5, 5].every(odd);  // =>true 每个元素为奇数
```

上面的`not()`函数就是一个高阶函数，因为它接收一个函数作为参数，并返回一个新函数。来看下面的`mapper()`函数，它也是接收一个函数作为参数，并返回一个新函数，这个新函数将一个数组映射到另一个使用这个函数的数组上。这个函数使用了之前定义的`map()`函数。

```js
// 所返回的函数的参数应当是一个实参数组，并对每个函数数组元素执行函数f()
// 并返回所有的计算结果组成数组
// 可以对比下这个函数和上下文提到的map()函数
function mapper(f) {
  return function(a) {
    return map(a, f);
  };
}
var increment = function(x) {
  return x + 1;
};
var incrementer = mapper(increment);

incrementer([1, 2, 3]) // => [2,3,4]
```

这里是一个更常见的例子，它接收两个函数`f()`和`g()`，并返回一个新的函数用以计算`f(g())`：

```js
// 返回一个新的可计算f(g(...))的函数
// 返回的函数h()将它所有的实参传入g(),然后将g()的返回值传入f()
// 调用f()和g()时的this值和调用h()时的this值是同一个this
function compose(f, g){
  return function(){
    // 需要给f()传入一个参数，所以使用f()的call方法
    // 需要给g()传入很多参数，所以使用g()的apply()方法
    return f.call(this, g.apply(this, arguments));
  };
}
var square = function(x){return x*x;};
var sum = function(x,y){return x+y;};
var squareofsum = compose(square, sum);
squareofsum(2, 3) // => 25
```

### 8.8.3 不完全函数

函数`f()`的`bind()`方法返回一个新函数，给新函数传入特定的上下文和一组特定的参数，然后调用函数`f()`。我们说它把函数“绑定至”对象并传入一部分参数。`bind()`方法只是把实参放在（完整实参列表的）左侧，也就是说传入`bind()`的实参都是放在传入原始函数逇实参列表开始的位置，但有时我们期望将传入`bind()`的实参放在（完整实参列表的）右侧：

```js
// 实现一个工具函数将类数组对象（或对象）转换为正真的数组
// 在后面示例代码中用到了这个方法将arguments对象转化为正真的数组
function array(a, n) {
  return Array.prototype.slice.call(a, n || 0);
}

// 这个函数的实参传递至左侧
function partialLeft(f /*,...*/ ) {
  var args = arguments; // 保存外部实参数组
  return function() { // 并返回这个函数
    var a = array(args, 1); // 开始处理外部的地图份额args
    a = a.concat(array(arguments)); // 然后增加内所有内部实参
    return f.apply(this, a); // 然后基于这个实参列表调用f()
  };
}

// 这个函数的实参传递至右侧
function partialRight(f /*,...*/ ) {
  var args = arguments; // 保存外部实参数组
  return function() { // 返回这个函数
    var a = array(arguments); // 从内部参数开始
    a = a.concat(array(args, 1)); // 然后从外部第一个args开始添加
    return f.apply(this, a); // 然后基于这个实参列表调用f()
  };
}

// 这个函数的实参被用做模板
// 实参列表中的undefeined值都被填充
function partial(f /*,...*/ ) {
  var args = arguments; // 保存外部实参数组
  return function() {
    var a = array(args, 1); // 从外部的args开始
    var i = 0,
        j = 0;
    // 遍历args,从内部实参填充undefined值
    for (; i < a.length; i++)
      if (a[i] === undefined) a[i] = arguments[j++];
      // 现在将剩下的内部实参都追加进去
    a = a.concat(array(arguments, j))
    return f.apply(this, a);
  };
}
// 这个函数带有三个实参
var f = function(x, y, z) {
  return x * (y - z);
};
// 注意三个不完全调用之前的区别
partialLeft(f, 2)(3, 4) // => -2: 绑定第一个实参:2*(3-4)
partialRight(f, 2)(3, 4) // => 6: 绑定最后一个实参:3*(4-2)
partial(f, undefined, 2)(3, 4) // => -6 绑定中间的实参:3*(2-4)
```

利用这种不完全函数的编程技巧，可以编写一些有意思的代码，利用已有的函数定义新的函数。

```js
var increment = partialLeft(sum,1);
var cuberoot = partialRight(Math.pow,1/3);
String.prototype.first = partial(String.prototype.charAt,0);
String.prototype.last = partial(String.prototype.substr,-1,1);
```

当将不完全调用和其他高阶函数整合在一起的时候，事情就变得格外有趣。比如，这里的例子定义了`not()`函数，它用到了刚才提到的不完全调用：

```js
var not = partialLeft(compose,function(x){
  return !x;
});
var even = function(x) {
  return x % 2 === 0;
};
var odd = not(even);
var isNumber = not(isNaN)
```

我们也可以使用不完全调用的组合来重新足足求平均数和标准差的代码，这种编码风格是非常纯粹的函数式编程：

```js
// 要处理的数据
var data = [1,1,3,5,5]
// 两个初等函数
var sum =function(x,y){return x+y;}; 
var product =function(x,y){return x*y;};
// 定义其他函数
var neg = partial(product-1);
var square = partial(Math.pow, undefined, 2);
var sqrt = partial(Math.pow, undefined, .5);
var reciprocal = partial(Math.pow, undefined, -1);

// 现在来计算平均值和标准差，所有的函数调用都不带运算符
// 这段代码看起来很像lisp代码
var mean = product(reduce(data,sum),reciprocal(data.length));
var stddev = sqrt(product(reduce(map(data,
  compose(square,
    partial(sum, neg(mean))))
,sum),
reciprocal(sum(data.length, -1))));
```

### 8.8.4 记忆

在 8.4.1 节中定义了一个阶乘函数，它可以将上次的计算结果缓存起来。在函数式编程当中，这种缓存技巧叫做“记忆”（memorization）。下面的代码展示了一个高阶函数，`memorize()`接收一个函数作为实参，并返回带有记忆能力的函数。

```js
// 返回f()的带有记忆功能的版本
// 只有当f()的实参的字符串表示都不相同时它才会工作
function memorize(f) {
  var cache = {}; // 将值保存在闭包内
  return function() {
    // 将实参转换为字符串形式，并将其用做缓存的键
    var key = arguments.length + Array.prototype.join.call(arguments, ",");
    if (key in cache) return cache[key];
    else return cache[key] = f.apply(this, arguments);
  };
}
```

`memorize()`函数创建一个新的对象，这个对象被当作缓存（的宿主）并赋值给一个局部变量，因此对于返回的函数来说它是私有的（在闭包中）。所返回的函数将它的实参数组转换字符串，并将字符串用作缓存对象的属性名。如果在缓存中存在这个值，则直接返回它。

否则，就调用既定的函数对实参进行计算，将计算结果缓存起来并返回，下面的代码展示了如何使用`memorize()`：

```js
// 返回两个整数的最大公约数
// 使用欧几里德算法
function gcd(a, b){ // 这里省略对a和b的类型检查
  var t;
  if (a > b) t = b, b = a, a = t; // 确保a>=b
  while(b != 0) {
    t = b, b = a%b, a = t; // 这里是求最大公约数的欧几里德算法
  }
  return a;
}
var gcdmemo = memorize(gcd);
gcdmemo(85,187); //=>17

// 注意，我们写一个递归函数时，往往需要实际记忆功能
// 我们更希望调用了实现了记忆功能的递归函数，而不是原递归函数
var factorial = memorize(function(n){
  return(n <= 1)?1:n *factorial(n-1);
});
factorial(5) // => 120：对4-1的值也有缓存
```

# 第9章 类和模块

第6章详细介绍了 JavaScript 对象，每个 JavaScript 对象都是一个属性集合，相互之间没有任何联系。在 JavaScript 中也可以定义对象的类，让每个对象都共享某些属性，这种“共享”的特性是非常有用的。类的成员或实例都包含一些属性，用以存放它们的状态，其中有些属性定义了它们的行为（通常称为方法）。这些行为通常是由类定义的，而且为所有实例所共享。例如，假如有一个名为 Complex 的类用来表示复数，同时还定义了一些复数运算。一个 Complex 实例应当包含复数的实部和虚部（状态），同样 Complex 还会定义复数的加法和乘法操作（行为）。

在 JavaScript 中，类的实现是基于其原型继承机制的。如果两个实例都从一个原型对象上继承了属性，我们说它们是同一个类的实例。 JavaScript 原型和继承在 6.1.3 和 6.2.2 节中有详细讨论，本章会在 9.1 节中对原型做进一步讨论。

如果两个对象继承自同一个原型，往往意味着（但不是绝对）它们是由同一个构造函数创建并初始化的。我们已经在 4.6 , 6.2 和 8.2.3 节详细了解构造函数，9.2 节会有更近一步讨论。

如果你对 Java 和 C++ 这种强类型（强、弱类型是指类型检查的严格程度，为所有变量指定数据类型称为强类型）的面向对象编程比较熟悉，你会发现 JavaScript 中的类和 Java 及 C++ 的类型有很大不同。尽管在写法上类似，而且在 JavaScript 中也能“模拟”出很大经典的特性（比如传统类的封装、继承和多态），但是最好要理解 JavaScript 类和基于原型的继承机制，以及和传统的 Java （当然还有类似 Java 的语言）的类和基于类的继承机制的不同之处，9.3 节展示了如果在 JavaScript 中实现经典的类。

JavaScript 中类的一个重要特征是“动态可继承”（dynamically extendable），9.4 节会详细解释这一特性。我们可以将类看做是类型，9.5 节讲解检测对象的类的几种方式，该节还介绍了一种编程哲学——“鸭式辨型”，它弱化了对象的类型，强化了对象功能。

在讨论了 JavaScript 中所有基本面向对象编程特性之后，我们将关注点从抽象的概念转化为一些实例。9.6 节介绍了两种非常重要实现类的方法，包括很多实现面向对象的技术，这些技术可以在很大程度上增强类的功能。9.7 节展示（包含很多示例代码）如何实现类的继承，包括如何在 JavaScript 中实现类的继承。9.8 节讲解如何使用 ECMAScript5 中的新特性来实现类及面向对象编程。

定义类是模块开发和重用代码的有效方式之一，本章最后一节会集中讨论 JavaScript 中的模块。

## 9.1 类和对象

在 JavaScript 中，类的所有实例对象都从一个类型对象上继承属性。因此，原型对象是类的核心。在例 6.1 中定义了`inherit()`函数，这个函数返回一个新创建的对象，然后继承自某个原型对象。如果定义了一个原型对象，然后通过`inherit()`函数创建了一个继承自它的对象，这样就定义了一个 JavaScript 类。通常，类的实例还需要进一步的初始化，通常是通过定义一个函数来创建并初始化这个新对象。参照下例子，给出一个表示“值的范围”定义了原型对象。还定义了一个“工厂”函数（参照工厂方法）用以创建并初始化类的实例。

```js
// 一个简单的 JavaScript 类
// 实现一个能表示值的范围的类

// 这个工厂方法返回一个新的“范围对象”
function range(from,to){
  // 使用inherit()函数来创建对象，这个对象继承自下面定义的原型对象
  // 原型对象作为函数的一个属性存储，并定义所有“范围对象”所共享的方法（行为）
  var r = inherit(range.methods);

  // 储存新的“范围对象”启始位置和结束位置（状态）
  // 这两个属性是不可继承的，每个对象都拥有唯一的属性
  r.from = from;
  r.to = to;

  // 返回这个新创建的对象                
  return r;
}

// 原型对象定义方法，这些方法为每个范围对象所继承
range.methods = {
  // 如果x在范围内，则返回true；否则返回false
  // 如果这个方法可以比较数字范围。也可以比较字符串和日期范围
  includes: function(x){
    return this.from <= x && x <= this.to;},
  // 对于范围内每个整数都调用一次f
  // 这个方法只可用作数字范围
  foreach: function (f){
    for (var x = Math.ceil(this.from); x <= this.to ; x++) f(x);
  },
  // 返回表示这个范围的字符串
  toString: function(){
    return "("+ this.from + "..." + this.to + ")";
  }
};

// 这是使用范围对象的一些例子
var r = range(1, 3); // 创建一个范围对象
r.includes(2); // => true:2 在这个范围内
r.foreach(console.log); // 输出 1 2 3
console.log(r); // 输出 (1...3)
```

在这个例子中有一些代码是没有用的。这段代码定义了一个工厂方法`range()`，用来创建新的范围对象。我们注意到，这里给`range()`函数定义了一个属性`range.methods`，用以便捷地存放定义类的原型对象。把原型对象挂载函数上没什么大不了，但也不是惯用做法。再者，注意`range()`函数给每个范围对象定义了from和to属性，用以定义范围的起始位置和结束位置，这两个属性是非共享的，当然也是不可继承的。最后，注意在`range.methods`中定义的那些可共享、可继承的方法都用到了 form 和 to 属性，而且使用了 this 关键字，为了指代它们，二者使用的 this 关键字来指代调运这个方法的对象。任何类的方法都可以通过 this 的这种基本用法来读取对象的属性。

## 9.2 类和构造函数

上边的例子中展示了 JavaScript 中定义类的其中一种方法。但这种方法并不常用，毕竟它没有定义构造函数，构造函数是用来初始化和创建对象的。8.2.3已经讲到，使用 new 关键字来调用构造函数，使用 new 调用构造函数会创建一个新对象，因此，构造函数本身只需要初始化这个新对象的状态即可。调用构造函数的一个重要特征是，构造函数的 prototype 属性被用做新对象的原型。这意味着通过同一个构造函数创建的对象都是继承自一个相同的对象，因此它们都是一个类的成员。下面的例子对上面的例子的“范围类”做了修改，使用构造函数代替工厂函数：

```js
// 表示值的范围的类的另一种实现

// 这是一个构造函数，用以初始化新创建的“范围对象”
// 注意，这里并没有创建并返回一个对象，仅仅是初始化
function Range(from, to) {
  // 存储这个“范围对象”的起始位置和结束位置（状态）
  // 这两个属性是不可继承的，每个对象都拥有唯一的属性
  this.from = from;
  this.to = to;
}

// 所有的“范围对象”都继承自这个对象
// 属性的名字必须是"prototype"
Range.prototype = {
  // 如果x在范围内，则返回true;否则返回false
  // 这个方法可以比较数字范围，也可以比较字符串和日期范围
  includes: function(x) {
    return this.from <= x && x <= this.to;
  },
  // 对于这个范围内的每个整数都调用一次f
  // 这个方法只可用于数字范围
  foreach: function(f) {
    for (var x = Math.ceil(this.from); x <= this.to; x++) f(x);
  },
  // 返回表示这个范围的字符串
  toString: function() {
    return "(" + this.from + "..." + this.to + ")";
  }
};

// 这里是使用“范围对象”的一些例子
var r = new Range(1, 3); // 创建一个范围对象
r.includes(2); // => true：2在这个范围内
r.foreach(console.log); // 输出1 2 3
console.log(r); // 输出对象(1...3)
```

将上面的两个例子对比，就发现两种定义类的技术差别。首先：工厂函数`range()`转化为构造函数时被重命名`Range()`。这里遵循了一个常见的编程约定：从某种意义上来讲，定义构造函数既是定义类，并且类首字母要大写，而普通的函数和方法首字母都是小写。

再者，注意`Range()`构造函数是通过 new 关键字调用的，而`range()`工厂函数则不必使用 new 。前一个例子调用普通函数来创建新对象，后一个则使用构造函数来创建新对象。由于`Range()`函数就是通过 new 关键字来调用的，所有不必调用`inherit()`或者其它什么的逻辑来创建新的对象。在调用构造函数之前就已经创建了新对象，通过 this 关键字可以获取这个新对象。`Range()`构造函数只不过是初始化 this 而已。构造函数甚至不必返回这个新创建的对象，构造函数会自动创建对象，然后将构造函数作为这个对象的方法来调用一次，最后返回这个新对象。事实上，构造函数的命名规则和普通函数是如此不同还有另外一个原因，构造函数调用和普通函数的调用是不尽相同的。构造函数就是用来“构造新对象”的，它必须通过关键字 new 来调用，如果将构造函数做普通函数的话，往往不会正常工作。开发者可以通过命名约定来判断是否应当在函数之前冠以关键字 new 。

上面两个例子还有一个非常重要的区别：就是原型对象的命名。在第一段示例代码中的原型是`range.methods`。这种命名方式很方便同时具有很好的语义，但有过于随意。在第二段代码中的原型是`Rang.prototype`，这是一个强制命名。对`Range()`构造函数的调用会自动使用`Rang.prototype`作为新Range对象的原型。

最后，需要注意的是前两个例子中两种类定义方法的相同之处，两者的范围方法定义和调用方式是完全一致的。

### 9.2.1 构造函数和类的标识：

上文提到，原型对象是类的唯一标识：当且仅当两个对象继承自同一个原型对象时，它们在属于同一个类的实例。而初始化对象的状态的构造函数则不能作为类的标识，两个构造函数的 prototype 属性可能指向同一个原型对象。那么这两个构造函数创建的实例是属于一个类的。

尽管构造函数不像原型那样基础，但构造函数是类的“外在表现”。 很明显，构造函数的名字通常用做类名。比如,我们说`Range()`构造函数创建 Range 对象，然后根本的讲，当使用 instanceof 运算符来检测对象是否属于某个类时会用到构造函数。假设这里有一个对象 r ，我们想知道 r 是否是 Range 对象，我们来这样写：

```js
r instanceof Range // 如果r继承自Rang.prototype,则返回true
```

实际上 instanceof 运算符不不会检查 r 是否是由`Range()`构造函数初始化而来，而会检查r是否继承`Range.prototype`。不过 instanceof 的语法强化了“构造函数是类公有标识”的概念，在本章的后面还会碰到对 instanceof 运算符的介绍。

### 9.2.2 constructor属性

在上面的例子中，将`Range.prototype`定义为一个新对象，这个对象包含类所需要的方法。其实没必要新创建一个对象，用单个对象的直接量的属性就可以方便地定义原型上的方法。任何 JavaScript 函数都可以用做构造函数，并且调用构造函数是需要用到一个 prototype 属性 ，因此，每个 JavaScript 函数（ ECMAScript 5 中的`function.bind()`方法返回的函数除外）都自动拥有一个 prototype 属性。这个属性的值是一个对象，这个对象包含唯一一个不可枚举的属性 constructor 。 constructor 属性的值是一个函数对象：

```js
var F = function() {}; // 这是一个函数对象：
var p = F.prototype; // 这是F相关联的原型对象
var c = p.constructor; // 这是与原型相关的函数
c === F; // =>true  对于任意函数F.prototype.constructor == F
```

可以看到构造函数的原型中存在预先定义好的 constructor 属性，这意味着对象通常继承的 constructor 均代指他们的构造函数。由于构造函数是类的“公共标识”，因此这个 constructor 属性为对象提供了类。

```js
var o = new F(); // 创建类F的一个对象
o.constructor === F // => true  constructor属性指代这个类
```

如下图所示，展示了构造函数和原型之间的关系，包括原型到构造函数的反向引用及构造函数创建的实例。

需要注意的是，使用早前的`Range()`构造函数作为示例，但实际上，定义的 Range 类使用它自身的一个新对象重写了预定义的`Range.prototype`对象。这个新定义的原型对象不含有 constructor 属性。因此 Range 类的实例也不包含有 constructor 属性。我们可以通过补救措施来修正这个问题，显式的给原型添加一个构造函数：

```js
Range.prototype = {
  constructor: Range, // 显式的设置构造函数反向引用
  includes: function(x) {
    return this.from <= x && x <= this.to;
  },
  foreach: function(f) {
    for (var x = Math.ceil(this.from); x <= this.to; x++) f(x);
  },
  toString: function() {
    return "(" + this.from + "..." + this.to + ")";
  }
};
```

另外一种常见的解决办法是使用预定义的原型对象，预定义的原型对象包含 constructor 属性，然后依次给原型对象添加方法：

```js
Rang.prototype = {
  // 扩展预定义的Range.prototype对象，而不重写之
  // 这样就自动创建Range.prototype.constructor属性
  Range.prototype.includes = function(x) {
    return this.from <= x && x <= this.to;
  };
  Range.prototype.foreach = function(f) {
    for (var x = Math.ceil(this.from); x <= this.to; x++) f(x);
  }
  toString: function() {
    return "(" + this.from + "..." + this.to + ")";
  }
};
```

## 9.3 JavaScript中Java式的类继承

如果你有过 Java 或者其它类似强类型面向对象语言开发的经历的话，在你的脑海中，类成员的模样可能是这个样式：

- 实例字段：它们是基于实例的属性或变量，用以保存独立对象的状态
- 实例方法：它们是类的所有实例所共享的方法，有每个独立的实例调用
- 类字段：这些属性或变量是属于类的，而不属于类的某个实例
- 类方法：这些方法是属于类的，而不是属于类的某个实例的。

JavaScript 和 Java 的一个不同之处在于， JavaScript 中的函数都是以值的形式出现的，方法和字段之间并没有太大的区别，如果属性值是函数，那么这个属性就定义一个方法；否则，它是一个普通的属性或“字段”。尽管存在出多差异，我们还是可以用 JavaScript 模拟出 Java 中的这四种类成员类型。 JavaScript 中的类牵扯三种不同的对象（参照上图），三种对象的属性的行为和下面三种类成员非常相似：

- 构造函数对象：构造函数（对象）为 JavaScript 的类定义了名字。任何添加到这个构造函数对象中的属性都是类字段和类方法（如果属性值是函数的话就是离方法）。
- 原型对象：原型对象的属性被类的所有实例所继承，如果原型对象的属性值是函数的话，这个函数就作为类的实例方法来调用。
- 实例对象：类的每个实例对象都是一个独立的对象，直接给这个实例定义的属性是不会为所有实例对象锁共享的。定义在实例上的非函数属性，实际上是实例的字段。

在 JavaScript 中定义类的步奏可以缩减为一个分三步的算法。第一步，先定义一个构造函数，并设置初始化新对象的实例属性。第二步，给构造函数的 prototype 对象定义实例的方法。第三步：给构造函数定义类字段和类属性。我们可以将这三个步骤封装进一个简单的`defineClass()`函数中（这里用到了`extend()`函数）：

```js
// 一个用以定义简单类的函数
function defineClass(constructor, // 用以设置实例的属性的函数
  methods, // 实例的方法，复制至原型中
  statics) // 类属性，复制至构造函数中
{
  if (methods) extend(constructor.prototype, methods);
  if (statics) extend(constructor, statics);
  return constructor;
}
// 这个是Rang类的另一个实现
var SimpleRange =
  defineClass(function(f, t) {
    this.f = f;
    this.t = t;
  }, {
      inclueds: function(x) {
        return this.f <= x && x <= this.t;
      },
      toString: function() {
        return this.f + "..." + this.t;
      }
  }, {
      upto: function(t) {
        return new SimpleRange(o, t);
      }
  });
```

下面的定义类的代码更长一些，这里定义了一个表示复数的类，这段代码展示了如何使用 JavaScript 来模拟实现 Java 式的类成员，这里的代码没有用到上面的`defineClass()`函数，而是“手动”来实现：

```js
/*
 *这个文件定义了Complex类，用来描述复数
 *回忆一下，复数是实数和虚数的和，并且虚数i是-1的平方根
 */
/*
 *这个构造函数为它所创建的每个实例定义了实例字段r和i
 *这两个字段分别保存复数的实部和虚部
 *他们是对象的状态
 */ 
function Complex(real, imaginary) {
  if (isNaN(real) || isNaN(imaginary)) //确保两个实参都是数字
    throw new TypeError();
  this.r = real;
  this.i = imaginary;
}
/*
 *类的实例方法定义为原型对象的函数值的属性
 *这个库定义的方法可以被所有实例继承，并为它们提供共享的行为
 *需要注意的是，javascript的实例方法必须使用关键字this才存取实例的字段
 *当前复数对象加上另外一个复数，并返回一个新的计算乘积之后的复数对象
 */
Complex.prototype.add = function(that) {
  return new Complex(this.r + that.r, this.i + that.i);
};
//当前复数乘以另外一个复数，并返回一个新的计算乘积之后的复数对象
Complex.prototype.mul = function(that) {
  return new Complex(this.r * taht.r - this.i * that.i, this.r * that.i + this.i * that.r);
};
//计算复数的模，复数的模的定义为原点（0,0）到复平面的距离
Complex.prototype.mag = function() {
  return Math.sqrt(this.r * this.r + this.i * this.i);
};
//复数的求负运算
Complex.prototype.neg = function() {
  return new Complex(-this.r, -this.i);
}
//将复数对象转换为一个字符串
Complex.prototype.toString = function() {
  return "{" + this.r + "," + this.i + "}";
};
//检测当前复数对象是否和另外一个复数值相等
Complex.prototype.equals = function(that) {
  return taht != null && //必须有定义且不能是null
    that.constructor === Complex && //并且必须是Complex实例
    this.r === that.r && this.i === that.i; //并且必须包含相同的值
};
/*
*类字段（比如常量）和类方法直接定义为构造函数的属性
* 需要注意的是，类的方法通常不使用关键字this
* 它们只对其参数操作
* */
//这里定义了一些对复数运算有帮助的类的字段
//它们的命名全都是大写，用以表明它们是常量
//在ECMAScript5中，还可以设置这些类字段的属性为只读
Complex.ZERO = new Complex(0, 0);
Complex.ONE = new Complex(1, 0);
Complex.I = new Complex(0, 1);
//这个类方法将由实例对象的toSring方法返回的字符串格式解析为一个Complex对象
//或者抛出一个类型错误异常
Complex.parse = function(s) {
  try { //假设解析成功
    var m = Complex._format.exec(s); //用正则表达式进行匹配
    return new Complex(parseFloat(m[1]), parseFloat(m[2]));
  } catch (x) { //如果解析失败则抛出异常
    throw new TypeError("cat not parse" + s + "as a complex number");
  }
};
//定义类的“私有字段”，这个字段在Complex.parse()用到了
//下划线前缀表明他是类内部使用的，而不书序类的公有API的部分
Complex._format = /^\{([^,]+),([^}]+)\}$/;
```

从上个例子所定义的 Complex 类我们看出，我们使用到了构函数、实例字段、实例方法、类字段和类方法，看一下这段示例代码：

```js
var c = new Complex(2, 3) //使用构造函数创建新对象
var d = new Complex(c.i, c.r); //用到了c的实例属性
c.add(d).toString(); // {5,5}:使用了实例的方法

//这个稍复杂的表达式用到了类方法和类字段
Complex.parse(c.toString()).  //将C转换为字符串
add(c.neg()). //加上它的负数
equals(Complex.ZERO) //结果永远是零
```

尽管 JavaScript 可以模拟出 Java 式的类成员，但 Java 中很多重要的特性是无法在 JavaScript 类中模拟的。首先对于 Java 类的实例方法来说，示例字段可以做局部变量，而不需要使用关键字 this 来引导他们。 JavaScript 是无法模拟这个特性的。但可以使用 with 语句来近似的模拟实现这个功能（不推荐）。

```js
Complex.prototype.toString = function() {
  with(this) {
    return "{" + r + "," + i + "}";
  }
};
```

在Java中可以使用 final 声明字符段为常量，并且可以将字段和方法声明为 private ，用以表示它们是私有成员切在类的外面是不可见的。在 JavaScript 中没有这些关键字。上面 Java 式的类继承的例子中，使用了一些命名写法上约定来给出的一些暗示，比如那些成员是不能修改的（大写字母命名的命名），那些成员在类外部是不可见的（以下划线前缀的命名）。关于这两个主题的讨论会在本章后续讨论：私有属性可以使用闭包里的局部变量来模拟（9.6.6节），常量属性在 ECMAScript 5 中直接实现 9.8.2 节。

## 9.4 类的扩充

JavaScript 中基于原型的继承机制是动态的：对象从其原型继承属性，如果创建对象之后原型的属性发生改变，也会影响到继承这个原型的所有实例对象。这意味着我们可以通过给原型对象添加新的方法来扩充 JavaScript 类。这里我们给 Complex 类添加方法计算复数的共轭复数（两个实部相等，虚部互为相反的复数互为共轭复数）。

```js
//返回当前复数的共轭复数
Complex.prototype.conj = function(){
  return new Complex(this.r, -this.i);
};
```

JavaScript 内置类的原型对象也是一样的如此“开放”，也就是说可以给数字，字符串、数组、函数等数据类型添加方法。8.7.5 节我们曾给 ECMAScript 3 中的函数类添加了`bind()`方法，这个方法原来是没有的：

```js
if(!Function.prototype.bind){
  Function.prototype.bind = function(o/*,agrs*/){
    //bind()代码的方法...
  };
}
```

还有一些其他的例子：

```js
// 多次调用这个函数f,传入一个迭代数
// 比如输出三次"hello"
// var n =3
// n.times(function(n){console.log(n + "hello");});
Number.prototype.times = function(f, context){
  var n = Number(this);
  for(var i = 0;i< n;i++) f.call(context,i);
};

// 如果不存在ECMAscript5的String.trim()方法的话，就定义它
// 这个方法用于去除字符串开头和结尾的空格
String.prototype.trim = String.prototype.trim || function(){
  if (!this) return this;
  return this.replace(/^\s|\S+$/g,""); //使用正则表达式 进行空格替换
};

// 返回函数的名字，如果它有（非标准的）name属性，则直接使用name属性
// 否则，将函数转换为字符串然后从中提取名字
// 如果是没有名字的函数，则返回一个空字符串
Function.prototype.getName = function(){
  return this.name || this.toString().match(/function\s*([^(]*]\(/)[1];
};
```

可以给`Object.prototype`添加方法，从而使所有的对象都可以调用这些方法。但这样的做法并不推荐，因为在 ECMAScript 5 之前，无法将这些新增的方法设置为不可枚举的，如果给`Object.prototype`添加属性，这些属性是可以被for/in循环遍历到的。在 9.8.1 节将给出 ECMAScript 5 的一个例子，其中使用`Object.defineProperty()`方法安全地扩充`Object.prototype`。

然而并不是所有的宿主环境（比如web浏览器）都可以使用`Object.defineProperty()`，这跟 ECMAScript 具体实现有关。比如在很多web浏览器里，可以给`HTMLElement.prototype`添加方法，这样当前文档中表示HTML标记的所有对象就可以继承这些方法，但IE有可能不支持这样做。这对客户端编程实用技术有严重的限制。

## 9.5 类和类型

回想一下第三章的内容， Javascript 定义了少量的数据类型：null、undefined、布尔值、数字、字符串、函数和对象。typeof运算符（4.13.2节）可以得出值的类型。然而我们往往更希望将类作为类型来对待，这样就可以根据对象所属的类来区分它们。 Javascript 语言核心中的内置对象（通常是指客户端 Javascript 的宿主对象）可以根据它们的 class 属性（6.8.2）来区分彼此，比如`classof()`函数，实例的 class 属性都是"Object",这时`calssof()`函数也无用武之地。

接下来的几节介绍了三种用以检测任意对象的类的技术：instanceof运算符，constructor属性，以及构造函数的名字。但每种技术都不甚至完美，本节总计讨论了鸭式辨型，这种编程哲学更加注意对象可以完成什么构造（包含什么方法）而不是对象属于那个类。

### 9.5.1 instanceof运算符

左操作数是待检测其类的对象，右操作数是定义类的构造函数。如果 o 继承自`c.protoype`，则表达式`o intanceof c`的值为true。这里的继承可以不是直接继承，如果 o 所继承的对象继承自另一个对象，后一个对象继承自`c.prototype`这个表达式的运算结果也是true.

正如在本章前面所讲到的，构造函数是类的公共标识，但原型是唯一的标识。尽管 instanceof 运算符的右操作数是构造函数，但计算过程实际上是检测了对象的继承关系，而不是检测创建对象的构造函数。
如果你想检测对象的原型链上是否存在某个特定的原型对象，有没有不使用构造函数作为中介的方法？答案是肯定的，可以使用`isPrototypeOf()`方法。比如可以通过如下代码来检测对象 r 是否是例 9.1 中定义的范围类的成员：

```js
range.methods.isPrototypeOf(r); // range.method是原型对象
```

instanceof 运算符和`isPrototypeOf()`方法的缺点是，我们无法通过对象来获得类名，只能检测对象是否属于指定的类名。在客户端 Javascript 中还有一个比较严重的不足，就是在多窗口和多框架子页面的 web 应用中兼容性性不佳。每个窗口和框架子页面都具有段杜的执行上下文，每个上下文都包含独有的全局变量和一组构造函数。在两个不同框架页面中创建的两个数组继承自两个相同但相互独立的原型对象，其中一个框架页面中的数组不是另一个框架`Array()`构造函数的实例， instanceof 运算符结果是 false 。

### 9.5.2 constructor属性

另外一种识别对象是否属于某个类的方法是使用 constructor 属性。因为构造函数是类的公共标识，所以最直接的方法就是使用 constructor 属性，比如：

```js
function typeAndValue (x){
  if (x == null) return ""; // Null和undefined没有构造函数
  switch(x.constructor){
    case Number: return "Number:" + x; // 处理原始类型
    case String: return "String:" + x;
    case Date: return "Date:" + x; // 处理内置类型
    case RegExp: return "RegExp" + x; 
    case Complex: return "Complex" + x; // 处理自定义类型
  }
}
```

需要注意的是，在代码中关键字 case 后的表达式都是函数，如果改用 typeof 运算符或取到对象的 class 属性的话，它们应当改为字符串。

使用 constructor 属性检测对象属于某个类的技术不足之处和 instanceof 一样。在多个执行上下文的场景中它是无法正常的工作（比如在浏览器窗口的多个框架子页面中）。在这样的情况下，每个框架页面各自拥有独立的构造函数集合，一个框架页面中的 Array 构造函数和另外一个框架页面的 Array 构造函数不是同一个构造函数。

同样在 Javascript 并非所有的对象都包含 constructor 属性。在每个新创建的函数上默认会有 constructor 属性，但我们常常忽略原型上的 constructor 比如本章前面示例代码中定义的两个类，他们的实例都没有 constructor 属性。

### 9.5.3 构造函数的名称

使用 instanceof 运算符和 constructor 属性来检测对象所属的类有一个主要的问题，在多个执行上下文中存在构造函数的多个副本时，这两种方法的检测结果会出错。多个执行上下文的函数看起来是一模一样的，但它们是相互独立的对象，因此彼此也不相等。

一种可能的解决方案是使用构造函数的名字而不是使用构造函数本身作为类标识符。一个窗口里的 Array 构造函数和令一个窗口的 Array 构造函数是不相等的，但是它们的名字是一样的。在一些 Javascript 的实现中为了给函数对象提供一个非标准的属性name，用来表示函数的名称。对于那些没有那么属性的 Javascript 实现来说，可以将函数转换为字符串，然后从中提取出函数名（9.4中示例的代码给Function类添加了`getName()`方法，就是使用这种方法来得到函数名）。

下面定义的`type()`函数以字符串的方法返回对象的类型。它用typeof运算符来处理原始的值和函数。对于对象来说，它要么返回class属性的值要么返回构造函数的名字。`type()`函数用到了前面`classof()`函数和9.4节的Function,`getName()`方法。为了简单起见，这里包含了函数和方法的代码：

```js
// 例9.4：可以判断值的类型的type()函数
/**
  *以字符串的形式返回o的类型
  * -如果o是null，返回"null",如果o是NaN，返回“NaN”
  * -如果typeof所返回的值不是"object",则返回这个值（有一些javascript的实现将正则表达式识别为函数）
  * -如果o的类不是“Object”，则返回这个值
  * -如果o包含构造函数并且这个构造函数具有名称，则返回这个名称
  * -否则，一切返回“Object”
  **/
function type(o) {
  var t, c, n; // type,class,name
  // 处理null值的特殊情形
  if (o === null) return "null";
  // 另外一种特殊情形：NaN和它自身不相等
  if (o !== o) return "NaN";
  // 如果typeof的值不是“object”，则使用这个值
  // 这可以识别出原始值的类型和函数
  if ((t = typeof o) !== "object") return t;
  // 返回对象的类名，除非值为"Object"
  // 这种方式可以识别出大多数的内置对象
  if ((c = classof(o)) !== "Object") return c;
  // 如果对象构造函数的名字存在的话，则返回它
  if (o.constructor && typeof o.constructor === "function" && (n = o.constructor.getName())) return n;
  // 其它的类型都无法识别 一律返回“Object”
}
// 返回对象的类
function classof(o){
  return Object.prototype.toString.call(o).slice(8,-1);
};
// 返回函数的名字，（可能是空白串），不是函数返回null
Function.prototype.getName = function(){
  if("name" in this) return this.name;
  return this.name = this.toString().match(/function\s*([^(]*)\(/)[1];
};
```

这种使用函数的名字来识别对象的做法和使用 constructor 属性一样有一个问题：并不是所有的对象都具有 constructor 属性。此外，并不是所有的函数都有名字。如过使用不带名字的函数定义表达式（参照4.3节）定义一个构造函数，`getName()`方法则会返回空字符串。

```js
//这个构造函数没名字
var Complex = function(x, y){
  this.r = x; this.i = y;
}
//这个构造函数有名字
var Range = function Range(f, t){
  this.from = f, this.to = t;
}
```
### 9.5.3 鸭式辨型

上文所描述的检测对象的类的各种技术，多少都有些问题，至少在客户端 Javascript 中是如此。解决的办法就是规避掉这些问题，不要关注“对象的类是什么”，而是关注“对象的类能做什么”。这种思考问题的方式在 Python 和 Ruby 中非常普遍，被称为“鸭式辨型”。

> 像鸭子一样走路、游泳并且嘎嘎叫的鸟就是鸭子

对于 Javascript 程序员来说，“如果一个对象可以像鸭子一样走路、游泳并且嘎嘎叫，就认为这个对象就是鸭子，哪怕它并不是从鸭子类的原型对象而继承而来的”

我们拿例 9.2 中的 Range 来举例。期初定义这个类用于描述数字的范围。但要注意，`Range()`构造函数并没有对实参进行检测确保实参是数字类型。但将参数使用“>”运算符进行比较运算，因为这里假定它们是可比较的。同样，`includes()`方法使用“<=”运算符进行比较，但没有对范围的结束点进行类似的假设。因为类并没有强制使用特定的类型，它的`inclides()`方法可以用作任何结束点，只要结束点可以用作关系运算符执行比较运算。

```js
var lowercase =new Range("a", "z");
var thisYear = new Range(new Date(2015,2,18),new Date(2016,2,18));
```

Range 类的`foreach()`方法中也没有显式地检测表示范围的结束点的类型，但`Math.ceil()`和“++”运算符表明它只能对数字结束点进行操作。

另外一个例子，回想一下在7.11节中所讨论的类数组对象，在很多场景下，我们并不知道一个对象是否真的是 Array 实例，当然可以通过判断是否包含非负的 length 属性来得知是否是 Array 的实例。我们说，“包含一个值是非负整数的length”是数组的一个特征————“会走路”，任何具有“会走路”这个正在的对象都可以当做数组来对待（在很多情形中）。

然而我们必须要了解的是，真正数组的 length 属性具有一些独有的行为，当添加时，数组长度会自动更新，当 length 属性设置一个更小的整数时，数组会被截断。我们说这些特征是“会游泳”和“嘎嘎叫”。如果所实现的代码需要“会游泳”且能“嘎嘎叫”，则不能使用只"会走路"的类似数组对象。

上文讲到的鸭式辨型的例子提到了进行对象的“<”运算符的职责以及 length 属性的特殊行为。当我们提到鸭式辨型时，往往是说检测对象是否实现了一个或多个方法。一个强类型的`triathlon()`函数所需要的参数必须是 TruAthlete 对象。而一种“鸭式辨型”式的做法是，只要对象包含`walk()`、`swim()`、`bike()`这三个方法就可以作为参数传入。同理，可以重新设计Range类，使用结束点对象的`compareTo()`和`succ()`方法来代替“<”和"++"运算符。

下面按照鸭式辨型的理念定义了`quacks()`函数。`quacks()`用以检查一个对象（第一个实参）是否实现了剩下的参数所表示的方法。对于除第一个参数外的每个参数，如果是字符串的话则直接检查是否存在以它命名的方法；如果是对象的话则检查第一个对象中的方法是否在这个对象中也具有同名的方法；如果参数是函数，则假定它是构造函数，函数将检查第一个对象实现的方法是否在构造函数的原型对象中也具有同名的方法。

```js
/**
  *利用鸭式辨型实现的函数
  **/
  //如果o实现了除第一个参数之外的参数所表示的方法，则返回true
function quacks(o /*,...*/ ) {
  for (var i = 1; i < arguments.length; i++) { //遍历o之后的所有参数
    var arg = arguments[i];
    switch (typeof arg) { //如果参数是
      case 'string': //直接用名字做检查
        if (typeof o[arg] !== "function") return false;
        continue;
      case 'function': //检查函数的原型对象上的方法
        //如果实参是函数，则使用它的原型
        arg = arg.prototype; //进入下一个case
      case 'object': //object:检测匹配的方法
        for (var m in arg) { //遍历每个对象的属性
          if (typeof arg[m] !== "function") continue; //跳过不是方法的属性
          if (typeof o[m] !== "function") return false;
        }
    }
  }
  //如果程序执行到了这里，则说明o实现了所有的方法
  return true;
}
```

关于上面`quacks()`函数还有一些地方是需要尤其注意的。首先，这里只是通过特定的名称来检测对象是否包含一个或多个值为函数的属性。我们无法得知这些已经存在的属性的细节信息，比如：函数是用来什么的？它需要多少参数，参数的类型是什么？然后这些是鸭式辨型的本质所在。如果是使用鸭式辨型而不是强制类型检测的方式定义API，那么创建的API应当更具有灵活性才可以，这样才能确保你提供给用户的API更安全可靠。

关于`quacks()`函数还有另一问题需要注意，就是它不能应用内置类。比如，不能通过`quacks(o,Array)`来检测o是否实现了Array中所有同名的方法。原因是内置类的方法都是不可枚举的，`quacks()`中的for/in循环无法遍历到他们（注意：在ECMAScript5中有一个补救办法，就是使用`Ojbect.getOwnPropertyNames()`）。

## 9.6 Javascript中的面向对象技术

到目前为止，我们讨论了 JavaScript 中的类的基础知识：面向对象的重要性、它和构造函数之间的联系、instanceof运算符是如何工作的等。本节将目标转向一些实际的例子（尽管这不是基础知识），包括如何利用 JavaScript 的类进行编辑。我们从两个重要的例子开始，这两个例子中的实现非常有意思，接下来我们将基础工作展开。

### 9.6.1 一个例子：结合类

集合（set）是一种数据结构，用以表示非重复值的无序集合。集合的基础方法包括添加值、检测值是否在集中中，这种集合需要一种通用的实现，以保证操作效率。 JavaScript 的对象是属性， 以及对于的值的集合。因此将对象只用作字符串的集合是大材小用。下面的例子用 JavaScript 实现了一个更加通用的 Set 类，它实现了从 JavaScript 值到唯一字符串的映射，然后将字符串用作属性名。对象和函数都不具备如此简明可靠的唯一字符串表示。因此，集合类必须给集合中的没一个对象或函数定义一个唯一的属性标识。

```js
/*值的任意集合*/
function Set(){//这是一个构造函数
  this.value = {}; //集合数据保存在对象的属性里
  this.n = 0; //集合中值的个数
  this.add.apply(this,arguments); //把所有参数都添加进这个集合
}

//将每个参数都添加至集合中
Set.prototype.add  = function(){
  for(var i = 0; i < arguments.length; i++){//遍历每个参数
    var val = arguments[i]; //待添加到集合中的值
    var str = Set._v2s(val); //把它转换为字符串
    if(!this.values.hasOwnProperty(str)){//如果不在集合中
      this.values[str] = val; //将字符串和值对于起来
      this.n++; //集合中值的计数加1
    }
  }
  return this; //支持链式方法调用
}

//从集合删除元素，这些元素由参数指定
Set.prototype.remove = function(){
  for (var i = 0; i<arguments.length; i++){//遍历每个参数
    var str = Set._v2s(arguments[i]); //将字符串和值对应起来
    if (this.values.hasOwnProperty(str)){//如果它在集合中
      delete this.values[str]; //删除它
      this.n--; // 集合中只的计算数减-
    }            
  }
  return this;//支持链式方法调用
}

//如果这个集合包含这个值，则返回true，否则返回false
Set.prototype.contains = function(value){
  return this.values.hasOwnProperty(set._v2s(value));
};

//返回集合的大小
Set.prototype.size = function(){
  return this.n;
};

//遍历集合中所有元素，在丁丁的上下文中调用f
Set.prototype.forEach = function(f,context){
  for(var s in this.values)//遍历集合中所有的字符串
  if(this.values.hasOwnProperty(s))//忽略继承的属性
  f.call(context,this.values[s]);//调用f，传入vaule
};

//这是一个内部函数 ，所有将任意的javascript值和唯一的字符串对应起来
Set._v2s = function(val){
  switch(val){
    case undefined: return'u';//特殊的原始值
    case null :return 'n'; //值只有一个字母
    case true: return 't'; //代码
    case false: return 'f'; 
    default: switch(typeof val){
      case 'number':return '#' + val; //数字带有#前缀
      case 'string':return '"' + val; //字符串都带有"前缀
        default:return '@' + objectId(val); //Object and funcs get @
    }
  }
  //对应任意对象来说，都返回一个字符串
  //征对不同对象，这个函数会返回不同的字符串
  //对于同一个对象的多次调用，总会返回相同的字符串
  //为了做到这一点，它给o创建了一个属性，在ECMAScript5中，这个属性是不可枚举且是可读的
  
  function objectId(o){
    var prop = "|**objectid**|"; //私有属性，用以存放id
    if (!o.hasOwnProperty(prop)) //对公对象没有id
    o[prop] = set._v2s.next++; //将下一个值赋值给他
    return o[prop]; //返回这个id
  }
};
Set._v2s.next = 100; //设置初始id值
```

### 9.6.2 一个例子：枚举类型

枚举类型（enumerated type）是一种类型，它的值是有限集合，如果值定义为这个类型则该值是可以列出（或“可枚举”）的。在 C 及其派生语言中 ，枚举类是通过关键字 enum 声明的。 enum 是 ECMAScript 5 中的保留字（还未使用），很有可能在将来就会内置支持枚举类型。到那时候，下面的例子展示了如何在 JavaScript 中定义枚举类型的数据。需要注意的是，这里用到了`inherit()`函数。
下面的第二个例子包含一个单独函数`enumeration()`。但它不是构造函数，它并没有定义一个名叫“enumeration”的类，相反，它是一个工厂方法，每次调用它都会创建并返回一个新的类。比如：

```js
//使用4个值创建新的Coin类：比如Coin.Penny,Coin.Nickel等
var Coin = enumeration({Penny:1,Nickel:5,Dime:10,Quarter:25});
var c = Coin.Dime; //这是新类的实例
c instanceof Coin; //=>true:instanceof正常构造
c.constructor == Coin  //=>true: 构造函数的属性正常工作
Coin.Qiarter + 3*Coin.Nickel //=>40:将值转换为数字
Coin.Dime == 10; //=>true:更多转换为数字的例子
Coin.Dime > Coin.Nickel //=>true关系运算符正常工作
String(Coin>Dime) + ":" + Coin.Dime //=>"Dime:10":强制转换为字符串
```

这个 JavaScript 清楚的展示了 JavaScript 类的灵活性， JavaScript 中的类要比 C++ 和 Java 语言中的静态类要更加灵活。

```js
/*javascript中的枚举类型*/
//这个函数创建一个新的枚举类型，实参对象表示类的每个实例的 名字和值
//返回值是一个构造函数，它标识这个新类
//注意，这个构造函数也会抛出异常：不能使用它来创建该类型的新实例
//返回的构造函数包含：名/值对于的映射表
//包括由值组成的数组，以及一个foreach()迭代器函数
function enumeration(namesToValues) {
//这个虚拟的构造函数是返回值
var enumeration = function() {
  throw "Cant not Istantiate Enumerations";
};
//枚举值继承自这个对象
var proto = enumeration.prototype = {
  constructor: enumeration, //表示类型
  toSting: function() {
    return this.name;
  }, //返回名字
  valueOf: function() {
    return this.value;
  }, //返回值
  toJSON: function() {
    return this.name;
  } //转换为JSON
};
enumeration.values = []; //存放枚举对象的数组
//现在创建新类型的实例
for (name in namesToValues) { //遍历每个值
    var e = inherit(proto); //创建一个代表它的对象
    e.name = name; //给它一个名字
    e.value = namesToValues[name]; //给它一个值
    enumeration[name] = e; //将它设置为构造函数的属性
    enumeration.values.push(e); //将它存储到数值数组中
}
//一个类方法，用来对类的实例进行迭代
enumeration.foreach = function(f, c) {
    for (var i = 0; i < this.values.length; i++) f.call(c, this.values[i]);
};
//返回标识这个新类型的构造函数
return enumeration;
}
```

如果用这个枚举类型实现一个“hello world”小程序的话，就可以使用枚举类型表示一副扑克牌。下面的例子使用`enumeration()`函数实现了这个表示一副扑克牌的类（本例子的最初作者是Joshua Bloch,最初是基于java写的）。

```js
/*使用枚举类来表示一副扑克牌*/
//定义一个表示“玩牌”的类
function Card(suit, rank) {
  this.suit = suit; //每张牌都有花色
  this.rank = rank; //以及点数
}
//使用枚举类定义花色和点数
Card.Suit = enumeration({
  Clubs: 1,
  Diamonds: 2,
  Hearts: 3,
  Spades: 4
});
Card.Rank = enumeration({
  Two: 2,
  Three: 3,
  Four: 4,
  Five: 5,
  Six: 6,
  Seven: 7,
  Eigth: 8,
  Nine: 9,
  Ten: 10,
  Jack: 11,
  Queen: 12,
  King: 13,
  Ace: 14
});
//定义用以描述牌面的文本
Card.prototype.toString = function() {
  return this.rank.toString() + "of" + this.suit.toString();
};
//比较扑克牌中两张牌的大小
Card.prototype.compareTo = function(that) {
  if (this.rank < that.rank) return -1;
  if (this.rank > that.rank) return 1;
  return 0;
};
//以扑克牌的玩法规则对牌进行排序的函数
Card.orderByRank = function(a, b) {
  return a.compareTo(b);
};
//以桥牌的玩法规则对扑克牌进行排序的函数
Card.orderBySuit = function(a, b) {
  if (a.suit < b.suit) return -1;
  if (a.suit > b.suit) return 1;
  if (a.rank < b.rank) return -1;
  if (a.rank > b.rank) return 1;
  return 0;
};
//定义用以表示一副标准扑克牌的类
function Deck() {
  var cards = this.cards = [];
  //一副牌就是由牌组组成的数组
  Card.Suit.foreach(function(s) { //初始化这个数组
    Card.Rank.foreach(function(r) {
      cards.push(new Card(s, r));
    });
  });
}
//洗牌的方法：重新洗牌并返回洗好的牌
Deck.prototype.shuffle = function() {
  //遍历数组中的每个元素，随机找出牌面最小的元素，并与之（当前遍历的元素）交换
  var deck = this.cards,
    len = deck.length;
  for (var i = len - 1; i > 0; i--) {
    var r = Math.floor(Math.random() * (i + 1)),
      temp; //随机数
    temp = deck[i], deck[i] = deck[r], deck[r] = temp; //交换
  }
  return this;
};
//发牌的方法，返回牌的数组
Deck.prototype.deal = function(n) {
  if (this.cards.length < n) throw "Out of cards";
  return this.cards.splice(this.cards.length - n, n);
};
//创建一副新扑克，洗牌并发牌
var deck = (new Deck()).shuffle();
var hand = deck.deal(13).sort(Card.orderBySuit);
```
### 9.6.3 标准转换方法

3.8.3和6.10节讨论了对象类型转化所多用到的重要方法，有一些方法是需要做类型转换时由javascript解释器自动调用的。不需要为定义的每个类都实现这些方法，但这些方法的确非常重要，如果没有为自定义的类实现这些方法，也应当是有意为之，而不应当因为疏忽而漏掉了它们。

最重要的方法首当`toString()`。这个方法的作用是返回一个表示这个对象的字符串。在希望使用字符串的地方用到对象的话（比如将对象用作属性名或使用“+”运算符来进行字符串的链接运算）， JavaScript 会自动调用这个方法，如果没有实现这个方法，类会默认的从`Object.prototype`中继承`toString()`方法，这个方法的运算结果是“[object object]”，这个字符串的用处不大。`toString()`方法应当返还一个可读的字符串，这样最终用户才能将这个输出值利用起来，然而有时候并不一定非要如此，不管怎样，可以返回可读字符串的`toString()`方法也会让程序调试变得更加轻松。例如上文中的 Range 类和 Complex 类都定义了`toString()`方法。

`toLocaleString()`和`toString()`极为类似：`toLocaleString()`是以本地敏感性（locale-sensitive）的方式来讲对象转换为字符串。默认情况下，对象所继承的`toLocaleString()`方法只是简单的调用`toString()`方法。有一些内置类型包含有用的`toLocaleString()`方法用以实际上返回本地化相关的字符串，如果需要为对象到字符串的转换定义`toString()`方法，那么同样需要定义`toLocaleString()`方法处理本地化的对象到字符串的转换。下面的Set类中的定义中会有相关代码。

第三个方法是`valueOf()`，它用来将对象转换为原始值。比如，当数学运算符（除了“+”运算符）和关系运算符作用于数字文本表示的对象时，会自动调用`valueOf()`方法。大多数对象都没有合适的原始值来表示它们，也没有定义这个方法。但在枚举类型中实现说明`valueOf()`方法是非常重要。

第四个方法是`toJSON()`，这个方法是由`JSON.stringify()`自动调用的。JSON格式用于序列化良好的数据结构，而且可以处理 JavaScript 原始值、数组和纯对象。它和类无关，当对于一个对象执行序列化操作时，将会忽略对象的原型和构造函数。比如将 Range 对象或 Complex 对象作为参数传`JSON.stringify()`，将会返回诸如`{"form":1,"to":3}`或`{"r":1,"i":-1}`这种字符串。如果将这些字符串传入传入`JSON.parse()`，则会得到一个和 Rangge 对象和 Complex 对象具有相同的属性和纯对象，但这个对象不会包含从 Range 和 Complex 继承的方法。

这种序列化操作非常适用于诸如 Range 和 Complex 这种类，但对于其他一些类则必须自定义`toJSON()`方法来定制个性化的格式。如果一个对象有`toJSON()`方法,`JSON.stringify()`并不会传入的对象做序列化操作，而会调用`toJSON()`来执行序列化操作（序列化的值可能是原始值也可能是对象）。比如Date对象的`toJSON()`方法会返回一个表示日期的字符串。例如上上个例子的枚举类型也是如此：它们的`toJSON()`方法和`toString()`方法完全一样。如果要模拟一个集合，最接近的 JSON 表示方法就是数组，因此在下面的例子中将定义的`toJSON()`方法用以将集合对象转换为值数组。

在下面的例子中，Set 类并没有定义上述方法中的任何一个。 JavaScript 中没有那个原始值表示集合，因此也没必要定义`valueOf()`方法，但该类包含`toString()`、`toLocaleString()`、和`toJSON()`方法。可以用如下代码来实现。注意`extend()`函数的用法，这里使用`extend()`来向`Set.prototype`来添加方法：

```js
//将这些方法添加至Set类型的原型对象中
extend(Set.prototype, {
  //将集合转换为字符串
  toString: function() {
    var s = "{",
      i = 0;
    this.foreach(function(v) {s += ((i++ > 0) ? "," : "") + v;});
    return s + "}";
  },
  //类似toString,但是对于所有的值都将调用toLocaleString()
  toLocaleString: function() {
    var s = "{",i = 0;
    this.foreach(function(v) {
      if (i++ > 0) s += ",";
        if (v == null) s += v; //null和undefined
        else s += v.toLocaleString(); //其它情况
    });
    return s + "}";
  },
  //将集合转换为值数组
  toArray:function() {
    var a = [];
    this.foreach(function(v) {a.push(v);});
    return a;
  }
});
//对于要从JSON转换为字符串的集合都当做数组来对待
Set.prototype.toJSON = Set.prototype.toArray;
```

### 9.6.4 比较方法

JavaScript 的相等运算符比较对象时，比较的是引用而不是值。也就是说，给定两个对象引用，如果要它们是否指向同一个对象，不是检查者两个对象是否具有相同的属性名和相同的属性值，而是直接比较这两个单独的对象是否相等，或者比较它们的顺序（就像"<"和">"运算符进行的比较一样）。如果定义一个类，并且希望比较实例，应该定义合适的方法来执行比较操作。

Java 编程语言有很多用于对象比较的方法，将 Java 中的这些方法借用到 JavaScript 中是一个不错的注意。为了能让自定义类的实例具备比较的功能，定义一个名叫`equals()`实例方法。这个只能接收一个实参，如果这个实参和调用此方法的对象相等的话则返回true。当然所说的“相等”的含义是根据类的上下文来决定的。对于简单的类，可以通过简单地比较它们的 constructor 属性来确保两个对象是相同的类型，然后比较两个对象的实例属性以保证它们的值相等。上文的Complex类就实现了这一的`equals()`方法，我们可以轻易地为 Range 类也实现类似的方法：

```js
//Range类重写它的constructor属性，现在将它添加进去
Range.prototype.constructor = Range;
//一个Range对象和其它不是Range的对象均不相等
//当且仅当两个范围的端点相等，它们才相等
Range.prototype.equals = function(that){
  if(that == null) return false; //处理null和undefined
  if(that.constructor !== Range) return false;//处理非Range对象
  //当且仅当端点相等，才返回true
  return this.form == that.from && this.to == that.to;
}
```

给Set类定义`equals()`方法稍微有些复杂。不能简单地比较两个集合的values属性，还要进行更深层次的比较：

```js
Set.prototype.equals = function(that){
  //一些次要情况的便捷处理 
  if(this === that) return true;
  
  //如果that对象不是一个集合，它和this不相等
  //我们用到了instanceof,使得这个方法可以用于Set的任何子类
  //如果希望采用鸭辨型的方法，可以降低检测的严格程度
  //或者可以通过this.constructor == that.constructor来加强检查的严格程度
  //注意，null和undefined这个值是无法用于instanceof运算的
  if(!(that instanceof Set))return false;
  
  //如果这两个集合的大小不一样，则它们不相等
  if (this.size() != this.size()) return false;
  
  //现在检测两个集合中的元素是完全一样
  //如过两个集合不相等，则通过抛出异常来终止foreach循环
  try{
    this.foreach(function(v){if(!that.contains(v)) throw false;});
    return true; //所有的元素都匹配：两个集合相等
  }catch(x){
    if (x === false) return false;//如果集合中有元素在另一个元素集合中不存在
    throw x; //重新抛出异常
  }
};
```

按照我们需要的方式比较对象是否相等常常是很有用的。对于某些类来说，往往需要比较一个实例“大于”或者“小于”另外一个示例。比如：你可能会基于Range对象的下边界来定义实例大小关系。枚举类型可以根据名字的字母顺序来定义实例的大小，也可以根据它包含的数值（假设它包含的都是数字）来定义大小。令一方面，Set对象其实是无法排序的。

如果将对象用于 JavaScript 的关系比较运算，比如“<”和"<=", JavaScript 会首先调用对象的`valueof()`方法，如果这个方法返回一个原始值，则直接比较原始值。例如上上例子中由`enumeration()`方法所返回的枚举类型包含`valueOf()`方法，因此可以使用关系运算符对它们做有意义的比较。但大多数没有`valueOf()`方法，为了按照显式定义规则来比较这些类型的对象，可以定义一个叫`compareTo()`方法（同样，这里遵照java中的命名约定）。

`compareTo()`方法只能接收一个参数，这个方法将这个参数和调用它的对象进行比较。如果this对象小于参数对象，如果this对象小于参数对象，`compareTo()`应当返回比0小的值。如果this对象大于参数对象，应当返回比0大的值。如果两个对象相等，应当返还0。这些关于返回值的约定非常重要，这样我们可以用下面的表达式替换掉关系比较和相等性运算符：

| 待替换  | 替换为                 |
|--------|---------------------|
| `a<b`  | a.compareTo(b)<0    |
| `a<=b` | a.compareTo(b) <= 0 |
| `a>b`  | a.compareTo(b)>0    |
| `a>=b` | a.compareTo(b)>=0   |
| `a==b` | a.compareTo(b)==0   |
| `a!=b` | a.compareTo(b)!=0   |


在Card类定义了该类的`compareTo()`方法，可以给Range类添加一个类似的方法，可以给Range类添加一个类似的方法，用以比较它们的下边界：

```js
Range.prototype.compareTo = function(that){
  return this.from - that.from;
};
```

需要注意的是，这个方法中的减法操作根据两个 Range 对象的关系正确地返回了小于0、等于0、和大于0的值。`Card.Rank`枚举值包含`valueOf()`,其实也给Card类实现类似的`compareTo()`方法。

上文所提到的`equals()`方法对其参数执行了类检查，如果参数类型不合法则返回false。`compareTo()`方法并没有返回一个表示“两个值不能比较”的值，由于`compareTo()`如果没有对参数做任何类型检查，因此如果给`compareTo()`方法传入错误类型的参数，往往会抛出异常。

注意，如果两个范围对象的下边界相等，为Range类定义的`compareTo()`方法返回0。这意味着就`compareTo()`而言，任何两个起始点相同（这里所说的起始点相同就是下边界相同）的Range对象都相等。这个相等概念的定义和`equals()`方法定义的相等概念是相背的，`equals()`要求两个端点均相等才算相等。这种相等概念上的差异会造成很多bug，最好将Range类的`equals()`和`compareTo()`方法中处理相等的逻辑保持一致。这里是Range类修正后的`compareTo()`方法，它的比较逻辑和`equals()`保持一致，但当传入不可比较的值时任然会报错。

```js
//根据下边界来对Range对象排序，如果下边界相等则比较上边界
//如果传入非Range值，则抛出异常
//当且仅当this.equals(that)时，才返回0
Rang.prototype.compareTo = function(that){
  if(!(that instanceof Range))
  throw new Error("can not compare a Range with" + that);
  var diff = this.from - that.from;//比较下边界
  if(diff == 0) diff = this.to - that.to; //如果相等，比较上边界
  return diff;
};
```

给类定义了`compareTo()`方法，这样就可以对类实例组成的数组进行排序了。`Array.sort()`方法可以接收一个可选的参数，这个参数是一个函数，用来比较两个值的大小，这个函数返回值的约定和`compareTo()`方法保持一致，假定有了上文提到的`compareTo()`方法，就可以很方便地对Rangge对象组成数组进行排序了

```js
ranges.sort(function(a,b){return a.compareTo(b);});
```

排序运算非常重要，如果已经为类定义了实例方法`compareTo()`，还应当参照这个方法定义一个可传入两个参数的比较函数。使用`compareTo()`方法可以非常轻松地定义这个函数，比如：

```js
Range.byLowerBound = function(a,b){return a.compareTo(b);};
```

使用这个方法可以让数组排序的操作变得非常简单：

```js
ranges.sort(Rang.byLowerBound);
```

有些类可以有多方法进行排序，比如 Card 类，可以定义两个方法分别按照花色排序和按照点数排序。

### 9.6.5 方法借用

JavaScript 中的方法没有什么特别，无非是一些简单的函数，赋值给了对象的属性，可以通过对象来调用它。一个函数可以赋值给两个属性，然后作为两个方法来调用它。比如，我们在Set类中就这样做了，`toArray()`方法创建了一个副本，并让他可以和`toJSON()`方法一样完成同样的功能。

多个类中的方法可以共用一个单独函数。比如，Array类通常定义了一些内置的方法，如果定义了一个类，它的实例是类数组的对象，则可以从`Array.prototype`中函数复制至所定义的类的原型对象中。如果以经典面向对象语言的视觉来看 JavaScript 的话，把一个类的方法用到其他类中的做法也陈做“多重继承”（multiple inherittance）。然而在 JavaScript 并不是经典的面向对象语言，我们更倾向于将这种方法重用更正式的称为“方法借用”（borrowing）。

不仅Array的方法可以借用，还可以自定义泛型的方法（generic method）,下面的例子定义了泛型方法toString和equals，可以被Range/Complex和Card这些简单的类使用。如果Range类没有定义`equals()`方法，这样这样借用泛型方法`equals()`:

```js
Rang.prototype.equals = generic.equals;
```

注意，`genneric.equals()`只会执行浅比较，因此这个方法并不适合适用于太复杂的类，他们的实例属性通过其`equals()`方法指代对象。同样需求注意，这个方法包含一些特殊情况的程序逻辑，以处理新增至Set对象中的属性

```js
/*方法借用的泛型实现*/
var genric = {
  //返回一个字符串，这个字符串包含构造函数的名字（如果构造函数包含名字）
  //以及所有非继承来的、非函数属性的名字和值
  toString: function() {
    var s = '['
    //如果这个对象包含构造函数，且构造函数包含名字
    //如果这个名字作为返回字符串的一部分
    //需要注意的是函数的名字属性属性是非标准的，并不是在所有的环境中都可用
    if (this.constructor && this.constructor.name)
      s += this.constructor.name + ":";
    //枚举所有非继承且非函数的属性
    var n = 0;
    for (var name in this) {
      if (!this.hasOwnProperty(name)) continue; //跳过继承来的属性
      var value = this[name];
      if (typeof value === "function") continue; //跳过方法
      if (n++) s += ",";
      s += name + '=' + value;
    }
    return s + ']';
  },
  //通过比较this和that的构造函数和实例属性来判断它们是否相等
  //这种方法只适合用于那行实例属性是原始值的情况，原始值可以通过"==="来比较
  //这里还处理一种特殊情况，就是忽略由set类添加的特殊属性
  equals: function(that) {
    if (that == null) return false;
    if (this.constructor !== that.constructor) return false;
    for (var name in this) {
      if (name === "|**object**|") continue; //跳过特殊属性
      if (!this.hasOwnProperty(name)) continue; //跳过继承来的属性
      if (this[name] !== that[name]) return false; //比较是否相等
    }
    return true; //如果所有属性都匹配，两个对象相等
  }
};
```

### 9.6.6 私有状态

在经典的面向对象编程中，经常需要将对象的某个状态封装或隐藏在对象内，只有通过对象的方法才能访问这些状态，对外只暴露一些重要的状态变量可以直接读写。为了实现这个目的，类似 Java 的编程语言允许声明类的“私有”实例字段，这些私有字段只能被类的实例方法访问，且在类的外部都是不可见的。

我们可以通过将变量（或参数）闭包在一个构造函数内来模拟实现私有实例字段，调用构造函数会创建一个实例。为了做到这一点，需要在构造函数内定义一个函数（因此这个函数可以访问构造函数内部的参数和变量），并将这个函数赋值给新创建对象的属性。

下面的例子展示了对Rang类的令一种封装，新版的类的实例包含`from()`和`to()`方法用于返回范围的端点，而不是用from和to属性来获取端点。这里的`from()`和`to()`方法是定义在每个Range对象上 的，而不是从原型继承出来的。其它的`Range()`方法还是和之前一样定义在原型中，但获取端点的方式从之前直接从属性读取变成了通过`from()`和`to()`方法来读取

```js
/*对Range类读取端点的方法的简单封装*/
function Range(from,to){
  //不要将端点保存为对象的属性，想法定义存取器函数来返回端点的值
  //这些值都保存在闭包中
  this.from = function(){return from;};
  this.to = function(){return to;};
}
//原型上 的方法无法直接操作端点，他们必须调用存取器方法
Range.prototype={
  constructor:Range,
  includes:function(x){return this.from() <=x && x <= this.to();},
  foreach:function(f){
    for(var x = Math.ceil(this.from()),max = this.to(); x <= max; x++)f(x);
  },
  toString:function(){return "(" + this.from() + "..." + this.to() +")"; }
};
```

这个新的Range类定义了用于读取范围端点的方法，但没有定义设置端点的方法或属性。这让类的实例看起来是不可修改的，如果正确的话，一旦创建Range对象，端点数据就不可修改了。除非使用 ECMAScript 5 (9.3节)中的某些特性，但from和to的属性依然是可写的，并且Range对象实际上并不是真正可以不可修改的：

```js
var r = new Range(1,5);//一个不可修改的范围
r.from = function(){return 0;}; //通过方法替换来修改它
```

但需要注意的是，这种封装技术造成了更多的系统开销。使用闭包来封装类的状态的类一定比不使用分装的状态变量的等价类运行速度更慢，并占用更多内存。

### 9.6.7 构造函数的重载和工厂方法

有时候，我们希望对象的初始化有多重方式。比如，我们想通过半径和角度（极坐标）来初始化一个Complex对象，而不是通过实部和虚部来初始化，或者通过元素组成的数组来初始化一个Set对象，而不是通过传入构造函数的参数来初始化它。

有一个方法可以实现，通过重载（overload）这个构造函数能它根据传入参数的不同来执行不同的初始化方法。下面这段代码就是重载`Set()`构造函数的例子：

```js
function Set() {
  this.values = {}; //用这个对象的属性来保持这个集合
  this.n = 0; //集合中值的个数
  //如果传入一个类数组的对象，将这个元素添加至集合中
  //否则将所有的参数都添加至集合中
  if (arguments.length == 1 && isArrayLike(arguments[0]))
    this.add.apply(this, arguments[0]);
  else if (arguments.length > 0)
    this.add.apply(this.arguments);
}
```

这段代码所定义的`Set()`构造函数可以显式将一组元素作为参数列表传入，也可以传入元素组成的数组。但这个构造函数有多义性，如果集合的某个成员是一个数组就无法通过这个构造函数来创建这个集合了（为了做到这一点，需要首先创建一个空集合，然后显式调用`add()`方法）。

在使用极坐标来初始化复数的例子中，实际上并没有看到有函数重载。代表复数有两个维度的数字都是浮点数，除非给构造函数传入第三个参数，否则构造函数无法识别到底传入是极坐标还是直角坐标参数。相反，可以写一个工厂方法————一个类的用法用于返回一个实例。下面的例子即是使用工厂方法来返回一个使用极坐标初始化的Complex对象

```js
Complex.polar = function(r, theta) {
  return new Complex(r * Math.cos(thera), r * Math.sin(theta));
};
```

下面这个工厂方法用来通过数组初始化Set对象

```js
Set.formArray = function(a) {
  s = new Set(); //创建一个空集合
  s.add.apply(s, a); //将数组a的成员作为参数传入add方法
  return s;
};
```

可以给工厂方法定义任意名字，不同的名字工厂方法用以执行不同的初始化。但由于构造函数是类的共有标识，因此每个类只能有一个构造函数。但这并不是一个“必须遵守”的规则。在 JavaScript 中可以定义多个构造函数继承自一个原型对象的，如果这样做的话，这些构造函数的任意一个所创建的对象都属于同一类型。并不推荐这种技术法，但下面的示例代码使用这种技术定义了该类型的一个辅助构造函数。

```js
//Set类的一个辅助构造函数
function SetFromArray(a){
  //通过以函数的形式调用Set()来初始化这个新对象
  //将a的元素作为参数传入（apply()的第二个参数是一个数组，数组成员就是参数列表）
  Set.apply(this,a);
}
//设置原型，以便SetFromArray能创建Set的实例
SetFromArray.prototype = Set.prototype;

var s = new SetFromArray([1,2,3,4,5])
s instanceof Set; //=>true
```

## 9.7 子类

在面向对象编程中，类B可以继承自另外一个类A。我们将A称为父类（superclass）,将B称为子类（subclass）。B的实例从A继承了所有的实例方法。类B可以定义自己的实例方法，有些方法可以重载A的同名方法，这种做法称为“方法链”（method chaining）。同样，子类的构造函数`B()`有时需要调用父类的构造函数`A()`,这种做法称为“构造函数链”（constructor chaining）。子类还可以有子类，当涉及类的层次结构时，往往需要定义抽象类（abstract class）。抽象类中定义的方法没有实现。抽象类中的抽象方法是在抽象类的具体子类中实现的。

JavaScript 中创建子类的关键之处在于，采用合适的方法对原型对象进行初始化。如果类B继承自类A，`B.prototype`必须是`A.prototype`的后嗣。B的实例继承自B.prototype,后者同样也继承自`A.prototype`.本节将会对刚才提到的子类相关的术语做一一解释，还会介绍类继承的替代方案：“组合”（composition）。

从上文中的Set类开始讲解，本节将会讨论如何定义子类。如何实现构造函数链并重载方法，如何使用组合来代替继承，以及如何通过抽象类从实现中提炼出接口。本节以一个扩展的例子结束。这个例子定义了Set类的层次结构。注意本节开始的几个例子着重讲述了实现子类的基础技术，其中某些技术有重要的缺陷，后续几节会讲到。

### 9.7.1 定义子类

JavaScript 的对象可以从类的原型对象中继承属性（通常继承是方法）。如果O是类B的实例，B是A的子类，那么O也一定从A中继承了属性。为此，首先要确保B的原型对象继承A的原型对象，通过inherit函数可以这样来实现：

```js
B.prototype = inherit(A.prototype); //子类派生父类
B.prototype.constructor = B; //重载继承来的constructor属性
```

末尾这两行代码是在 JavaScript 中创建子类的关键。如果不这样做，原型对象仅仅是一个普通对象，它只继承自Object.prototype，这意味着你的类和所有的类一样是Object的子类。如果将这两行代码添加至defienClass()函数中（9.3）节，可以将它变成下面的例子中的defineSubclass()函数和Function.prototype.extend()方法：

```js
/*定义子类*/
//用一个简单的函数创建简单的子类
function defineSubclass(superclass, //父类的构造函数
  constructor, //新的子类的构造函数
  methods, //实例方法：复制至原型中
  statics) //类属性：复制至构造函数中
{
  //建立子类的原型对象
  constructor.prototype = inherit(superclass.prototype);
  constructor.prototype.constructor = constructor;
  //像对常规类一样复制方法和类属性
  if (methods) extend(constructor.prototype, methods);
  if (statics) extend(constructor, statics);
  //返回这个类
  return constructor;
}
//也可以通过父类构造函数的方法来做到这一点
Function.prototype.extend = function(constructor, methods, statics) {
  return defineSubclass(this, constructor, methods, statics);
};
```

下面的例子展示了不使用`defineSubclass()`函数如何“手动”实现子类。这里定义了Set的子类`SingletonSet.SingletonSet`是一个特殊的集合，它是只读的，而且含有单独的常量成员。

```js
/*SingletonSet:一个简单子类*/
//构造函数
function SingletonSet(member) {
  this.member = member; //记住这个集合中这个唯一的成员
}
//创建一个原型对象，这个原型对象继承自S儿童的原型
SingletonSet.prototype = inherit(Set.prototype);
//给原型添加属性
//如果有同名属性就覆盖Set.prototype中的同名属性
extend(SingletonSet.prototype,{
  //设置合适的constructor属性
  constructor:SingletonSet,
  //这个集合是只读的 ：调用add()和remove()都会报错
  add:function(){throw "read-only set";},
  remove:function(){throw "read-only set";},
  //singletonSet的实例中永远只有一个元素
  size:function(){return 1;},
  //这个方法只调用一次，传入这个集合的唯一成员
  foreach:function(f,context){f.call(context,this.member);},
  //contains()方法非常简单：只需简单传入的值是否匹配这个集合唯一的成员即可
  contains:function(x){return x === this.member;}
});
```

这里的SingletonSet类是一个比较简单的实现，它包含5个简单的方法定义。它实现了5个核心的Set方法，但从它的父类中继承了`toString()`,`toArray()`和`equals()`方法。定义子类就是为了继承这些方法。比如，Set类的`equals()`方法（在9.4节中定义）用来对Set实例进行比较，只要Set的实例包含`size()`和`foreach()`方法，就可以通过`equals()`比较。

因为SingletonSet是Set的子类 ，所有它自动继承了`equals()`的实现，不用再实现一次。当然，如果想要简单的实现方式，那么给SingletonSet类定义它自己的`equals()`版本会更高效一些：

```js
SingletonSet.prototype.equals = function(that){
  return that instanceof Set && that.size() ==1 && that.contains(this.member);
};
```

需要注意的是，SingletonSet不是将Set中的方法列表静态地借用过来，而是动态的从Set类继承方法。如果给`Set.prototype`添加新的方法，Set和SingletonSet的所有实例会立即拥有这个方法（假定SingletonSet没有定义与之同名的方法）。

### 9.7.2 构造函数和方法链

最后一节的SingletonSet类定义了全新的集合实现，而且将它继承自其父类的核心方法全部替换。然而定义子类的时，我们往往希望对父类的行为进行修改或扩充，而不是完全替换掉它们。为了做到这一点，构造函数和子类的的方法需要调用或链接到父类构造函数和父类的方法。

下面的例子对此做了展示。它定义了Set的子类NonNullSet,它不允许null和undefined作为它的成员。为了使用这种方式对成员做限制，NonNullSet需要在其add()方法中对null和undefined值做检测。但它需要完全重新实现一个`add()`方法，因此它调用了父类中的这个方法。注意，`NonNullSet()`构造函数同样不需要重新实现，它只须将它的参数传入父类构造函数（作为函数 来调用它，而不是通过构造函数来调用），通过父类的构造函数来初始化新创建的对象。

```js
/*在子类中调用父类的构造函数和方法*/
/**
*NonNullSet 是Set的子类，它的成员不能是null和undefined
* */
function NonNullSet() {
  //仅链接到父类
  //作为普通函数调用父类的构造函数来初始化通过构造函数调用创建的对象
  Set.apply(this, arguments);
}
//将NonNullSet设置为Set的子类
NonNullSet.prototype = inherit(Set.prototype);
NonNullSet.prototype.constructor = NonNullSet;
//为了将null和undefined排除在外，只须重写add()方法
NonNullSet.prototype.add = function() {
  //检测参数是不是null货站undefined
  for(var i = 0; i < arguments.length; i++)
  if (arguments[i] == null)
    throw new Error("can not add null or  undefined to a NonNullSet");
    //调运父类的add()方法以只须实际的插入操作
    return Set.prototype.add.apply(this,arguments);
};
```

让我们将这个非null集合的概念推而广之，称为“过滤后的集合”，这个集合中成员首先传入一个过滤函数再执行添加操作。为此，定义一个类工厂函数，类似`enumeration()`函数，传入一个过滤函数，返回一个新的Set子类，实际上，可以对此做进一步的通用化的处理，定义一个可接受两个参数的类工厂：子类和用于add()方法的过滤函数。这个工厂方法称为`filteredsetSubclass()`,并通过这样的代码来使用它：

```js
//定义一个只能保持字符串的“集合”类
var StringSet = filteredSetSubclass(set, function(x) {return typeof x === "string";});
//这个集合类的成员不能是null、undefeined或函数
var Myset = filteredSetSubclass(NonNullSet,function(x){return typeof x !== "function";});
```

下面的这个例子是工厂函数的实现代码。注意，这个例子中的方法链和构造函数链和NonNullset中的实现是一样的。

```js
/**
*类工厂和方法链
* 这个函数返回具体的Set类子链
* 并重写该类的add()方法用以对添加的元素做特殊的过滤
**/
function filteredSetSubClass(superclass,filter){
  var constructor = function(){//子类的构造函数
    superclass.apply(this,arguments); //调用父类构造函数
  };
  var proto = constructor.prototype = inherit(superclass.prototype);
  proto.constructor = constructor;
  proto.add = function(){
    //在添加任何成员之前首先使用过滤器将所有参数进行过滤
    for(var i=0; i<arguments.length;i++){
        var v = arguments[i];
        if(!filter(v)) throw ("value" + v +"rejected by filter");
    }
    //调运父类的add()方法
    superclass.prototype.add.apply(this,arguments);
  };
  return constructor;
}
```

上面的例子中一个比较有趣的事情是，用一个函数将创建子类的代码包装起来，这样就可以在构造函数和方法链中使用父类的参数，而不是通过写死某个父类的名字来使用它的参数。也就是说，如果想修改父类 ，只须修改下一处的代码即可，而不比对每个用到父类类名的地方都做修改。已经有足够的理由证明这种技术的可行性，即使不是定义类工厂的场景中，这种技术也是值得提倡使用的。比如，可以这样使用包装函数和上面的例子中`Function.prototype.extend()`方法来重写NonNullSet:

```js
var NonNullSet = (function() { //定义并立即调用这个函数
var superclass = Set; //仅指定父类
return superclass.extend(function() {
  superclass.apply(this.arguments);
}, //构造函数
{
  add: function() {
      //检测参数是否为null或undefined
      for (var i = 0; i < arguments.length; i++)
          if (arguments[i] == null)
            throw new Error("can not add null or undefined");
          //调用父亲类的add()方法以只须实际的插入操作
      return superclass.prototype.add.apply(this, arguments);
  }
});
}());
```
最后，值得强调是的，类似这种创建工厂的能力是javascript语言动态特性的一个体现，类工厂是一种非常强大和有用的特性，这在java和c++等语言中是没有 的。

### 9.7.3 组合vs子类

在前一节中，定义的集合可以根据特定的标准对集合成员做限制，而且使用了子类的技术来实现这种功能，所创建的自定义子类使用了特定的过滤函数来对集合中的成员做限制。父类和过滤函数的每个组合都需要创建一个新的类。

然后还有另一种更好的方法来完成这种需求，即面向对象编程中一条广为人知的设计原则：“组合优于继承”（可参照Erich Gamma et al所著的《Design Patterns》和Joshua Bloch所著的《Effective Java》）。这样可以利用组合的原理定义一个新的集合实现，它“包装”了另外一个集合对象，在将受限制的成员过滤掉之后会用到这个（包装的）集合对象。下面的例子展示了其工作原理：

```js
/*使用组合代替继承的集合的实现*/
/**
*实现一个FilteredSet,它实现包装某个指定的“集合”对象。
* 并对传入add()方法的值应用的了某种指定的过滤器
* “范围”类中其他所有的核心方法延续到包装后的实例中
**/
var FileredSet = Set.extend(
  function FileredSet (set,filter){//构造函数
    this.set = set;
    this.filter = filter;
  },
  {//实例方法
    add:function(){
        //如果已经有过滤器，直接使用它
      if(this.filter){
          for(var i = 0;i<arguments.length;i++){
            var v =arguments[i];
            if(!this.filter(v))
            throw new Error ("FilteredSet:value" + v + "rejeced by filter");
          }
        }
        //调用set中的add()方法
        this.set.add.apply(this.set,arguments);
        return this;
    },
    contains:function(v){return this.set.contains(v);},
    size:function(){return this.set.size();},
    foreach:function(f,c){this.set.foreach(f,c);}
  }
);
```

在这个例子中使用组合的一个好处是，只须创建一个单独的FilteredSet子类即可。可以利用这个类的实例来创建任意带有成员限制的集合实例。比如不用上文中定义的NonNullSet类，可以这样做：

```js
var s = new FilteredSet(new Set(),function(x){return x !== null;});
```

甚至还可以对已经过滤的集合进行过滤：

```js
var t = new FileredSet(s,function(x){return !(x instanceof Set);})
```

### 9.7.4 类的层次结构和抽象类

在上节中给出了“组合优于继承”的原则，但为了将这条原则阐述清楚，创建了Set的子类。这样做的原因就是最终得到类是Set的实例（本书作者这里表示稍微有含糊，作者的意思应该就是“Set子类的实例也是Set的实例”，而不是“子类是Set的实例”）。它会从Set继承有用的辅助方法，比如`toString()`和`equals()`。尽管这是一个很实际的原因，但不用创建类似Set类这样具有类的子类也可以很好的用组合来实现“范围”。上文中的SingletonSet类可以有另外一种类型的实现，这个类还是继承自Set，因此它可以继承很多辅助方法，但它的实现和其父类的实现完全不一样。SingletonSet并不是Set类的专用版本，而是完全不同的另一种Set。在类层次结构中SingletonSet和Set应当是兄弟的关系，而非父子关系。

不管是在经典面向对象编程的语言中还是在javascript中，通行的解决办法是（这里指的是实现类的不同定制版本的解决办法，更直接的讲究是实现多态的方法）“从实现中抽离出接口”。假定定义了一个AbstractSet类，其中定义了一些辅助方法比如`toString()`,但并没有实现诸如foreach()的核心方法。这样，实现Set、SingletonSet和FilteredSet都是这个抽象类的子类，FilteredSet和SlingletonSet都不必再显示为了某个不相关的子类了。

下面的例子在这个思路上更进了一步，定义了一个层次结构的抽象的集合类。bstractSet只定义了一个抽象方法，`contains()`。任何类只要"声称"自己是一个表示范围的类，就必须定义这个`contains()`方法。然后定义AbstractSet的子类AbstractSet的子类AbstractEnumerableSet。这个类增加了抽象的`size()`和`foreach()`方法，而且定义了一些有用的非抽象方法(toString/toArray/equals等)AbstractEnumerableSet并没有定义`add()`和`remove()`方法，它只代表只读集合。SingletonSet可以实现为非抽象子类。最后，定义了AbstractEnumerableSet的子类AbstractWritableSet。这个final抽象集合定义了抽象方法`add()`和`remove()`，并实现了诸如union()和intersection()等具体方法，这两个方法调用了`add()`和`remove()`。AbstractWritableSet是Set和FilteredSet相应的父类。但这个例子中并没有实现它。而是实现了一个新的名叫ArraySet的非抽象类。

这个例子很长，但是还是应当完整的看一遍。这里用到了`Function.prototype.extend()`作为创建子类的快捷方法。

```js
/*抽象类和非抽象类Set类的层次结构*/
//这个函数可以用作任何抽象方法，非常方便
function abstractmethod() {throw new Error("abstract method");} 
/*AbstractSet类定义了一个抽象方法：contains()*/
function AbstractSet(){throw new Error("can not instantiate abstract classes");}
AbstractSet.prototype.contains = abstractmethod;

/**
*NotSet是AbstractSet的一个非抽象子类
* 所有不在其他集合中的成员都在这个集合中
* 因为它是在其它集合中不可写的条件下而定义的，同时由于它的成员个数是无限个，因此它是不可枚举的
* 我们只能用它来检测元素成员的归属情况
* 注意我们使用了Function.prototype.extend()方法来定义这个子类
**/
var NotSet = AbstractSet.extend(
  function NotSet(set){this.set = set;},
  {
    contains:function(x){return !this.set.contains(x);},
    toString:function(x){return "~" + this.set.toString();},
    equals:function (that){
      return that instanceof NotSet && this.set.equals(that.set);
    }
  }
);

/**
* AbstractEnumerableSet是AbstractSet的一个抽象子类
* 它定义了抽象方法size()和foreach(),然后实现了非抽象方法isEmpty、toArray、to[locale]String()和equals()方法
* 子类实现了contains()、size()和foreach()，这三个方法可以很轻易的地调用这5个非抽象方法
**/
var AbstractEnumerableSet = AbstractSet.extend(
  function(){throw new Error("can not instantiate abstract classes");},
  {
    size:abstractmethod,
    foreach:abstractmethod,
    isEmpty:function(){return this.size()==0;},
    toString:function(){
      var s = "{",i = 0;
      this.foreach(function(v){
        if(i++ > 0) s += ",";
        s += v;
      });
      return s + "}";
    },
    toLocaleString:function(){
      var s = "{", i = 0;
      this.foreach(function(v){
        if (i++ > 0) s += ",";
        if (v == null) s += v; //null和undefined
        else s += v.toLocaleString(); //其它情况下
      });
      return s + "}";
    },
    toArray:function(){
      var a = [];
      this.foreach(function(v){a.push(v);});
      return a;
    },
    equals: function(that){
      if(!(that instanceof AbstractEnumerableSet)) return false;
      //如果他们的大小不同，则它们不相等
      if(this.size() != that.size()) return false;
      //检测每一个元素是否也在that中
      try{
        this.foreach(function(v){if (!that.contains(v)) throw false;});
        return true; //所有的元素都匹配：集合相等
      }catch(x){
        if(x === false)return false; //集合不相等
          throw x; //发生了其它的异常：重新抛出异常
      }
    }
  }
);

/**
  * SingletonSet是AbstractEnumerableSet的非抽象子类
  * singleton的集合是只读的，它只包含一个成员
  **/
var SingletonSet = AbstractEnumerableSet.extend(
  function SingletonSet(member){this.member = member;},
  {
    contains:function(x){return x === this.member;},
    size:function(){return 1;},
    foreach:function(f,ctx){f.call(ctx,this.member);}
  }
);

/**
*AbstractWriteableSet是AbstractEnumerableSet的抽象子类
* 它定义了抽象方法add()和remove()
* 然后实现了非抽象方法union(),intersection()和difference()
**/
var AbstractWritableSet = AbstractEnumerableSet.extend(
  function(){throw new Error("can not instantiate abstract classes");},
  {
    add:abstractmethod,
    remove:abstractmethod,
    union:function(that){
      var self = this;
      that.foreach(function(v){self.add(v);});
      return this;
    },
    intersection:function(that){
      var self = this;
      this.foreach(function(v){if(!that.contains(v)) self.remove(v);});
      return this;
    },
    difference:function(that){
      var self = this;
      that.foreach(function (v){self.remove(v);});
      return this;
    }
  }
);

/**
*ArraySet是AbstractWritableSet的非抽象子类
* 它以数组的形式表示集合中的元素
* 对于它的contains()方法使用了数组的线性查找，因为contains()方法的算法复杂度是0(n)而不是0(1)
* 它非常使用于相对小型的结合，注意，这里的实现用到了ECMAscript5数组方法indexof()和forEach()
**/
var ArraySet = AbstractWritableSet.extend(
  function ArraySet(){
      this.values = [];
      this.add.apply(this,arguments);
  },
  {
    contains:function(v){return this.values.indexOf(v) != -1;},
    size:function(){return this.values.forEach(f,c);},
    add:function(){
      for (var i = 0; i<arguments.length; i++){
        var arg =arguments[i];
        if(!this.contains(arg)) this.values.push(arg);
      }
      return this;
    },
    remove:function(){
      for(var i = 0; i < arguments.length; i++){
        var p = this.values.indexOf(arguments[i]);
        if(p == -1) continue;
        this.values.splice(p,1);
      }
      return this;
    }
  }
);
```

## 9.8 ECMAScript5中的类

ECMAScript5给属性特性增加了方法（getter、setter、可枚举性、可写性和可配置性），而且增加了对象的可扩展性的限制。这些方法在6.6节，6.7节和6.8.3都有详细的讨论，然而这些方法非常适合用于类定义。下面几节讲述了如何使用 ECMAScript 5 的特性使类更加健壮。

### 9.8.1 让属性不可枚举

在9.6.1中Set类使用了一个小技巧，将对象存储为“集合成员”：它给添加至这个“集合”的任意对象定义了“对象id”属性.之后如果在for/in循环中对这个对象 做遍历，这个新添加的属性（对象id属性）也会遍历到。ECMScript5可以设置属性为“不可枚举”（nonenumerable）来让属性不会遍历到。下面的例子展示了如何通过`Object.defineProperty()`来做到这一点。同时也展示了如何定义一个getter函数以检测对象是否是可以扩展的（extensible）。

```js
/**
*定义不可枚举的属性
**/
//将代码包装至一个匿名函数中这样定义的变量就在这个函数作用域内
(function() {
//定义一个不可枚举的属性objectId,它可以被所有对象继承，当读取这个属性时，调用getter函数
//它没有定义setter，因此它是只读的，而且它是不可配置的，因此它是不能删除的
Object.defineProperty(Object.prototype, "objectId", {
  get: idGetter, //取值器
  enumerable: false, //不可枚举
  configurable: false //不可删除
});
//当读取objectId的时候直接调用getter函数
function idGetter() { //getter函数返回该id
  if (!(idprop in this)){ //如果这个对象中不存在id
      if (!Object.isExtensible(this)) //并且可以增加属性
        throw Error("can not define id for none extensible objects");
      Object.defineProperty(this, idprop, {
        value: nextid++, //给它一个值
        writable: false, //只读的
        enumerable: false, //不可枚举的
        configurable: false //不可删除的
      });
    }
    return this[idprop]; //返回已有活新的值
  };
  // idGetter()用到了这些变量，这些都属于私有变量
  var idprop = "|**objectId**|"; //假设这个属性没有用到
  var nextid = 1; //给它设定初始值
}()); //包装函数立即执行
```
### 9.8.2 定义不可变的类

除了可以设置属性为不可枚举的， ECMAScript 5 还可以设置属性为只读的，当我们希望类的实例都是不可变的，这个特性非常有帮助，下面的例子使用`Object.defineProperties()`和`Object.create()`定义不可变的Range类.它同样使用`Object.defineProperties()`来为类创建原型对象，并将原型对象的实例方法设置为不可枚举的，就想内置类的方法一样。不仅如此，它还将这些实例方法设置为“只读”和“不可删除”，这样就可以防止对类做任何修改（monkey-patching:是指修改现有对象的原型，在javascript中，修改对象的原型就相当于修改了实例化的类。）。

最后本例子展示了一个有趣的技巧，其中实现的构造函数也可用作工厂函数，这样不论调用函数之前是否带有new关键字，都可以正确的创建实例。

```js
/**
*创建一个不可变的类，它的属性和方法都是只读的
**/
//这个方法可以使用new调用，也可以省略new，它可以用作构造函数也可以用作工厂函数。
function Range2(from, to) {
    //这些都是对from和to只读属性的描述符
    var props = {
        from: {
            value: from,
            enumerable: true,
            writable: false,
            configurable: false
        },
        to: {
            value: to,
            enumerable: true,
            writable: false,
            configurable: false
        }
    };
    if (this instanceof Range2) //如果作为构造函数来调用
        Object.defineProperties(this, props); //定义属性
    else
        return Object.create(Range2.prototype, //创建并返回这个新Range2对象
            props); //属性由props指定
}
//如果用同样的方法给Range2.protptype对象添加属性，那么需要给这些属性设置他们的特性
//因为我们无法识别出他们的可枚举性，可写性和可配置性，这些属性的特征默认false

Object.defineProperties(Range2.prototype,{
    includes:{
        value:function(x){return this.from <= x && x <= this.to;}
    },
    foreach:{
        value:function(f){
            for(var x = Math.ceil(this.from); x <= this.to; x++)f(x);
        }
    },
    toString:{
        value:function(){return "(" + this.from + "..." + this.to + ")";}
    }
});

var c = Range2(100,22); //
console.log(c.toString()) //=> (100...22)
```

上面的例子用到了`Object.defineProperties()`和`Object.create()`定义不可变的和不可枚举的属性，这两个方法非常强大，但属性描述符对象让代码的可读性变得更差。另一种改进的做法是将修个这个已定义属性的特性操作定义为一个工具函数，下面的例子就展示了这样的练个工具函数：

```js
/**
  *属性描述符工具函数 
  **/
//将o的指定名字（或所有）的属性设置为不可写的和不可配置的
function freezeProps(o){
    var props = (arguments.length == 1) //如果只有一个参数
    ? Object.getOwnPropertyNames(o) //所有属性名称
    :Array.prototype.splice.call(arguments,1); //否则传入了指定的名字的属性
    props.forEach(function(n){//设置属性
        //忽略配置的属性
        if(!Object.getOwnPropertyDescriptor(o,n).configurable)return;
        Object.defineProperty(o,n,{writable:false,configurable:false});
    });
return o;//继承它
}
//将o的指定名字（或所有）的属性设置为不可枚举和可配置的
function hideProps(o){
    var props = (arguments.length == 1) //如果只有一个参数
    ?Object.getOwnPropertyNames(o) //使用所有的属性
    :Array.prototype.splice.call(arguments,1);//否则传入了指定名字的属性
props.forEach(function(n){//将它们设置为不可枚举的
    //忽略不可配置的属性
    if(!Object.getOwnPropertyDescriptor(o,n).configurable)return;
    Object.defineProperty(o,n,{enumerable:false});
});
return o;
}
```

`Object.defineProperty()`和`Object.defineProperties()`可以用来创建新属性，也可以修改已有的属性特征。当用它们用来创建新的属性时，默认的属性特性值都是false。但当它们修改意见存在的属性是，默认的值任然保持不不变。比如在上面修改枚举属性的`hideProps()`函数，只指定了 enumerable 特性，因为只想修改这个属性。

使用这些工具函数，就可以充分的利用ECMAScript5特性来实现一个不可变的类，而且不用动态的修改这个类，下面的例子中不可变的Rang3就用到了刚才定义的工具函数。

```js
/**
  *一个简单不可不变的类 
  **/
function Range3(from,to){//不可变的类Range3的构造函数
    this.from = from;
    this.to = to;
    freezeProps(this) //将属性设置为不可变的
}

Range3.prototype = hideProps({//使用不可枚举的属性来定义原型
    constructor:Range3,
    includes:function(x){return this.from <= x && x <= this.to;},
    foreach:function(f){for(var x = Math.ceil(this.from);x <= this.to; x++) f(x);},
    toString:function(){return "(" + this.from + "..." + this.to + ")";}
});
```

### 9.8.3 封装对象状态

如9.6.6所示构造函数中的变量和参数都可以用作它创建的对象的私有状态。该方法和在ECMAScript3中的一个缺点是，访问这些私有状态存取器方法是可以替换的。在ECMScript5中可以通过定义存取器属性getter和setter方法将状态变量更健壮的封装起来，这两个方法是无法删除的，如下:

```js
/**
  *封装对象状态
  **/
  //这个版本的Range类是可变的，但将端点变量进行了狂好的封装。但是端点大小顺序还是固定的：from <= to
function Range(from, to){
  //from大于to
if (from > to) throw new Error("from mustbe <= to");
//定义存取器方法以维持不变
function getFrom() {
  return from;
}

function getTo() {
  return to;
}

function setFrom(f){//设置from的值时，不允许from大于to
  if (f <= to) form = f;
  else throw new Error("from mustbe <= to");
}

function setTo(t){//设置to的值时，不允许to小于from
  if(t >= form) to = t;
  else throw new Error("to mustbe >= from");
}
//将使用取值器的属性设置为可枚举并且不可配置之的。
Object.defineProperties(this, {
  from: {
    get: getFrom,
    set: setFrom,
    enumerable: ture,
    configurable: false
  },
  to: {
    get: getTo,
    set: setTo,
    enumerable: ture,
    configurable: false
  }
});
}
//和前面的例子相比，原型对象没有做任何修改
//实例方法可以像读取普通的属性一样读取from和to
Range.prototype = hideProps({
  constructor:Range,
  includes:function(x){return this.from <= x && x <= this.to;},
  foreach:function(f){for(var x = Math.ceil(this.from);x <= this.to; x++) f(x);},
  toString:function(){return "(" + this.from + "..." + this.to + ")";}
});
```
### 9.8.4 防止类的扩展

通常认为，通过给原型对象添加方法可以动态地对类进行扩展，这是javascript本身的特性，在ECMAScript5中根据需要对此特性加以限制。`Object.preventExtensions()`可以将对象设置为不可扩展的（6.8.3节）也就是说不能给对象添加任何新属性。Object.seal()则更加强大，它除了能阻止用户给添加新属性，还能将当前已有的属性设置为不可配置的，这样就不能删除这些属性了（但不可配置的属性可以是可写的，也可以抓换为只读属性）。可以通过这样语句简单的代码来阻止对`Object.prototype`的扩展：

```js
Object.seal(Object.prototype)
```

javascript的另外一个动态特性是“对象的方法可以随时替换”（或称为“monkey-patch”）:

```js
var oiginal_sort_method = Array.prototype.sort;
Array.prototype.sort = function(){
  var start =new Date();
  oiginal_sort_method.apply(this,arguments);
  var end = new Date();
  console.log("Array sort took" + (end - start) + "milliseconds.");
};
```

可以通过将实例方法设置为只读来防止这类修改，一种方法就是使用上面代码所定义的`freezeProps()`,它的功能和`Object.seal()`完全一样，它同样会把所有属性都设置为只读和不可配置的。

理解类的只读属性的特性至观重要。如果对象o继承了只读属性p，那么给o.p的赋值操作将会失败，就不会给o创建新属性。如果你想重写一个继承来的只读属性，就必须使用`Object.defineProperty()`和`Object.defineProperties()`或`Object.create()`来创建这个新属性。也就是说，如果将类的实例方法设置为只读的，那么重写它的子类的这些方法的难度会更大。

这种锁定原型对象的做法往往没有必要，但的确有一些场景是需要阻止对象的扩展的。回想一下`enumeration()`，这是一个类工厂函数。这个函数将枚举和数组是表示枚举实例的正式实例列表，是可以执行“冻结”（freezing）操作的，这样就不能给他添加新的实例，已有的实例也无法删除或修改。可以给`enumeration()`函数添加几行简单的代码：

```js
Object.freeze(enumeration.values);
Object.freeze(enumeration);
```

需要注意的是，通过在枚举类型中调用`Object.freeze()`，在（9.8.1）中定义的objectId属性之后也无法使用了，这个问题的解决办法是，在枚举类型被“冻结”之前读取一次它的objectId属性（调用潜在的存取器方法并设置内部属性）。

### 9.8.5 子类和ECMAScript5

在下面的例子ECMAScript5特的特性实现子类。这里使用AbstractSet类中的AbstractWritableSet类做进一步说明，来定义这类类的子类StringSet。下面这个例子的最大的特点是使用`Object.create()`创建原型对象，这个原型对象继承自父类的原型，同时给新创建的对象定义属性。这种实现方法的困难之处在于，正如上文所提到的，它需要使用难看的属性描述符。

这个例子中另外一个有趣之处在于，使用`Object.create()`创建对象时传入了参数null,这个创建的对象没有任何继承任何成员，这个对象用来存储集合的成员，同时，这个对象没有原型，这样我们就能对它直接使用in运算符（使用in运算符可以对对象成员进行遍历，包括对原型对象中的非内置成员进行遍历。）而不使用`hasOwnProperty()`方法。

```js
/**
  * StringSet:利用ECMAScript5的特性定义子类
  **/
function StringSet(){
    this.set = Object.create(null); //创建一个不可包含原型的对象
    this.n = 0;
    this.add.apply(this,arguments);
}
//注意，使用Object.create()可以继承父类的原型
//而且可以定义单独调用的方法，因为我们我们制定属性的可写性、可枚举性和可配置性。
//因此这些属性特性的默认值都是false ， 只读方法让这个类难于子类化(被继承)
StringSet.prototype = Object.create(AbstractEnumerableSet.prototype,{
    constructor:{value:StringSet},
    contains:{value:function(x){return x in this.set;}},
    size:{value:function(x){return this.n;}},
    foreach:{value:function(f,c){Object.keys(this.set).forEach(f,c);}},
    add:{
        value:function(){
            for(var i = 0; i< arguments.length; i++){
                if(!(arguments<[i] in this.set)){
                    this.set[arguments[i]] = true;
                    this.n++;
                }
            }
            return this;
        }
    },
    remove:{
        value:function(){
            for(var i = 0; i < arguments.length; i++){
                if (arguments[i] in this.set){
                    delete this.set[arguments[i]];
                    this.n--;
                }
            }
            return this;
        }
    }
});
```
### 9.8.6 属性描述符

6.7节讨论了ECMAScript5中的属性描述符，但没有给出他们的示例代码，本节给出一个例子，来讲述基于ECMAscript5如何对属性进行各种操作。下面的例子中给Object.prototype添加了`properties()`方法（这个方法是不可枚举的）。这个方法的返回值是一个对象，用于表示属性的列表，并定义了有用的方法用来输出属性和属性特征（对于调试非常有用），用来获得属性描述符（当复制属性时同时复制属性特性时非常有用）以及用来设置属性的特征（是上文定义的`hideProps()`和`freezeProps()`函数不错的替代方案）。这个例子展示了ECMAScript5的大多数属性相关的特性。同时使用了一种模块编程技术，这将在下一节讨论。

```js
/**
  * ECMAScript5属性操作
  * 给Object.prototype定义properties()方法，这个方法返回一个表示调用它的对象上的属性名列表的对象
  * （如果不带参数调用它，就表示该对象的所有属性）
  * 返回的对象定义了4个有用的方法：toString()、descriptors()、hide()和show()
  **/
(function namespace() { //将所有逻辑闭包在一个私有函数作用域中
    //这个函数成为所有对象的方法
    function properties() {
            var names; //属性名组成的数组
            if (arguments.length == 0) //所有的自由属性
                names = Object.getOwnPropertyNames(this);
            else if (arguments.length == 1 && Array.isArray(arguments[0]))
                names = Array.prototype.splice.call(arguments, 0);
            //返回一个新的properties对象，用以表示属性名字
            return new properties(this, names);
        }
        //将它设置为Object.prototype的新的不可枚举的属性
        //这是从私有函数作用域导出的唯一一个值
    Object.defineProperty(Object.prototype, "properties", {
        value: properties,
        enumerable: false,
        writable: true,
        configurable: true
    });
    //这个构造函数是由上面的properties()函数所调用的
    //properties类表示一个对象的属性集合
    function Properties(o, names) {
            this.o = o; //属性所属的对象
            this.names = names; //属性的名字
        }
        //将代表这些属性的对象设置为不可枚举的
    Properties.prototype.hide = function() {
        var o = this.o,
            hidden = {
                enumerable: false
            };
        this.names.forEach(function(n) {
            if (o.hasOwnProperty(n))
                Object.defineProperty(o, n, hidden);
        });
        return this;
    };
    //将这些属性设置为只读的和不可配置的
    Properties.prototype.freeze = function() {
        var o = this.o,
            frozen = {
                writable: false,
                configurable: false
            };
        this.names.forEach(function(n) {
            if (o.hasOwnProperty(n))
                Object.defineProperty(o, n, frozen);
        });
        return this;
    };
    
    //返回一个对象，这个对象是名字到属性描述符的映射表，用它来复制属性，联通属性特征一起赋值
    //Object.defineProperties(dest,src.properties().descriptors());
    Properties.prototype.descriptors = function(){
        var o = this.o,desc ={};
        this.names.forEach(function(n){
            if(!o.hasOwnProperty(n)) return;
            desc[n] = Object.getOwnPropertyDescriptor(o,n);
        });
        return desc;
    };
    
    //返回一个格式化良好的属性列表
    //列表中包含名字、值和属性特性，使用"permanent"表示不可配置，使用"readonly"表示不可写，使用"hidden"表示不可枚举
    //普通的可枚举，可写和可配置属性不包含特性列表
    Properties.prototype.toString = function(){
        var o = this.o; //在下面嵌套的函数中使用
        var lines = this.names.map(nameToString);
        return "{\n" + lines.join(",\n") + "\n";
        function nameToString(n){
            var s = "",desc = Object.getOwnPropertyDescriptor(o,n);
            if(!desc) return "nonexistent" + n + ":undefined";
            if (!desc.configurable) s += "permanent";
            if((desc.get && !desc.set) || !desc.writable) s += "redyonly";
            if(!desc.enumerable) s += "hidden";
            if(desc.get ||desc.set) s += "accessor" + n
            else s += n + ":" +((typeof desc.value ==="function")?"function":desc.value);
            return s;
        }
    };
    //最后，将原型对象中的实例方法设置为不可枚举的
    //这里用到了刚定义的方法
    Properties.prototype.properties().hide();
}());//执行匿名函数
```

## 9.9 模块

将代码组织到类中的一个重要原因是，让代码更加“模块化”，可以在很多不同场景中实现代码的重用。但类不是唯一的模块化代码方式。一般来讲，模块是一个独立的javascript文件。模块文件可以包含一个类定义、一组相关的类、一个使用函数库或者是一些待执行的代码。只要以模块的形式编写代码。任何javascript代码段就可以当做一个模块（作者这里的表述是围绕“模块是一个可重用的代码段”这一观念，不论是代码法结构上解藕，还是将代码拆分至不同的文件中，只要用某种方式将代码“分离”，就认为是一个模块，因此作者可以说任何代码都可以处理为一个模块）。javascript中并没有定义用于支持模块的语言结构（但imports和exports的确是javascript保留的关键字，因此javascript的未来版本可能会支持），这也意味着在javascript中编写模块化的代码更多是遵循某一种代码约定。

很多javascript库和客户端编程框架都包含一些模块系统。比如Dojo工具包和google的Closure库定义了`provide()`和`require()`函数，用以声明和加载模块。并且，commonJS服务器端javascript标准规范（参照commonjs.org）创建一个模块规范，后者同样使用`require()`函数。这种模块系统通常用来处理模块加载和依赖性管理。如果使用这些框架，则必须按照框架提供的模块编写约定来定义模块。本节仅对模块约定做一些简单的讨论。

模块化的目标是支持大规模程序的开发，处理分散源中代码的组装，并且能让代码正确的运行，哪怕包含了作者所部期望出现的模块代码，也可以正确执行代码。为了做到这一点，不同的模块必须避免修改全局执行执行上下文，因此后续模块应当在它们所期望的运行元素（或接近原始）上下文中执行（这里的“原始上下文”是指调用模块时所在的上下文，可能处在一个很深的闭包中，但这个模块的逻辑不应该影响到其他上下文特别是全局上下文。）。这实际上意味着模块应当尽可能少地定义全局标识。理想状况是，所有模块都不应当定义超过一个（全局标识）。

接下来我们给出的一种简单的方法可以做到这一点。你会发现在javascript中实现一个模块代码并不困难：在本书中很多实力代码都用到了这种技术。

### 9.9.1 用作命名空间的对象

在模块创建过程中避免污染全局变量的一种方法是只有一个对象作为命名空间。它将函数和值作为命名空间对象属性存储起来（可以通过全局变量引用），而不是定义全局函数和变量。拿例子Set类说，它定义了一个全局构造函数`Set()`。然后给这个类定义了很多实例方法，但将这些实例方法存储为Set.prototype的属性，因此这些方法不是全局的。实例代码也包含一个`_v2s()`工具函数，但也没有定义它为全局函数，而是把它存储为Set的属性。

接下来看一下原来的AbstractSet类的例子，这个例子定义了很多抽象类和非抽象类。每个类都只包含一个全局标识，但这个模块（这个javascript文件）定义了很少的全局变量。基于这种“保持干净的全局命名空间”的观点，一种好的做法是将“集合”类定义为一个单独的全局对象：

```js
var sets = {};
```

这个sets对象是模块的命名空间，并将每个“集合”类都定义为这个对象的属性：

```js
set.SingletonSet = sets.AbstractEnumerableSet.extend(...);
```

如果想使用这样定义的类，需要通过命名空间来调用所需的构造函数：

```js
var s = new sets.SingletonSet(1);
```

模块的作者并不知道它的模块会和那些其他的模块一起构造，因此尤为注意这些命名空间的用法带来的命名冲突。然而，使用这个模块的开发者是知道它用了那些模块。用到了那些名字的。程序员并不一定要严格遵循命名空间的写法，只须将常用的值“导入”到全局命名空间中。程序员如果要检测使用set命名空中的set类，可以这样将它导入：

```js
var Set = sets.Set; //将Set导入到全局命名空间中
var s = new Set(1,2,4); //这样每次使用它就不必添加set前缀了
```

有时模块作者会使用更深层次嵌套的命名空间。如果sets模块是另外一组更强大的模块集合的话，它的命名空间可能是collections.sets,模块的代码开始这样写：

```js
var collections; //声明(或者重新声明)这个全局变量
if (!collections) //如果它原本不存在
    collections = {}; //创建一个顶层的命名空间对象
collections.sets = {} //将set命名空间创建在它的内部
    //在collections.sets内定义set类
collections.sets.AbstractSet = function() {...}
```

最顶层的命名空间往往采用表示创建模块的作者或组织，并避免命名空间的命名冲突。比如google的Clossure库在它的命名空间goog.structs中定义了Set类。每个开发者都反转互联网域名的组成部分，这样创建的命名空间是全局伟业的。一般不会其他模块者采用，比如我的网站是ahthw.com，我们可以通过命名空间来发布我的sets模块`com.ahthw.collections.sets`。

使用很长的命名空间来导入模块的方式非常重要，然而程序员往往将整个模块导入全局命名空间，而不是导入(命名空间的某个)单独的类。

```js
var sets = com.ahthw.collections.sets
```

按照约定，模块的文件名应当和命名空间匹配。sets模块应当保存在sets.js中。如果这个模块使用命名空间collections.sets，那么这个文件应当保存在目录collections/下（这个目录应该还有另外一个文件maps.js）。并且使用命名空间com.ahthw.collections.sets模块应该在文件com/ahthw/collections/sets.js中。

### 9.9.2 作为私有命名空间的函数

模块对外导出一些公用的API,这些API是给其它程序员使用的。它包括函数、类、属性和方法。但模块的实现往往需要一些额外的辅助函数和方法，这些函数和方法并不需要在模块外部可见。比如`Set._v2s()`函数，模块的作者不希望Set类的用户在某时候调用这个函数，因此这个方法最好在类的外部是不可访问的。

可以通过将模块(本例中的Set类)定义在某个函数的内部来实现，正如8.5节描述的一样，在一个函数中定义的变量和函数都属于函数的局部成员，在函数的外部是不可见的。实际上，可以将这个函数作用域用作模块的私有命名空间。(有时候称为“模块函数”)，下面的例子展示了如何使用“模块函数”来实现Set类：

```js
/**
  * 模块函数中的Set类
  **/
//声明全局变量Set,使用一个函数的返回值给它赋值
//函数结束时紧跟的一堆圆括号说明这个函数定义后立即执行
//它的返回值将赋值给Set,而不是将这个函数赋值给Set
//注意它是一个函数表达式，不是一条语句，因此函数"invocation"并没有创建全局变量
var Set = (function invocation(){
    function Set(){//这个构造函数是局部变量
        this.values = {};//这个对象的属性用来保存这个集合
        this.n = 0; //集合中值的个数
        this.add.apply(this,arguments);//将所有的参数都添加至集合中
    }
    //给Set.prorotype定义实例方法
    //这里省略了详细代码
    Set.prototype.contains = function(value){
        //注意我们调用了v2s()而不是调用带有笨重前缀的set._v2s()
        return this.values.hasOwnProperty(v2s(value));
    };
    Set.prototype.size = function(){return this.n};
    Set.prototype.add =function(){/*...*/};
    Set.prototype.remove =function(){/*...*/};
    Set.prototype.foreach =function(f,context){/*...*/};
    
    //这里是上面方法调用到的一些辅助的函数和变量
    //它们不属于模块的共有API,但它们都隐藏在函数的作用域内
    //因此我们不必将它们定义为Set的属性或使用下划线做其前缀
    
    function v2s(val){/*...*/}
    function objectId(o){/*...*/}
    var nextId = 1;
    //这个模块的共有API是Set()构造函数
    //我们需要把这个函数从私有命名空间中导出来
    //以便在外部可以使用它，在这种全局下，我们通过返回这个构造函数来导出它
    //它变成第一行代码所芝的表达式的值
    return Set;
}());
```

注意，这里我们使用了立即执行的匿名函数，这在javascript中是一种惯用法。如果想让代码在一个私有命名空间中运行，只须给这段代码加上前缀“(function(){"和后缀"}())”开始的左园括号确保这是一个函数表达式，而不是函数定义语句，因此可以给该前缀加上一个函数名来让代码变得更加清晰。在上面的例子中，使用了名字“invocation”用来强调这个函数应当在定义之后立即执行。名字“namespace”也可以用来强调这个函数被用作命名空间。

一旦将模块代码封装进一个函数，就需要一些方法导出公用API，以便在模块函数的外部调用它们。在上面的例子中，模块函数返回构造函数，这个构造函数随后赋值给一个全局变量。将值返回已经清楚的表明API已经导出早函数作用域之外。如果模块API包含多个单元，则它库返回命名空间对象。对于sets模块历来是，可以将代码写成这样：

```js
//创建一个全局变量来存放集合相关的模块
var collections;
if(!collections) collections = {};
//定义sets模块
collections.sets = (function namespace(){
    //在这里定义多种“集合”类，使用局部变量和函数
    //..代码
    
    //通过返回命名空间对象将API导出
    return{
        //导出的属性名；局部比安了名字
        AbstracSet:AbstractSet,
        NoSet:NoSet,
        AbstractEnumerableSet:AbstractEnumerableSet,
        SingletonSet:SingletonSet,
        AbstractWritableSet:AbstractWritableSet,
        ArraySet:ArraySet
    };
}());
```

令一种类似技术是将模块函数当做构造函数，通过new来调用，通过将它们（构造函数创建的新实例）赋值给this来将其导出（使用构造函数和模块函数来实现私有成员的原理是一模一样的，只是调用的方式不一样）：

```js
var collections;
if(!collections) collections = {};
collections.sets = (new Function namespace(){
    //..省略很多代码。。
    
    //将API导出至this对象
    this.AbstracSet = AbstractSet;
    this.NotSet = NotSet;//...
    //注意，这里没有返回值
}())
```

作为替代方案，如果已经定义了全局命名对象，这个模块函数可以直接设置那个对象的属性，不返回任何内容。

```js
var collections;
if(!collections) collections = {};
collections.sets = {};
(function namespace(){
    //..省略代码
    
    //将共用的API导出到上面创建的命名空间对象上
    collections.sets.AbstractSet = AbstractSet;
    collections.sets.NotSet = NotSet; //....
    
    //导出的操作已经执行了，这里就不需要在写return语句了
}());
```

有些框架已经实现了模块加载的功能，其中包括其他一些导出模块API的方法。比如：使用`provides()`函数来注册其API,提供exports对象用以存储模块API.由于javascript目前还不具备模块管理的能力。因此应当根据使用的框架和工具包来选择合适的模块创建和导出API方式。

# 第10章 正则表达式的模式匹配
# 第11章 JavaScript的子集和扩展
# 第12章 服务端JavaScript
# 第二部分 客户端JavaScript
# 第13章 Web浏览器中的JavaScript
# 第14章 Window对象

# 第15章 脚本化文档

客户端 JavaScript 的存在使得静态的HTML文档变成了交互式的 Web 应用。脚本化 Web 页面内容是 JavaScript 的核心目标。

第13章和第14章解释了每一个 Web 浏览器窗口、标签页和框架由一个 Window 对象所表示。每个 Window 对象有一个 document 属性引用了 Document 对象。 Document 对象表示窗口的内容，它就是本章的主题。尽管如此，Document对象并非独立的，它是一个巨大的API中的核心对象，叫做文档对象模型（Document Object Model，DOM），它代表和操作文档的内容。

本章开始部分解释DOM的基本架构，然后进一步解释以下内容：
- 如何在文档中查询或选取单独的元素。
- 如何将文档作为节点树来遍历，如何找到任何文档元素的祖先、兄弟和后代元素。
- 如何查询和设置文档元素的属性。
- 如何查询、设置和修改文档内容。
- 如何通过创建、插入和删除节点来修改文档结构。
- 如何与 HTML 表单一起工作。

本章最后一节涵盖其他各种文档特性，包含 referrer 属性、`write()`方法和查询当前文档中选取的文档文本的技术等。

## 15.1 DOM概览

文档对象模型（DOM）是表示和操作 HTML 和 XML 文档内容的基础API。API不是特别复杂，但是需要理解大量的架构细节。首先，应该理解 HTML 或 XML 文档的嵌套元素在DOM树对象中的表示。 HTML 文档的树状结构包含表示 HTML 标签或元素（如`<body>``、<p>`）和表示文本字符串的节点，它也可能包含表示 HTML 注释的节点。考虑以下简单的 HTML 文档：

```html
<html>
  <head>
    <title>title name</title>
  </head>
  <body>
    <h1>an html Document</h1>
    <p>this is a <i>simple</i>docuent</p>
  </body>
</html>    
```

如果还未熟悉计算机编程中的树状结构，借用家谱图来形容是比较有用的方法。在一个节点之上的直接节点是其父节点，在其下一层的直接节点是其子节点。在同一层上具有相同父节点的节点是兄弟节点。在一个节点之下的所有层级的一组节点是其后代节点。一个节点的任何父节点、祖父节点和其上层的所有节点是祖先节点。

图15-1中的每个方框是文档的一个节点，它表示一个 Node 对象。我们将在后续几节中讨论 Node 的属性和方法，并且可以在第四部分查找这些属性和方法。注意，图15-1包含3种不同类型的节点。树形的根部是 Document 节点，它代表整个文档。代表 HTML 元素的节点是 Element 节点，代表文本的节点是 Text 节点。 Document 、 Element 和 Text 是 Node 的子类，在第四部分中它们有自己的条目。 Document 和 Element 是两个重要的 DOM 类，本章大部分内容将阐述它们的属性和方法。

图15-2展示了 Node 及其在类型层次结构中的子类型。注意，通用的 Document 和 Element 类型与 HTMLDocument 和 HTMLElement 类型之间是有严格的区别的。 Document 类型代表一个 HTML 或 XML 文档， Element 类型代表该文档中的一个元素。 HTMLDocument 和 HTMLElement 子类只是针对于 HTML 文档和元素。此书中，我们经常使用通用类名 Document 和 Element ，甚至在指代 HTML 文档时也不例外。在第四部分中也是如此： HTMLDocument 和 HTMLElement 类型的属性和方法记录于 Document 和 Element 参考页中。

值得注意的是，在图15-2中有 HTMLElement 的很多子类型代表 HTML 元素的具体类型。每个类型定义多个 JavaScript 属性，它们对应具体的元素或元素组（参照15.4.1节）的HTML属性。有些具体元素类也定义额外的属性和方法，它们并不是简单地映射 HTML 语法。第四部分涵盖这些类型及其额外的特性。

最后，请注意图15-2也展示了到目前为止还未提及的一些节点类型。 Comment 节点代表 HTML 或 XML 的注释。由于注释基本上是文本字符串，因此它们很像表示文档中显示文本的 Text 节点。 CharacterData 通常是 Text 和 Comment 的祖先，它定义这两种节点所共享的方法。 Attr 节点类型代表 XML 或 HTML 属性，但它几乎从不使用，因为和文档节点不同， Element 类型定义了将属性当做“名/值”对使用的方法。 DocumentFragment 类（未在图15-2上显示）在实际文档中并不存在的一种节点：它代表一系列没有常规父节点的节点。对一些文档操作来说 DocumentFragment 非常有用，15.6.4节涵盖这部分内容。 DOM 也定义了一些不经常使用的类型，如像代表 doctype 声明和XML处理指令等类型。

## 15.2 选取文档元素

大多数客户端 JavaScript 程序运行时总是在操作一个或多个文档元素。当这些程序启动时，可以使用全局变量 document 来引用 Document 对象。但是，为了操作文档中的元素，必须通过某种方式获得或选取这些引用文档元素的 Element 对象。 DOM 定义许多方式来选取元素，查询文档的一个或多个元素有如下方法：

- 用指定的 id 属性；
- 用指定的 name 属性；
- 用指定的标签名字；
- 用指定的 CSS 类；
- 匹配指定的 CSS 选择器。

### 15.2.1 通过ID选取元素

任何 HTML 元素可以有一个 id 属性，在文档中该值必须唯一，即同一个文档中的两个元素不能有相同的 ID 。可以用 Document 对象的`getElementById()`方法选取一个基于唯一 ID 的元素。此方法我们在第13章和第14章都已经使用过了：

```js
var section1 = document.getElementById("section1")
```

这是最简单和常用的选取元素的方法。如果想要操作某一组指定的文档元素，提供这些元素的 id 属性值，并使用 ID 查找这些Element对象。如果需要通过 ID 查找多个元素，会发现例15-1中的`getElements()`函数非常有用：

```js
/**
  * 函数接受任意多的字符串参数
  * 每个参数将当做元素的id传给document.getElementById()
  * 返回一个对象，它把这些id映射到对应的Element对象
  * 如任何一个id对应的元素未定义，则抛出一个Error对象
  **/
function getElements( /*ID(s)*/ ) {
  var elements = {}; //开始是一个map映射对象
  for (var i = 0; arguments.length; i++) { //循环每个参数
    var id = arguments[i]; //参数是元素的id
    var elt = document.getElementById(id); //查找元素
    if (elt == null)
        throw new Error("No element with id: " + id); //抛出异常
    elements[id] = elt; //id和元素之间的映射
  }
  return elements; //对于元素映射返回id
}
```

在低于IE 8版本的浏览器中，`getElementById()`对匹配元素的 ID 不区分大小写，而且也返回匹配 name 属性的元素。

### 15.2.2 通过名字选取元素

HTML 的 name 属性最初打算为表单元素分配名字，在表单数据提交到服务器时使用该属性的值。类似 id 属性， name 是给元素分配名字，但是区别于 id ， name 属性的值不是必须唯一：多个元素可能有同样的名字，在表单中，单选和复选按钮通常是这种情况。而且，和 id 不一样的是 name 属性只在少数 HTML 元素中有效，包括表单、表单元素、`<iframe>`和`<img>`元素。

基于 name 属性的值选取 HTML 元素，可以使用 Document 对象的`getElementsByName()`方法。

```js
var radiobuttons = document.getElementsByName("favorite_color");
```

`getElementsByName()`定义在 HTMLDocument 类中，而不在 Document 类中，所以它只针对 HTML 文档可用，在 XML 文档中不可用。它返回一个 NodeList 对象，后者的行为类似一个包含若干 Element 对象的只读数组。在 IE 中，`getElementsByName()`也返回 id 属性匹配指定值的元素。为了兼容，应该小心谨慎，不要将同样的字符串同时用做名字和 ID 。

在14.7节中我们看到，为某些 HTML 元素设置 name 属性值将自动为 Window 对象中创建对应的属性，对 Document 对象也类似。为`<form>`、`<img>`、`<iframe>`、`<applet>`、`<embed>`或`<object>`元素（其中只有`<object>`元素没有后备对象）设置 name 属性值，即在 Document 对象中创建以此 name 属性值为名字的属性（当然，假设此文档还没有该名字的属性）。

如果给定的名字只有一个元素，自动创建的文档属性对应的该值是元素本身。如果有多个元素，该文档属性的值是一个 NodeList 对象，它表现为一个包含这些元素的数组。如14.7节所示，为若干命名`<iframe>`元素所创建的文档属性比较特殊：它们指代这些框架的 Window 对象而不是 Element 对象。

这就意味着有些元素可以作为 Document 属性仅通过名字来选取：

```js
//征对<form name="shipping">元素，得到Element对象
var form = document.shipping;
```

在14.7节介绍了为什么不要用为窗口对象自动创建的属性，这同样适用于为文档对象自动创建的属性。如果需要查找命名的元素，最好显式地调用`getElementsByName()`来查找它们。

### 15.2.3 通过标签名选取元素

Document 对象的`getElementsByTagName()`方法可用来选取指定类型（标签名）的所有 HTML 或 XML 元素。例如，如下代码，在文档中获得包含所有`<span>`元素的只读的类数组对象：

```js
var spans = document.getElementsByTagName("span");
```

类似于`getElementsByName()`，`getElementsByTagName()`返回一个 NodeList 对象（关于 NodeList 类，见本节的补充信息）。在 NodeList 中返回的元素按照在文档中的顺序排序的，所以可用如下代码选取文档中的第一个`<p>`元素：

```js
var firstspan = document.getElementsByTagName("span")[0];
```

HTML 标签是不区分大小写的，当在 HTML 文档中使用`getElementsByTagName()`时，它进行不区分大小写的标签名比较。例如，上述的变量 span 将包含所有写成`<SPAN>`的 span 标签。

给`getElementsByTagName()`传递通配符参数`*`将获得一个代表文档中所有元素的 NodeList 对象。

Element 类也定义`getElementsByTagName()`方法，其原理和 Document 版本的一样，但是它只选取调用该方法的元素的后代元素。因此，要查找文档中第一个`<p>`元素里面的所有`<span>`元素，代码如下：

```js
var firstpara = document.getElementsByTagName("p")[0];
var firstParaSpan = firstpara.getElementsByTagName("span");
```

由于历史的原因， HTMLDocument 类定义一些快捷属性来访问各种各样的节点。例如，images、forms和links等属性指向行为类似只读数组的`<img>`、`<form>`和`<a>`（但只包含那些有href属性的`<a>`标签）元素集合。这些属性指代 HTMLCollection 对象，它们很像 NodeList 对象，但是除此之外它们可以用元素的 ID 或名字来索引。早些时候，我们已经看到用如下的表达式来引用一个命名的`<form>`元素：

```js
document.shiping;
```

用 document.forms 属性也可以更具体地引用命名（或有ID的）表单，如下：

```js
document.forms.shipping
```

HTMLDocument 也定义 embeds 和 plugins 属性，它们是同义词，都是 HTMLCollection 类型的`<embed>`元素的集合。anchors 是非标准属性，它指代有一个 name 属性的`<a>`元素而并不是一个 href 属性。 scripts 在 HTML5 中是标准属性，它是 HTMLCollection 类型的`<script>`元素的集合，但是在写本书的时候，它还未普遍实现。

HTMLDocument 对象还定义两个属性，它们指代特殊的单个元素而不是元素的集合。`document.body`是一个HTML文档的`<body>`元素，`document.head`是`<head>`元素。这些属性总是会定义：如果文档源代码未显式地包含`<head>`和`<body>`元素，浏览器将隐式地创建它们。 Document 类的 documentElement 属性指代文档的根元素。在 HTML 文档中，它总是指代`<html>`元素。

> 节点列表和HTML集合
> `getElementsByName()`和`getElementsByTagName()`都返回 NodeList 对象，而类似`document.images`和`document.forms`的属性为 HTMLCollection 对象。这些对象都是只读的类数组对象（见7.11节）。它们有length属性，也可以像真正的数组一样索引（只是读而不是写）。可以对一个 NodeList 或 HTMLCollection 的内容用如下标准的循环进行迭代：
> 不能直接在 NodeList 和HTML集合上调用Array的方法，但可以间接地使用：
>  HTMLCollection 对象也有额外的命名属性，也可以通过数字和字符串来索引。
> 由于历史的原因， NodeList 和 HTMLCollection 对象也都能当做函数：以数字或字符串为参数调用它就如同使用数字或字符串索引它们一般。不鼓励使用这种怪异的方式。 
> NodeList 和 HTMLCollection 接口都不是为像JavaScript这样的动态语言设计的。它们都定义了item()方法，期望输入一个整数，并返回此索引处的元素。在JavaScript中根本没有必要调用此方法，因为简单地使用数组索引就能替代。类似地， HTMLCollection 定义了namedItem()方法，它返回指定属性名的值，但在JavaScript程序中可以用数组索引或常规属性来访问。
>  NodeList 和 HTMLCollection 对象不是历史文档状态的一个静态快照，而通常是实时的，并且当文档变化时它们所包含的元素列表能随之改变，这是其中一个最重要和令人惊讶的特性。假设在一个没有`<div>`元素的文档中调用`getElementsByTagName('div')`，此时返回值是一个length为0的 NodeList 对象。如果再在文档中插入一个新的`<div>`元素，此元素将自动成为 NodeList 的一个成员，并且它的length属性变成1。
> 通常， NodeList 和 HTMLCollection 的实时性非常有用。但是，如果要在迭代一个 NodeList 对象时在文档中添加或删除的元素，首先会需要对 NodeList 对象生成一个静态的副本：

### 15.2.4 通过CSS类选取元素

HTML 元素的 class 属性值是一个以空格隔开的列表，可以为空或包含多个标识符。它描述一种方法来定义多组相关的文档元素：在它们的 class 属性中有相同标识符的任何元素属于该组的一部分。在 JavaScript 中 class 是保留字，所以客户端 JavaScript 使用 className 属性来保存 HTML 的 class 属性值。 class 属性通常与 CSS 样式表一起使用，对某组内的所有元素应用相同的样式，在第16章中将再次看到它。尽管如此， HTML 定义了`getElementsByClassName()`方法，它基于其 class 属性值中的标识符来选取成组的文档元素。

类似`getElementsByTagName()`，在 HTML 文档和 HTML 元素上都可以调用`getElementsByClassName()`，它的返回值是一个实时的 NodeList 对象，包含文档或元素所有匹配的后代节点。`getElementsByClassName()`只需要一个字符串参数，但是该字符串可以由多个空格隔开的标识符组成。只有当元素的class属性值包含所有指定的标识符时才匹配，但是标识符的顺序是无关紧要的。注意，class属性和`getElementsByClassName()`方法的类标识符之间都是用空格隔开的，而不是逗号。如下是使用`getElementsByClassName()`的一些例子：

```js
// 找到所有class属性值为"warning"的元素
var warnings = document.getElementsByClassName("warning");

// 查找以log命名且包含有"error"和"fatal"类的元素的所有后代
var log = document.getElementById("log");
var total = log.getElementsByClassName("error fatal");
```

如今的Web浏览器依赖于文档开头处对`<!DOCTYPE>`声明的严格程度来选择“怪异模式”或“标准模式”方式显示HTML文档。怪异模式是为了向后兼容性而存在的，其中一个怪异行为就是在class属性中和CSS样式表中的类标识符不区分大小写。`getElementsByClassName()`方法使用样式表的匹配算法。如果文档以怪异模式渲染，该方法将执行不区分大小写的字符串比较；否则，该比较区分大小写。

在写本书这段时间内，除了IE 8及其较低的版本，`getElementsByClassName()`在所有当前的浏览器中都实现了。IE 8确实支持`querySelectorAll()`方法，下一节会介绍它，而`getElementsByClassName()`方法是可以在其之上实现的。

### 15.2.5 通过CSS选择器选取元素

CSS样式表有一种非常强大的语法，那就是选择器，它用来描述文档中的若干或多组元素。CSS选择器语法的全部细节介绍超出了本书的范围，但是这里有一些例子来说明基本的语法。元素可以用ID、标签名或类来描述：

```js
#nav //id="nav"的元素
div //所有的<div>元素
.warning //所有早class属性值包含了“waring”的元素
```

更一般地，元素可以基于属性值来选取：

```js
p[lang = "fr"] //所有使用语法段落，如：<p lang="fr">
* [name = "x"] //所有包含name = "x"属性的元素
```

这些基本的选择器可以组合使用：

```js
span.fatal.error //其class中 包含"fatal"和"error"的所有<span>元素
span[lang = "fr"].warning //所有使用语法且class中包含"warning"的<span>元素
```

选择器可以指定文档结构：

```js
#log span //id="log"元素中所有的<span>元素
#log>span //id="log"元素的子元素中的所有<span>元素
body>h1:first-child //<body>的子元素中的第一个<h1>元素
```

选择器可以组合起来选取多个或多组元素：

```js
div, #log //所有的元素，以及id="log"的元素
```

如你所见， CSS 选择器可以使用上述所有方法选取元素：通过ID、名字、标签名和类名。与 CSS3 选择器的标准化一起的另一个称做“选择器API”的W3C标准定义了获取匹配一个给定选择器的元素的 JavaScript 方法。该 API 的关键是 Document 方法`querySelectorAll()`。它接受包含一个 CSS 选择器的字符串参数，返回一个表示文档中匹配选择器的所有元素的 NodeList 对象。与前面描述的选取元素的方法不同，`querySelectorAll()`返回的 NodeList 对象并不是实时的：它包含在调用时刻选择器所匹配的元素，但它并不更新后续文档的变化。如果没有匹配的元素，`querySelectorAll()`将返回一个空的 NodeList 对象。如果选择器字符串非法，`querySelectorAll()`将抛出一个异常。

除了`querySelectorAll()`，文档对象还定义了`querySelector()`方法。与`querySelectorAll()`的工作原理类似，但它只是返回第一个匹配的元素（以文档顺序）或者如果没有匹配的元素就返回null。

这两个方法在 Element 节点中也有定义（并且也在DocumentFragment节点中，见15.6.4节）。在元素上调用时，指定的选择器仍然在整个文档中进行匹配，然后过滤出结果集以便它只包含指定元素的后代元素。这看起来是违反常规的，因为它意味着选择器字符串能包含元素的祖先而不仅仅是上述所匹配的元素。

注意，CSS定义了“:first-line”和“:first-letter”等伪元素。在CSS中，它们匹配文本节点的一部分而不是实际元素。如果和`querySelectorAll()`或`querySelector()`一起使用它们是不匹配的。而且，很多浏览器会拒绝返回“:link”和“:visited”等伪类的匹配结果，因为这会泄露用户的浏览历史记录。

所有当前的浏览器都支持`querySelector()`和`querySelectorAll()`方法。但是注意，这些方法的规范并不要求支持 CSS3 选择器：鼓励浏览器支持和在样式表中一样的选择器集合。当前的浏览器除了IE都支持 CSS3 选择器。IE 7和8支持 CSS2 选择器。（期望IE 9能支持 CSS3 选择器。）

`querySelectorAll()`是终极的选取元素的方法：它是一种非常强大的技术，通过它客户端 JavaScript 程序能够选择它们想要操作的元素。幸运的是，甚至在没有`querySelectorAll()`的原生支持的浏览器中也可以使用 CSS 选择器。jQuery库（见第19章）使用这种基于 CSS 选择器的查询作为它的核心编程范式。基于jQuery的Web应用程序使用一个轻便的、跨浏览器的、和`querySelectorAll()`等效的方法，命名为`$()`。

jQuery的 CSS 选择器匹配代码已经作为一个独立的标准库提出来并发布了，命名为Sizzle。它已经被Dojo和其他一些客户端库所采纳。使用一个类似Sizzle的库（或一个包含Sizzle的库）的好处就是在老式浏览器中选取元素也能正常工作，并保证一个基准的选择器集合在所有的浏览器中都能运行。

### 15.2.6 document.all[]

在DOM标准化之前，IE 4引入了`document.all[]`集合来表示所有文档中的元素（除了Text节点）。`document.all[]`已经被标准的方法（如`getElementById()`和`getElementsByTagName()`）等所取代，现在已经废弃不应该再使用了。但是，在引入之时它是革命性的，它在以各种方式使用的已有代码中仍然可以看到：

```js
document.all[0] //文档中的第一个元素
document.all["nav"] //id或name为"nav"的元素(或多个元素)
document.all.nav //同上
document.all.tags("div") //文档中的所有div元素
document.all.tags("p")[0] //文档中的第一个<p>元素
```

## 15.3 文档结构和遍历

一旦从文档中选取了一个元素，有时需要查找文档中与之在结构上相关的部分（父亲、兄弟和子女）。文档从概念上可以看做是一棵节点对象树，如图15-1所示。节点类型定义了遍历该树所需的属性，我们将在节15.3.1中介绍。另一个API允许文档作为元素对象树来遍历。15.3.2节介绍这个新的（通常也更容易使用的）API。

### 15.3.1 作为节点树的文档

Document 对象、它的 Element 对象和文档中表示文本的 Text 对象都是 Node 对象。Node定义了以下重要的属性：

- parentNode：该节点的父节点，或者针对类似Document对象应该是null，因为它没有父节点。
- childNodes：只读的类数组对象（NodeList对象），它是该节点的子节点的实时表示。
- firstChild、lastChild：该节点的子节点中的第一个和最后一个，如果该节点没有子节点则为null。
- nextSibling、previoursSibling：该节点的兄弟节点中的前一个和下一个。具有相同父节点的两个节点为兄弟节点。节点的顺序反映了它们在文档中出现的顺序。这两个属性将节点之间以双向链表的形式连接起来。
- nodeType：该节点的类型。9代表Document节点，1代表Element节点，3代表Text节点，8代表Comment节点，11代表DocumentFragment节点。
- nodeValue：Text节点或Comment节点的文本内容。
- nodeName：元素的标签名，以大写形式表示。

使用这些 Node 属性，可以用以下类似的表达式得到文档的第一个子节点下面的第二个子节点的引用：

假设上述提到的文档代码如下：

```js
document.childNodes[0].childNodes[1];
document.firstChild.firstChild.nextSibling;
```

假如上述的代码如下：

```html
<html>
  <head>
    <title>test</title>
  </head>
  <body>
    hello world!
  </body>
</html>
```

那么第一个子节点下面的第二个子节点就是`<body>`元素，它的 nodeType 为1， nodeName 为“BODY”。

但请注意，该API对文档文本的变化及其敏感。例如，如果修改了文档，在`<html>`和`<head>`标签之间插入一个新行，那么表示该新行的Text节点就是文档的第一个子节点下面的第一个子节点，并且`<head>`元素就是第二个子节点而不是`<body>`元素了。

### 15.3.2 作为元素树的文档

当将主要的兴趣点集中在文档中的元素上而非它们之间的文本（和它们之间的空白）上时，我们可以使用另外一个更有用的 API 。它将文档看做是 Element 对象树，忽略部分文档：Text和Comment节点。

该 API 的第一部分是 Element 对象的 children 属性。类似 ChildNodes ，它也是一个 NodeList 对象，但不同的是 children 列表只包含 Element 对象。 children 并非标准属性，但是它在所有当前的浏览器中都能工作。IE已经实现有一段很长的时间了，其他大多数浏览器也已如法炮制。最后采纳它的主流浏览器是Firefox3.5。

注意， Text 和 Comment 节点没有 children 属性，它意味着上述`Node.parentNode`属性不可能返回Text或Comment节点。任何 Element 的 parentNode 总是另一个 Element ，或者，追溯到树根的 Document 或 DocumentFragment 节点。

基于元素的文档遍历 API 的第二部分是 Element 属性，后者类似Node对象的子属性和兄弟属性：

- firstElementChild, lastElementChild：类似firstChild和lastChild，但只代表子Element。
- nextElementSibling, previousElementSibling：类似nextSibling和previousSibling，但只代表兄弟Element。
- childElementCount：子元素的数量。返回的值和`children.length`值相等。子元素和兄弟元素的属性是标准属性，并在除了IE之外的浏览器中都已实现。

由于逐个元素的文档遍历的 API 并未完全标准化，我们仍然可以通过像例15-2中可移植的遍历函数那样来实现这种功能： 

```js
/*****可移植的遍历函数******/
/**
* 返回元素e的第n层祖先元素，如果不存在此类祖先或祖先不是Element，例如（Document或者DocumentFragment）则返回null
* 如果n为0，则返回e本身，如果n为1（或省略），则返回父元素。如果n为2，则返回祖父元素，依次类推
**/
function parent(e, n) {
  if (n === undefined) n = 1;
  while (n-- && e) e = e.parentNode;
  if (!e || e.nodeType !== 1) return null;
  return e;
}


/**
  *返回元素e的第n个兄弟元素，如果n为正，返回后续的第n个兄弟元素；
  * 如果n为负，返回前面n个兄弟元素，如果n为零，返回e本身
  **/
function sibling(e, n) {
  while (e && n !== 0) { //如果e未定义，立刻返回它
    if (n > 0) { //查找后续的兄弟元素
      if (e.nextElementSibling) e = e.nextElementSibling;
      else {
        for (e = e.nextSibling; e && e.nodeType !== 1; e = e.nextSibling)
        /*空循环*/
        ;
      }
      n--;
    } else { //查找前边的兄弟元素
      if (e.previousElementSibling) e = e.previousElementSibling;
      else {
        for (e = e.previousElementSibling; e && e.nodeType !== 1; e = e.previousElementSibling)
        /*空循环*/
        ;
      }
      n++
    }
  }
  return e;
}


/**
  * 返回元素e的第n代子元素，如果不存在则为null
  * 负值n代表从后往前计数，0表示第一个子元素，而-1代表最后一个，-2代表倒数第二，依次类推
  **/
function child(e, n) {
if (e.children) { //如果children数组存在
  if (n < 0) n += e.children.length; //转换负的n为数组索引
  if (n < 0) return null; //如果它仍为负，说明没有子元素
  return e.children[n]; //返回值指定的子元素
}
//如果e没有children数组，找到第一个字元素并向前数，或找到最后一个子元素并往回鼠
if (n >= 0) { //非负，从第一个元素向前数
  //找到e的第一个子元素
  if (e.firstElementChild) e = e.firstElementChild;
  else {
    for (e = e.firstElementChild; e && e.nodeType !== 1; e = e.nextSibling)
    /*空循环*/
    ;
  }
  return sibling(e, n); //返回第一个子元素的第n个兄弟严肃
} else { //n为负数，从第一个元素往回数
  if (e.lastElementChild) e = e.lastElementChild;
  else {
    for (e.lastElementChild; e && e.nodeType !== 1; e = e.previousElementSibling)
    /*空循环*/
    ;
  }
  return sibling(e, n + 1); //+1来转化最后1个子元素的最后1个兄弟元素
}
}
```

## 15.4 属性

HTML 元素由一个标签和一组称为属性（attribute）的名/值对组成。例如，`<a>`元素定义了一个超链接，它的 href 属性值作为链接的目的地址。 HTML 元素的属性值在代表这些元素的 HTMLElement 对象的属性（property）中是可用的。 DOM 还定义了另外的 API 来获取或设置 XML 属性值和非标准的 HTML 属性。详细信息见以下各节。

### 15.4.1 HTML作为Element的属性

表示HTML文档元素的 HTMLElement 对象定义了读/写属性，它们映射了元素的HTML属性。 HTMLElement 定义了通用的HTTP属性（如id、标题lang和dir）的属性，以及事件处理程序属性（如onclick）。特定的Element子类型为其元素定义了特定的属性。例如，查询一张图片的URL，可以使用表示`<img>`元素的 HTMLElement 对象的src属性：

同样地，可以为一个`<form>`元素设置表单提交的属性，代码如下：

```js
var image = document.getElementById("myimage");
var imgurl = image.src; //src是图片的url
image.id === "myimage"; //true
```

相似地，你通过下面这样的代码设置`<form>`元素提交的属性：

```js
var f = document.forms[0]; // First <form> in the document
f.action = "http://www.example.com/submit.php"; // Set URL to submit it to.
f.method = "POST";
```

HTML 属性名不区分大小写，但 JavaScript 属性名则大小写敏感。从 HTML 属性名转换到 JavaScript 属性名应该采用小写。但是，如果属性名包含不止一个单词，则将除了第一个单词以外的单词的首字母大写，例如：defaultChecked和tabIndex。

有些 HTML 属性名在 JavaScript 中是保留字。对于这些属性，一般的规则是为属性名加前缀“html”。例如，HTML的for属性（`<lable>`元素）在 JavaScript 中变为htmlFor属性。“class”在 JavaScript 中是保留字（但还未使用），它是HTML非常重要的class属性，是上面规则的一个例外：在 JavaScript 代码中它变为 className 。我们将在第16章中再次见到 className 属性。

表示 HTML 属性的值通常是字符串。当属性为布尔值或数值（例如，`<input>`元素的defaultChecked和maxLength属性），属性也是布尔值或数值，而不是字符串。事件处理程序属性值总是为Function对象（或null）。HTML5规范定义了一个新的属性（如`<input>`和相关元素的form属性）用以将元素ID转换为实际的Element对象。最后，任何 HTML 元素的 style 属性值是 CSSStyleDeclaration 对象，而不是字符串。我们将在第16章中看到关于这个重要属性的更多信息。

注意，这个基于属性的API用来获取和设置属性值，但没有定义任何从元素中删除属性的方法。奇怪的是，delete操作符也无法完成此目的。下一节描述一种可以实现此目的的方法。

### 15.4.2 获取和设置非标准的属性

如上所述， HTMLElement 和其子类型定义了一些属性，它们对应于元素的标准 HTML 属性。Element类型还定义了`getAttribute()`和`setAttribute()`方法来查询和设置非标准的 HTML 属性，也可用来查询和设置XML文档中元素上的属性。

```js
var image = document.images[0];
var width = parseInt(image.getAttribute("width"));
image.setAttribute("class","firstImage");
```

上述代码给出了这些方法和前面的基于属性的 API 之间两个重要的区别。首先，属性值都被看做是字符串。`getAttribute()`不返回数值、布尔值或对象。其次，方法使用标准属性名，甚至当这些名称为 JavaScript 保留字时也不例外。对 HTML 元素来说，属性名不区分大小写。

Element 类型还定义了两个相关的方法，`hasAttribute()`和`removeAttribute()`，它们用来检测命名属性是否存在和完全删除属性。当属性为布尔值时这些方法特别有用：有些属性（如 HTML 的表单元素的 disabled 属性）在一个元素中是否存在是重点关键，而其值却无关紧要。

如果操作包含来自其他命名空间中属性的 XML 文档，可以使用这4个方法的命名空间版本：`getAttributeNS()`、`setAttributeNS()`、`hasAttributeNS()`和`removeAttributeNS()`。这些方法需要两个属性名字符串作为参数，而不是一个。第一个是标识命名空间的URI，第二个通常是属性的本地名字，在命名空间中是无效的。但特别地，`setAttributeNS()`的第二个参数应该是属性的有效名字，它包含命名空间的前缀。可以在本书的第四部分中阅读更多关于命名空间识别的属性的方法。

### 15.4.3 数据集属性

有时候在 HTML 元素上绑定一些额外的信息也是很有帮助的，当 JavaScript 选取这些元素并以某种方式操纵这些信息时就是很典型的情况。有时可以通过给 class 属性添加特殊的标识符来完成。其他时候针对更复杂的数据，客户端程序员会借助使用非标准的属性。如上所述，可以使用`getAttribute()`和`setAttribute()`来读和写非标准属性的值。但为此而付出的代价是文档将不再是合法有效的 HTML 。

HTML5 提供了一个解决方案。在HTML5文档中，任意以“data-”为前缀的小写的属性名字都是合法的。这些“数据集属性”将不会对其元素的表现产生影响，它们定义了一种标准的、附加额外数据的方法，并不是在文档合法性上做出让步。

HTML5 还在 Element 对象上定义了 dataset 属性。该属性指代一个对象，它的各个属性对应于去掉前缀的`data-`属性。因此`dataset.x`应该保存`data-x`属性的值。带连字符的属性对应于驼峰命名法属性名：`data-jquery-test`属性就变成`dataset.jqueryTest`属性。

看一个更具体的例子，假设文档包含如下标记：

```js
<span class="sparkline" data-ymin="0" data-ymax="10">
1 1 1 2 2 3 4 5 5 4 3 5 6 7 7 4 2 1
</span>
```

火花线（sparkline）是个小图案——通常是一条线——设计用来在文本流中显示。为了生成一条火花线，也许可以同如下代码提取上述 dataset 属性的值：

```js
//假设ES5 Array.map() 方法 (或类似的方法）有定义
var sparklines = document.getElementsByClassName("sparkline");
for (var i = 0; i < sparklines.length; i++) {
  var dataset = sparklines[i].dataset;
  var ymin = parseFloat(dataset.ymin);
  var ymax = parseFloat(dataset.ymax);
  var data = sparklines[i].textContent.split(" ").map(parseFloat);
  drawSparkline(sparklines[i], ymin, ymax, data); // 该方法未实现
}
```

在写本书的这段时间中， dataset 属性还没有在当前的浏览器中实现，上述代码应该写成这样：

```js
var sparklines = document.getElementsByClassName("sparkline");
for (var i = 0; i < sparklines.length; i++) {
  var elt = sparklines[i];
  var ymin = parseFloat(elt.getAttribute("data-ymin"));
  var ymin = parseFloat(elt.getAttribute("data-ymax"));
  var points = elt.getAttribute("data-points");
  var data = elt.textContent.split(" ").map(parseFloat);
  drawSparkline(elt, ymin, ymax, data); // 此方法未实现
}
```

注意， dataset 属性是（或将是，当实现以后）元素的`data-`属性的实时、双向接口。设置或删除dataset 的一个属性就等同于设置或移除对应元素的`data-`属性。

上述例子中的`drawSparkline()`函数是虚构的，但例21-13给出了用`<canvas>`元素绘制类似火花线的标记代码。

### 15.4.4 作为Attr节点的属性

还有一种使用 Element 的属性的方法。Node类型定义了 attributes 属性。针对非 Element 对象的任何节点，该属性为null。对于 Element 对象， attributes 属性是只读的类数组对象，它代表元素的所有属性。类似 NodeLists ， attributes 对象也是实时的。它可以用数字索引访问，这意味着可以枚举元素的所有属性。并且，它也可以用属性名索引：

```js
document.body.attributes[0]; //<body>元素的第一个属性
document.body.attributes.bgColor //<body>元素的bgColor属性
document.body.attributes["ONLOAD"] //<body>元素的onload属性
```

当索引 attributes 对象时得到的值是 Attr 对象。 Attr 对象一类特殊的 Node ，但从来不会像 Node 一样去用。 Attr 的 name 和 value 属性返回该属性的名字和值。

## 15.5 元素的内容

再看一下图15-1，并问自己一个问题：`<p>`元素的“内容”是什么？回答这个问题也许有3个方法：

- 内容是 HTML 字符串`This is a<i>simple</i>document`。
- 内容是纯文本字符串`This is a simple document`。
- 内容是一个 Text 节点、一个包含了一个 Text 子节点的 Element 节点和另外一个 Text 节点。

每一种回答都有效，并且各有千秋。后面几节解释如何使用HTML表示、纯文本表示和元素内容的树状表示。

### 15.5.1 作为HTML的元素内容

读取 Element 的 innerHTML 属性作为字符串标记返回那个元素的内容。在元素上设置该属性调用了Web浏览器的解析器，用新字符串内容的解析展现形式替换元素当前内容。（不要管它的名字，除了在HTML元素上， innerHTML 也可以在XML元素上使用。）

Web 浏览器很擅长解析 HTML ，通常设置 innerHTML 效率非常高，甚至在指定的值需要解析时效率也是相当不错。但注意，对 innerHTML 属性用“+=”操作符重复追加一小段文本通常效率低下，因为它既要序列化又要解析。

innerHTML 是在 IE4 中引入的。虽然所有的浏览器都支持它已经有很长一段时间了，但随着 HTML5 的到来它才变得标准化。 HTML5 说 innerHTML 应该在Document节点以及 Element 节点上工作正常，但这还未被普遍地支持。

HTML5 还标准化了 outerHTML 属性。当查询 outerHTML 时，返回的HTML或XML标记的字符串包含被查询元素的开头和结尾标签。当设置元素的 outerHTML 时，元素本身被新的内容所替换。只有 Element 节点定义了 outerHTML 属性，Document节点则无。在写本书的这段时间里， outerHTML 在除了Firefox的所有当前浏览器中都支持。（见本章后面的例15-5，基于 innerHTML 实现outerHTML。）

IE 引入的另一个特性是`insertAdjacentHTML()`方法，它将在 HTML5 中标准化，它将任意的HTML标记字符串插入到指定的元素“相邻”的位置。标记是该方法的第二个参数，并且“相邻”的精确含义依赖于第一个参数的值。第一个参数为具有以下值之一的字符串：“beforebegin”、“afterbegin”、“beforeend”和“afterend”。这些值对应的插入点如图15-3所示。

图15-3：`insertAdjacentHTML()`的插入点`insertAdjacentHTML()`在当前版本的Firefox中不支持。本章后面的内容，例15-6展示了如何用 innerHTML 属性实现`insertAdjacentHTML()`，也展示了如何写出不需要一个字符串参数来指定插入点的HTML插入方法。

### 15.5.2 作为纯文本的元素内容

有时需要查询纯文本形式的元素内容，或者在文档中插入纯文本（不必转义 HTML 标记中使用的尖括号和 & 符号）。标准的方法是用 Node 的 textContent 属性来实现：

```js
var para = document.getElementsByTagName("p")[0];
var text = para.textContent; //'this is a simple document'
para.textContent = "hello world!" //修改段落内容
```

textContent 属性在除了IE的所有当前的浏览器中都支持。在 IE 中，可以用 Element 的 innerText 属性来代替。微软在 IE 4 中引入了 innerText 属性，它在除了Firefox的所有当前浏览器中都支持。

textContent 和 innerText 属性非常相似，通常可以互相替换使用。不过要小心空元素（在 JavaScript 中字符串""是假值）和未定义的属性之间的区别：

```js
/**
*一个参数，返回元素的textContent或innerText
* 两个参数，用value值代替参数设置元素的textContent或innerText
**/
function textContent(element, value) {
  var content = element.textContent;  // 检测textContent是否定义
  if (value === undefined) {  // 没传递value,因此返回当前文本
    if (content !== undefined) return content;
    else return element.innerText;
  } else {  // 传递value,设置文本
    if (content !== undefined) element.textContent = value;
    else element.innerText = value;
  }
}
```

textContent 属性就是将指定元素的所有后代 Text 节点简单地串联在一起。 innerText 没有一个明确指定的行为，但是和 textContent 有一些不同。 innerText 不返回<`script>`元素的内容。它忽略多余的空白，并试图保留表格格式。同时， innerText 针对某些表格元素（如`<table>`、`<tbody>`和`<tr>`）是只读的属性。

> `<script>`元素中的文本
> 内联的`<script>`元素（也就是那些没有src属性的）有一个text属性用来获取它们的文本。浏览器不显示`<script>`元素的内容，并且HTML解析器忽略脚本中的尖括号和星号。这使得`<script>`元素成为应用程序用来嵌入任意文本内容的一个理想的地方。简单地将元素的type属性设置为某些值（如“text/x-custom-data”），就标明了脚本为不可执行的JavaScript代码。如果这样做，JavaScript解释器将忽略该脚本，但该元素将仍然存在于文档树中，它的text属性还将返回数据给你。

### 15.5.3 作为Text节点的元素内容

另一种方法处理元素的内容来是当做一个子节点列表，每个子节点可能有它自己的一组子节点。当考虑元素的内容时，通常感兴趣的是它的 Text 节点。在 XML 文档中，你也必须准备好处理 CDATASection 节点——它是 Text 的子类型，代表了 CDATA 段的内容。

例15-3展示了一个`textContent()`函数，它递归地遍历元素的子节点，然后连接后代节点中所有的 Text 节点的文本。为了理解代码，回想一下 nodeValue 属性（定义在Node类型中），它保存 Text 节点的内容。

```js
/**查找元素的后代节点中所有的Text节点**/
//返回元素e的纯文本内容，递归进入其子元素
//该方法的效果类似于textContent属性
function textContent(e) {
  var child, type, s = ""; //s保存所有字节点文本
  for (child = e.firstChild; child != null; child = child.nextSibling) {
    type = child.nodeType;
    if (type === 3 || type === 4) //text和CDATASection节点
      s += child.nodeValue;
    else if (type === 1)
      s += textContent(child);
  }
  return s;
}
```

nodeValue 属性可以读/写，设置它可以改变 Text 或 CDATASection 节点所显示的内容。 Text 和 CDATASection 都是 CharacterData 的子类型，可以在第四部分查看相关信息。 CharacterData 定义了data属性，它和 nodeValue 的文本相同。以下函数通过设置data属性将Text节点的内容转换成大写形式：

```js
//递归把n的后代子节点中的所有Text节点内容转换为大写形式
cd = document.getElementsByTagName("p")[0];

function upCase(n) {
  if (n.nodeType == 3 || n.nodeType == 4) //如果n是Text或CDATA节点
    n.data = n.data.toUpperCase(); //转换为大写
  else
    for (var i = 0; i < n.childNodes.length; i++)
      upCase(n.childNodes[i]);
}
```

CharacterData 还定义了一些在 Text 或 CDATASection 节点中不太常用的方法来添加、删除、插入和替换文本。除了修改已存在Text节点的内容，还可以在 Element 中插入全新的Text节点或用新 Text 节点来替换已有节点。创建、插入和删除节点就是下一节的主题。

## 15.6 创建、插入和删除节点

我们已经看到用 HTML 和纯文本字符串如何来查询和修改文档内容，也已经看到我们能够遍历 Document 来检查组成 Document 的每个 Element 和 Text 节点。在每个节点级别修改文档也是有可能的。 Document 类型定义了创建 Element 和 Text 对象的方法， Node 类型定义了在节点树中插入、删除和替换的方法。例13-4展示了节点的创建和插入，这里复制了这个简短的示例：

```js
function loadsync(url){
  var hand = document.getElementsByTagName("head")[0];
  var s = document.createElement("script");
  s.src = url;
  hand.appendChild(s);
}
```

以下小节包含了节点创建、插入和删除的更多细节和具体例子，也包含在操作多个节点时的一种捷径：使用 DocumentFragment 。

### 15.6.1 创建节点

如以上代码所示，创建新的 Element 节点可以使用 Document 对象的`createElement()`方法。给方法传递元素的标签名：对 HTML 文档来说该名字不区分大小写，对XML文档则区分大小写。

Text节点用类似的方法创建：

```js
var newnode = document.createTextNode("Text node");
var newelement = document.createElement("p");
```

Document 也定义了一些其他的工厂方法，如不经常使用的`createComment()`。在15.6.4节中使用了`createDocumentFragment()`方法。在使用了XML命名空间的文档中，可以使用`createElementNS()`来同时指定命名空间的URI和待创建的 Element 的标签名字。

另一种创建新文档节点的方法是复制已存在的节点。每个节点有一个`cloneNode()`方法来返回该节点的一个全新副本。给方法传递参数true也能够递归地复制所有的后代节点，或传递参数false只是执行一个浅复制。在除了 IE 的其他浏览器中，Document 对象还定义了一个类似的方法叫`importNode()`。如果给它传递另一个文档的一个节点，它将返回一个适合本文档插入的节点的副本。传递true作为第二个参数，该方法将递归地导入所有的后代节点。

### 15.6.2 插入节点

一旦有了一个新节点，就可以用Node的方法`appendChild()`或`insertBefore()`将它插入到文档中。`appendChild()`是在需要插入的 Element 节点上调用的，它插入指定的节点使其成为那个节点的最后一个子节点。

`insertBefore()`就像`appendChild()`一样，除了它接受两个参数。第一个参数就是待插入的节点，第二个参数是已存在的节点，新节点将插入该节点的前面。该方法应该是在新节点的父节点上调用，方法的第二个参数必须是该父节点的子节点。如果传递null作为第二个参数，`insertBefore()`的行为类似`appendChild()`，它将节点插入在最后。

这是一个在数字索引的位置插入节点的简单函数。它同时展示了`appendChild()`和`insertBefore()`方法：

```js
// 将child节点插入到parent中，使其成为第n个子节点
function inserAt(parent, child, n)
if (n < 0 || n > parent.childNodes.length) throw new Error("invalid index");
else if (n == parent.childNodes.length) parent.appendChild(child);
else parent.insertBefore(child, parent.childNodes[n]);
```

如果调用`appendChild()`或`insertBefore()`将已存在文档中的一个节点再次插入，那个节点将自动从它当前的位置删除并在新的位置重新插入：没有必要显式删除该节点。例15-4展示了一个函数，基于表格指定列中单元格的值来进行行排序。它没有创建任何新的节点，只是用`appendChild()`来改变已存在节点的顺序罢了。

```js
/**表格的排序**/
//根据指定表格每行第n个单元格的值，对第一个<tbody>中的进行排序
//如果存在comparator函数则使用它，否则按字母表顺序比较
function sortrows(table, n, comparator) {
  var tbody = table.tBodies[0]; //第一个<tbody>,可能是隐式窗口的
  var rows = tbody.getElementsByTagName("tr"); //tbody中所有行
  rows = Array.prototype.slice.call(rows, 0); //真实的数组
  //基于第n个<td>元素的值对行排序
  rows.sort(function(row1, row2) {
    var cell1 = row1.getElementsByTagName("td")[n]; //获得第n个单元格
    var cell2 = row2.getElementsByTagName("td")[n]; //两行都是
    var val1 = cell1.textContent || cell1.innerText; //获得文本内容
    var val2 = cell2.textContent || cell2.innerText; //同上，两单格都是
    if (comparator) return comparator(val1, val2); //    进行比较
    if (val1 < val2) return -1;
    else if (val1 > val2) return 1;
    else return 0;
  });
  //在tobody中按他们的顺序把行添加到最后
  //这将自动把它们从当前位置移走，故没必要预先删除它们
  //如果<tbody>还包含除了<tr>的任何其他元素，这些节点都将会悬浮到顶部位置
  for (var i = 0; i < rows.length; i++) tbody.appendChild(rows[i]);
}

//查找表格的<th>元素，假设只有一行，它们可以单击
//以便单击列标题，按列对行排序。
function makeSortable(table) {
  var headers = table.getElementsByTagName("th");
  for (var i = 0; i < headers.length; i++) {
    (function(n) { //嵌套函数来创建本地域
      headers[i].onclick = function() {
        sortrows(table, n);
      };
    }(i)); //将i的全局变量赋值给局部变量n
}
}
```

### 15.6.3 删除和替换节点

`removeChild()`方法是从文档树中删除一个节点。但是请小心：该方法不是在待删除的节点上调用，而是（就像其名字的一部分“child”所暗示的一样）在其父节点上调用。在父节点上调用该方法，并将需要删除的子节点作为方法参数传递给它。在文档中删除n节点，代码可以这样写：

```js
n.parentNode.removeChild(n);
```

`replaceChild()`方法删除一个子节点并用一个新的节点取而代之。在父节点上调用该方法，第一个参数是新节点，第二个参数是需要代替的节点。例如，用一个文本字符串来替换节点n，代码可以这样写：

```js
n.parentNode.replaceChild(document.createTextNode("[redactd]"),n);
```

以下函数展示了`replaceChild()`的另一种用法：

```js
function embolden(n) {
  // 假设参数为字符串而不是节点，将其当做元素的id
  if (typeof n == "string") n = document.getElementById(n);
  var parent = n.parentNode; // 获得n的父节点
  var b = document.createElement("b"); //创建一个b元素
  parent.replaceChild(b, n); // 使用<b>元素替换节点n
  b.appendChild(n); // 使你成为<b>元素的子节点
}
```

15.5.1节介绍过元素的outerHTML属性，也解释过在当前版本的Firefox中还未实现它。例15-5展示了在Firefox中（和其他任何支持innerHTML的浏览器，要有一个可扩展的`Element.prototype`对象，还要有一些方法来定义属性的getter和setter）如何来实现该属性。同时代码也展示了`removeChild()`和`cloneNode()`方法的实际用法。

```js
/**使用innerHTML实现outerHTML属性**/
//为那些不支持它的浏览器实现outerHTML属性
//假设浏览器的确支持innerHTML，并有个可扩展的Element.prototype
//并且可以定义getter和setter
(function() {
  //如果outer存在，直接返回
  if (document.createElement("div").outerHTML) return;
  //返回this所引用元素的外部HTML
  function outerHTMLGetter() {
    var container = document.createElement("div"); //虚拟元素
    container.appendChild(this.cloneNode(true)); //复制到虚拟节点
    return container.innerHTML; //返回虚拟节点的innerHTML
  }

  //用指定的值设置元素的外部的HTML
  function outerHTMLSetter(value) {
    //创建一个虚拟元素，设置其内容为指定的值
    var container = document.createElement("div");
    container.innerHTML = value;
    //将虚拟元素的节点全部移动到文档中
    while (container.firstChild) //循环知道container没有子节点为止
      this.parentNode.insertBefore(container.firstChild, this);
    //删除被取代的节点
    this.parentNode.removeChild(this);
  }

  //现在使用着两个函数作为所有Element对象的outerHTML属性的getter和setter
  //如果它存在则使用ECMAScript5的Object.defineProperty()方法
  //否则，退而求其次，使用__defineProperty__()和__definedSetter__()
  if (Object.defineProperty) {
    Object.defineProperty(Element.prototype, "outerHTML", {
      get: outerHTMLGetter,
      set: outerHTMLSetter,
      enumerable: false,
      configurable: true
    });
  } else {
    Element.prototype.__defineGetter__("outerHTML", outerHTMLGetter);
    Element.prototype.__defineSetter__("outerHTML", outerHTMLSetter);
  }
}
());
```

### 15.6.4 使用DocumentFragment

DocumentFragment 是一种特殊的Node，它作为其他节点的一个临时的容器。像这样创建一个 DocumentFragment ：

```js
var frag = document.createDocumentFragment();
```

像 Document 节点一样， DocumentFragment 是独立的，而不是任何其他文档的一部分。它的parentNode总是为null。但类似Element，它可以有任意多的子节点，可以用`appendChild()`、`insertBefore()`等方法来操作它们。

DocumentFragment 的特殊之处在于它使得一组节点被当做一个节点看待：如果给`appendChild()`、`insertBefore()`或`replaceChild()`传递一个 DocumentFragment ，其实是将该文档片段的所有子节点插入到文档中，而非片段本身。（文档片段的子节点从片段移动到文档中，文档片段清空以便重用。）以下函数使用 DocumentFragment 来倒序排列一个节点的子节点：

```js
//倒序排列节点n的子节点
function reverseDome(n) {
  //创建一个DocumentFragment()
  var f = document.createDocumentFragment();
  //从后至前循环子节点，将每一个字节点移动到文档片段中
  //n的最后一个子节点变成第一个子节点
  //注意，给f添加一个节点，该节点自动会从n中删除
  while (n.lastChild) f.appendChild(n.lastChild);
  
  //最后将所有的子节点一次移动回n中
  n.appendChild(f);
}
```

例15-6使用 innerHTML 属性和 DocumentFragment 实现`insertAdjacentHTML()`方法（见15.5.1节）。它还定义一些名字更符合逻辑的HTML插入函数，可以替换让人迷惑的`insertAdjacentHTML()`API。内部工具函数`fragment()`可能是代码中最有用的部分：它返回一个对指定HTML字符串文本进行解析后的DocumentFragment。

```js
/**用innerHTML实现insertAdjacentHTML**/
//本模块为不支持它的浏览器定义了Element.insertAdjacentHTML
//还定义了一些可移植的HTML插入函数，它们的名字比insertAdjacentHTML更符合逻辑
//Insert.before、Insert.after、Insert.atStart和Insert.atEnd
var Insert = (function() {
  //如果命名空间有原生的insertAdjacentHTML.在4个函数名更名了的HTML使用它。
  if (document.createElement("div").insertAdjacentHTML) {
    return {
      before:function(e, h) {e.insertAdjacentHTML("beforebegin", h);},
      after:function(e, h) {e.insertAdjacentHTML("afterend", h);},
      atStart:function(e, h) {e.insertAdjacentHTML("afterbegin", h);},
      atEnd:function(e, h) {e.insertAdjacentHTML("beforeend");}
    };
  }
  //否则，无元素的insertAdjacentHTML同样实现4个插入函数，并定义insertAdjacentHTML
  //首先，定义一个工具函数，传入HTML字符串，返回一个DocumentFragment
  //包含解析后的HTML的表示
  function fragment(html) {
    var elt = document.createElement("div"); //创建空元素
    var frag = document.createDocumentFragment(); //创建文本片段
    elt.innerHTML = html; //设置元素内容
    while (elt.firstChild) //移动所有的节点
      frag.appendChild(elt.firstChild); //从elt到frag
    return frag; //返回frag
  }
  var Insert = {
    before:function(elt, html) {elt.parentNode.insertBefore(fragment(html), elt);},
    after:function(elt, html) {elt.parentNode.insertBefore(fragment(html), elt.nextSibling);},
    atStart: function(elt, html) {elt.insertBefore(fragment(html), elt.firstChild);},
    atEnd: function(elt, html) {elt.appendChild(fragment(html));}
  };
  //基于以上函数实现insertAdacentHTMLs
  Element.prototype.insertAdjacentHTML = function(pos, html) {
    switch(pos.toLowerCase()) {
      case "beforebegin":return Insert.before(this.html);
      case "afterend":return Insert.after(this.html);
      case "afterbegin":return Insert.atStart(this, html);
      case "beforeend":return Isert.atEnd(this, html);
    }        
  };
  return Insert; //最后返回4个插入函数
}());
```


## 15.7 例子：生成目录表

例15-7说明了如何为文档动态地创建一个目录表。它展示了上一节所描述的文档脚本化的很多概念：元素选取、文档遍历、元素属性设置、innerHTML属性设置和在文档中创建与插入新节点等。本例注释详尽，理解代码应该不会有问题。

```js
/**一个动态自动生成的目录表**/
/* *
* 这个模块注册一个可在页面加载完成后自动运行的匿名函数。当执行这个函数时会去文档中查找id为“TOC”的元素
*
* 生成的TOC目录应该具有自己的css样式。这个目录区域的样式className设置为“TOCEntry”
* 统一我们为不同层级的目录模板标题定义不同的样式。<h1>标签生成的标题className为“TOCLevel1”，<h2>标签生成的标题className为"TOCLevel2",依次类推
*段编号的样式为“TOCSectNum”
* 这个模块需要onLoad()工具函数
* */
(function() { // 匿名函数定义了一个局部作用域
  // 查找TOC容器元素
  // 如果不存在，则在文档开头处新建一个
  var toc = document.getElementById("TOC");
  if (!toc) {
    toc = document.createElement("div");
    toc.id = "TOC"
    document.body.insertBefore(toc, document.body.firstChild);
  }
  // 查找所有的标题元素
  var headings;
  if (document.querySelectorAll) // 我们能否使用这个简单的方法？
    headings = document.querySelectorAll("h1, h2, h3, h4, h5, h6");
  else // 否则查找的方法稍微复杂些
    headings = findHeadings(document.body, []);
  // 递归遍历document的body，查找元素
  function findHeadings(root, sects) {
    for (var c = root.firstChild; c != null; c = c.nextSibling) {
      if (c.nodeType !== 1) continue;
      if (c.tagName.length == 2 && c.tagName.charAt(0) == "H")
        sects.push(c);
      else
        findHeadings(c, sects);
    }
    return sects;
  }
  // 初始化一个数组来保持跟踪章节好
  var sectionNumbers = [0, 0, 0, 0, 0, 0];
  // 现在循环已经找到的标题元素
  for (var h = 0; h < headings.length; h++) {
    var heading = headings[h];
    // 跳过在TOC容器中的标题元素
    if (heading.parentNode == toc) continue;
    // 判定标题的级别
    var level = parseInt(heading.tagName.charAt(1));
    if (isNaN(level) || level < 1 || level > 6) continue;
    
    // 对于重要的标题级别增加sectionNumber对于的数字
    // 重置所有标题比它级别低的数字为零
    sectionNumbers[level-1]++;
    for(var i = level; i<6;i++) sectionNumbers[i] =0;
    
    // 现在讲所有标题级别的章节号组合产生一个章节号，如2.3.1
    var sectionNumber = sectionNumbers.slice(0,level).join(".")
    
    // 为标题级别增加章节号
    // 把数字放在<span>中，是的其可以用样式修饰
    var span = document.createElement("span");
    span.calssName = "TOCSectNum";
    span.innerHTML =sectionNumber;
    heading.insertBefore(span,heading.firstChild);
    
    // 用命名的锚点将标题包起来，以便它增加链接
    var anchor = document.createElement("a");
    anchor.name = "TOC"+ sectionNumber;
    heading.parentNode.insertBefore(anchor,heading);
    anchor.appendChild(heading);
    
    // 现在为该节点创建一个链接
    var link = document.createElement("a");
    link.href = "#TOC" + sectionNumber; // 链接目标的地址
    link.innerHTML = heading.innerHTML; // 链接文本与实际标题一致
    
    // 将链接放在一个div中，div用于基于级别名字的样式修饰
    var entry = document.createElement("div");
    entry.className = "TOCEntry TOCLevel" +level;
    
    entry.appendChild(link);
    // 改div添加到TOC容器
    toc.appendChild(entry)
  }
}); 
```

## 15.8 文档和元素的几何形状和滚动

在本章中，到目前为止我们考虑的文档被看做是元素和文本节点的抽象树。但是当浏览器在窗口中渲染文档时，它创建文档的一个视觉表现层，在那里每个元素有自己的位置和尺寸。通常，Web应用程序可以将文档看做是元素的树，并且不用关心在屏幕上这些元素是如何渲染的。但有时，判定一个元素精确的几个形状也是非常有必要的。例如，将在第16章中看到利用CSS为元素指定位置。如果想用CSS动态定位一个元素（如工具提示或插图）到某个已经由浏览器定位后的普通元素的旁边，首先需要判定那个元素的当前位置。

本节阐述了在浏览器窗口中完成文档的布局以后，怎样才能在抽象的基于树的文档模型与几何形状的基于坐标的视图之间来回变换。本节描述的属性和方法已经在浏览器中实现了有相当长的一段时间了（虽然有些是IE特有的，有些直到IE 9才实现）。在写本书的这段时间里，它们通过了W3C的标准化流程，作为[CSSOM-View模块](http://www.w3.org/TR/cssom-view/)。

### 15.8.1 文档坐标和视口坐标

元素的位置是以像素来度量的，向右代表X坐标的增加，向下代表Y坐标的增加。但是，有两个不同的点作为坐标系的原点：元素的X和Y坐标可以相对于文档的左上角或者相对于在其中显示文档的视口的左上角。在顶级窗口和标签页中，“视口”只是实际显示文档内容的浏览器的一部分：它不包括浏览器“外壳”（如菜单、工具条和标签页）。针对框架页中显示的文档，视口是定义了框架页的`<iframe>`元素。无论在何种情况下，当讨论元素的位置时，必须弄清楚所使用的坐标是文档坐标还是视口坐标。（注意，视口坐标有时也叫做窗口坐标。）

如果文档比视口要小，或者说它还未出现滚动，则文档的左上角就是视口的左上角，文档和视口坐标系统是同一个。但是，一般来说，要在两种坐标系之间互相转换，必须加上或减去滚动的偏移量（scroll offset）。例如，在文档坐标中如果一个元素的Y坐标是200像素，并且用户已经把浏览器向下滚动75像素，那么视口坐标中元素的Y坐标是125像素。同样，在视口坐标中如果一个元素的X坐标是400像素，并且用户已经水平滚动了视口200像素，那么文档坐标中元素的X坐标是600像素。

文档坐标比视口坐标更加基础，并且在用户滚动时它们不会发生变化。不过，在客户端编程中使用视口坐标是非常常见的。当使用CSS指定元素的位置时运用了文档坐标（见第16章）。但是，最简单的查询元素位置的方法（见15.8.2节）返回视口坐标中的位置。类似地，当为鼠标事件注册事件处理程序函数时，报告的鼠标指针的坐标是在视口坐标系中的。

为了在坐标系之间互相转换，我们需要判定浏览器窗口的滚动条的位置。Window对象的 pageXOffset 和 pageYOffset 属性在所有的浏览器中提供这些值，除了IE 8及更早的版本以外。IE（和所有现代浏览器）也可以通过 scrollLeft 和 scrollTop 属性来获得滚动条的位置。令人迷惑的是，正常情况下通过查询文档的根节点（document.documentElement）来获取这些属性值，但在怪异模式下（见13.4.4节），必须在文档的`<body>`元素（document.body）上查询它们。例15-8显示了如何简便地查询滚动条的位置。

```js
/*查询窗口滚动条的位置*/
//以一个对象的x和y属性的方法返回滚动条的偏移量
function getScrollOffsets(w) {
  //使用指定才窗口，如果不带参数则使用当前窗口
  w = w || window;

  //除了IE8及更早的版本以外，其它的浏览器都能用
  if (w.pageXOffset != null) return {x: w.pageXOffset, y:w.pageYOffset};

  //对标准模式下的IE，或任何浏览器
  var d = w.document;
  if (document.compatMode == "CSS1Compat")
    return {x:d.documentElement.scrollLeft, y:d.documentElement.scrollTop};

  //怪异模式下的浏览器
  return { x: d.body.scrollLeft, y: d.body.scrollTop };
}
```

有时能够判定视口的尺寸也是非常有用的——例如，为了确定文档的哪些部分是当前可见的。利用滚动偏移量查询视口尺寸的简单方法在IE 8及更早的版本中无法工作，而且该技术在IE中的运行方式还要取决于浏览器是处于怪异模式还是标准模式。例15-9介绍了如何简便地查询视口尺寸。注意，它和例15-8的代码是如此相似。

```js
/*查询窗口的视口尺寸*/
//作为一个对象的w和h属性返回视口的尺寸
function getViewportSize(w) {
  //使用指定的窗口，如果不带参数则使用当前窗口
  w = w || window;
  //除了ie8和更早的版本，其它浏览器都能用
  if (w.innerWidth != null) return {
    w: w.innerWidth,
    h: w.innerHeight
  };
  //对于标准模式下的IE或其任何浏览器
  var d = w.document;
  if (document.compatMode == "CSS1Compat")
    return {
      w: d.documentElement.clientWidth,
      h: d.documentElement.clientHeight
    };
  //对于怪异模式下的浏览器
  return{w:d.body.clientWidth,h:d.body.clientHeight};
}
```

上述两个例子已经用到了scrollLeft、scrollTop、clientWidth和clientHeight属性。我们将在15.8.5节中再次遇到这些属性。

### 15.8.2 查询元素的几何尺寸

判定一个元素的尺寸和位置最简单的方法是调用它的`getBoundingClientRect()`方法。该方法是在IE 5中引入的，而现在当前的所有浏览器都实现了。它不需要参数，返回一个有left、right、top和bottom属性的对象。left和top属性表示元素的左上角的X和Y坐标，right和bottom属性表示元素的右下角的X和Y坐标。

这个方法返回元素在视口坐标中的位置。（`getBoundingClientRect()`方法名中的“Client”是一种间接指代，它就是Web浏览器客户端 ——专指它定义的窗口或视口。）为了转化为甚至用户滚动浏览器窗口以后仍然有效的文档坐标，需要加上滚动的偏移量：

```js
var box = e.getBoundingClientRect(); //获得视口在坐标中的位置
var offsets = getScrollOffsets(); //上面定义的工具函数
var x = box.left + offsets.x; // 转换为文档坐标
var y = box.top + offsets.y;
```

在很多浏览器（和W3C标准）中，getBoundingClientRect()返回的对象还包含width和height属性，但是在原始的IE中未实现。为了简便起见，可以这样计算元素的width和height：

```js
var box = e.getBoundingClientRect(); //获得视口在坐标中的位置
var w = box.width || (box.right - box.left);
var h = box.height || (box.bottom - box.top);
```

在第16章中将学到元素内容被一块可选的空白区域所包围，叫做内边距。内边距被边框所包围，边框被外边距所包围。内边距、边框和外边距都是可选的。`getBoundingClientRect()`所返回的坐标包含元素的边框和内边距，但不包含元素的外边距。

如果`getBoundingClientRect()`方法名中的“Client”指定了返回的矩形的坐标系，那么方法名中的“Bounding”做何解释呢？浏览器在布局时块状元素（如图片、段落和`<div>`元素等）总是为矩形。但是，内联元素（如`<span>`、`<code>`和`<b>`等）可能跨了多行，因此可能由多个矩形组成。想象一下，例如，一些被断成两行的斜体文本（用`<i>`和`</i`>标签标记的）。它的形状是由第一行的右边部分和第二行的左边部分两个矩形组成的（假设文本顺序是从左向右）。如果在内联元素上调用`getBoundingClientRect()`，它返回“边界矩形”。对于如上描述的`<i>`元素，边界矩形会包含整整两行的宽度。

如果想查询内联元素每个独立的矩形，调用`getClientRects()`方法来获得一个只读的类数组对象，它的每个元素类似于`getBoundingClientRect()`返回的矩形对象。

我们已经见过如`getElementsByTagName()`这样的DOM方法返回的结果是“实时的”，当文档变化时这些结果能自动更新。但`getBoundingClientRect()`和`getClientRects()`所返回的矩形对象（和矩形对象列表）并不是实时的。它们只是调用方法时文档视觉状态的静态快照，在用户滚动或改变浏览器窗口大小时不会更新它们。

### 15.8.3 判定元素在某点

`getBoundingClientRect()`方法使我们能在视口中判定元素的位置。但有时我们想反过来，判定在视口中的指定位置上有什么元素。这可以用Document对象的`elementFromPoint()`方法来判定。传递X和Y坐标（使用视口坐标而非文档坐标），该方法返回在指定位置的一个元素。在写本书的这段时间里，选取元素的算法还未详细指定，但是该方法的意图就是它返回在那个点的最里面的和最上面的（见16.2.1节中CSS的z-index属性）元素。如果指定的点在视口以外，`elementFromPoint()`返回null，即使该点在转换为文档坐标后是完美有效的，返回值也一样。

`elementFromPoint()`方法看上去很有用，典型的案例是将鼠标指针的坐标传递给它来判定鼠标在哪个元素上。但是，我们将在第17章学到，鼠标事件对象已经在target属性中包含了这些信息。因此，实际上`elementFromPoint()`不经常使用。

### 15.8.4 滚动

例15-8展示了如何在浏览器窗口中查询滚动条的位置。该例子中的scrollLeft和scrollTop属性可以用来设置让浏览器滚动，但有一种更简单的方法从JavaScript最早的时期开始就支持的。Window对象的`scrollTop()`方法（和其同义词`scroll()`）接受一个点的X和Y坐标（文档坐标），并作为滚动条的偏移量设置它们。也就是，窗口滚动到指定的点出现在视口的左上角。如果指定的点太接近于文档的下边缘或右边缘，浏览器将尽量保证它和视口的左上角之间最近，但是无法达到一致。以下代码滚动浏览器到文档最下面的页面可见：

```js
//获得文档和视口的高度，offsetHeight会在下面解释
var documentHeight = document.documentElement.offsetHeight;
var viewportHeight = windows.innerHeight; //或使用上面的getViewportSize()
//然后，滚动让最后一页在视口中可见
window.scrollTo(0, documentHeight - viewportHeight);
```

Window的`scrollBy()`方法和`scroll()`和`scrollTo()`类似，但是它的参数是相对的，并在当前滚动条的偏移量上增加。例如，快速阅读者可能会喜欢这样的书签（见13.2.5节）：

```js
//每200毫秒向下滚动10像素。注意，它无法关闭
javascript:void setInterval(function() {
  scrollBy(0,10)
}, 200)
```

通常，除了滚动到文档中用数字表示的位置，我们只是想它滚动使得文档中的某个元素可见。可以利用`getBoundingClientRect()`计算元素的位置，并转换为文档坐标，然后用`scrollTo()`方法达到目的。但是在需要显示的HTML元素上调用`scrollIntoView()`方法更加方便。该方法保证了元素能在视口中可见。默认情况下，它试图将元素的上边缘放在或尽量接近视口的上边缘。如果只传递false作为参数，它将试图将元素的下边缘放在或尽量接近视口的下边缘。只要有助于元素在视口内可见，浏览器也会水平滚动视口。

`scrollIntoView()`的行为与设置`window.location.hash`为一个命名锚点（`<a name="">`元素）的名字后浏览器产生的行为类似。

### 15.8.5 关于元素尺寸、位置和溢出的更多信息

`getBoundingClientRect()`方法在所有当前的浏览器上都有定义，但如果需要支持老式浏览器，不能依靠此方法而必须使用更老的技术来判定元素的尺寸和位置。元素的尺寸比较简单：任何HTML元素的只读属性offsetWidth和offsetHeight以CSS像素返回它的屏幕尺寸。返回的尺寸包含元素的边框和内边距，除去了外边距。

所有HTML元素拥有offsetLeft和offsetTop属性来返回元素的X和Y坐标。对于很多元素，这些值是文档坐标，并直接指定元素的位置。但对于已定位元素的后代元素和一些其他元素（如表格单元），这些属性返回的坐标是相对于祖先元素的而非文档。offsetParent属性指定这些属性所相对的父元素。如果offsetParent为null，这些属性都是文档坐标，因此，一般来说，用offsetLeft和offsetTop来计算元素e的位置需要一个循环：

```js
function getElementPosition(e){
  var x = 0, y = 0;
  while(e != null){
    x += e.offsetLeft;
    y += e.offsetTop;
    e = e.offsetParent;
  }
  return {x:x, y:y};
}
```

通过循环offsetParent对象链来累加偏移量，该函数计算指定元素的文档坐标。（回想一下`getBoundingClientRect()`返回的是视口坐标。）这里不能对元素的位置就一锤定音，尽管如此——这个`getElementPosition()`函数也不总是计算正确的值，下面看看如何来修复它。

除了这些名字以offset开头的属性以外，所有的文档元素定义了其他两组属性，其名称一组以client开头，另一组以scroll开头。即，每个HTML元素都有以下这些属性：

| offsetWidth  | clientWidth  | scrollWidth  |
|:-------------|:-------------|:-------------|
| offsetHeight | clientHeight | scrollHeight |
| offsetLeft   | clientLeft   | scrollLeft   |
| offsetTop    | clientTop    | scrollTop    |
| offsetParent |              |              |

为了理解这些client和scroll属性，你需要知道HTML元素的实际内容有可能比分配用来容纳内容的盒子更大，因此单个元素可能有滚动条（见16.2.6节中CSS的overflow属性）。内容区域是视口，就像浏览器的窗口，当实际内容比视口更大时，需要把元素的滚动条位置考虑进去。

clientWidth和clientHeight类似offsetWidth和offsetHeight，不同的是它们不包含边框大小，只包含内容和它的内边距。同时，如果浏览器在内边距和边框之间添加了滚动条，clientWidth和clientHeight在其返回值中也不包含滚动条。注意，对于类似`<i>`、`<code>`和`<span>`这些内联元素，clientWidth和clientHeight总是返回0。

在例15-9的`getViewportSize()`方法中使用了clientWidth和clientHeight。有一个特殊的案例，在文档的根元素上查询这些属性时，它们的返回值和窗口的innerWidth和innerHeight属性值相等。

clientLeft和clientTop属性没什么用：它们返回元素的内边距的外边缘和它的边框的外边缘之间的水平距离和垂直距离，通常这些值就等于左边和上边的边框宽度。但是如果元素有滚动条，并且浏览器将这些滚动条放置在左侧或顶部（可这不太常见），clientLeft和clientTop也就包含了滚动条的宽度。对于内联元素，clientLeft和clientTop总是为0。

scrollWidth和scrollHeight是元素的内容区域加上它的内边距再加上任何溢出内容的尺寸。当内容正好和内容区域匹配而没有溢出时，这些属性与clientWidth和clientHeight是相等的。但当溢出时，它们就包含溢出的内容，返回值比clientWidth和clientHeight要大。

最后，scrollLeft和scrollTop指定元素的滚动条的位置。在`getScrollOffsets()`方法（例15-8）中在文档的根元素上我们查询过它们。注意，scrollLeft和scrollTop是可写的属性，通过设置它们来让元素中的内容滚动。（HTML元素并没有类似Window对象的`scrollTo()`方法。）

当文档包含可滚动的且有溢出内容的元素时，上述定义的`getElementPosition()`方法就不能正常工作了，因为它没有把滚动条考虑进去。这里有一个修改版，它从累计的偏移量中减去了滚动条的位置，这样一来，将返回的位置从文档坐标转换为视口坐标。

```js
function getElementPos(elt){
  var x = 0, y = 0;
  //循环以累加偏移量
  for(var e = elt; e != null; e = e.offsetParent){
    x += e.offsetLeft;
    y += e.offsetTop;
  }
  //再次循环所有的祖先元素，减去滚动的偏移量
  //这也减去了主滚动条，并转换为视口坐标
  for(var e = elt.parentNode; e != null && e.nodeType == 1; e = e.parentNode) {
    x -= e.scrollLeft;
    y -= e.scrollTop;
  }
  return {x:x, y:y};
}
```

在现代浏览器中，getElementPos()方法的返回值和`getBoundingClientRect()`的返回值一样（但是更低效）。理论上，如`getElementPos()`这样的函数可以在不支持`getBoundingClientRect()`的浏览器中使用。但实际上，不支持`getBoundingClientRect()`的浏览器在元素位置方面有很多的不兼容性，像这样如此简陋的函数无法可靠地工作。实际类似jQuery这样的客户端类库包含了一些函数来计算元素的位置，它们扩充了这个基本的位置计算算法，修复了一系列浏览器特定的bug。如果需要代码在所有不支持`getBoundingClientRect()`的浏览器中正确计算元素的位置，你很可能需要像jQuery这样的类库。

## 15.9 HTML表单

HTML的`<form>`元素和各种各样的表单输入元素（如`<input>`、`<select>`和`<button>`）在客户端编程中有着重要的地位。这些HTML元素可以追溯到Web的最开始，比JavaScript本身更早。HTML表单就是第一代Web应用程序背后的运作机制，它根本就不需要JavaScript。用户的输入从表单元素来收集；表单将这些输入递交给服务器；服务器处理输入并生成一个新的HTML页面（通常有一个新的表单元素）显示在客户端。

即使当整个表单数据都是由客户端JavaScript来处理并不会提交到服务器时，HTML表单元素仍然是收集用户数据很好的方法。在服务端程序中，表单必须要有一个“提交”按钮，否则它就没有用处。另一方面，在客户端编程中，“提交”按钮不是必须的（虽然它可能仍然有用）。服务端程序是基于表单提交动作的——它们按表单大小的块处理数据——这限制了它们的交互性。客户端程序是基于事件的——它们可以对单独的表单元素上的事件做出响应——这使得它们有更好的响应度。例如，在用户打字时客户端程序就能校验输入的有效性。或者通过单击一个复选框来启用一组选项，也就是说当复选框被选中时那组选项才有意义。

以下小节阐述了用HTML表单如何做到这些事情。表单由HTML元素组成，就像HTML文档的其他部分一样，并且可以用本章中介绍过的DOM技术来操作它们。但是表单是第一批脚本化的元素，在最早的客户端编程中它们还支持比DOM更早的一些其他的API。

请注意，本节是关于脚本化HTML表单，而不是HTML本身。假设你已经对用于定义表单的HTML元素（`<input>`、`<textarea>`、`<select>`等）有一定的了解。尽管如此，表15-1列出了最常使用的表单元素。更详细的内容请参考第四部分中的表单和表单元素API，在Form、Input、Option、Select和TextArea下面。

| HTML元素 | 类型属性 | 事件处理程序 | 描述和事件 |
|---|---|---|---|
| input type="button"或button type="button" | "button" | onclick | 按钮 |
| input type="checkbox" | "checkbox" | onchange | 复选按钮 |
| input type="file" | "file" | onchange | 载入web服务器的文件的文件名输入域；它的value是只读的 |
| input type="hidden" | "hidden" | none | 数据由表单提交，但对用户不可见 |
| option | none | none | Select对象中的单个选项，事件处理程序在select对象上，而非单独的Option对象上 |
| input type="password" | "password" | onchange | 密码输入框，输入的字符不可见 |
| input type="radio" | "radio" | onchange | 单选按钮，只能选一个 |
| input type="reset"或button type="reset" | "reset" | onclick | 重置表单的按钮 |
| select | "select-one" | onchange | 选项只能单选的列表或选项可多选的下拉菜单，另见option |
| select multiple | select-multiple | onchange | 选项可以多选的列表，另见option |
| input type="submit"或button type="sumit" | "submit" | onclick | 表单提交按钮 |
| input type="text" | "text" | onchange | 单行文本输入域；type属性缺少或无法识别时，默认的input元素 |
| textarea | "textarea" | onchange | 多行文本输入域 |


### 15.9.1 选取表单和表单元素

表单和它们所包含的元素可以用如`getElementById()`和`getElementsByTagName()`等标准的方法从文档中来选取：

```js
var fields = document.getElementById("address").getElementsByTagName("input");
```

在支持`querySelectorAll()`的浏览器中，从一个表单中选取所有的单选按钮或所有同名的元素的代码如下：

```js
//id为"shipping"的表单中的单选按钮
document.querySelectorAll('#shipping input[type="radio"]');
//id为"shipping"的表单中所有name为"method"的单选按钮
document.qierySelectorAll('#shipping input[type="radio"][name="method"]')
```

尽管如此，如同在14.7节、15.2.2节和15.2.3节所描述的，有name或id属性的`<form>`元素能够通过很多方法来选取。name="address"属性的`<form>`可以用以下任何方法来选取：

```js
window.address //不可靠，不要使用
document.address //仅当表单有name属性时可用
document.forms.address //仅当方法有name或id的表单
document.forms[n] //不可靠：n是表单的序号
```

15.2.3节阐述了document.forms是一个HTMLCollection对象，可以通过数字序号或id或name来选取表单元素。Form对象本身的行为类似于多个表单元素组成的HTMLCollection集合，也可以通过name或数字序号来索引。如果名为“address”的表单的第一个元素的name是“street”，可以使用以下任何一种表达式来引用该元素：

```js
document.forms.address[0];
document.forms.address.street;
document.address.street //当有name = "address",而不是id="address"
```

如果要明确地选取一个表单元素，可以索引表单对象的elements属性：

```js
document.forms.address.elements[0]
document.forms.address.elements.street
```

一般来说指定文档元素的方法用id属性要比name属性更佳。但是，name属性在HTML表单提交中有特殊的目的，它在表单中较为常用，在其他元素较少使用。它应用于相关的复选按钮组和强制共享name属性值的、互斥的单选按钮组。请记住，当用name来索引一个HTMLCollection对象并且它包含多个元素来共享name时，返回值是一个类数组对象，它包含所有匹配的元素。考虑以下表单，它包含多个单选按钮来选择运输方式：

```js
<form name="shipping">
  <fieldset>
    <legend>shipping method</legend>
    <label><input type="radio" name="method" value="1st">第一次</label>
    <label><input type="radio" name="method" value="2day">第二次</label>
    <label><input type="radio" name="method" value="3rd">第三次</label>
  </fieldset>
</form>
```

对于该表单，用如下代码来引用单选按钮元素数组：

```js
var methods = document.forms.shipping.elements.method;
```

注意，`<form>`元素本身有一个HTML属性和对应的JavaScript属性叫“method”，所以在此案例中，必须要用该表单的elements属性而非直接访问method属性。为了判定用户选取哪种运输方式，需要遍历数组中的表单元素并检测它们的checked属性：

```js
var shipping_method;
for (var i = 0; i < methods.length; i++)
  if (methods[i].checked) shipping_method = method[i].value;
```

在下一节中可以看到更多表单元素的属性，如checked和value。

### 15.9.2 表单和元素的属性

上面描述的`elements[]`数组是Form对象中最有趣的属性。Form对象中的其他属性相对没有如此重要。action、encoding、method和target属性（property）直接对应于`<form>`元素的action、encoding、method和target等HTML属性（attribute）。这些属性都控制了表单是如何来提交数据到Web服务器并如何显示的。客户端JavaScript能够设置这些属性值，不过仅当表单真的会将数据提交到一个服务端程序时它们才有用。

在JavaScript产生之前，要用一个专用的“提交”按钮来提交表单，用一个专用的“重置”按钮来重置各表单元素的值。JavaScript的Form对象支持两个方法：`submit()`和`reset()`，它们完成同样的目的。调用Form对象的`submit()`方法来提交表单，调用`reset()`方法来重置表单元素的值。

所有（或多数）表单元素通常都有以下属性。如果一些元素有其他专用的属性，会在后面单独考虑各种类型的表单元素时描述它们：

- type：标识表单元素类型的只读的字符串。针对用<input>标签定义的表单元素而言，就是其type属性的值。其他表单元素（如<textarea>和<select>）定义type属性是为了轻松地标识它们，与<input>元素在类型检测时互相区别。表15-1的第二列给出了各个表单元素此属性的值。
- form：对包含元素的Form对象的只读引用，或者如果元素没有包含在一个`<form>`元素中则其值为null。
- name：只读的字符串，由HTML属性name指定。
- value：可读/写的字符串，指定了表单元素包含或代表的“值”。它就是当提交表单时发送到Web服务器的字符串，也是JavaScript程序有时候会感兴趣的内容。针对Text和Textarea元素，该属性值包含了用户输入的文本。针对用<input>标签创建的按钮元素（除了用<button>标签创建的按钮），该属性值指定了按钮显示的文本。但是，针对单选和复选按钮元素，该属性用户不可见也不能编辑。它仅是用HTML的value属性来设置的一个字符串。它在表单提交时使用，但在关联表单元素的额外数据时也很有用。在本章后面关于不同类目的表单元素小节中将深入讨论value属性。

### 15.9.3 表单和元素的事件处理程序

每个Form元素都有一个onsubmit事件处理程序来侦测表单提交，还有一个onreset事件处理程序来侦测表单重置。表单提交前调用onsubmit程序；它通过返回false能够取消提交动作。这给JavaScript程序一个机会来检查用户的输入错误，目的是为了避免不完整或无效的数据通过网络提交到服务端程序。注意，onsubmit事件处理程序只能通过单击“提交”按钮来触发。直接调用表单的`submit()`方法不触发onsubmit事件处理程序。

onreset事件处理程序和onsubmit是类似的。它在表单重置之前调用，通过返回false能够阻止表单元素被重置。在表单中很少需要“重置”按钮，但如果有，你可能需要提醒用户来确认是否重置：

```
<form...
    onreset="return confirm('Really erase ALL input and start over?')">
  ...
  <button type="reset">Clear and Start Over</button>
</form>
```

类似onsubmit事件处理程序，onreset只能通过单击“重置”按钮来触发。直接调用表单的`reset()`方法不触发onreset事件处理程序。

当用户与表单元素交互时它们往往会触发click或change事件，通过定义onclick或onchange事件处理程序可以处理这些事件。表15-1的第三列给出了各个表单元素主要的事件处理程序。一般来说，当按钮表单元素激活（甚至当通过键盘而不是实际的鼠标单击发生激活）时它们会触发click事件。当用户改变其他表单元素所代表的值时它们会触发change事件。当用户在一个文本域输入文本或从下拉列表中选择了一个选项后就发生这样的改变。注意，在一个文本域中该事件不是每次用户输入一个键值时都会触发。它仅当用户改变了元素的值然后将焦点移到其他元素上时才会触发。也就是说，调用该事件处理程序就意味着一个完整的改变。单选按钮和复选框都有一个状态标识，它们的click和change事件都会触发；两个之中change事件更加有用。

表单元素在收到键盘的焦点时也会触发focus事件，失去焦点时会触发blur事件。

关于事件处理程序有一点非常重要，在事件处理程序代码中关键字this是触发该事件的文档元素的一个引用（我们将在第17章中再次讨论）。既然在`<form>`元素中的元素都有一个form属性引用了该包含的表单，这些元素的事件处理程序总是能够通过this.form来得到Form对象的引用。更进一步，这意味着某个表单元素的事件处理程序能够通过`this.form.x`得到该表单中以x命名的元素。

### 15.9.4 按钮

按钮是最常用的表单元素之一，因为它们是一种视觉上明确让用户触发某种脚本动作的方法。按钮元素本身没有默认的行为，除非它有onclick事件处理程序，否则它并没有什么用处。以`<input>`元素定义的按钮会将value属性值以纯文本显示。以`<button>`元素定义的按钮会将元素的一切内容显示出来。

注意，超级链接与按钮一样提供了onclick事件处理程序。当onclick事件所触发的动作可以概念化为“跟随此链接”时就用一个链接；否则，用按钮。

提交和重置元素本就是按钮，不同的是它们有与之相关联的默认动作（表单的提交和重置）。如果onclick事件处理程序返回false，这些按钮的默认动作就不再执行了。可以使用提交元素的onclick事件处理程序来执行表单校验，但是更为常用的是使用Form对象本身的onsubmit事件处理程序来执行表单校验。

本书第四部分未包含按钮。关于所有按钮表单元素的详细内容请参看input项，它包含了用`<button>`元素创建的按钮。

### 15.9.5 开关按钮

复选框和单选元素是开关按钮，或称有两种视觉状态的按钮：选中或未选中。通过对其单击用户可以改变它的开关状态。单选元素为整组有相关性的元素而设计的，组内所有按钮的HTML属性name的值都相同。按这种方式创建的单选按钮是互斥的：选中其一，之前选中的即变成未选中。复选框通常也整组使用并共享name属性，必须注意的是当利用做为表单属性的名字来选中这些元素时，它返回一个类数组对象而不是单个元素。

单选和复选框元素都定义了checked属性。该属性是可读/写的布尔值，它指定了元素当前是否选中。defaultChecked属性也是布尔值，它是HTML属性checked的值；它指定了元素在第一次加载页面时是否选中。

单选和复选框元素本身不显示任何文本，它们通常和相邻的HTML文本一起显示（或与`<label>`元素相关联）。这意味着设置复选框或单选元素的value属性不改变元素的视觉表现。设置value只改变提交表单时发送到Web服务器的字符串。

当用户单击单选或复选开关按钮，单选或复选框元素触发onclick事件。如果由于单击开关按钮改变了它的状态，它也触发onchange事件。（但注意，当用户单击其他单选按钮而导致这个单选按钮状态的改变，后者不触发onchange事件。）

### 15.9.6 文本域

文本输入域在HTML表单和JavaScript程序中可能是最常用的元素。用户可以输入单行简短的文本字符串。value属性表示用户输入的文本。通过设置该属性值可以显式地指定应该在输入域中显示的文本。

在HTML5中，placeholder属性指定了用户输入前在输入域中显示的提示信息：

```html
Arrival Date: <input type="text" name="arrival" placeholder="yyyy-mm-dd">
```

文本输入域的onchange事件处理程序是在用户输入新的文本或编辑已存在的文本时触发，它表明用户完成了编辑并将焦点移出了文本域。

Textarea元素类似文本输入域元素，不同的是它允许用户输入（和JavaScript程序显示）多行文本。Textarea元素用`<textarea>`标签来创建，与用`<input>`标签创建的文本域在语法上有显著的区别。（见第四部分的TextArea。）尽管如此，两种元素的行为非常类似。如同针对Text元素一样，可以用Textarea元素的value属性和onchange事件处理程序。

`<input type="password">`元素在用户输入时显示为星号，它修改了输入的文本。其名字表明，用户输入密码时不用担心他背后的人能看到，这很有用。注意，密码输入元素只能防止眼睛窥视，但在提交表单时输入未经任何加密（除非通过安全的HTTPS连接提交它），当在网络上传输时它可能被看见。

最后，`<input type="file">`元素将用户输入待上传到Web服务器的文件的名称。它由一个文本域和一个单击打开文件选择对话框的按钮所组成。该文件选取元素拥有onchange事件处理程序，就像普通的输入域一样。但不同的是它的value属性是只读的。这个防止恶意的JavaScript程序欺骗用户上传本意不想共享的文件。

不同的文本输入元素定义onkeypress、onkeydown和onkeyup事件处理程序。可以从onkeypress或onkeydown事件处理程序返回false，防止记录用户的按键。这很有用，例如，如果希望强制用户在特定文本输入域中仅输入数字。该技术的说明参见例17-6。

### 15.9.7 选择框和选项元素

Select元素表示用户可以做出选择的一组选项（用Option元素表示）。浏览器通常将其渲染为下拉菜单的形式，但当指定其size属性值大于1时，它将显示为列表中的选项（可能有滚动）。Select元素能以两种不同的方式运作，这取决于它的type属性值是如何设置的。如果`<select>`元素有multiple属性，也就是Select对象的type属性值为“select-multiple”，那就允许用户选取多个选项。否则，如果没有多选属性，那只能选取单个选项，它的type属性值为“select-one”。

某种程度上“select-multiple”元素与一组复选框元素类似，“select-one”元素和一组单选元素类似。但是，由Select元素显示的选项并不是开关按钮：它们由`<option>`元素定义。Select元素定义了options属性，它是一个包含了多个Option元素的类数组对象。

当用户选取或取消选取一个选项时，Select元素触发onchange事件处理程序。针对“select-one”Select元素，它的可读/写属性selectedIndex指定了哪个选项当前被选中。针对“select-multiple”元素，单个selectedIndex属性不足以表示被选中的一组选项。在这种情况下，要判定哪些选项被选中，就必须遍历`options[]`数组的元素，并检测每个Option对象的selected属性值。

除了其selected属性，每个Option对象有一个text属性，它指定了在Select元素中的选项所显示的纯文本字符串。设置该属性可以改变显示给用户的文本。value属性指定了在提交表单时发送到Web服务器的文本字符串，它也是可读/写的。甚至在写纯客户端程序并且不可能有表单提交时，value属性（或它所对应的HTML属性value）是用来保存任何数据的好地方，在用户选取特定的选项时可以使用这些数据。注意，Option元素并没有与表单相关的事件处理程序：用包含Select元素的onchange事件处理程序来代替。

除了设置Option对象的text属性以外，使用options属性的特殊功能可以动态改变显示在Select元素中的选项，这些功能可以追溯到最早期的客户端编程。通过设置options. length为一个希望的值可以截断Option元素数组，而设置options.length为0可以从Select元素中移除所有的选项。设置`options[]`数组中某点的值为null可以从Select元素中移除单个Option对象。这将删除该Option对象，`options[]`数组中高端的元素自动移下来填补空缺。

为Select元素增加一个新的选项，首先用`Option()`构造函数创建一个Option对象，然后将其添加到`options[]`属性中，代码如下：

```js
//创建一个新的属性
var zaire = new Option("Zaire", // text属性
  "zaire", //value属性
  false, //defaultSelected属性
  false); //selected属性
//通过添加到options数组中，在Select元素中现在改选项
var countries = document.address.country;//得到Select对象
countries.options[countries.options.length] = zaire;
```

请牢记一点，这些专用的Select元素的API已经很老了。可以用那些标准的调用更明确地插入和移除选项元素：Document.`createElement()`、Node.`insertBefore()`、Node. `removeChild()`等。

## 15.10 其它文档特性

本章在一开始就声明了它是本书中最重要的一章。由其必要性，它也是最长的一章之一。本章最后一节涵盖了Document对象的若干混杂的特性。

### 15.10.1 Document的属性

本章已经介绍的Document的属性有body、documentElement和forms等这些特殊的文档元素。文档还定义了一些其他有趣的属性：

- cookie：允许JavaScript程序读、写HTTP cookie的特殊的属性。第20章涵盖该属性。
- domain：该属性允许当Web页面之间交互时，相同域名下互相信任的Web服务器之间协作放宽同源策略安全限制（见13.6.2节）。
- lastModified：包含文档修改时间的字符串。
- location：与Window对象的location属性引用同一个Location对象。
- referrer：如果有，它表示浏览器导航到当前链接的上一个文档。该属性值和HTTP的Referer头信息的内容相同，只是拼写上有两个r。
- title：文档的`<title>`和`</title>`标签之间的内容。
- URL：文档的URL，只读字符串而不是Location对象。该属性值与location.href的初始值相同，只是不包含Location对象的动态变化。例如，如果用户在文档中导向到一个新的片段，location.href会发生变化，但是document.URL则不会。

referrer是这些属性中最有趣的属性之一：它包含用户链接到当前文档的上一个文档的URL。可以用如下代码来使用该属性：

```js
if (document.referrer.indexOf("http://www.google.com/search?") == 0) {
  var args = document.referrer.substring(ref.indexOf("?") + 1).split("&");
  for (var i = 0; i < args.length; i++) {
    if (args[i].substring(0, 2) == "q=") {
      document.write("<p>welcome google User.");
      document.write("You searched for:" + unescape(args[i].substring(2)).replace('+', ''))
        break;
    }
  }
}
```

上述代码中使用的`document.write()`方法将是下一节的主题。

### 15.10.2 document.write()方法

`document.write()`方法是其中一个由Netscape 2浏览器实现的非常早期的脚本化API。它曾在DOM之前就被很好地引入了，也曾是在文档中显示计算后的文本的唯一方法。新代码中已经不再需要它了，但在已有的代码中你还能不时地看到该方法。

`document.write()`会将其字符串参数连接起来，然后将结果字符串插入到文档中调用它的脚本元素的位置。当脚本执行结束，浏览器解析生成的输出并显示它。例如，以下代码使用`write()`动态把信息输出到一个静态的HTML文档中：

```js
<script>
  document.write("<p>Document title:" + document.title);
  document.write("<br>URL:" + document.URL);
  document.write("<br>Referred by:" + document.referrer);
  document.write("<br>Modified on:" + document.lastModified);
  document.write("<br>Accessed on:" + new Date());
</script>
```

只有在解析文档时才能使用`write()`方法输出HTML到当前文档中，理解这点非常重要。也就是说能够在`<script>`元素中的顶层代码中调用`document.write()`，就是因为这些脚本的执行是文档解析流程的一部分。如果将`document.write()`放在一个函数的定义中，而该函数的调用是从一个事件处理程序中发起的，产生的结果未必是你想要的——事实上，它会擦除当前文档和它包含的脚本！（马上你将看到为什么。）同理，在设置了defer或async属性的脚本中不要使用`document.write()`。

第13章中的例13-3以这种方式使用了`document.write()`来产生更加复杂的输出。

还可以使用`write()`方法在其他的窗口或框架页中来创建整个全新文档。（但是，当有多个窗口或框架页时，必须注意不要违反同源策略。）第一次调用其他文档的`write()`方法即会擦除该文档的所有内容。可以多次调用`write()`来逐步建立新文档的内容。传递给`write()`的内容可能缓存起来（并且不会显示）直到调用文档对象的`close()`方法来结束该写序列。本质上这告诉HTML解析器文档已经达到了文件的末尾，应该结束解析并显示新文档。

值得一提的是Document对象还支持`writeln()`方法，除了在其参数的输出之后追加一个换行符以外它和`write()`方法完全一样。例如，在`<pre>`元素内输出预格式化的文本时这非常有用。

在当今的代码中document.`write()`方法并不常用：innerHTML属性和其他DOM技术提供了更好的方法来为文档增加内容。另一方面，某些算法的确使得它们本身成为很好的流式I/O API，如同`write()`方法提供的API一样。如果你正在书写在运行时计算和输出文本的代码，可能会对例15-10感兴趣，它利用指定元素的innerHTML属性包装了简单的`write()`和`close()`方法。

```js
/*征对innerHTML属性的流式API*/
//设置元素的innerHTML定义简单的“流式”API
function ElementStream(elt) {
  if (typeof elt === "string")
    elt = document.getElementById(elt);
  this.elt = elt;
  this.buffer = "";
}
//连接所有的参数，添加到缓存中
ElementStream.prototype.wirte = function() {
  this.buffer += Array.prototype.join.call(arguments, "");
};
//类似write(),只是添加了换行符
ElementStream.prototype.writeln = function() {
  this.buffer += Array.prototype.join.call(arguments, "") + "\n";
};
//从缓存中设置元素的内容，然后清空缓存
ElementStream.prototype.close = function() {
  this.elt.innerHTML = this.buffer;
  this.buffer = "";
};
```

### 15.10.3 查询选取的文本

有时判定用户在文档中选取了哪些文本非常有用。可以用类似如下的函数达到目的：

```js
function getSelectedText() {
  if (window.getSelection) //HTML5标准API
    return window.getSelection().toString();
  else if (document.selection) //IE独有技术
    return document.selection.createRange().text;
}
```

标准的`window.getSelection()`方法返回一个Selection对象，后者描述了当前选取的一系列一个或多个Range对象。Selection和Range定义了一个不太常用的较为复杂的API，本书中并没有文档记录。toString()方法是Selection对象中最重要的也广泛实现了（除了IE）的特性，它返回选取的纯文本内容。

IE定义了一个不同的API，它在本书中也没有文档记录。document.selection对象代表了用户的选择。该对象的createRange()方法返回IE特有的TextRange对象，它的text属性包含了选取的文本。

如上的代码在书签工具（见13.2.5节）中特别有用，它操作选取的文本，然后利用搜索引擎或参考站点查找某个单词。例如，如下HTML链接在Wikipedia上查找当前选取的文本。收藏书签后，该链接和它包含的JavaScript URL就变成了一个书签工具：

```js
<a href="javascript: var q;
    if (window.getSelection) q = window.getSelection().toString();
    else if (document.selection) q = document.selection.createRange().text;
    void window.open('https://www.baidu.com/s?wd=' + q)">
  选取后点击链接查找
  </a>
```

上述展示的查询选取代码的兼容性不佳：Window对象的getSelection()方法无法返回那些表单元素`<input>`或`<textarea>`内部选中的文本，它只返回在文档主体本身中选取的文本。另一方面，IE的document.selection属性可以返回文档中任意地方选取的文本。

从文本输入域或`<textarea>`元素中获取选取的文本可使用以下代码：

```js
elt.value.substring(elt.selectionStart,elt.selectionEnd);
```

IE8以及更早版本的浏览器不支持selectionStart和selectionEnd属性。

### 15.10.4 可编辑的内容

我们已经知道HTML表单元素包含了文本字段和文本域元素，用户可以输入并编辑纯文本。跟随IE的脚步，所有当今的Web浏览器也支持简单的HTML编辑功能：你也许已经看到过这在页面上使用了（如博客评论页），它嵌入了一个富文本编辑器，包含了一个有一系列按钮的工具栏来设置排版样式（粗体、斜体）、对齐和插入图片与链接。

有两种方法来启用编辑功能。其一，设置任何标签的HTMLcontenteditable属性；其二，设置对应元素的JavaScript contenteditable属性；这都将使得元素的内容变成可编辑。当用户单击该元素的内容时就会出现插入光标，用户敲击键盘就可以插入其中。如以下代码，一个HTML元素创建了一个可编辑的区域：

```js
<div id="editor" contenteditable>
click to edit
</div>
```

浏览器可能为表单字段和contenteditable元素支持自动拼写检查。在支持该功能的浏览器中，检查可能默认开启或关闭。为元素添加spellcheck属性来显式开启拼写检查，而使用spellcheck=false来显式关闭该功能（例如，当一个`<textarea>`将显示源代码或其他内容包含了字典里找不到的标识符时）。

将Document对象的designMode属性设置为字符串“on”使得整个文档可编辑。（设置为“off”将恢复为只读文档。）designMode属性并没有对应的HTML属性。如下代码使得`<iframe>`内部的文档可编辑（注意，这里用了例13-5中的`onLoad()`函数）：

```js
<iframe id="editor" src="about:blank"></iframe> // 空iframe
<script>
onload = function() {
  var editor = document.getElementById("editor");
  editor.contentDocument.designMode = "on"; //开启编辑
}
</script>
```

所有当今的浏览器都支持contenteditable和designMode属性。但是，当谈到它们实际的可编辑行为时，它们是不太兼容的。所有的浏览器都允许插入与删除文本并用鼠标与键盘移动光标。在所有的浏览器中，Enter键另起一行，但不同的浏览器生成了不同的标记。有些开始了新的段落，而其他的只是插入一个`<br/>`元素。

有些浏览器允许键盘快捷键（如Ctrl+B）来加粗当前选中的文本。在其他浏览器（如Firefox）中，标准的字处理快捷键（如Ctrl+B和Ctrl+I）被绑定到浏览器相关的其他功能上了而无法应用到文本编辑器上。浏览器定义了多项文本编辑命令，大部分没有键盘快捷键。为了执行这些命令，应该使用Document对象的`execCommand()`方法。（注意，这是Document的方法，而不是设置了contenteditable属性的元素的方法。如果文档中有多个可编辑的元素，命令将自动应用到选区或插入光标所在那个元素上。）用`execCommand()`执行的命令名字都是如“bold”、“subscript”、“justifycenter”或“insertimage”之类的字符串。命令名是`execCommand()`的第一个参数。有些命令还需要一个值参数——例如，“createlink”需要一个超级链接URL。理论上，如果`execCommand()`的第二个参数为true，浏览器会自动提示用户输入所需值。但为了提高可移植性，你应该提示用户输入，并传递false作为第二参数，传递用户输入的值作为第三个参数。

```js
function bold() {
  document.execCommand("blod", false, url);
}

function link() {
  var url = prompt("输入link描述");
  if (url) document.execCommand("createlink", false, url)
}
```

`execCommand()`所支持的命令通常是由工具栏上的按钮触发的。当要触发的命令不可用时，良好的UI会使对应的按钮无效。可以给`document.queryCommandSupport()`传递命令名来查询浏览器是否支持该命令。调用`document.queryCommandEnabled()`来查询当前所使用的命令。（例如，一条需要文本选择区域的命令在无选区的情况下有可能是无效的。）有一些命令如“bold”和“italic”有一个布尔值状态，开或关取决于当前选区或光标的位置。这些命令通常用工具栏上的开关按钮表示。要判定这些命令的当前状态可以使用`document.queryCommandState()`。最后，有些命令（如“fontname”）有一个相关联的值（字体系列名）。用`document.queryCommandValue()`查询该值。如果当前选取的文本使用了两种不同的字体，“fontname”的查询结果是不确定的。使用`document. queryCommandIndeterm()`来检测这种情况。

不同的浏览器实现了不同的编辑命令组合。只有一少部分命令得到了很好的支持，如“bold”、“italic”、“createlink”、“undo”和“redo”等。在写本书这段时间里HTML5草案定义了以下命令。但由于它们并没有被普遍地支持，这里就不做详细的文档记录：

| blod          | insertLineBreak     | slectAll    |
|:--------------|:--------------------|:------------|
| createLink    | insertOrderedList   | subscript   |
| delete        | insertUnorderedList | superscript |
| formatBlock   | insertParagraph     | undo        |
| forwardDelete | insertText          | unlink      |
| insertImage   | italic              | unselect    |
| insertHTML    | redo                |             |


如果Web应用程序需要富文本编辑器功能，很可能需要采纳一个预先构建的解决浏览器之间的各种差异的解决方案。在网上可以找到很多这样的编辑器组件。值得注意的是，浏览器内置的编辑功能对用户输入少量的富文本来说是足够强大了，但要解决所有种类的文档的编辑来说还是过于简陋了。特别要注意，这些编辑器生成的HTML标记很可能是杂乱无章的。

一旦用户编辑了某元素的内容，该元素设置了conteneditable属性，就可以使用innerHTML属性得到已编辑内容的HTML标记。如何处理该富文本由你自己决定。可以把它存储在隐藏的表单字段中，并通过提交该表单把它发送到服务器。可以使用第18章描述的技术直接把已编辑文本发送到服务器。或者使用第20章的技术在本地保存用户的编辑文本。

# 第16章 脚本化CSS
# 第17章 事件处理

客户端 JavaScript 程序采用了异步事件驱动编程模型（13.3.2节有介绍）。在这种程序设计风格下，当文档、浏览器、元素或与之相关的对象发生某些有趣的事情时，Web浏览器就会产生事件（event）。例如，当Web浏览器加载完文档、用户把鼠标指针移到超链接上或敲击键盘时，Web浏览器都会产生事件。如果 JavaScript 应用程序关注特定类型的事件，那么它可以注册当这类事件发生时要调用的一个或多个函数。请注意，这种风格并不只应用于 Web 编程，所有使用图形用户界面的应用程序都采用了它，它们静待某些事情发生（即，它们等待事件发生），然后它们响应。

请注意，事件本身并不是一个需要定义的技术名词。简而言之，事件就是 Web 浏览器通知应用程序发生了什么事情。事件不是 JavaScript 对象，不会出现在程序源代码中。当然，会有一些事件相关的对象出现在源代码中，它们需要技术说明，因此，本章从一些重要的定义开始。

事件类型（event type）是一个用来说明发生什么类型事件的字符串。例如，“mousemove”表示用户移动鼠标，“keydown”表示键盘上某个键被按下，而“load”表示文档（或某个其他资源）从网络上加载完毕。由于事件类型只是一个字符串，因此实际上有时会称之为事件名字（eventname），我们用这个名字来标识所谈论的特定类型的事件。现代浏览器支持许多事件类型，17.1节会有一个概述。

事件目标（event target）是发生的事件或与之相关的对象。当讲事件时，我们必须同时指明类型和目标。例如， window 上的 load 事件或`<button>`元素的 click 事件。在客户端的 JavaScript 应用程序中， Window 、 Document 和 Element 对象是最常见的事件目标，但某些事件是由其他类型的对象触发。例如，第18章会介绍由 XMLHttpRequest 对象触发的 readystatechange 事件。

事件处理程序（event handler）或事件监听程序（event listener）是处理或响应事件的函数。应用程序通过指明事件类型和事件目标，在 Web 浏览器中注册它们的事件处理程序函数。当在特定的目标上发生特定类型的事件时，浏览器会调用对应的处理程序。当对象上注册的事件处理程序被调用时，我们有时会说浏览器“触发”（fire、trigger）和“派发”（dispatch）了事件。有很多注册事件处理程序的方法，17.2节和17.3节会详细说明处理程序的注册和调用。

事件对象（event object）是与特定事件相关且包含有关该事件详细信息的对象。事件对象作为参数传递给事件处理程序函数（不包括IE8及之前版本，在这些浏览器中有时仅能通过全局变量 event 才能得到）。所有的事件对象都有用来指定事件类型的 type 属性和指定事件目标的 target 属性。（在IE8及之前版本中用 srcElement 而非 target 。）每个事件类型都为其相关事件对象定义一组属性。例如，鼠标事件的相关对象会包含鼠标指针的坐标，而键盘事件的相关对象会包含按下的键和辅助键的详细信息。许多事件类型仅定义了像type和target这样少量的标准属性，就无法获取许多其他有用的信息。对于这些事件而言，只是事件简单地发生，无法得到事件的详细信息。本章没有专门的小节来介绍Event对象，而是在介绍特定事件类型时会说明事件对象的属性。在第四部分描述特定事件类型时会解释事件对象的属性。

事件传播（event propagation）是浏览器决定哪个对象触发其事件处理程序的过程。对于单个对象的特定事件（比如 Window 对象的 load 事件），必须是不能传播的。当文档元素上发生某个类型的事件时，然而，它们会在文档树上向上传播或“冒泡”（bubble）。如果用户移动鼠标指针到超链接上，在定义这个链接的`<a>`元素上首先会触发 mousemove 事件，然后是在容器元素上触发这个事件，也许是`<p>`元素、`<div>`元素或 Document 对象本身。有时，在Document或其他容器元素上注册单个事件处理程序比在每个独立的目标元素上都注册处理程序要更方便。事件处理程序能通过调用方法或设置事件对象属性来阻止事件传播，这样它就能停止冒泡且将无法在容器元素上触发处理程序。17.3.6节会详细介绍事件传播。

事件传播的另外一种形式称为事件捕获（eventcapturing），在容器元素上注册的特定处理程序有机会在事件传播到真实目标之前拦截（或“捕获”）它。IE 8及之前版本不支持事件捕获，所以不常用它。但是，当处理鼠标拖放事件时，捕获或“夺取”鼠标事件的能力是必需的，例17-2会展示如何实现这种能力。

一些事件有与之相关的默认操作。例如，当超链接上发生 click 事件时，浏览器的默认操作是按照链接加载新页面。事件处理程序可以通过返回一个适当的值、调用事件对象的某个方法或设置事件对象的某个属性来阻止默认操作的发生。这有时称为“取消”事件，17.3.6节会介绍它。

有了这些定义好的术语，现在我们能继续深入学习事件和事件处理。17.1节会概述浏览器支持的许多事件类型。它没有介绍任何单个事件的详细信息，而是告诉大家 Web 应用中有哪些事件类型可以使用。这一节交叉引用了本书的其他部分内容，用于演示一些事件实战。

在17.1节之后，接着两节会介绍如何注册事件处理程序和浏览器如何调用这些事件处理程序。由于 JavaScript 事件模型的历史演变和IE 9之前版本缺乏对标准的支持，因此这两个主题可能会超出想象的复杂。

本章后面会演示特定事件类型如何工作的示例，这些特定事件类型包括：

- 文档加载和准备就绪事件
- 鼠标事件
- 鼠标滚轮事件
- 拖放事件
- 键盘事件
- 文本输入事件

## 17.1 事件类型

在 Web 初期，客户端程序员只能使用少部分事件，比如“load”、“click”和“mouseover”等。这些传统事件类型在所有浏览器中都得到了很好的支持，17.1.1节主要介绍这些内容。随着 Web 平台发展到包括更强大的API，事件集合随之越来越大，没有单个标准能定义完整的事件集合。在写本章时，浏览器所支持的事件数量正在快速地增长，这些新事件有3个来源：

- 3 级 DOM 事件（DOM Level 3 Events）规范，经过长期的停滞之后，在W3C的主持下又开始焕发生机。17.1.2节介绍 DOM 事件。
- HTML5 规范及相关衍生规范的大量新API定义了新事件，比如历史管理、拖放、跨文档通信，以及视频和音频的播放。17.1.3节会概述这些事件。
- 基于触摸和支持 JavaScript 的移动设备的出现，比如iPhone，它们需要定义新的触摸和手势事件类型。在17.1.4节会看到一些针对Apple产品的例子。

注意，许多新事件类型尚未广泛实现，定义它们的标准也依旧处于草案阶段。接下来的几节将概述这些事件，但不会列出详细信息。本章剩下的部分将全面涵盖事件处理模型，及大量已经得到良好支持的事件应用示例。如果大概理解了事件的工作原理，那么就能轻松地处理作为新 Web API 定义和实现的新事件类型。

**事件分类**

事件大致可以分成几类，了解这些分类将有助于理解和组织如下长长的事件列表：

1. 依赖于设备的输入事件。  
有些事件和特定输入设备直接相关，比如鼠标和键盘。包括诸如“mousedown”、“mousemove”、“mouseup”、“keydown”、“keypress”和“keyup”这样的传统事件类型，也包括像“touchmove”和“gesturechange”这样新的触摸事件类型。

2. 独立于设备的输入事件。  
有些输入事件没有直接相关的特定输入设备。例如，click事件表示激活了链接、按钮或其他文档元素，这通常是通过鼠标单击实现，但也能通过键盘或触摸感知设备上的手势来实现。尚未广泛实现的textinput事件就是一个独立于设备的输入事件，它既能取代按键事件并支持键盘输入，也可以取代剪切和粘贴与手写识别的事件。

3. 用户界面事件。  
用户界面事件是较高级的事件，通常出现在定义 Web 应用用户界面的HTML表单元素上。包括文本输入域获取键盘焦点的focus事件、用户改变表单元素显示值的change事件和用户单击表单中的“提交”按钮的submit事件。

4. 状态变化事件。  
有些事件不是由用户活动而是由网络或浏览器活动触发，用来表示某种生命周期或相关状态的变化。当文档完全加载时，在Window对象上会发生load事件，这可能是这类事件中最常用的。在13.3.4节讨论过的DOMContentLoaded事件与此类似。HTML5历史管理机制会（见22.2节）触发popstate事件来响应浏览器的后退按钮。HTML5离线Web应用API（见20.4节）包括online和offline事件。第18章将展示当向服务器请求的数据准备就绪时，如何利用readystatechange事件得到通知。类似地，用于读取用户选择本地文件的新API（见22.6.5节）使用像“loadstart”、“progress”和“loadend”事件来实现I/O过程的异步通知。

5. 特定API事件。  
HTML5及相关规范定义的大量Web API都有自己的事件类型。拖放API（见17.7节）定义了诸如“dragstart”、“dragenter”、“dragover”和“drop”事件，应用程序想自定义拖放源（drag source）或拖放目标（drop target）就必须处理这些相关事件。HTML5的`<video>`和`<audio>`元素（见21.2节）定义一长串像“waiting”、“playing”、“seeking”和“volumechange”等相关事件，这些事件通常仅用于Web应用，这些Web应用希望为视频和音频的播放定义自定义控件。

6. 计时器和错误处理程序。  
已经在第14章介绍过的计时器（timer）和错误处理程序（error handler）属于客户端 JavaScript 异步编程模型的部分，并有相似的事件。虽然本章不会讨论计时器和错误处理程序，但思考它们同事件处理之间的关系是有益的，所以在本章的语境中重读14.1节和14.6节会发现很有趣。

### 17.1.1 传统事件类型

处理鼠标、键盘、 HTML 表单和 Window 对象的事件都是 Web 应用中最常用的，它们已经存在很长的时间并得到了广泛的支持。接下来会说明这类事件的许多重要详细信息。

**1.表单事件**

回到Web和 JavaScript 的早期，表单和超链接都是网页中最早支持脚本的元素。这就意味着表单事件是所有事件类型中最稳定且得到良好支持的那部分。当提交表单和重置表单时，`<form>`元素会分别触发 submit 和 reset 事件。当用户和类按钮表单元素（包括单选按钮和复选框）交互时，它们会发生click事件。当用户通过输入文字、选择选项或选择复选框来改变相应表单元素的状态时，这些通常维护某种状态的表单元素会触发change事件。对于文本输入域，只有用户和表单元素完成交互并通过 Tab 键或单击的方式移动焦点到其他元素上时才会触发change事件。响应通过键盘改变焦点的表单元素在得到和失去焦点时会分别触发focus和blur事件。

15.9.3节涵盖了所有表单相关事件的详细信息。不过，这里还有一些进一步说明。

通过事件处理程序能取消submit和reset事件的默认操作，某些click事件也是如此。focus和blur事件不会冒泡，但其他所有表单事件都可以。IE定义了focusin和focusout事件可以冒泡，它们可以用于替代foucs和blur事件。jQuery库（见第19章）为不支持 focusin 和 focusout 事件的浏览器模拟了这两个事件，同时3级DOM事件规范也正在标准化它们。

最后注意，无论用户何时输入文字（通过键盘或剪切和粘贴）到`<textarea>`和其他文本输入表单元素，除IE外的浏览器都会触发input事件。不像 change 事件，每次文字插入都会触发 input 事件。遗憾的是， input 事件的事件对象没有指定输入文本的内容。（稍后介绍的 textinput 事件将会成为这个事件的有用替代方案。）

**2.Window事件**

Window 事件是指事件的发生与浏览器窗口本身而非窗口中显示的任何特定文档内容相关。但是，这些事件中有一些会和文档元素上发生的事件同名。

load 事件是这些事件中最重要的一个，当文档和其所有外部资源（比如图片）完全加载并显示给用户时就会触发它。有关 load 事件的讨论贯穿整个第13章。DOMContentLoaded和readystatechange是load事件的替代方案，当文档和其元素为操作准备就绪，但外部资源完全加载完毕之前，浏览器就会尽早触发它们。17.4节有这些与文件加载相关事件的示例。

unload 事件和 load 相对，当用户离开当前文档转向其他文档时会触发它。unload事件处理程序可以用于保存用户的状态，但它不能用于取消用户转向其他地方。beforeunload事件和unload类似，但它能提供询问用户是否确定离开当前页面的机会。如果beforeunload的处理程序返回字符串，那么在新页面加载之前，字符串会出现在展示给用户确认的对话框上，这样用户将有机会取消其跳转而留在当前页上。

Window 对象的 onerror 属性有点像事件处理程序，当 JavaScript 出错时会触发它。但是，它不是真正的事件处理程序，因为它能用不同的参数来调用。更多详细信息请看14.6节。

像`<img>`元素这样的单个文档元素也能为load和error事件注册处理程序。当外部资源（例如图片）完全加载或发生阻止加载的错误时就会触发它们。某些浏览器也支持abort事件（HTML5将其标准化），当图片（或其他网络资源）因为用户停止加载进程而导致失败就会触发它。

前面介绍的表单元素的focus和blur事件也能用做Window事件，当浏览器窗口从操作系统中得到或失去键盘焦点时会触发它们。

最后，当用户调整浏览器窗口大小或滚动它时会触发resize和scroll事件。scroll事件也能在任何可以滚动的文档元素上触发，比如那些设置CSS的overflow属性（见16.2.6节）的元素。传递给resize和scroll事件处理程序的事件对象是一个非常普通的Event对象，它没有指定调整大小或发生滚动的详细信息属性，但可以通过15.8节介绍的技术来确定新窗口的尺寸和滚动条的位置。

**3.鼠标事件**

当用户在文档上移动或单击鼠标时都会产生鼠标事件。这些事件在鼠标指针所对应的最深嵌套元素上触发，但它们会冒泡直到文档最顶层。传递给鼠标事件处理程序的事件对象有属性集，它们描述了当事件发生时鼠标的位置和按键状态，也指明当时是否有任何辅助键按下。 clientX 和 clientY 属性指定了鼠标在窗口坐标中的位置，button和which属性指定了按下的鼠标键是哪个。（无论如何请看Event参考页，因为这些属性难以简单使用。）当键盘辅助键按下时，对应的属性 altkey 、 ctrlKey 、 metaKey 和 shiftKey 会设置为 true。 而对于click事件，detail属性指定了其是单击、双击还是三击。

用户每次移动或拖动鼠标时，会触发 mousemove 事件。这些事件的发生非常频繁，所以 mousemove 事件处理程序一定不能触发计算密集型任务。当用户按下或释放鼠标按键时，会触发mousedown和mouseup事件。通过注册mousedown和 mousemove 事件处理程序，可以探测和响应鼠标的拖动。合理地这样做能够捕获鼠标事件，甚至当鼠标从开始元素移出时我们都能持续地接受到 mousemove 事件。17.5节包含一个处理拖动的示例。

在 mousedown 和 mouseup 事件队列之后，浏览器也会触发click事件。之前介绍过click事件是独立于设备的表单事件，但实际上它不仅仅在表单元素上触发，它可以在任何文档元素上触发，同时传递拥有之前介绍的所有鼠标相关额外字段的事件对象。如果用户在相当短的时间内连续两次单击鼠标按键，跟在第二个click事件之后是dblclick事件。当单击鼠标右键时，浏览器通常会显示上下文菜单（context menu）。在显示菜单之前，它们通常会触发contextmenu事件，而取消这个事件就可以阻止菜单的显示。这个事件也是获得鼠标右击通知的简单方法。

当用户移动鼠标指针从而使它悬停到新元素上时，浏览器就会在该元素上触发mouseover事件。当鼠标移动指针从而使它不再悬停在某个元素上时，浏览器就会在该元素上触发mouseout事件。对于这些事件，事件对象将有relatedTarget属性指明这个过程涉及的其他元素。（到Event参考页查看relatedTarget属性的IE等效属性。）mouseover和mouseout事件和这里介绍的所有鼠标事件一样会冒泡。但这通常不方便，因为当触发mouseout事件处理程序时，你不得不检查鼠标是否真的离开目标元素还是仅仅是从这个元素的一个子元素移动到另一个。正因为如此，IE提供了这些事件的不冒泡版本mouseenter和mouseleave。JQuery模拟非IE的浏览器中这些事件的支持（见第19章），同时3级DOM事件规范把它们标准化了。

当用户滚动鼠标滚轮时，浏览器触发mousewheel事件（或在Firefox中是DOMMouseScroll事件）。传递的事件对象属性指定滚轮转动的大小和方向。3级DOM事件规范正在标准化一个更通用的多维wheel事件，一旦实现将取代mousewheel和DOMMouseScroll事件。17.6节包含一个mousewheel事件示例。

**4.键盘事件**

当键盘聚焦到 Web 浏览器时，用户每次按下或释放键盘上的按键时都会产生事件。键盘快捷键对于操作系统和浏览器本身有特殊意义，它们经常被操作系统或浏览器“吃掉”并对 JavaScript 事件处理程序不可见。无论任何文档元素获取键盘焦点都会触发键盘事件，并且它们会冒泡到Document和Window对象。如果没有元素获得焦点，可以直接在文档上触发事件。传递给键盘事件处理程序的事件对象有keyCode字段，它指定按下或释放的键是哪个。除了keyCode，键盘事件对象也有altKey、ctrlKey、metaKey和shiftKey，描述键盘辅助键的状态。

keydown 和 keyup 事件是低级键盘事件，无论何时按下或释放按键（甚至是辅助键）都会触发它们。当keydown事件产生可打印字符时，在keydown和keyup之间会触发另外一个keypress事件。当按下键重复产生字符时，在keyup事件之前可能产生很多keypress事件。keypress是较高级的文本事件，其事件对象指定产生的字符而非按下的键。

所有浏览器都支持keydown、keyup和keypress事件，但有一些互用性问题，因为事件对象的keyCode属性值从未标准化过。3级DOM事件规范尝试解决之前的互用性问题，但尚未实施。17.9节包含处理keydown事件的示例，17.8节包含处理keypress事件的示例。

### 17.1.2 DOM事件

W3C开发3级DOM事件规范已经长达十年之久。在写本章时，它已经做了大量修订使其适合当前浏览器的现状，现在终于处于标准化的“最后征集工作草案”（last call working draft）阶段。它标准化了前面介绍的许多传统事件，同时增加了这里介绍的一些新事件。这些新事件类型尚未得到广泛支持，一旦标准确定，我们就期望浏览器厂商能实现它们。

如上所述，3级DOM事件规范标准化了不冒泡的 focusin 和 focusout 事件来取代冒泡的 focus 和 blur 事件，标准化了冒泡的mouseenter和mouseleave事件来取代不冒泡的mouseover和mouseout事件。此版本的标准也弃用了大量由2级DOM事件规范定义但未得到广泛实现的事件类型。浏览器依旧允许产生像DOMActivate、DOMFocusIn和DOMNodeInserted这样的事件，但它们不再必要，同时本书的文档也不会列出它们。

3级DOM事件规范中新增内容有通过wheel事件对二维鼠标滚轮提供标准支持，通过textinput事件和传递新KeyboardEvent对象作为参数给keydown、keyup和keypress的事件处理程序来给文本输入事件提供更好的支持。

wheel事件的处理程序接收到的事件对象除了所有普通鼠标事件属性，还有deltaX、deltaY和deltaZ属性来报告三个不同的鼠标滚轴。大多数鼠标滚轮是一维或两维的，并不使用deltaZ。更多关于mousewheel事件的内容请参见17.6节。

如上所述，3级DOM事件规范定义了keypress事件，但不赞成使用它而使用称为textinput的新事件。传递给textinput事件处理程序的事件对象不再有难以使用的数字keyCode属性值，而有指定输入文本字符串的data属性。textinput事件不是键盘特定事件，无论通过键盘、剪切和粘贴、拖放等方式，每当发生文本输入时就会触发它。规范定义了事件对象的inputMethod属性和一组代表各种文本输入种类的常量（键盘、粘贴、拖放、手写和语音识别等）。在写本章时，Safari和Chrome使用混合大小写的textInput来支持这个事件版本，其事件对象有data属性但没有inputMethed属性。17.8节包含使用textInput事件的示例。

新 DOM 标准通过在事件对象中加入新的key和char属性来简化keydown、keyup和keypress事件，这些属性都是字符串。对于产生可打印字符的键盘事件，key和char值将等于生成的文本。对于控制键，key属性将会是像标识键的“Enter”、“Delete”和“Left”这样的字符串，而char属性将是null，或对于像Tab这样的控制键有一个字符编码，它将是按键产生的字符串。在写本章时，尚未有浏览器支持key和char属性，但如果key属性实现了，例17-8将使用它。

### 17.1.3 HTML5事件

HTML5及相关标准定义了大量新的Web应用API（见第22章），其中许多API都定义了事件。本节列出并简要介绍这些HTML5和Web应用事件。其中一些事件现在已经可以开始使用，但更详细的信息在本书的其他地方，另外一些尚未得到广泛实现，也没有详细文档。

广泛推广的HTML5特性之一是加入用于播放音频和视频的`<audio>`和`<video>`元素。这些元素有长长的事件列表，它们触发各种关于网络事件、数据缓冲状况和播放状态的通知：

canplay                loadeddata          playing             stalled￼
canplaythrough         loadedmetadata      progress            suspend￼
durationchange         loadstart           ratechange          timeupdate￼
emptied                pause               seeked              volumechange￼
ended                  play                seeking             waiting

传递给媒体事件处理程序的事件对象普通且没有特殊属性，target属性用于识别`<audio>`和`<video>`元素，然而这些元素有许多相关的属性和方法。21.2节有更多关于这些元素及其属性和事件的详细内容。

HTML5的拖放API允许 JavaScript 应用参与基于操作系统的拖放操作，实现Web和原生应用间的数据传输。该API定义了如下7个事件类型：

dragstart         drag            dragend￼
dragenter         dragover        dragleave￼
drop

触发拖放事件的事件对象和通过鼠标事件发送的对象类似，其附加属性 dataTransfer 持有 DataTransfer 对象，它包含关于传输的数据和其中可用的格式的信息。17.7节将对HTML5拖放API进行说明和演示。

HTML5定义了历史管理机制（见22.2节），它允许Web应用同浏览器的返回和前进按钮交互。这个机制涉及的事件是hashchange和popstate。这些事件是类似load和unload的生命周期通知事件，它在Window对象上触发而非任何单独的文档元素。

HTML5为HTML表单定义了大量的新特性。除了标准化前面介绍的表单输入事件外，HTML5也定义了表单验证机制，包括当验证失败时在表单元素上会触发invalid事件。除Opera外的浏览器厂商已经慢慢实现HTML5的新表单特性和事件，但本书没有涵盖它们。

HTML5包含了对离线Web应用的支持（见20.4节），它们可以安装到本地应用缓存中，所以即使浏览器离线时它们依旧能运行，比如当移动设备不在网络范围内时。相关的两个最重要事件是offline和online，无论何时浏览器失去或得到网络连接都会在 Window 对象上触发它们。标准还定义了大量其他事件来通知应用下载进度和应用缓存更新：

cached        checking             downloading            error￼
noupdate      obsolete             progress               updateready

很多新Web应用API都使用message事件进行异步通信。跨文档通信API（见22.3节）允许一台服务器上的文档脚本能和另一台服务器上的文档脚本交换消息。其工作受限于同源策略（见13.6.2节）这一安全方式。发送的每一条消息都会在接收文档的Window上触发message事件。传递给处理程序的事件对象包含data属性，它有保存信息内容以及用于识别消息发送者的source属性和origin策略。message事件的使用方式与使用WebWorker（见13.6.2节）通信、通过Server-Sent事件（见18.3节）和WebSocket（见22.9节）进行网络通信相似。

HTML5及相关标准定义了一些不在窗口、文档和文档元素的对象上触发的事件。XMLHttpRequest规范第2版和File API规范都定义了一系列事件来跟踪异步I/O的进度。它们在XMLHttpRequest或FileReader对象上触发事件。每次读取操作都是以loadstart事件开始，接着是progress和loadend事件。此外，每个操作仅在最终loadend事件之前会有load、error或abort事件。更多详细信息请参见18.1.4节和22.6.5节。

最后，HTML5及相关标准定义了少量庞杂的事件类型。在Window对象上发生的Web存储（见20.1节）API定义了storage事件（在Window对象上）用于通知存储数据的改变。HTML5也标准化了最早由Microsoft在IE中引入的beforeprint和afterprint事件。顾名思义，当文档打印之前或之后立即在Window对象上触发这些事件，它提供了打印文档时添加或删除类似日期或时间等内容的机会。（这些事件不应该用于处理打印文档的样式，因为CSS媒体类型更适合这个用途。）

### 17.1.4 触摸屏和移动设备事件

强大的移动设备的广泛采用（特别是使用触摸屏的那些设备）需要建立新的事件类别。在许多情况下，触摸屏事件映射到传统的事件类型（比如click和srcoll），但不是每次和触摸屏UI的交互都能仿效鼠标，也不是所有的触摸都可以当做鼠标事件处理。本节主要介绍运行在Apple的iPhone和iPad设备上的Safari所产生的手势和触摸事件，还包括用户旋转这些设备时产生的orientationchange事件。在写本章时，这些事件尚未标准化，但W3C已经开始用Apple的触摸事件作为起点制定“触摸事件规范”。本书第四部分并没有记录这些事件，但你可以在Apple的[开发者中心](http://developer.apple.com/)查询更多信息。

Safari产生的手势事件用于两个手指的缩放和旋转手势。当手势开始时生成gesturestart事件，而手势结束时生成gestureend事件。在这两个事件之间是跟踪手势过程的gesturechange事件队列。这些事件传递的事件对象有数字属性scale和rotation。scale属性是两个手指之间当前距离和初始距离的比值。“捏紧”手势的scale值小于1.0，而“撑开”手势的scale值大于1.0。rotation属性是指从事件开始手指旋转的角度，它以度为单位，正值表示按照顺时针方向旋转。

手势事件是高级事件，用于通知已经翻译的手势。如果想实现自定义手势，你可以监听低级触摸事件。当手指触摸屏幕时会触发touchstart事件，当手指移动时会触发touchmove事件，而当手指离开屏幕时会触发touchend事件。不像鼠标事件，触摸事件并不直接报告触摸的坐标。相反，触摸事件传递的事件对象有一个changedTouches属性，该属性是一个类数组对象，其每个元素都描述触摸的位置。

当设备允许用户从竖屏旋转到横屏模式时会在Window对象上触发orientationchanged事件，该事件传递的事件对象本身没有用。但是，在移动版的Safari中，Window对象的orientation属性能给出当前方位，其值是0、90、180或-90。

## 17.2 注册事件处理程序
## 17.3 事件处理程序的调用
## 17.4 文档加载事件
## 17.5 鼠标事件
## 17.6 鼠标滚轮事件
## 17.7 拖放事件
## 17.8 文本事件
## 17.9 键盘事件

# 第18章 脚本化HTTP
# 第19章 jQuery类库
# 第20章 客户端存储
# 第21章 多媒体和图形编程
# 第22章 HTML5 API
# 第三部分 JavaScript核心参考
# JavaScript核心参考
# 第四部分 客户端JavaScript参考
# 客户端JavaScript参考