# 最长替代奇偶子序列

> 原文:[https://www . geesforgeks . org/最长-替代-奇偶校验-子序列/](https://www.geeksforgeeks.org/longest-alternative-parity-subsequence/)

给定一个大小为 **N** 的数组**。任务是打印最长的可选奇数/偶数或偶数/奇数子序列的长度。
**例:**** 

> ****输入:** a[] = { 13，16，8，9，32，10 }
> **输出:** 4
> {13，16，9，10 }或长度为 4 的任何其他子序列都可以是答案。
> **输入:** a[] = {1，2，3，3，9}
> **输出:** 3**

****接近**:最长的可选奇偶子序列的答案将是**【奇数，偶数，奇数，偶数，…..】**或**【偶，奇，偶，奇，…。】**序列。因此，在数组中迭代，首先找到最长的奇数/偶数子序列，然后找到最长的偶数/奇数序列。寻找最长子序列的步骤是:** 

*   **迭代并找到下一个奇数并增加长度。**
*   **迭代并找到下一个奇数并增加长度。**
*   **从**步骤** 1 开始，交替重复**步骤 1** 和**步骤 2** 直到结束，找到最长的奇数/偶数子序列。**
*   **从**第二步**开始，交替重复**第一步**和**第二步**直到结束，找到最长的偶/奇子序列。**

**以下是上述方法的实现:** 

## **C++**

```
// C++ program to find the length
// of the longest alternative parity
// subsequence
#include <iostream>
using namespace std;

// Function to find the longest
int longestAlternativeSequence(int a[], int n)
{
    int maxi1 = 0;

    // Marks the starting of odd
    // number as sequence and
    // alternatively changes
    int f1 = 0;

    // Finding the longest odd/even sequence
    for (int i = 0; i < n; i++) {

        // Find odd number
        if (!f1) {
            if (a[i] % 2) {
                f1 = 1;
                maxi1++;
            }
        }

        // Find even number
        else {
            if (a[i] % 2 == 0) {
                maxi1++;
                f1 = 0;
            }
        }
    }

    int maxi2 = 0;
    int f2 = 0;

    // Length of the longest even/odd sequence
    for (int i = 0; i < n; i++) {

        // Find odd number
        if (f2) {
            if (a[i] % 2) {
                f2 = 1;
                maxi2++;
            }
        }

        // Find even number
        else {
            if (a[i] % 2 == 0) {
                maxi2++;
                f2 = 0;
            }
        }
    }

    // Answer is maximum of both
    // odd/even or even/odd subsequence
    return max(maxi1, maxi2);
}

// Driver Code
int main()
{
    int a[] = { 13, 16, 8, 9, 32, 10 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << longestAlternativeSequence(a, n);
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to find the length
// of the longest alternative parity
// subsequence
class GFG
{

// Function to find the longest
static int longestAlternativeSequence(int a[], int n)
{
    int maxi1 = 0;

    // Marks the starting of odd
    // number as sequence and
    // alternatively changes
    int f1 = 0;

    // Finding the longest odd/even sequence
    for (int i = 0; i < n; i++)
    {

        // Find odd number
        if (f1 % 2 != 0)
        {
            if (a[i] % 2 == 1)
            {
                f1 = 1;
                maxi1++;
            }
        }

        // Find even number
        else
        {
            if (a[i] % 2 == 0)
            {
                maxi1++;
                f1 = 0;
            }
        }
    }

    int maxi2 = 0;
    int f2 = 0;

    // Length of the longest even/odd sequence
    for (int i = 0; i < n; i++)
    {

        // Find odd number
        if (f2 % 2 != 0)
        {
            if (a[i] % 2 == 1)
            {
                f2 = 1;
                maxi2++;
            }
        }

        // Find even number
        else
        {
            if (a[i] % 2 == 0)
            {
                maxi2++;
                f2 = 0;
            }
        }
    }

    // Answer is maximum of both
    // odd/even or even/odd subsequence
    return Math.max(maxi1, maxi2);
}

// Driver Code
public static void main(String[] args)
{
    int a[] = { 13, 16, 8, 9, 32, 10 };
    int n = a.length;
    System.out.println(longestAlternativeSequence(a, n));
}
}

// This code is contributed by 29AjayKumar
```

## **蟒蛇 3**

```
# Python3 program to find the length
# of the longest alternative parity
# subsequence

# Function to find the longest
def longestAlternativeSequence(a, n):
    maxi1 = 0

    # Marks the starting of odd
    # number as sequence and
    # alternatively changes
    f1 = 0

    # Finding the longest odd/even sequence
    for i in range(n):

        # Find odd number
        if (f1 == 0):
            if (a[i] % 2):
                f1 = 1
                maxi1 += 1

        # Find even number
        else:
            if (a[i] % 2 == 0):
                maxi1 += 1
                f1 = 0

    maxi2 = 0
    f2 = 0

    # Length of the longest even/odd sequence
    for i in range(n):

        # Find odd number
        if (f2):
            if (a[i] % 2):
                f2 = 1
                maxi2 += 1

        # Find even number
        else:
            if (a[i] % 2 == 0):
                maxi2 += 1
                f2 = 0

    # Answer is maximum of both
    # odd/even or even/odd subsequence
    return max(maxi1, maxi2)

# Driver Code
a = [13, 16, 8, 9, 32, 10]
n = len(a)
print(longestAlternativeSequence(a, n))

# This code is contributed by Mohit Kumar
```

## **C#**

```
// C# program to find the length
// of the longest alternative parity
// subsequence
using System;

class GFG
{

// Function to find the longest
static int longestAlternativeSequence(int []a,
                                      int n)
{
    int maxi1 = 0;

    // Marks the starting of odd
    // number as sequence and
    // alternatively changes
    int f1 = 0;

    // Finding the longest odd/even sequence
    for (int i = 0; i < n; i++)
    {

        // Find odd number
        if (f1 != 0)
        {
            if (a[i] % 2 == 0)
            {
                f1 = 1;
                maxi1++;
            }
        }

        // Find even number
        else
        {
            if (a[i] % 2 == 0)
            {
                maxi1++;
                f1 = 0;
            }
        }
    }

    int maxi2 = 0;
    int f2 = 0;

    // Length of the longest even/odd sequence
    for (int i = 0; i < n; i++)
    {

        // Find odd number
        if (f2 == 0)
        {
            if (a[i] % 2 == 0)
            {
                f2 = 1;
                maxi2++;
            }
        }

        // Find even number
        else
        {
            if (a[i] % 2 == 0)
            {
                maxi2++;
                f2 = 0;
            }
        }
    }

    // Answer is maximum of both
    // odd/even or even/odd subsequence
    return Math.Max(maxi1, maxi2);
}

// Driver Code
public static void Main()
{
    int []a = { 13, 16, 8, 9, 32, 10 };
    int n = a.Length;
    Console.Write(longestAlternativeSequence(a, n));
}
}

// This code is contributed by Nidhi
```

## **java 描述语言**

```
<script>

// Javascript program to find the length
// of the longest alternative parity
// subsequence

// Function to find the longest
function longestAlternativeSequence(a, n)
{
    let maxi1 = 0;

    // Marks the starting of odd
    // number as sequence and
    // alternatively changes
    let f1 = 0;

    // Finding the longest odd/even sequence
    for (let i = 0; i < n; i++) {

        // Find odd number
        if (!f1) {
            if (a[i] % 2) {
                f1 = 1;
                maxi1++;
            }
        }

        // Find even number
        else {
            if (a[i] % 2 == 0) {
                maxi1++;
                f1 = 0;
            }
        }
    }

    let maxi2 = 0;
    let f2 = 0;

    // Length of the longest even/odd sequence
    for (let i = 0; i < n; i++) {

        // Find odd number
        if (f2) {
            if (a[i] % 2) {
                f2 = 1;
                maxi2++;
            }
        }

        // Find even number
        else {
            if (a[i] % 2 == 0) {
                maxi2++;
                f2 = 0;
            }
        }
    }

    // Answer is maximum of both
    // odd/even or even/odd subsequence
    return Math.max(maxi1, maxi2);
}

// Driver Code
    let a = [ 13, 16, 8, 9, 32, 10 ];
    let n = a.length;
    document.write(longestAlternativeSequence(a, n));

</script>
```

****Output:** 

```
4
```** 

****时间复杂度–**O(n)**

****空间复杂度**–O(1)**