# 在[0，K]范围内找到一个值 X，该值可以最大化给定数组上的 X 异或和

> 原文:[https://www . geeksforgeeks . org/find-a-value-x-in-range-0-k-哪个能最大化-x-xor-sum-over-给定数组/](https://www.geeksforgeeks.org/find-a-value-x-in-range-0-k-which-can-maximize-x-xor-sum-over-given-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**a【】**和一个整数 **K，**任务是在**【0，K】**范围内找到一个值 **X** ，该值可以使给定函数的值最大化

> *   Xor-sum(X)=(X Xor A[0])+(X Xor A[1])+(X Xor A[2])+_ _ _ _ _ _ _+(X Xor A[N-1]).

**示例:**

> **输入:** a[] = {1，2，3，4，5，6}，N=6，K=10
> **输出:** 8
> **说明:**X 的值为 1，要求的和变为最大。
> 
> **输入:** a[] = {1，6}，N=2，K = 7
> T3】输出: 0

**逼近:**思路是考虑 **K** 的每一个值，然后找到满足上述条件的 **X** 的值。按照以下步骤解决问题:

*   将变量 **max** 和 **X** 初始化为 **0** 和 **-1** ，以存储定义的最大值和正在发生的 **X** 的值。
*   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，K】**，并执行以下任务:
    *   将变量**总和**初始化为 **0** 以存储定义的总和。
    *   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N)** ，并执行以下任务:
        *   将**总和**的值设置为**总和+ j^a[i].**
    *   如果**总和**大于**最大值，**则将**最大值**的值设置为**总和**，将 **X** 设置为 **j.**
*   执行上述步骤后，打印 **X** 的值作为答案。

下面是上述方法的实现

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the value of X for which
// the given sum maximises
void findValue(vector<int>& a, int N, int K)
{

    // Variables to store the maximum
    // sum and that particular value
    // of X.
    long long int max = 0, X = -1;

    // Check every value of K
    for (int j = 0; j <= K; j++) {

        // Variable to store the desired sum
        long long int sum = 0;
        for (int i = 0; i < N; i++) {

            (sum = sum + (j ^ a[i]));
        }

        // Check the condition
        if (sum > max) {
            max = sum;
            X = j;
        }
    }

    // Print the result
    cout << X;
}

// Driver Code
int main()

{

    vector<int> a = { 1, 2, 3, 4, 5, 6 };
    int N = 6, K = 10;

    findValue(a, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    // Function to find the value of X for which
    // the given sum maximises
    public static void findValue(int[] a, int N, int K) {

        // Variables to store the maximum
        // sum and that particular value
        // of X.
        int max = 0, X = -1;

        // Check every value of K
        for (int j = 0; j <= K; j++) {

            // Variable to store the desired sum
            int sum = 0;
            for (int i = 0; i < N; i++) {

                sum = sum + (j ^ a[i]);
            }

            // Check the condition
            if (sum > max) {
                max = sum;
                X = j;
            }
        }

        // Print the result
        System.out.println(X);
    }

    // Driver Code
    public static void main(String args[])
    {
        int[] a = { 1, 2, 3, 4, 5, 6 };
        int N = 6, K = 10;

        findValue(a, N, K);

    }

}

// This code is ontributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the value of X for which
# the given sum maximises
def findValue(a, N, K) :

    # Variables to store the maximum
    # sum and that particular value
    # of X.
    max = 0; X = -1;

    # Check every value of K
    for j in range( K + 1) :

        # Variable to store the desired sum
        sum = 0;
        for i in range(N) :

            sum = sum + (j ^ a[i]);

        # Check the condition
        if (sum > max) :
            max = sum;
            X = j;

    # Print the result
    print(X);

# Driver Code
if __name__ == "__main__" :

    a = [ 1, 2, 3, 4, 5, 6 ];
    N = 6; K = 10;

    findValue(a, N, K);

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;

public class GFG {

    // Function to find the value of X for which
    // the given sum maximises
    public static void findValue(int[] a, int N, int K) {

        // Variables to store the maximum
        // sum and that particular value
        // of X.
        int max = 0, X = -1;

        // Check every value of K
        for (int j = 0; j <= K; j++) {

            // Variable to store the desired sum
            int sum = 0;
            for (int i = 0; i < N; i++) {

                sum = sum + (j ^ a[i]);
            }

            // Check the condition
            if (sum > max) {
                max = sum;
                X = j;
            }
        }

        // Print the result
        Console.WriteLine(X);
    }

    // Driver Code
    public static void Main(string []args)
    {
        int[] a = { 1, 2, 3, 4, 5, 6 };
        int N = 6, K = 10;

        findValue(a, N, K);
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the value of X for which
        // the given sum maximises
        function findValue(a, N, K) {

            // Variables to store the maximum
            // sum and that particular value
            // of X.
            let max = 0, X = -1;

            // Check every value of K
            for (let j = 0; j <= K; j++) {

                // Variable to store the desired sum
                let sum = 0;
                for (let i = 0; i < N; i++) {

                    (sum = sum + (j ^ a[i]));
                }

                // Check the condition
                if (sum > max) {
                    max = sum;
                    X = j;
                }
            }

            // Print the result
            document.write(X);
        }

        // Driver Code
        let a = [1, 2, 3, 4, 5, 6];
        let N = 6, K = 10;

        findValue(a, N, K);

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
8
```

***时间复杂度:** O(K*N)*
***辅助空间:** O(1)*