# [二叉树的镜像](https://leetcode-cn.com/problems/er-cha-shu-de-jing-xiang-lcof/)

简单

## 描述

请完成一个函数，输入一个二叉树，该函数输出它的镜像。

例如输入：

     4
   /   \
  2     7
 / \   / \
1   3 6   9
镜像输出：

     4
   /   \
  7     2
 / \   / \
9   6 3   1

```
示例 1：

输入：root = [4,2,7,1,3,6,9]
输出：[4,7,2,9,6,3,1]
```

## 解法——递归

很经典的递归解法

### 代码

时间复杂度 O(N) ： 其中 N 为二叉树的节点数量，建立二叉树镜像需要遍历树的所有节点，占用 O(N)时间。
空间复杂度 O(N)： 最差情况下（当二叉树退化为链表），递归时系统需使用 O(N) 大小的栈空间。

```java
public TreeNode mirrorTree(TreeNode root) {
        if(root==null){
            return root;
        }
        TreeNode temp = root.left;
        root.left = mirrorTree(root.right);
        root.right = mirrorTree(temp);  
        return root;  
    }
```





# [从头到尾打印链表](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

简单

## 描述

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

**示例 1：**

```
输入：head = [1,3,2]
输出：[2,3,1]
```

## 解法1

先反转链表（时间复杂度n） 再遍历链表（时间复杂度n） 总的空间复杂度1

## 解法2

先遍历链表得到长度（时间复杂度n），反着存到数组里（时间复杂度n） ，空间复杂度1

## 解法3

递归遍历链表，顺便统计长度，这样可以倒序存储数组，时间复杂度n，空间复杂度n

### 代码

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    private int[] ret;
    private int size;
    private int index;
    public int[] reversePrint(ListNode head) {
        if(head==null){
            ret = new int[0];
            return ret;
        }
        int temp = helper(head);
        ret[index++] = temp;
        return ret;    
    }
    public int helper(ListNode head){
        size++;
        if(head.next==null){
            ret = new int[size];
            //添加到数组
            return head.val;
        }else{
            int temp = helper(head.next);
            ret[index++] = temp;
            return head.val;
        }
    }
}
```



# [数组中重复的数字](https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof)

简单

## 描述

找出数组中重复的数字。

在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

```
示例 1：
输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 
```

## 解法1——hashset

时间复杂度O(n) 空间复杂度O(n)

### 代码

```java
public int findRepeatNumber(int[] nums) {
        Set<Integer> hashset = new HashSet<>();
        for(int num:nums){
            if(hashset.contains(num)){
                return num;
            }else{
                hashset.add(num);
            }
        }
        return -1;
    }
```

# 二维数组中的查找

中等

## 解法1——暴力法

时间复杂度O（mn） 空间复杂度1

## 解法2——线性查找

从二维数组的右上角开始查找。如果当前元素等于目标值，则返回 `true`。如果当前元素大于目标值，则移到左边一列。如果当前元素小于目标值，则移到下边一行。

时间复杂度O(m+n) 空间复杂度O(1)

### 代码

```java
public boolean findNumberIn2DArray(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return false;
        }
        int rows = matrix.length, columns = matrix[0].length;
        int row = 0, column = columns - 1;
        while (row < rows && column >= 0) {
            int num = matrix[row][column];
            if (num == target) {
                return true;
            } else if (num > target) {
                column--;
            } else {
                row++;
            }
        }
        return false;
    }

```

# [替换空格](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof)

简单

## 描述

请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

 ```
示例 1：
输入：s = "We are happy."
输出："We%20are%20happy."
 ```

## 解法1

构建StringBuilder 时间复杂度O(N) 空间复杂度O(N) 不过既然已经知道新的字符串最长长度为3N，就可以创建一个3N的字符数组，用一个变量记录真实的新的字符串的长度即可

### 代码1

```java
public String replaceSpace(String s) {
        int n=s.length();
        StringBuilder stringBuilder = new StringBuilder(3*n);
        for(int i=0;i<n;i++){
            if(s.charAt(i)==' '){
                stringBuilder.append("%20");
            }else{
                stringBuilder.append(s.charAt(i));
            }
        }
        return stringBuilder.toString();

    }
```



### 代码2

[代码来源](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/solution/mian-shi-ti-05-ti-huan-kong-ge-by-leetcode-solutio/)

```java
public String replaceSpace(String s) {
        int length = s.length();
        char[] array = new char[length * 3];
        int size = 0;
        for (int i = 0; i < length; i++) {
            char c = s.charAt(i);
            if (c == ' ') {
                array[size++] = '%';
                array[size++] = '2';
                array[size++] = '0';
            } else {
                array[size++] = c;
            }
        }
        String newStr = new String(array, 0, size);
        return newStr;
    }



```



