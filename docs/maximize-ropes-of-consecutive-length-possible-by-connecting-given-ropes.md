# 通过连接给定的绳索

最大化连续长度的绳索

> 原文:[https://www . geeksforgeeks . org/通过连接给定绳索来最大化连续长度的绳索/](https://www.geeksforgeeks.org/maximize-ropes-of-consecutive-length-possible-by-connecting-given-ropes/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**，其中每个[数组](https://www.geeksforgeeks.org/array-data-structure/)元素代表一根绳子的长度，任务是找到从长度 **1** 开始连接给定绳子可以创建的连续长度的绳子的数量。

**示例:**

> **输入:** N = 5，A[ ] = {1，2，7，1，1}
> 
> **输出:**5
> T3】说明:T5】长度|绳索
> 1 | [1]
> 2 | [1，1]
> 3 | [1，2]
> 4 | [1，2，1]
> 5 | [1，2，1，1]
> 
> **输入** N = 5，A = {1，3，2，4，2 }
> T3】输出: 12

**方法:**如果我们能够创建范围为**【1，K】**长度的绳索，并且存在长度为 **L** 的剩余绳索，使得 **(L < =** **K+1)** 则我们可以通过将 **L** 长度的绳索添加到范围为**的每根绳索来创建范围为**【1，K+L】**的绳索，从而解决这个问题所以要解决这个问题，首先[对数组](https://www.geeksforgeeks.org/arrays-sort-in-java-with-examples/)进行排序，然后[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，每次检查当前元素是否小于等于我们得到的最大连续长度+ 1。如果发现为真，则将该元素添加到最大连续长度。否则，返回答案。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find maximized count
// of ropes of consecutive length
int maxConsecutiveRopes(int ropes[], int N)
{
    // Stores the maximum count
    // of ropes of consecutive length
    int curSize = 0;

    // Sort the ropes by their length
    sort(ropes, ropes + N);

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If size of the current rope is less
        // than or equal to current maximum
        // possible size + 1, update the
        // range to curSize + ropes[i]

        if (ropes[i] <= curSize + 1) {
            curSize = curSize + ropes[i];
        }

        // If a rope of size (curSize + 1)
        // cannot be obtained
        else
            break;
    }
    return curSize;
}

// Driver Code
int main()
{
    // Input
    int N = 5;
    int ropes[] = { 1, 2, 7, 1, 1 };

    // Function Call
    cout << maxConsecutiveRopes(ropes, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;
class GFG {

    // Function to find maximized count
    // of ropes of consecutive length
    static int maxConsecutiveRope(int ropes[], int N)
    {
        // Stores the maximum count
        // of ropes of consecutive length
        int curSize = 0;

        // Sort the ropes by their length
        Arrays.sort(ropes);

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // If size of the current rope is less
            // than or equal to current maximum
            // possible size + 1, update the
            // range to curSize + ropes[i]

            if (ropes[i] <= curSize + 1) {
                curSize = curSize + ropes[i];
            }

            // If a rope of size (curSize + 1)
            // cannot be obtained
            else
                break;
        }
        return curSize;
    }

    // Driver code
    public static void main(String[] args)
    {
        // Input
        int N = 5;
        int ropes[] = { 1, 2, 7, 1, 1 };

        // Function Call
        System.out.println(
            maxConsecutiveRope(ropes, N));
    }
}
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to find maximized count
# of ropes of consecutive length
def maxConsecutiveRopes(ropes, N):

    # Stores the maximum count
    # of ropes of consecutive length
    curSize = 0

    # Sort the ropes by their length
    ropes = sorted(ropes)

    # Traverse the array
    for i in range(N):

        # If size of the current rope is less
        # than or equal to current maximum
        # possible size + 1, update the
        # range to curSize + ropes[i]
        if (ropes[i] <= curSize + 1):
            curSize = curSize + ropes[i]

        # If a rope of size (curSize + 1)
        # cannot be obtained
        else:
            break

    return curSize

# Driver Code
if __name__ == '__main__':

    # Input
    N = 5
    ropes = [ 1, 2, 7, 1, 1 ]

    # Function Call
    print (maxConsecutiveRopes(ropes, N))

# This code is contributed by mohit kumar 29
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find maximized count
// of ropes of consecutive length
static int maxConsecutiveRope(int[] ropes, int N)
{

    // Stores the maximum count
    // of ropes of consecutive length
    int curSize = 0;

    // Sort the ropes by their length
    Array.Sort(ropes);

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // If size of the current rope is less
        // than or equal to current maximum
        // possible size + 1, update the
        // range to curSize + ropes[i]
        if (ropes[i] <= curSize + 1)
        {
            curSize = curSize + ropes[i];
        }

        // If a rope of size (curSize + 1)
        // cannot be obtained
        else
            break;
    }
    return curSize;
}

// Driver code
public static void Main ()
{

    // Input
    int N = 5;
    int[] ropes = { 1, 2, 7, 1, 1 };

    // Function Call
    Console.WriteLine(maxConsecutiveRope(ropes, N));
}
}

// This code is contributed by souravghosh0416
```

## **java 描述语言**

```
<script>
// Javascript program for the above approach

// Function to find maximized count
// of ropes of consecutive length
function maxConsecutiveRopes(ropes, N)
{
    // Stores the maximum count
    // of ropes of consecutive length
    let curSize = 0;

    // Sort the ropes by their length
    ropes.sort((a, b) => a - b)

    // Traverse the array
    for (let i = 0; i < N; i++) {

        // If size of the current rope is less
        // than or equal to current maximum
        // possible size + 1, update the
        // range to curSize + ropes[i]

        if (ropes[i] <= curSize + 1) {
            curSize = curSize + ropes[i];
        }

        // If a rope of size (curSize + 1)
        // cannot be obtained
        else
            break;
    }
    return curSize;
}

// Driver Code

// Input
let N = 5;
let ropes = [ 1, 2, 7, 1, 1 ];

// Function Call
document.write(maxConsecutiveRopes(ropes, N));

// This contributed by _saurabh_jaiswal
</script>
```

****Output:** 

```
5
```** 

****时间复杂度:**O(N)
T3】辅助空间: O(1)**