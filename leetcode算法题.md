### 1.字符串和数组

**1.1 从排序数组中删除重复项**

思路一：先用sort()排序，再逐一比较，相等的项用splice()删掉

思路二：两重循环

**1.2 字符串删除连续重复字符**

思路：新建一个字符串result用来存储不重复的字符，定义一个count用来计数，一重循环，相邻两字符不相等即存入result,count+1.

**1.3 从数组中找到中心索引**

思路：应尽量减少循环次数，数组的和是固定的，找到令左右两边和相等的索引

两次循环：一次求和，一次判断

### 2.关于递归：

##### 2.1 递归的定义

一般来说，能够用递归解决的问题应该满足以下三个条件：

（1）需要解决的问题可以转化为一个或多个子问题来求解，而这些子问题的求解方法与原问题完全相同，只是在数量规模上会有所不同。

（2）递归调用的次数必须是有限的。

（3）必须有结束递归的条件来终止递归

##### 2.2 何时使用递归

以下三种情况，常常用到递归方法：

（1）定义是递归的，如n!和Fibonacci数列

（2）数据结构是递归的，如单链表，

（3）问题的求解方法是递归的，如Hanoi问题

##### 2.3 递归模型

一般的，一个递归模型是由递归出口和递归体两部分组成

##### 2.4递归调用的实现原理：

（1）每递归调用一次，就需进栈一次，进栈次数称为递归深度，当n越大，递归深度越深，开辟的栈空间也越大；

（2）每当遇到递归出口或完成本次执行时，需从栈顶元素中得到返回地址，并恢复参量值，当全部执行完毕时，栈应为空。

#### 4.树

##### 4.1二叉树

前序遍历：中→左→右

中序遍历：左→中→右

后序遍历：左→右→中

