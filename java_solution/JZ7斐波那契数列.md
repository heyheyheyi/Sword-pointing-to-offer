# 题目描述

要求输入一个正整数 n ，请你输出斐波那契数列的第 n 项。

斐波那契数列的标准公式为：F(1)=1，F(2)=1, F(n)=F(n-1)+F(n-2)（n>=3，n∈N*）

# 题解

## 1.递归法

根据公式直接写出

```java
public class Solution {
    public int Fibonacci(int n) {
        if(n<=1){
            return n;
        }
        return Fibonacci(n-1) + Fibonacci(n-2);
    }
}
```

时间复杂度：O(2^n) 

空间复杂度：O(1)

## 2.优化递归

递归会造成大量的重复计算，所以可以用数组把结果存起来。

```java
public class Solution {
    public int Fibonacci(int n) {
        int ans[] = new int[40];
        ans[0] = 0;
        ans[1] = 1;
        for(int i=2;i<=n;i++){
            ans[i] = ans[i-1] + ans[i-2];
        }
        return ans[n];
    }
}
```

时间复杂度：O(n) 

空间复杂度：O(n)

## 3.优化存储

其实我们可以发现每次就用到了最近的两个数，所以我们可以只存储最近的两个数

- sum 存储第 n 项的值
- one 存储第 n-1 项的值
- two 存储第 n-2 项的值

```java
public class Solution{
    public int Fibonacci(int n){
        if(n==0){
            return 0;
        }else if(n==1){
            return 1;
        }
        int sum = 0;
        int two = 0;
        int one = 1;
        for(int i=2;i<=n;i++){
            sum = two+one;
            two = one;
            one = sum;
        }
        return sum;
    }
}
```

时间复杂度：O(n) 

空间复杂度：O(1)

## 4.最终优化

可以减少一个变量的使用，利用sum来存储第n-1项。

![img](https://uploadfiles.nowcoder.com/images/20190809/1078265_1565356960932_D0096EC6C83575373E3A21D129FF8FEF)

```java
public class Solution {
    public int Fibonacci(int n) {
        if(n == 0){
            return 0;
        }else if(n == 1){
            return 1;
        }
        int sum = 1;
        int one = 0;
        for(int i=2;i<=n;i++){
            sum = sum + one;
            one = sum - one;
        }
        return sum;
    }
}
```

时间复杂度：O(n) 

空间复杂度：O(1)
