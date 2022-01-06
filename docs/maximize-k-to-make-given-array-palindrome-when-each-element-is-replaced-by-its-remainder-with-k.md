# 当每个元素被其余数替换为 K 时，最大化 K 使给定的数组成为回文

> 原文:[https://www . geeksforgeeks . org/maximize-k-make-给定数组-回文-当每个元素被其余数替换为-k/](https://www.geeksforgeeks.org/maximize-k-to-make-given-array-palindrome-when-each-element-is-replaced-by-its-remainder-with-k/)

给定一个包含 **N** 正整数的[数组](https://www.geeksforgeeks.org/array-data-structure/)****A【】**，任务是找到最大可能数 **K** ，这样在用元素模 **K(A[i]=A[i]%K，对于所有 0 < =i < N)替换所有元素后，**数组变成一个[回文](https://www.geeksforgeeks.org/check-if-all-elements-of-the-array-are-palindrome-or-not/)。如果 **K** 无限大，打印-1。**

****示例:****

> ****输入:** A={1，2，3，4}，N=4
> **输出:**
> 1
> **解释:**
> 对于 K=1，A 变成{1%1，2%1，3%1，4%1}={0，0，0，0}这是一个回文数组。**
> 
> ****输入:** A={1，2，3，2，1}，N=5
> **输出:**
> -1**

****观察:**以下观察有助于解决问题:**

1.  **如果数组已经是回文， **K** 可以无限大。**
2.  **两个数字，比如说 **A** 和 **B** 可以通过取它们的模和它们的差 **(|A-B|)** 以及它们差的因子而相等。**

****方法:**问题可以通过使 **K** 等于[T5】GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/)**的**A【I】**和**A【N-I-1】的绝对差来解决。**按照以下步骤解决问题:****

1.  ****检查 **A** 是否已经是[回文。](https://www.geeksforgeeks.org/program-to-check-if-an-array-is-palindrome-or-not/)如果是，返回 **-1** 。****
2.  ****将数组的第一个和最后一个元素的绝对差存储在一个变量中，比如 **K** ，它将存储将 **A** 变成回文所需的最大数。****
3.  ****从 **1 到 N/2-1** 遍历，对于每个当前索引 I，执行以下操作:

    1.  用 **K** 的 [**GCD**](https://www.geeksforgeeks.org/stdgcd-c-inbuilt-function-finding-gcd/) 以及**A【I】**和**A【N-I-1】的绝对差更新 **K** 。****** 
4.  **返回 **K** 。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// utility function to calculate the GCD of two numbers
int gcd(int a, int b)
{
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}
// Function to calculate the largest K, replacing all
// elements of an array A by their modulus with K, makes A a
// palindromic array
int largestK(int A[], int N)
{
    // check if A is palindrome
    int l = 0, r = N - 1, flag = 0;
    while (l < r) {
        // A is not palindromic
        if (A[l] != A[r]) {
            flag = 1;
            break;
        }
        l++;
        r--;
    }
    // K can be infitely large in this case
    if (flag == 0)
        return -1;

    // variable to store the largest K that makes A
    // palindromic
    int K = abs(A[0] - A[N - 1]);
    for (int i = 1; i < N / 2; i++)
        K = gcd(K, abs(A[i] - A[N - i - 1]));
    // return the required answer
    return K;
}
// Driver code
int main()
{
    // Input
    int A[] = { 1, 2, 3, 2, 1 };
    int N = sizeof(A) / sizeof(A[0]);

    // Function call
    cout << largestK(A, N) << endl;
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;

class GFG{

// Utility function to calculate the GCD
// of two numbers
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}

// Function to calculate the largest K,
// replacing all elements of an array A
// by their modulus with K, makes A a
// palindromic array
static int largestK(int A[], int N)
{

    // Check if A is palindrome
    int l = 0, r = N - 1, flag = 0;
    while (l < r)
    {

        // A is not palindromic
        if (A[l] != A[r])
        {
            flag = 1;
            break;
        }
        l++;
        r--;
    }

    // K can be infitely large in this case
    if (flag == 0)
        return -1;

    // Variable to store the largest K
    // that makes A palindromic
    int K = Math.abs(A[0] - A[N - 1]);
    for(int i = 1; i < N / 2; i++)
        K = gcd(K, Math.abs(A[i] - A[N - i - 1]));

    // Return the required answer
    return K;
}

// Driver code
public static void main(String[] args)
{

    // Input
    int A[] = { 1, 2, 3, 2, 1 };
    int N = A.length;

    // Function call
    System.out.println(largestK(A, N));
}
}

// This code is contributed by sanjoy_62
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# utility function to calculate the GCD of two numbers
def gcd(a, b):
    if (b == 0):
        return a
    else:
        return gcd(b, a % b)

# Function to calculate the largest K, replacing all
# elements of an array A by their modulus with K, makes A a
# palindromic array
def largestK(A, N):

    # check if A is palindrome
    l,r,flag = 0, N - 1, 0
    while (l < r):
        # A is not palindromic
        if (A[l] != A[r]):
            flag = 1
            break
        l += 1
        r -= 1
    # K can be infitely large in this case
    if (flag == 0):
        return -1

    # variable to store the largest K that makes A
    # palindromic
    K = abs(A[0] - A[N - 1])
    for i in range(1,N//2):
        K = gcd(K, abs(A[i] - A[N - i - 1]))

    # return the required answer
    return K

# Driver code
if __name__ == '__main__':
    # Input
    A= [1, 2, 3, 2, 1 ]
    N = len(A)

    # Function call
    print (largestK(A, N))

# This code is contributed by mohit kumar 29.
```

## **C#**

```
// c# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// utility function to calculate the GCD of two numbers
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}

// Function to calculate the largest K, replacing all
// elements of an array A by their modulus with K, makes A a
// palindromic array
static int largestK(int []A, int N)
{

    // check if A is palindrome
    int l = 0, r = N - 1, flag = 0;
    while (l < r) {
        // A is not palindromic
        if (A[l] != A[r]) {
            flag = 1;
            break;
        }
        l++;
        r--;
    }

    // K can be infitely large in this case
    if (flag == 0)
        return -1;

    // variable to store the largest K that makes A
    // palindromic
    int K = Math.Abs(A[0] - A[N - 1]);
    for (int i = 1; i < N / 2; i++)
        K = gcd(K, Math.Abs(A[i] - A[N - i - 1]));

    // return the required answer
    return K;
}

// Driver code
public static void Main()
{

    // Input
    int []A = { 1, 2, 3, 2, 1 };
    int N = A.Length;

    // Function call
    Console.Write(largestK(A, N));
}
}

// This code is contributed by ipg2016107.
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// utility function to calculate the
// GCD of two numbers
function gcd(a, b)
{
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}

// Function to calculate the largest
// K, replacing all elements of an
// array A by their modulus with K,
// makes A a palindromic array
function largestK(A, N)
{

    // Check if A is palindrome
    let l = 0, r = N - 1, flag = 0;

    while (l < r)
    {

        // A is not palindromic
        if (A[l] != A[r])
        {
            flag = 1;
            break;
        }
        l++;
        r--;
    }

    // K can be infitely large in this case
    if (flag == 0)
        return -1;

    // Variable to store the largest K
    // that makes A palindromic
    let K = Math.abs(A[0] - A[N - 1]);
    for(let i = 1; i < N / 2; i++)
        K = gcd(K, Math.abs(A[i] - A[N - i - 1]));

    // Return the required answer
    return K;
}

// Driver code

// Input
let A = [ 1, 2, 3, 2, 1 ];
let N = A.length;

// Function call
document.write(largestK(A, N) + "<br>");

// This code is contributed by gfgking

</script>
```

****Output**

```
-1
```** 

*****时间复杂度:** O(NLogM)，其中 M 是数组中最大的元素*
***辅助空间:** O(1)***