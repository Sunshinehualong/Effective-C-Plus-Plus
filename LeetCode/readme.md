
## Tabel of Contents(不同类别的分类)

 * [腾讯精选50题](#腾讯精选50题)
    - [104 给定一个二叉树，找出其最大深度](#104-给定一个二叉树找出其最大深度)
    - [334-字符串逆序原地修改字符串](#334-字符串逆序原地修改字符串)
    - [557-反转字符串中的单词](#557-反转字符串中的单词)
    - [292-Nim拿石头游戏](#292-Nim拿石头游戏)
    - [237-删除单向链表中的节点](#237-删除单向链表中的节点)
    - []()


* [递归思想解题](#递归思想解题)


* [string操作]()

## 腾讯精选50题

### 104-给定一个二叉树找出其最大深度
>题目描述:
二叉树的深度为根节点到最远叶子节点的最长路径上的节点数
```
测试用例： 给定二叉树 [3,9,20,null,null,15,7]， 返回最大深度为3
    3
   / \
  9  20
    /  \
   15   7
```
```
解题思路：递归思想出发，每次找左子树和右子树的深度去最大值

```

### 334-字符串逆序原地修改字符串
>问题描述：
将输入的字符串反转过来。输入字符串以字符数组 char[] 的形式给出。
必须原地修改输入数组、使用 O(1) 的额外空间解决这一问题。
```markdown
测试示例：
输入：["h","e","l","l","o"]
输出：["o","l","l","e","h"]
```
```markdown
解题思路：
直接遍历一遍进行逆序
```

### 557-反转字符串中的单词
>问题描述：
给定一个字符串，你需要反转字符串中每个单词的字符顺序，  
同时仍保留空格和单词的初始顺序。  
在字符串中，每个单词由单个空格分隔，并且字符串中不会有任何额外的空格。  
```
测试示例：
输入: "Let's take LeetCode contest"
输出: "s'teL ekat edoCteeL tsetnoc" 
```
```
解题思路：
spilt 以空格为间隔分开字符，再对每个字符反转
```


### 292-Nim拿石头游戏
>问题描述：
两个人一起玩 Nim游戏：桌子上有一堆石头，每次你们轮流拿掉 1 - 3 块石头  
拿掉最后一块石头的人就是获胜者。你作为先手。  
 编写一个函数，来判断你是否可以在给定石头数量的情况下赢得游戏。  
```markdown
测试示例：
4 ==> false
5 ==> true

```
```
解题思路：
博弈论的问题 通过归纳总结，寻找规律，发现只要是4的倍数就会输

```
### 237-删除单向链表中的节点
>问题描述：
删除某个链表中给定的（非末尾）节点，你将只被给定要求被删除的节点
```
测试示例：
输入: head = [4,5,1,9], node = 5
输出: [4,1,9]
```
```
解题思路：

```

### *-NewQuestion
>问题描述：

```
测试示例：

```
```
解题思路：

```


-------------------------------

## 递归思想解题

### 104-给定一个二叉树找出其最大深度
>递归思想出发，每次找左子树和右子树的深度去最大值


## string 操作

## 链表 操作
