# 从 arr[i]跳到 arr[arr[i]]

到达数组末尾的跳跃次数

> 原文:[https://www . geeksforgeeks . org/通过从 arri 到 arrarri 的跳跃到达数组末尾的跳跃计数/](https://www.geeksforgeeks.org/count-of-jumps-to-reach-the-end-of-array-by-jumping-from-arri-to-arrarri/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是为作为范围**【0，N】**中起始索引的 **i** 的所有值找到逃离数组**arr【】**所需的跳跃次数，其中从**arr【I】到**的唯一可能跳跃是**arr【arr[I]】**和逃离数组意味着 **arr**

**示例**:

> ***输入** : arr[] =* {2，3，4，1，10}
> ***输出** : 3 -1 2 -1 1*
> ***解释** :*
> 
> 1.  *对于 i = 0，最初当前索引 x 为 0。第一次跳转后，当前索引变为 x = arr[x] = arr[0] = 2。同样，第二次跳转后，当前索引变为 x = arr[2] = 4。第三次跳转后 x = arr[4] =10，大于数组大小。因此，转义数组所需的步骤数是 3。*
> 2.  *对于 i = 1，最初当前索引 x 为 1。第一次跳跃后，x = arr[1] = 3。在第二次跳转之后，x = arr[3] = 1，它已经被访问过，因此形成了一个闭环。因此，无法从索引 1 中转义数组。*
> 
> ***输入** : arr[] =* {3，12，2，7，4，10，35，5，9，27}
> ***输出**:*4 1-1 3-1 1 2 2 1

**逼近:**给定问题可以借助[递归](https://www.geeksforgeeks.org/recursion/)求解。以下是要遵循的步骤:

*   创建一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **访问过【】**，存储当前索引是否已经被访问过。最初，**访问了= {0}** 。
*   创建一个数组 **cntJumps[]** ，该数组存储范围[0，N]内所有索引所需的跳转次数。最初，**碳跳跃= {0}** 。
*   创建一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/) **countJumps()** ，计算从当前索引中转义数组所需的跳转次数。
*   在函数 **countJumps()** 中，如果已经计算出当前索引的答案，返回答案 else 如果已经访问了当前节点，则返回 **-1** 否则如果从当前索引跳转后数组将被转义，则返回 **1** 。
*   [递归](https://www.geeksforgeeks.org/recursion/)计算当前跳转后的跳转次数，即***count jumps(I)= 1+count jumps(arr[I])***。将答案存储在数组**中。**
*   [打印数组](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/)**cntJumps【】**，为必选答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Stores the number of jumps
int cntJumps[100];

// Stores if the current index is visited
int visited[100];

// Recursive function to find the number of
// jumps to escape the array from index i
int countJumps(int arr[], int N, int i)
{
    // If the answer for the current index is
    // already calculated
    if (cntJumps[i] != 0) {
        return cntJumps[i];
    }

    // If the current index is already visited
    if (visited[i]) {
        return -1;
    }

    // Mark current index as visited
    visited[i] = true;

    // If the array is escaped after the jump
    // from the current index
    if (arr[i] >= N) {
        return cntJumps[i] = 1;
    }

    // Recursive call for the next jump
    int val = countJumps(arr, N, arr[i]);

    // If it is impossible to escape the array
    if (val == -1)
        cntJumps[i] = -1;
    else
        cntJumps[i] = 1 + val;

    // Return answer
    return cntJumps[i];
}

// Function to print the number of jumps
// required to escape the array from
// ith index for all values of i in [0, N)
void printCountJumps(int arr[], int N)
{
    // Initialize visited array as 0
    memset(visited, 0, sizeof(visited));

    // Initialize cntJump array by 0
    memset(cntJumps, 0, sizeof(cntJumps));

    // Loop to iterate over all values of i
    for (int i = 0; i < N; i++) {

        // If the index i is not visited already
        if (!visited[i]) {
            countJumps(arr, N, i);
        }
    }

    // Print Answer
    for (int i = 0; i < N; i++) {
        cout << cntJumps[i] << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 3, 12, 2, 7, 4, 10, 35, 5, 9, 27 };
    int N = sizeof(arr) / sizeof(arr[0]);

    printCountJumps(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

public class GFG {

// Stores the number of jumps
static int cntJumps[] = new int[100];

// Stores if the current index is visited
static int visited[] = new int[100];

// Recursive function to find the number of
// jumps to escape the array from index i
static int countJumps(int arr[], int N, int i)
{
    // If the answer for the current index is
    // already calculated
    if (cntJumps[i] != 0) {
        return cntJumps[i];
    }

    // If the current index is already visited
    if (visited[i] != 0) {
        return -1;
    }

    // Mark current index as visited
    visited[i] = 1;

    // If the array is escaped after the jump
    // from the current index
    if (arr[i] >= N) {
        cntJumps[i] = 1;
        return cntJumps[i];
    }

    // Recursive call for the next jump
    int val = countJumps(arr, N, arr[i]);

    // If it is impossible to escape the array
    if (val == -1)
        cntJumps[i] = -1;
    else
        cntJumps[i] = 1 + val;

    // Return answer
    return cntJumps[i];
}

// Function to print the number of jumps
// required to escape the array from
// ith index for all values of i in [0, N)
static void printCountJumps(int arr[], int N)
{
    // Initialize visited array as 0
    for (int i = 0; i < visited.length; i++)
        visited[i] = 0;

    // Initialize cntJump array by 0
    for (int i = 0; i < cntJumps.length; i++)
        cntJumps[i] = 0;

    // Loop to iterate over all values of i
    for (int i = 0; i < N; i++) {

        // If the index i is not visited already
        if (visited[i] == 0) {
            countJumps(arr, N, i);
        }
    }

    // Print Answer
    for (int i = 0; i < N; i++) {
        System.out.print(cntJumps[i] + " ");
    }
}

    // Driver Code
    public static void main (String[] args)
    {
        int arr[] = { 3, 12, 2, 7, 4, 10, 35, 5, 9, 27 };
        int N = arr.length;

        printCountJumps(arr, N);

    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python program for the above approach

# Stores the number of jumps
cntJumps = [0 for _ in range(100)]

# Stores if the current index is visited
visited = [0 for _ in range(100)]

# Recursive function to find the number of
# jumps to escape the array from index i
def countJumps(arr, N, i):
    global visited
    global cntJumps

    # If the answer for the current index is
    # already calculated
    if (cntJumps[i] != 0):
        return cntJumps[i]

        # If the current index is already visited
    if (visited[i]):
        return -1

        # Mark current index as visited
    visited[i] = True

    # If the array is escaped after the jump
    # from the current index
    if (arr[i] >= N):
        cntJumps[i] = 1
        return cntJumps[i]

        # Recursive call for the next jump
    val = countJumps(arr, N, arr[i])

    # If it is impossible to escape the array
    if (val == -1):
        cntJumps[i] = -1
    else:
        cntJumps[i] = 1 + val

        # Return answer
    return cntJumps[i]

# Function to print the number of jumps
# required to escape the array from
# ith index for all values of i in [0, N)
def printCountJumps(arr,  N):

        # Loop to iterate over all values of i
    for i in range(0, N):

        # If the index i is not visited already
        if (not visited[i]):
            countJumps(arr, N, i)

    # Print Answer
    for i in range(0, N):
        print(cntJumps[i], end=" ")

# Driver Code
if __name__ == "__main__":

    arr = [3, 12, 2, 7, 4, 10, 35, 5, 9, 27]
    N = len(arr)
    printCountJumps(arr, N)

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;

public class GFG {

// Stores the number of jumps
static int []cntJumps = new int[100];

// Stores if the current index is visited
static int []visited = new int[100];

// Recursive function to find the number of
// jumps to escape the array from index i
static int countJumps(int []arr, int N, int i)
{

    // If the answer for the current index is
    // already calculated
    if (cntJumps[i] != 0) {
        return cntJumps[i];
    }

    // If the current index is already visited
    if (visited[i] != 0) {
        return -1;
    }

    // Mark current index as visited
    visited[i] = 1;

    // If the array is escaped after the jump
    // from the current index
    if (arr[i] >= N) {
        cntJumps[i] = 1;
        return cntJumps[i];
    }

    // Recursive call for the next jump
    int val = countJumps(arr, N, arr[i]);

    // If it is impossible to escape the array
    if (val == -1)
        cntJumps[i] = -1;
    else
        cntJumps[i] = 1 + val;

    // Return answer
    return cntJumps[i];
}

// Function to print the number of jumps
// required to escape the array from
// ith index for all values of i in [0, N)
static void printCountJumps(int []arr, int N)
{

    // Initialize visited array as 0
    for (int i = 0; i < visited.Length; i++)
        visited[i] = 0;

    // Initialize cntJump array by 0
    for (int i = 0; i < cntJumps.Length; i++)
        cntJumps[i] = 0;

    // Loop to iterate over all values of i
    for (int i = 0; i < N; i++) {

        // If the index i is not visited already
        if (visited[i] == 0) {
            countJumps(arr, N, i);
        }
    }

    // Print Answer
    for (int i = 0; i < N; i++) {
        Console.Write(cntJumps[i] + " ");
    }
}

    // Driver Code
    public static void Main (string[] args)
    {
        int []arr = { 3, 12, 2, 7, 4, 10, 35, 5, 9, 27 };
        int N = arr.Length;

        printCountJumps(arr, N);

    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Stores the number of jumps
let cntJumps = new Array(100);

// Stores if the current index is visited
let visited = new Array(100);

// Recursive function to find the number of
// jumps to escape the array from index i
function countJumps(arr, N, i)
{

  // If the answer for the current index is
  // already calculated
  if (cntJumps[i] != 0) {
    return cntJumps[i];
  }

  // If the current index is already visited
  if (visited[i]) {
    return -1;
  }

  // Mark current index as visited
  visited[i] = true;

  // If the array is escaped after the jump
  // from the current index
  if (arr[i] >= N) {
    return (cntJumps[i] = 1);
  }

  // Recursive call for the next jump
  let val = countJumps(arr, N, arr[i]);

  // If it is impossible to escape the array
  if (val == -1) cntJumps[i] = -1;
  else cntJumps[i] = 1 + val;

  // Return answer
  return cntJumps[i];
}

// Function to print the number of jumps
// required to escape the array from
// ith index for all values of i in [0, N)
function printCountJumps(arr, N) {
  // Initialize visited array as 0
  visited.fill(0);

  // Initialize cntJump array by 0
  cntJumps.fill(0);

  // Loop to iterate over all values of i
  for (let i = 0; i < N; i++) {
    // If the index i is not visited already
    if (!visited[i]) {
      countJumps(arr, N, i);
    }
  }

  // Print Answer
  for (let i = 0; i < N; i++) {
    document.write(cntJumps[i] + " ");
  }
}

// Driver Code

let arr = [3, 12, 2, 7, 4, 10, 35, 5, 9, 27];
let N = arr.length;

printCountJumps(arr, N);

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output:** 

```
4 1 -1 3 -1 1 1 2 2 1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)