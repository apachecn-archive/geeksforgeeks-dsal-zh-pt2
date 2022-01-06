# 用 Java 打印斐波那契数列的 3 种不同方式

> 原文:[https://www . geesforgeks . org/differential-to-print-Fibonacci-series-in-Java/](https://www.geeksforgeeks.org/different-ways-to-print-fibonacci-series-in-java/)

给定一个数字 **N** ，我们需要找到[斐波那契数列](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)直到 **N** 项。

> [斐波那契数列](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)是一系列元素，其中前两个元素相加得到下一个元素，从 0 和 1 开始。

**示例:**

> **输入:** N = 10
> **输出:** 0 1 1 2 3 5 8 13 21 34
> 这里斐波那契的第一项是 0，第二项是 1，所以第三项=第一(o) +第二(1)等等。
> 
> **输入:**N = 15
> T3】输出:0 1 2 3 5 8 13 21 34 55 89 144 233 377

**方法 1–迭代:**将第一个和第二个数字初始化为 **0 和 1** 。接下来，我们打印第一个和第二个数字。然后，我们将流程发送到迭代 while 循环，在此循环中，我们通过将前两个数字相加得到下一个数字，同时我们将第一个数字与第二个数字交换，将第二个数字与第三个数字交换。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

    // Function to print N Fibonacci Number
    static void Fibonacci(int N)
    {
        int num1 = 0, num2 = 1;

        int counter = 0;

        // Iterate till counter is N
        while (counter < N) {

            // Print the number
            System.out.print(num1 + " ");

            // Swap
            int num3 = num2 + num1;
            num1 = num2;
            num2 = num3;
            counter = counter + 1;
        }
    }

    // Driver Code
    public static void main(String args[])
    {
        // Given Number N
        int N = 10;

        // Function Call
        Fibonacci(N);
    }
}
```

**Output:**

```
0 1 1 2 3 5 8 13 21 34

```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**方法 2–使用** [**递归**](https://www.geeksforgeeks.org/recursion/) **:** 因为斐波那契数是前面两个数的和。我们可以按照以下条件使用递归:

1.  得到需要计算斐波那契数列的数字。
2.  递归地从值 N 迭代到 1:
    *   **基本情况:**如果递归调用的值小于 1，函数返回 1。
    *   **递归调用:**如果不满足基本情况，则递归调用前两个值为:

        > 递归 _ 函数(N–1)+递归 _ 函数(N–2)；

    *   **Return 语句:**每次递归调用时(基本情况除外)，将前两个值的递归函数返回为:

        > 递归 _ 函数(N–1)+递归 _ 函数(N–2)；

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive implementation of
// Fibonacci Series

class GFG {

    // Function to print the fibonacci series
    static int fib(int n)
    {
        // Base Case
        if (n <= 1)
            return n;

        // Recursive call
        return fib(n - 1)
            + fib(n - 2);
    }

    // Driver Code
    public static void
    main(String args[])
    {
        // Given Number N
        int N = 10;

        // Print the first N numbers
        for (int i = 0; i < N; i++) {

            System.out.print(fib(i) + " ");
        }
    }
}
```

**Output:**

```
0 1 1 2 3 5 8 13 21 34

```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**方法 3–使用** [**动态编程**](https://www.geeksforgeeks.org/dynamic-programming/) **:** 通过存储到目前为止计算的斐波那契数，我们可以避免方法 2 中重复的工作。以下是步骤:

1.  创建一个大小为 **N** 的数组 **arr[]** 。
2.  初始化 arr[0] = 0，arr[1] = 1。
3.  迭代**【2，N】**并将数组 **arr[]** 更新为:

    > arr[I]= arr[I–2]+arr[I–1]

4.  打印**arr【N】**的值。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Dynamic Programming approach for
// Fibonacci Series

class fibonacci {

    // Function to find the fibonacci Series
    static int fib(int n)
    {

        // Declare an array to store
        // Fibonacci numbers.
        // 1 extra to handle case, n = 0
        int f[] = new int[n + 2];

        int i;

        // 0th and 1st number of
        // the series are 0 and 1
        f[0] = 0;
        f[1] = 1;

        for (i = 2; i <= n; i++) {

            // Add the previous 2 numbers
            // in the series and store it
            f[i] = f[i - 1] + f[i - 2];
        }

        // Nth Fibonacci Number
        return f[n];
    }

    public static void
    main(String args[])
    {
        // Given Number N
        int N = 10;

        // Print first 10 term
        for (int i = 0; i < N; i++)
            System.out.print(fib(i) + " ");
    }
}
```

**Output:**

```
0 1 1 2 3 5 8 13 21 34

```

**时间复杂度:***O(N)*
T5】辅助空间: *O(N)*