# 根据给定的条件，尽可能准确地访问给定图中的每个节点一次

> 原文:[https://www . geesforgeks . org/find-如果可能的话-访问给定图中的每个节点-基于给定条件精确一次/](https://www.geeksforgeeks.org/find-if-possible-to-visit-every-nodes-in-given-graph-exactly-once-based-on-given-conditions/)

给定一个具有带 **2*N-1** 边的 **N+1** 节点和一个[布尔数组](https://www.geeksforgeeks.org/a-boolean-array-puzzle/)**arr【】**的[图，任务是找出是否可以访问每个节点一次并打印任何一条可能的路径。还知道如果**arr【I】**为 **0** 则 **N-1** 边转到第 I 至(i+1)个节点，其余边转到第 I 至(n+1)个节点，否则 **(n+1)转到第 I 个**。](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)

**示例:**

> **输入:** N = 3，arr = {0，1，0}
> **输出:**【1，2，3，4】
> **解释:**
> 从给定的数据来看，边将:
> 1->2
> 2->3
> 1->4
> 4->2
> 3->4
> 
> 因此，可以遵循以下路径:1 -> 2 -> 3 -> 4
> 
> **输入:** N = 4，arr = {0，1，1，1}
> **输出:**【1，4，2，3】

**逼近:**这个问题可以用[贪婪逼近](https://www.geeksforgeeks.org/greedy-algorithms/)结合一些观察来解决。观察结果如下:

*   如果 **arr[1]是 1** ，那么沿着路径**【N+1->1->2……..->N】**。
*   如果**arr【N】为 0** ，则沿着**【1->2->……。->N->N+1】**。
*   如果 **arr[1]为 0，arr[N]为 1** ，则必须存在整数 **i (1 ≤ i < N)** ，其中 **arr[i] =0，arr[i+1] = 1** ，则路径**【1->2->⋯->I->n+1->I+1->I+2->⋯n】**
*   上一步证明了这个图中总是存在 [**哈密顿路径**](https://www.geeksforgeeks.org/hamiltonian-path-using-dynamic-programming/) 。

下面是上述方法的实现:

## C++

```
// C++ program for above approach.
#include <bits/stdc++.h>
using namespace std;

// Function to find print path
void findpath(int N, int a[])
{

    // If a[0] is 1
    if (a[0]) {

        // Printing path
        cout <<" "<< N + 1;
        for (int i = 1; i <= N; i++)
            cout <<" " << i;
        return;
    }

    // Seeking for a[i] = 0 and a[i+1] = 1
    for (int i = 0; i < N - 1; i++) {
        if (!a[i] && a[i + 1]) {

            // Printing path
            for (int j = 1; j <= i; j++)
                cout <<" "<< j;
            cout <<" "<< N + 1;
            for (int j = i + 1; j <= N; j++)
                cout <<" "<< j;
            return;
        }
    }

    // If a[N-1] = 0
    for (int i = 1; i <= N; i++)
        cout <<" "<< i;
    cout <<" "<< N + 1;
}

// Driver Code
int main()
{

    // Given Input
    int N = 3, arr[] = { 0, 1, 0 };

    // Function Call
    findpath(N, arr);
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C++ program for above approach.
#include <bits/stdc++.h>
using namespace std;

// Function to find print path
void findpath(int N, int a[])
{

    // If a[0] is 1
    if (a[0]) {

        // Printing path
        printf("%d ", N + 1);
        for (int i = 1; i <= N; i++)
            printf("%d ", i);
        return;
    }

    // Seeking for a[i] = 0 and a[i+1] = 1
    for (int i = 0; i < N - 1; i++) {
        if (!a[i] && a[i + 1]) {

            // Printing path
            for (int j = 1; j <= i; j++)
                printf("%d ", j);
            printf("%d ", N + 1);
            for (int j = i + 1; j <= N; j++)
                printf("%d ", j);
            return;
        }
    }

    // If a[N-1] = 0
    for (int i = 1; i <= N; i++)
        printf("%d ", i);
    printf("%d ", N + 1);
}

// Driver Code
int main()
{

    // Given Input
    int N = 3, arr[] = { 0, 1, 0 };

    // Function Call
    findpath(N, arr);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG {

    // Function to find print path
    static void findpath(int N, int a[])
    {

        // If a[0] is 1
        if (a[0] == 1) {

            // Printing path
            System.out.print((N + 1) + " ");
            for (int i = 1; i <= N; i++)
                System.out.print((i) + " ");
            return;
        }

        // Seeking for a[i] = 0 and a[i+1] = 1
        for (int i = 0; i < N - 1; i++) {
            if (a[i] == 0 && a[i + 1] == 1) {

                // Printing path
                for (int j = 1; j <= i; j++)
                    System.out.print((j) + " ");
                System.out.print((N + 1) + " ");
                for (int j = i + 1; j <= N; j++)
                    System.out.print((j) + " ");
                return;
            }
        }

        // If a[N-1] = 0
        for (int i = 1; i <= N; i++)
            System.out.print((i) + " ");
        System.out.print((N + 1) + " ");
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 3, arr[] = { 0, 1, 0 };

        // Function Call
        findpath(N, arr);
    }
}

// This code is contributed by dwivediyash
```

## 蟒蛇 3

```
# Python 3 program for above approach.

# Function to find print path
def findpath(N, a):
    # If a[0] is 1
    if (a[0]):
        # Printing path
        print(N + 1)
        for i in range(1,N+1,1):
            print(i,end = " ")
        return

    # Seeking for a[i] = 0 and a[i+1] = 1
    for i in range(N - 1):
        if (a[i]==0 and a[i + 1]):

            # Printing path
            for j in range(1,i+1,1):
                print(j,end = " ")
            print(N + 1,end = " ");
            for j in range(i + 1,N+1,1):
                print(j,end = " ")
            return

    # If a[N-1] = 0
    for i in range(1,N+1,1):
        print(i,end = " ")
    print(N + 1,end = " ")

# Driver Code
if __name__ == '__main__':
    # Given Input
    N = 3
    arr = [0, 1, 0]

    # Function Call
    findpath(N, arr)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for above approach.
using System;

class GFG{

// Function to find print path
static void findpath(int N, int []a)
{

    // If a[0] is 1
    if (a[0]!=0) {

        // Printing path
        Console.Write(N + 1);
        for (int i = 1; i <= N; i++)
            Console.Write(i+ " ");
        return;
    }

    // Seeking for a[i] = 0 and a[i+1] = 1
    for (int i = 0; i < N - 1; i++) {
        if (a[i]==0 && a[i + 1] !=0) {

            // Printing path
            for (int j = 1; j <= i; j++)
                Console.Write(j+" ");
            Console.Write(N + 1 + " ");
            for (int j = i + 1; j <= N; j++)
                Console.Write(j + " ");
            return;
        }
    }

    // If a[N-1] = 0
    for (int i = 1; i <= N; i++)
        Console.Write(i+" ");
    Console.Write(N + 1 + " ");
}

// Driver Code
public static void Main()
{

    // Given Input
    int N = 3;
    int []arr = { 0, 1, 0 };

    // Function Call
    findpath(N, arr);
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find print path
        function findpath(N, a) {

            // If a[0] is 1
            if (a[0]) {

                // Printing path
                document.write(N + 1);
                for (let i = 1; i <= N; i++)
                    document.write(i);
                return;
            }

            // Seeking for a[i] = 0 and a[i+1] = 1
            for (let i = 0; i < N - 1; i++) {
                if (!a[i] && a[i + 1]) {

                    // Printing path
                    for (let j = 1; j <= i; j++)
                        document.write(j+" ");
                    document.write(N + 1+" ");
                    for (let j = i + 1; j <= N; j++)
                        document.write(j+" ");
                    return;
                }
            }

            // If a[N-1] = 0
            for (let i = 1; i <= N; i++)
                document.write(i+" ");
            document.write(N + 1+" ");
        }

        // Driver Code

        // Given Input
        let N = 3, arr = [0, 1, 0];

        // Function Call
        findpath(N, arr);

// This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
4 1 2 3
```

***时间复杂度:*** O(N)
***辅助空间:*** O(1)