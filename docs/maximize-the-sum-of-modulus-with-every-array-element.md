# 最大化每个数组元素的模和

> 原文:[https://www . geesforgeks . org/最大化每个数组元素的模和/](https://www.geeksforgeeks.org/maximize-the-sum-of-modulus-with-every-array-element/)

给定一个由正整数 **N** 组成的数组 **A[]** ，任务是找到最大可能值:

> **F(M) = M % A[0] + M % A[1] + …。+ M % A[N -1]** ，其中 **M** 可以是任意整数值

**例:**

> **输入:** arr[] = {3，4，6}
> **输出:** 10
> **解释:**
> M = 11 时出现最大和。
> (11% 3)+(11% 4)+(11% 6)= 2+3+5 = 10
> **输入:** arr[] = {2，5，3}
> **输出:** 7
> **解释:**
> M = 29 出现最大和。
> (29% 2)+(29% 5)+(29% 3)= 1+4+2 = 7。

**进场:**
按照以下步骤解决问题:

1.  计算所有数组元素的 [LCM。](https://www.geeksforgeeks.org/lcm-of-given-array-elements/)
2.  如果 **M** 等于数组的 LCM，那么 **F(M) = 0** 即 **F(M)** 的最小可能值。这是因为，**M % a【I】**对于每一个 **i <sup>th</sup>** 指标都将始终为 0。
3.  对于数组元素的 M = LCM–1， **F(M)** 最大化。这是因为， **M % a[i]** 等于每一个 **i <sup>第</sup>** 指数**a[I]–1**，这是最大可能。
4.  因此 **F(M)** 的最大可能值可以是 [**阵元之和**](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)**–N**。

以下是上述方法的实现:

## C++

```
// C++ program to find the
// maximum sum of modulus
// with every array element
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// maximum sum of modulus
// with every array element
int maxModulosum(int a[], int n)
{
    int sum = 0;

    // Sum of array elements
    for (int i = 0; i < n; i++) {
        sum += a[i];
    }

    // Return the answer
    return sum - n;
}

// Driver Program
int main()
{
    int a[] = { 3, 4, 6 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << maxModulosum(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum
// sum of modulus with every array
// element
import java.io.*;

class GFG{

// Function to return the maximum
// sum of modulus with every array
// element
static int maxModulosum(int a[], int n)
{
    int sum = 0;

    // Sum of array elements
    for(int i = 0; i < n; i++)
    {
       sum += a[i];
    }

    // Return the answer
    return sum - n;
}

// Driver Code
public static void main (String[] args)
{
    int a[] = new int[]{ 3, 4, 6 };
    int n = a.length;

    System.out.println(maxModulosum(a, n));
}
}

// This code is contributed by Shubham Prakash
```

## 蟒蛇 3

```
# Python3 program to find the
# maximum sum of modulus
# with every array element

# Function to return the
# maximum sum of modulus
# with every array element
def maxModulosum(a, n):

    sum1 = 0;

    # Sum of array elements
    for i in range(0, n):
        sum1 += a[i];

    # Return the answer
    return sum1 - n;

# Driver Code
a = [ 3, 4, 6 ];
n = len(a);
print(maxModulosum(a, n));

# This code is contributed by Code_Mech
```

## C#

```
// C# program to find the maximum
// sum of modulus with every array
// element
using System;
class GFG{

// Function to return the maximum
// sum of modulus with every array
// element
static int maxModulosum(int []a, int n)
{
    int sum = 0;

    // Sum of array elements
    for(int i = 0; i < n; i++)
    {
        sum += a[i];
    }

    // Return the answer
    return sum - n;
}

// Driver Code
public static void Main(String[] args)
{
    int []a = new int[]{ 3, 4, 6 };
    int n = a.Length;

    Console.Write(maxModulosum(a, n));
}
}

// This code is contributed
// by shivanisinghss2110
```

## java 描述语言

```
<script>

    // Javascript program to find the
    // maximum sum of modulus
    // with every array element

    // Function to return the
    // maximum sum of modulus
    // with every array element
    function maxModulosum(a, n)
    {
        let sum = 0;

        // Sum of array elements
        for (let i = 0; i < n; i++) {
            sum += a[i];
        }

        // Return the answer
        return sum - n;
    }

    let a = [ 3, 4, 6 ];
    let n = a.length;
    document.write(maxModulosum(a, n));

</script>
```

**Output:** 

```
10
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*