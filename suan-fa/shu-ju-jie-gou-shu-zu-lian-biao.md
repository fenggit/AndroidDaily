# 数据结构 - 数组、链表

数据结构的最底层的就是数组和链表。

参考地址

> [https://labuladong.gitbook.io/algo/bi-du-wen-zhang/xue-xi-shu-ju-jie-gou-he-suan-fa-de-gao-xiao-fang-fa](https://labuladong.gitbook.io/algo/bi-du-wen-zhang/xue-xi-shu-ju-jie-gou-he-suan-fa-de-gao-xiao-fang-fa)

## 数组

特点：线性表结构，连续存储的空间，随机访问查询快O\(1\)，增删和扩容数组，需要复制数组O\(N\)

## 链表

特点：通过指针关联元素，需要存储数据的同时，额外存储指向下一个元素的位置，耗费存储空间。增删快，查询慢，查询数据需要从头开始一点点查询。

## 查询数据的套路

* 线性查询：for、while
* 非线性：递归

### 1. 数组

```java
void traverse(int[] arr) {
    for (int i = 0; i < arr.length; i++) {
        // 迭代访问 arr[i]
    }
}
```

### 2. 链表

```java
/* 基本的单链表节点 */
class ListNode {
    int val;
    ListNode next;
}

void traverse(ListNode head) {
    for (ListNode p = head; p != null; p = p.next) {
        // 迭代访问 p.val
    }
}

void traverse(ListNode head) {
    // 递归访问 head.val
    traverse(head.next);
}
```

### 3. 二叉树

```java
/* 基本的 N 叉树节点 */
class TreeNode {
    int val;
    TreeNode[] children;
}

void traverse(TreeNode root) {
    for (TreeNode child : root.children)
        traverse(child);
}
```

### 4. N 叉树

```java
/* 基本的 N 叉树节点 */
class TreeNode {
    int val;
    TreeNode[] children;
}

void traverse(TreeNode root) {
    for (TreeNode child : root.children)
        traverse(child);
}
```

