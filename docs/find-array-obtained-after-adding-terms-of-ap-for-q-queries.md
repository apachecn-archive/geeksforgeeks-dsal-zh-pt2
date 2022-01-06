# 查找 Q 查询添加 AP 项后得到的数组

> 原文:[https://www . geeksforgeeks . org/find-array-add-terms-AP-for-q-query/](https://www.geeksforgeeks.org/find-array-obtained-after-adding-terms-of-ap-for-q-queries/)

给定一个由 **N** 整数和 **Q** 查询组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**，说出 **{L，R，A，d}** 形式的**查询【】【】【】**，使得每个查询代表无限 AP，第一项为 **a** 和公共差 **d** 。任务是在执行给定的查询之后打印更新的数组，从而对于每个查询 **{L，R，A，d}** 在范围**【L，R】**内为每个索引 **i** 添加[算术级数](https://www.geeksforgeeks.org/arithmetic-progression/)至**A【I】**的**(I–L+1)<sup>第</sup>T21】项的值。**

**示例:**

> **输入:** A[]= {5，4，2，8}，Q = 2，Query[][] = {{1，2，1，3}，{1，4，4，1}}
> **输出:** 10 13 8 15
> **解释:**
> 执行的查询如下:
> **查询 1:** 等差数列为{1，4，7，…}。在将级数的第一项添加到索引 1 和级数的第二项添加到索引 2 之后，数组修改为{6，8，2，8}。
> **查询 2:** 等差数列为{4，5，6，7，8，…}。将 4 加到 A[1]，5 加到 A[2]，6 加到 A[3]和 7 加到 A[4]后，数组修改为{10，13，8 15}。
> 因此，得到的数组是{10，13，8 15}。
> 
> **输入:** A[] = {1，2，3，4，5}，Q = 3，Query[][] = {{1，2，1，3}，{1，3，4，1}，{1，4，1，2}}
> **输出:【14 14 11 5**

**方法:**给定的问题可以通过[在每个运算中迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【L，R】**并在每个索引 **i** 处添加给定等差数列的对应项来解决。按照以下步骤解决问题:

*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)、**查询[][]** ，对于每个查询 **{L，R，A，d}** 执行以下步骤:
    *   [使用变量 **j** 在范围**【L–1，R–1】**内遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **A[]，**
        *   将 **a** 的值加到**A【j】**的值上。
        *   将 **a** 的值增加 **d** 。
*   完成以上步骤后，[打印数组](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/) **A[]** 作为结果更新数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to find array after performing
// the given query to the array elements
void addAP(int A[], int Q, int operations[2][4])
{

    // Traverse the given query
    for (int j = 0; j < 2; ++j)
    {
        int L = operations[j][0], R = operations[j][1], a = operations[j][2], d = operations[j][3];
        int curr = a;

        // Traverse the given array
        for(int i = L - 1; i < R; i++){

            // Update the value of A[i]
            A[i] += curr;

            // Update the value of curr
            curr += d;
        }
    }

    // Print the array elements
    for (int i = 0; i < 4; ++i)
        cout << A[i] << " ";
}

// Driver Code
int main() {
    int A[] = {5, 4, 2, 8};
    int Q = 2;
    int Query[2][4] = {{1, 2, 1, 3}, {1, 4, 4, 1}};

    // Function Call
    addAP(A, Q, Query);
    return 0;
}

// This code is contributed by shubhamsingh10.
```

## C

```
// C program for the above approach
#include <stdio.h>

// Function to find array after performing
// the given query to the array elements
void addAP(int A[], int Q, int operations[2][4])
{

    // Traverse the given query
    for (int j = 0; j < 2; ++j)
    {
        int L = operations[j][0], R = operations[j][1], a = operations[j][2], d = operations[j][3];
        int curr = a;

        // Traverse the given array
        for(int i = L - 1; i < R; i++){

            // Update the value of A[i]
            A[i] += curr;

            // Update the value of curr
            curr += d;
        }
    }

    // Print the array elements
    for (int i = 0; i < 4; ++i)
        printf("%d ", A[i]);
}

// Driver Code
int main() {
    int A[] = {5, 4, 2, 8};
    int Q = 2;
    int Query[2][4] = {{1, 2, 1, 3}, {1, 4, 4, 1}};

    // Function Call
    addAP(A, Q, Query);
    return 0;
}

// This code is contributed by shubhamsingh10.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    // Function to find array after performing
    // the given query to the array elements
    public static void addAP(int A[], int Q, int[][] operations)
    {

        // Traverse the given query
        for (int j = 0; j < 2; ++j) {
            int L = operations[j][0], R = operations[j][1],
          a = operations[j][2], d = operations[j][3];
            int curr = a;

            // Traverse the given array
            for (int i = L - 1; i < R; i++) {

                // Update the value of A[i]
                A[i] += curr;

                // Update the value of curr
                curr += d;
            }
        }

        // Print the array elements
        for (int i = 0; i < 4; ++i)
            System.out.print(A[i] + " ");
    }

    // Driver Code
    public static void main(String args[])
    {
        int A[] = { 5, 4, 2, 8 };
        int Q = 2;
        int query[][] = { { 1, 2, 1, 3 }, { 1, 4, 4, 1 } };

        // Function Call
        addAP(A, Q, query);
    }
}

// This code is contributed by _saurabh_jaiswal
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find array after performing
# the given query to the array elements
def addAP(A, Q, operations):

    # Traverse the given query
    for L, R, a, d in operations:

        curr = a

        # Traverse the given array
        for i in range(L-1, R):

            # Update the value of A[i]
            A[i] += curr

            # Update the value of curr
            curr += d

    # Print the array elements
    for i in A:
        print(i, end =' ')

# Driver Code

A = [5, 4, 2, 8]
Q = 2
Query = [(1, 2, 1, 3), (1, 4, 4, 1)]

# Function Call
addAP(A, Q, Query)
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find array after performing
// the given query to the array elements
public static void addAP(int[] A, int Q,
                         int[,] operations)
{

    // Traverse the given query
    for(int j = 0; j < 2; ++j)
    {
        int L = operations[j, 0], R = operations[j, 1],
            a = operations[j, 2], d = operations[j, 3];
        int curr = a;

        // Traverse the given array
        for(int i = L - 1; i < R; i++)
        {

            // Update the value of A[i]
            A[i] += curr;

            // Update the value of curr
            curr += d;
        }
    }

    // Print the array elements
    for(int i = 0; i < 4; ++i)
        Console.Write(A[i] + " ");
}

// Driver code
public static void Main(string[] args)
{
    int[] A = { 5, 4, 2, 8 };
    int Q = 2;
    int[,] query = { { 1, 2, 1, 3 },
                     { 1, 4, 4, 1 } };

    // Function Call
    addAP(A, Q, query);
}
}

// This code is contributed by avijitmondal1998
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find array after performing
// the given query to the array elements
function addAP(A, Q, operations)
{

    // Traverse the given query
    for( let Q of operations)
    {
        let L = Q[0], R = Q[1], a = Q[2], d = Q[3]
        curr = a

        // Traverse the given array
        for(let i = L - 1; i < R; i++){

            // Update the value of A[i]
            A[i] += curr

            // Update the value of curr
            curr += d
        }
    }

    // Print the array elements
    for (let i of A){
        document.write(i + " ")
    }
}

// Driver Code
let A = [5, 4, 2, 8]
let Q = 2
let Query = [[1, 2, 1, 3], [1, 4, 4, 1]]

// Function Call
addAP(A, Q, Query)

// Thi code is contributed by gfgking.
</script>
```

**Output**

```
10 13 8 15 
```

***时间复杂度:** O(N*Q)*
***辅助空间:** O(1)*