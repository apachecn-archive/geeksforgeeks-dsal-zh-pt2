# 求大完美平方自然数在 O(sqrt(sqrt(N))

中的所有因子

> 原文:[https://www . geeksforgeeks . org/find-大全因子-完美平方-osqrtskrtn 中的自然数/](https://www.geeksforgeeks.org/find-all-factors-of-large-perfect-square-natural-number-in-osqrtsqrtn/)

给定一个**完美平方**自然数 **N** 。任务是找到 **N** 的所有因素。

**示例**

> **输入:**N = 100
> T3】输出: 1 2 4 5 10 20 25 50 100
> 
> **输入:** N = 900
> **输出:**1 2 4 3 6 12 9 18 36 5 10 20 15 30 60 45 90 180 25 50 100 75 150 300 225 450 900

**进场:**

1.  求温度中 **N** 的平方根。
2.  使用[这篇](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)文章中讨论的方法，找出 **O(sqrt(temp))** 中的所有主要温度因子。
3.  用元素 1 初始化一个数组**因子[]** 。
4.  将以上步骤两次得到的**温度**的所有质因数存储在一个数组**因数【】**中。
5.  初始化一个矩阵 **M** ，使得对于**因子【】**中的每个元素，从索引 1 开始:
    *   如果**因子【I】**等于**因子【I-1】**，则将**因子【I】*因子【I-1】**存储在矩阵 **M** 中的**I–1**行。

    *   否则**因子【I】**不等于**因子【I-1】**，则将**因子【I】*因子【I-1】**存储在矩阵 **M** 中的第 **i** 行。
6.  用数组中的元素 1 初始化两个数组 **arr1[]** 和 **arr2[]** 。
7.  迭代矩阵的每一行 **M** ，使得**arr 1【】**中的每个元素与当前行的每个元素的乘积必须存储在**arr 2【】**中。
8.  完成上述步骤后，复制 arr1[]中 **arr2[]** 的每个元素。
9.  重复以上两个步骤，直到矩阵 **M** 的所有元素都被遍历。
10.  数组 **arr2[]** 包含了所有的数 **N** 的因子。

下面是上述方法的实现:

## C++

```
// C++ program to find the factors
// of large perfect square number
// in O(sqrt(sqrt(N))) time
#include "bits/stdc++.h"
using namespace std;

int MAX = 100000;

// Function that find all the prime
// factors of N
void findFactors(int N)
{
    // Store the sqrt(N) in temp
    int temp = sqrt(N);

    // Initialise factor array with
    // 1 as a factor in it
    int factor[MAX] = { 1 };
    int i, j, k;
    int len1 = 1;

    // Check divisibility by 2
    while (temp % 2 == 0) {

        // Store the factors twice
        factor[len1++] = 2;
        factor[len1++] = 2;

        temp /= 2;
    }

    // Check for other prime
    // factors other than 2
    for (j = 3; j < sqrt(temp); j += 2) {

        // If j is a prime factor
        while (temp % j == 0) {

            // Store the prime
            // factor twice
            factor[len1++] = j;
            factor[len1++] = j;
            temp /= j;
        }
    }

    // If j is prime number left
    // other than 2
    if (temp > 2) {

        // Store j twice
        factor[len1++] = temp;
        factor[len1++] = temp;
    }

    // Initialise Matrix M to
    // to store all the factors
    int M[len1][MAX] = { 0 };

    // tpc for rows
    // tpr for column
    int tpc = 0, tpr = 0;

    // Initialise M[0][0] = 1 as
    // it also factor of N
    M[0][0] = 1;
    j = 1;

    // Traversing factor array
    while (j < len1) {

        // If current and previous
        // factors are not same then
        // move to next row and
        // insert the current factor
        if (factor[j] != factor[j - 1]) {
            tpr++;
            M[tpr][0] = factor[j];
            j++;
            tpc = 1;
        }

        // If current and previous
        // factors are same then,
        // Insert the factor with
        // previous factor inserted
        // in matrix M
        else {
            M[tpr][tpc]
                = M[tpr][tpc - 1] * factor[j];
            j++;
            tpc++;
        }
    }

    // The arr1[] and arr2[] used to
    // store all the factors of N
    int arr1[MAX], arr2[MAX];
    int l1, l2;
    l1 = l2 = 1;

    // Initialise arrays as 1
    arr1[0] = arr2[0] = 1;

    // Traversing the matrix M
    for (i = 1; i < tpr + 1; i++) {

        // Traversing till column
        // element doesn't become 0
        for (j = 0; M[i][j] != 0; j++) {

            // Store the product of
            // every element of current
            // row with every element
            // in arr1[]
            for (k = 0; k < l1; k++) {
                arr2[l2++]
                    = arr1[k] * M[i][j];
            }
        }

        // Copying every element of
        // arr2[] in arr1[]
        for (j = l1; j < l2; j++) {
            arr1[j] = arr2[j];
        }

        // length of arr2[] and arr1[]
        // are equal after copying
        l1 = l2;
    }

    // Print all the factors
    for (i = 0; i < l2; i++) {
        cout << arr2[i] << ' ';
    }
}

// Drivers Code
int main()
{
    int N = 900;
    findFactors(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the factors
// of large perfect square number
// in O(Math.sqrt(Math.sqrt(N))) time
import java.util.*;

class GFG{

static int MAX = 100000;

// Function that find all the prime
// factors of N
static void findFactors(int N)
{
    // Store the Math.sqrt(N) in temp
    int temp = (int) Math.sqrt(N);

    // Initialise factor array with
    // 1 as a factor in it
    int []factor = new int[MAX];
    Arrays.fill(factor, 1);
    int i, j, k;
    int len1 = 1;

    // Check divisibility by 2
    while (temp % 2 == 0) {

        // Store the factors twice
        factor[len1++] = 2;
        factor[len1++] = 2;

        temp /= 2;
    }

    // Check for other prime
    // factors other than 2
    for (j = 3; j < Math.sqrt(temp); j += 2) {

        // If j is a prime factor
        while (temp % j == 0) {

            // Store the prime
            // factor twice
            factor[len1++] = j;
            factor[len1++] = j;
            temp /= j;
        }
    }

    // If j is prime number left
    // other than 2
    if (temp > 2) {

        // Store j twice
        factor[len1++] = temp;
        factor[len1++] = temp;
    }

    // Initialise Matrix M to
    // to store all the factors
    int [][]M = new int[len1][MAX];

    // tpc for rows
    // tpr for column
    int tpc = 0, tpr = 0;

    // Initialise M[0][0] = 1 as
    // it also factor of N
    M[0][0] = 1;
    j = 1;

    // Traversing factor array
    while (j < len1) {

        // If current and previous
        // factors are not same then
        // move to next row and
        // insert the current factor
        if (factor[j] != factor[j - 1]) {
            tpr++;
            M[tpr][0] = factor[j];
            j++;
            tpc = 1;
        }

        // If current and previous
        // factors are same then,
        // Insert the factor with
        // previous factor inserted
        // in matrix M
        else {
            M[tpr][tpc]
                = M[tpr][tpc - 1] * factor[j];
            j++;
            tpc++;
        }
    }

    // The arr1[] and arr2[] used to
    // store all the factors of N
    int []arr1 = new int[MAX];
    int []arr2 = new int[MAX];
    int l1, l2;
    l1 = l2 = 1;

    // Initialise arrays as 1
    arr1[0] = arr2[0] = 1;

    // Traversing the matrix M
    for (i = 1; i < tpr + 1; i++) {

        // Traversing till column
        // element doesn't become 0
        for (j = 0; M[i][j] != 0; j++) {

            // Store the product of
            // every element of current
            // row with every element
            // in arr1[]
            for (k = 0; k < l1; k++) {
                arr2[l2++]
                    = arr1[k] * M[i][j];
            }
        }

        // Copying every element of
        // arr2[] in arr1[]
        for (j = l1; j < l2; j++) {
            arr1[j] = arr2[j];
        }

        // length of arr2[] and arr1[]
        // are equal after copying
        l1 = l2;
    }

    // Print all the factors
    for (i = 0; i < l2; i++) {
        System.out.print(arr2[i] + " ");
    }
}

// Drivers Code
public static void main(String[] args)
{
    int N = 900;
    findFactors(N);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python 3 program to find the factors
# of large perfect square number
# in O(sqrt(sqrt(N))) time

import math

MAX = 100000

# Function that find all the prime
# factors of N
def findFactors( N):

    # Store the sqrt(N) in temp
    temp = int(math.sqrt(N))

    # Initialise factor array with
    # 1 as a factor in it
    factor = [1]*MAX
    len1 = 1

    # Check divisibility by 2
    while (temp % 2 == 0) :

        # Store the factors twice
        factor[len1] = 2
        len1 += 1
        factor[len1] = 2
        len1 += 1
        temp //= 2

    # Check for other prime
    # factors other than 2
    sqt = math.sqrt(temp)

    for j in range(3, math.ceil(sqt), 2):

        # If j is a prime factor
        while (temp % j == 0):

            # Store the prime
            # factor twice
            factor[len1] = j
            len1 += 1
            factor[len1] = j
            len1 += 1
            temp //= j

    # If j is prime number left
    # other than 2
    if (temp > 2) :

        # Store j twice
        factor[len1] = temp
        len1 += 1
        factor[len1] = temp
        len1 += 1

    # Initialise Matrix M to
    # to store all the factors
    M = [ [ 0 for x in range(MAX)] for y in range(len1)]

    # tpc for rows
    # tpr for column
    tpc , tpr = 0 , 0

    # Initialise M[0][0] = 1 as
    # it also factor of N
    M[0][0] = 1
    j = 1

    # Traversing factor array
    while (j < len1):

        # If current and previous
        # factors are not same then
        # move to next row and
        # insert the current factor
        if (factor[j] != factor[j - 1]):
            tpr+=1
            M[tpr][0] = factor[j]
            j += 1
            tpc = 1

        # If current and previous
        # factors are same then,
        # Insert the factor with
        # previous factor inserted
        # in matrix M
        else :
            M[tpr][tpc]= M[tpr][tpc - 1] * factor[j]
            j += 1
            tpc += 1

    # The arr1[] and arr2[] used to
    # store all the factors of N
    arr1 = [0]*MAX
    arr2 = [0]*MAX
    l1 = l2 = 1

    # Initialise arrays as 1
    arr1[0] = 1
    arr2[0] = 1

    # Traversing the matrix M
    # print("tpr ",tpr)
    for i in range(1 , tpr + 1) :

        # Traversing till column
        # element doesn't become 0
        j = 0
        while M[i][j] != 0:

            # Store the product of
            # every element of current
            # row with every element
            # in arr1[]
            for k in range(l1):
                arr2[l2]= arr1[k] * M[i][j]
                l2 += 1

            j += 1

        # Copying every element of
        # arr2[] in arr1[]
        for j in range(l1, l2):
            arr1[j] = arr2[j]

        # length of arr2[] and arr1[]
        # are equal after copying
        l1 = l2

    # Print all the factors
    for i in range(l2):
        print(arr2[i] ,end= " ")

# Drivers Code
if __name__ == "__main__":

    N = 900
    findFactors(N)

# This code is contributed by chitranayal
```

## C#

```
// C# program to find the factors
// of large perfect square number
// in O(Math.Sqrt(Math.Sqrt(N))) time
using System;

class GFG{

static int MAX = 100000;

// Function that find all the prime
// factors of N
static void findFactors(int N)
{
    // Store the Math.Sqrt(N) in temp
    int temp = (int) Math.Sqrt(N);

    // Initialise factor array with
    // 1 as a factor in it
    int []factor = new int[MAX];
    for(int l= 0; l < MAX; l++)
        factor[l] = 1;
    int i, j, k;
    int len1 = 1;

    // Check divisibility by 2
    while (temp % 2 == 0) {

        // Store the factors twice
        factor[len1++] = 2;
        factor[len1++] = 2;

        temp /= 2;
    }

    // Check for other prime
    // factors other than 2
    for (j = 3; j < Math.Sqrt(temp); j += 2) {

        // If j is a prime factor
        while (temp % j == 0) {

            // Store the prime
            // factor twice
            factor[len1++] = j;
            factor[len1++] = j;
            temp /= j;
        }
    }

    // If j is prime number left
    // other than 2
    if (temp > 2) {

        // Store j twice
        factor[len1++] = temp;
        factor[len1++] = temp;
    }

    // Initialise Matrix M to
    // to store all the factors
    int [,]M = new int[len1, MAX];

    // tpc for rows
    // tpr for column
    int tpc = 0, tpr = 0;

    // Initialise M[0,0] = 1 as
    // it also factor of N
    M[0, 0] = 1;
    j = 1;

    // Traversing factor array
    while (j < len1) {

        // If current and previous
        // factors are not same then
        // move to next row and
        // insert the current factor
        if (factor[j] != factor[j - 1]) {
            tpr++;
            M[tpr, 0] = factor[j];
            j++;
            tpc = 1;
        }

        // If current and previous
        // factors are same then,
        // Insert the factor with
        // previous factor inserted
        // in matrix M
        else {
            M[tpr,tpc]
                = M[tpr,tpc - 1] * factor[j];
            j++;
            tpc++;
        }
    }

    // The arr1[] and arr2[] used to
    // store all the factors of N
    int []arr1 = new int[MAX];
    int []arr2 = new int[MAX];
    int l1, l2;
    l1 = l2 = 1;

    // Initialise arrays as 1
    arr1[0] = arr2[0] = 1;

    // Traversing the matrix M
    for (i = 1; i < tpr + 1; i++) {

        // Traversing till column
        // element doesn't become 0
        for (j = 0; M[i, j] != 0; j++) {

            // Store the product of
            // every element of current
            // row with every element
            // in arr1[]
            for (k = 0; k < l1; k++) {
                arr2[l2++]
                    = arr1[k] * M[i, j];
            }
        }

        // Copying every element of
        // arr2[] in arr1[]
        for (j = l1; j < l2; j++) {
            arr1[j] = arr2[j];
        }

        // length of arr2[] and arr1[]
        // are equal after copying
        l1 = l2;
    }

    // Print all the factors
    for (i = 0; i < l2; i++) {
        Console.Write(arr2[i] + " ");
    }
}

// Drivers Code
public static void Main(String[] args)
{
    int N = 900;
    findFactors(N);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program to find the factors
// of large perfect square number
// in O(Math.sqrt(Math.sqrt(N))) time
let MAX = 100000;

// Function that find all the prime
// factors of N
function findFactors(N)
{

    // Store the Math.sqrt(N) in temp
    let temp = Math.floor(Math.sqrt(N));

    // Initialise factor array with
    // 1 as a factor in it
    let factor = new Array(MAX);
    for(let i = 0; i < MAX; i++)
    {
        factor[i] = 1;
    }
    let i, j, k;
    let len1 = 1;

    // Check divisibility by 2
    while (temp % 2 == 0)
    {

        // Store the factors twice
        factor[len1++] = 2;
        factor[len1++] = 2;

        temp = Math.floor(temp / 2);
    }

    // Check for other prime
    // factors other than 2
    for(j = 3; j < Math.sqrt(temp); j += 2)
    {

        // If j is a prime factor
        while (temp % j == 0)
        {

            // Store the prime
            // factor twice
            factor[len1++] = j;
            factor[len1++] = j;
            temp = Math.floor(temp / j);
        }
    }

    // If j is prime number left
    // other than 2
    if (temp > 2)
    {

        // Store j twice
        factor[len1++] = temp;
        factor[len1++] = temp;
    }

    // Initialise Matrix M to
    // to store all the factors
    let M = new Array(len1);
    for(let i = 0; i < len1; i++)
    {
        M[i] = new Array(MAX);
        for(let j = 0; j < MAX; j++)
        {
            M[i][j] = 0;
        }
    }

    // tpc for rows
    // tpr for column
    let tpc = 0, tpr = 0;

    // Initialise M[0][0] = 1 as
    // it also factor of N
    M[0][0] = 1;
    j = 1;

    // Traversing factor array
    while (j < len1)
    {

        // If current and previous
        // factors are not same then
        // move to next row and
        // insert the current factor
        if (factor[j] != factor[j - 1])
        {
            tpr++;
            M[tpr][0] = factor[j];
            j++;
            tpc = 1;
        }

        // If current and previous
        // factors are same then,
        // Insert the factor with
        // previous factor inserted
        // in matrix M
        else
        {
            M[tpr][tpc] = M[tpr][tpc - 1] * factor[j];
            j++;
            tpc++;
        }
    }

    // The arr1[] and arr2[] used to
    // store all the factors of N
    let arr1 = new Array(MAX);
    let arr2 = new Array(MAX);
    for(let i = 0; i < MAX; i++)
    {
        arr1[i] = 0;
        arr2[i] = 0;
    }
    let l1, l2;
    l1 = l2 = 1;

    // Initialise arrays as 1
    arr1[0] = arr2[0] = 1;

    // Traversing the matrix M
    for(i = 1; i < tpr + 1; i++)
    {

        // Traversing till column
        // element doesn't become 0
        for(j = 0; M[i][j] != 0; j++)
        {

            // Store the product of
            // every element of current
            // row with every element
            // in arr1[]
            for(k = 0; k < l1; k++)
            {
                arr2[l2++] = arr1[k] * M[i][j];
            }
        }

        // Copying every element of
        // arr2[] in arr1[]
        for(j = l1; j < l2; j++)
        {
            arr1[j] = arr2[j];
        }

        // length of arr2[] and arr1[]
        // are equal after copying
        l1 = l2;
    }

    // Print all the factors
    for(i = 0; i < l2; i++)
    {
        document.write(arr2[i] + " ");
    }
}

// Driver Code
let N = 900;

findFactors(N);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
1 2 4 3 6 12 9 18 36 5 10 20 15 30 60 45 90 180 25 50 100 75 150 300 225 450 900
```

**时间复杂度:** O(sqrt(sqrt(N)))

**辅助空间:** O(MAX)