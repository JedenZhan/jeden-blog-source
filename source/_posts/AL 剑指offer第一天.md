---
title: 剑指offer
tags: 剑指offer
---

## 1. 二维数组中的查找

答案:

```js
while(line=readline()){
    var index = line.indexOf(',');
    var left = parseInt(line.substring(0,index));
    var right = JSON.parse(line.substring(index+1));
    print(Find(left,right))
} // 吐槽读取输入...
function Find(target, array)
{
    // write code here
    let lenX = array.length;
    let lenY = array[0].length; // 内部数组长度相等
    for (let i = lenX - 1, j = 0; i >= 0 && j < lenY;) {
        if (target > array[i][j]) {
            j ++; // 横向递增
        } else if (target < array[i][j]) {
            i --; // 竖向也是递增的
        } else { // ..不大于不小于
            return true;
        }
    }
    return false
}
```



## 2. 替换空格

答案: 很简单

```js
function replaceSpace(str) {
  // write code here
  return str.replace(/\s/g, '%20')
}
```



## 3. 打印链表

链表: `一种数据结构, 每一个元素都有next属性来获取下一个元素`

当你知道链表特性的时候答案就出来了

```js
function printListFromTailToHead(head)
{
    // write code here
    let result = [];
    let first = head;
    while(first){ // 链表最后一个元素的next是null
        arr.push(first.val);
        first=first.next; // 不断获取下一个元素
    }
    return result.reverse();
}
```

