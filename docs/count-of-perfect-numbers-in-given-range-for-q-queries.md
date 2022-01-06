# Q 查询给定范围内的完全数计数

> 原文:[https://www . geeksforgeeks . org/q 查询给定范围内的完全数计数/](https://www.geeksforgeeks.org/count-of-perfect-numbers-in-given-range-for-q-queries/)

给定一个由 **N** [对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，其中每一对代表一个形式为 **{L，R}** 的查询，任务是为每个查询找到给定范围内的[完全数](https://www.geeksforgeeks.org/perfect-number/)的计数。

**示例:**

> **输入:** arr[][] = {{1，10}，{10，20}，{20，30 } }
> T3】输出:1 1 1
> T6】解释:
> 
> 1.  查询(1，10):范围内的完全数只有 6。
> 2.  查询(10，20):范围内没有完全数。
> 3.  查询(20，30):范围内的完全数只有 28。
> 
> **输入:** arr[][] = {{1，1000}，{1000，2000}，{2000，3000 }
> T3】输出:3 0 0
> T6】解释:
> 
> 1.  查询(1，1000):范围内的完全数是 6、28 和 496。
> 2.  查询(1000，2000):范围内没有完全数。
> 3.  查询(2000，3000):范围内没有完全数。

**天真方法:**最简单的方法是，在每个查询中遍历范围，检查 [<u>某个数字是否为完全数</u>](https://www.geeksforgeeks.org/perfect-number/) ，然后打印各个查询的范围内完全数的计数。

***时间复杂度:** O(N*M*√M))，其中 M 是范围的最大尺寸。*
***辅助空间:** O(1)*

**高效方法:**上述方法可以通过使用[前缀和数组技术](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)预先存储从 **1** 到每隔一个数字的完全数计数来优化，这导致每个查询的时间计算恒定。按照以下步骤解决问题:

*   通过[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** 找到范围右边界的最大值，并将其存储在一个变量中，比如 **MAX。**
*   初始化一个数组，说出大小为 **MAX+1** 的**前缀[]** ，每个元素的值为 **0** ，其中**前缀【I】**存储到 **i** 的完全数计数。
*   使用变量 **i** 迭代范围**【2，最大】**，并执行以下操作:
    *   将**前缀【I】**更新为**前缀【I-1】**，然后[检查当前整数 **i** 是否为完全数](https://www.geeksforgeeks.org/perfect-number/)，然后将**前缀【I】**增加 **1。**
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并在每次迭代中打印当前范围内的完全数计数，**【L，R】**作为**前缀【R】–前缀【L-1】。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
const int MAX = 100005;

// Function to check whether a number
// is perfect Number
bool isPerfect(long long int N)
{
    // Stores sum of divisors
    long long int sum = 1;

    // Iterate over the range[2, sqrt(N)]
    for (long long int i = 2; i * i <= N; i++) {
        if (N % i == 0) {
            if (i * i != N)
                sum = sum + i + N / i;
            else
                sum = sum + i;
        }
    }
    // If sum of divisors is equal to
    // N, then N is a perfect number
    if (sum == N && N != 1)
        return true;

    return false;
}

// Function to find count of perfect
// numbers in a given range
void Query(int arr[][2], int N)
{
    // Stores the count of perfect Numbers
    // upto a every number less than MAX
    int prefix[MAX + 1] = { 0 };

    // Iterate over the range [1, MAX]
    for (int i = 2; i <= MAX; i++) {
        prefix[i] = prefix[i - 1] + isPerfect(i);
    }

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {
        // Print the count of perfect numbers
        // in the range [arr[i][0], arr[i][1]]
        cout << prefix[arr[i][1]] - prefix[arr[i][0] - 1]
             << " ";
    }
}

// Driver Code
int main()
{
    int arr[][2]
        = { { 1, 1000 }, { 1000, 2000 }, { 2000, 3000 } };
    int N = sizeof(arr) / sizeof(arr[0]);

    Query(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// C++ program for the above approach
import java.util.*;
public class MyClass
{

static int MAX = 100005;

// Function to check whether a number
// is perfect Number
static int isPerfect(long N)
{

    // Stores sum of divisors
    long  sum = 1;

    // Iterate over the range[2, sqrt(N)]
    for (long i = 2; i * i <= N; i++) {
        if (N % i == 0) {
            if (i * i != N)
                sum = sum + i + N / i;
            else
                sum = sum + i;
        }
    }

    // If sum of divisors is equal to
    // N, then N is a perfect number
    if (sum == N && N != 1)
        return 1;

    return 0;
}

// Function to find count of perfect
// numbers in a given range
static void Query(int arr[][], int N)
{

    // Stores the count of perfect Numbers
    // upto a every number less than MAX
    int []prefix = new int [MAX + 1];
    Arrays.fill(prefix,0);

    // Iterate over the range [1, MAX]
    for (int i = 2; i <= MAX; i++) {
        prefix[i] = prefix[i - 1] + isPerfect(i);
    }

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)
    {

        // Print the count of perfect numbers
        // in the range [arr[i][0], arr[i][1]]
       System.out.print( prefix[arr[i][1]] - prefix[arr[i][0] - 1]+ " ");
    }
}

// Driver Code
public static void main(String args[])
{
    int [][]arr = { { 1, 1000 }, { 1000, 2000 }, { 2000, 3000 } };
    int N = arr.length;

    Query(arr, N);
}
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# python 3 program for the above approach
MAX = 100005

from math import sqrt

# Function to check whether a number
# is perfect Number
def isPerfect(N):

    # Stores sum of divisors
    sum = 1

    # Iterate over the range[2, sqrt(N)]
    for i in range(2,int(sqrt(N))+1,1):
        if (N % i == 0):
            if (i * i != N):
                sum = sum + i + N // i
            else:
                sum = sum + i

    # If sum of divisors is equal to
    # N, then N is a perfect number
    if (sum == N and N != 1):
        return True

    return False

# Function to find count of perfect
# numbers in a given range
def Query(arr, N):

    # Stores the count of perfect Numbers
    # upto a every number less than MAX
    prefix = [0 for i in range(MAX + 1)]

    # Iterate over the range [1, MAX]
    for i in range(2,MAX+1,1):
        prefix[i] = prefix[i - 1] + isPerfect(i)

    # Traverse the array arr[]
    for i in range(N):

        # Print the count of perfect numbers
        # in the range [arr[i][0], arr[i][1]]
        print(prefix[arr[i][1]] - prefix[arr[i][0] - 1],end= " ")

# Driver Code
if __name__ == '__main__':
    arr = [[1, 1000],[1000, 2000],[2000, 3000]]
    N = len(arr)
    Query(arr, N)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
public class MyClass {

    static int MAX = 100005;

    // Function to check whether a number
    // is perfect Number
    static int isPerfect(long N)
    {

        // Stores sum of divisors
        long sum = 1;

        // Iterate over the range[2, sqrt(N)]
        for (long i = 2; i * i <= N; i++) {
            if (N % i == 0) {
                if (i * i != N)
                    sum = sum + i + N / i;
                else
                    sum = sum + i;
            }
        }

        // If sum of divisors is equal to
        // N, then N is a perfect number
        if (sum == N && N != 1)
            return 1;

        return 0;
    }

    // Function to find count of perfect
    // numbers in a given range
    static void Query(int[, ] arr, int N)
    {

        // Stores the count of perfect Numbers
        // upto a every number less than MAX
        int[] prefix = new int[MAX + 1];
        // Arrays.fill(prefix,0);

        // Iterate over the range [1, MAX]
        for (int i = 2; i <= MAX; i++) {
            prefix[i] = prefix[i - 1] + isPerfect(i);
        }

        // Traverse the array arr[]
        for (int i = 0; i < N; i++) {

            // Print the count of perfect numbers
            // in the range [arr[i][0], arr[i][1]]
            Console.Write(prefix[arr[i, 1]]
                          - prefix[arr[i, 0] - 1] + " ");
        }
    }

    // Driver Code
    public static void Main()
    {
        int[, ] arr = { { 1, 1000 },
                        { 1000, 2000 },
                        { 2000, 3000 } };
        int N = arr.GetLength(0);

        Query(arr, N);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript program for the above approach

        const MAX = 100005;

        // Function to check whether a number
        // is perfect Number
        function isPerfect(N) {
            // Stores sum of divisors
            let sum = 1;

            // Iterate over the range[2, sqrt(N)]
            for (let i = 2; i * i <= N; i++) {
                if (N % i == 0) {
                    if (i * i != N)
                        sum = sum + i + Math.floor(N / i);
                    else
                        sum = sum + i;
                }
            }
            // If sum of divisors is equal to
            // N, then N is a perfect number
            if (sum == N && N != 1)
                return true;

            return false;
        }

        // Function to find count of perfect
        // numbers in a given range
        function Query(arr, N) {
            // Stores the count of perfect Numbers
            // upto a every number less than MAX
            let prefix = new Array(MAX + 1).fill(0);

            // Iterate over the range [1, MAX]
            for (let i = 2; i <= MAX; i++) {
                prefix[i] = prefix[i - 1] + isPerfect(i);
            }

            // Traverse the array arr[]
            for (let i = 0; i < N; i++) {
                // Print the count of perfect numbers
                // in the range [arr[i][0], arr[i][1]]
                document.write(prefix[arr[i][1]] - prefix[arr[i][0] - 1] + " ");
            }
        }

        // Driver Code

        let arr
            = [[1, 1000], [1000, 2000], [2000, 3000]];
        let N = arr.length;

        Query(arr, N);

    // This code is contributed by Potta Lokesh

    </script>
```

**Output**

```
3 0 0 
```

***时间复杂度:** O(M*√M+ N)，其中 M 为最大右边界。*
***辅助空间:** O(M)*