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



