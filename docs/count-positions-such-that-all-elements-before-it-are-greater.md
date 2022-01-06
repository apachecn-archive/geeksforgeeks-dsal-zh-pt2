# 计算位置，使其之前的所有元素都大于

> 原文:[https://www . geesforgeks . org/count-positions-这样-它之前的所有元素都大于/](https://www.geeksforgeeks.org/count-positions-such-that-all-elements-before-it-are-greater/)

给定一个数组 **A[]** ，任务是找到数组中位置 I 的个数，使得 A[i]之前的所有元素都大于 A[i]。
**注**:第一个元素总是计算在内，因为它之前没有其他元素。
**例:**

```
Input: N = 4, A[] = {2, 1, 3, 5} 
Output: 2
The valid positions are 1, 2.

Input : N = 3, A[] = {7, 6, 5}
Output: 3
All three positions are valid positions.
```

其思想是每次遍历数组时计算最小元素。即:

*   将第一个元素初始化为最小元素。
*   每次新元素到达时，检查这是否是新的最小值，如果是，增加有效位置的数量，并将最小值初始化为新的最小值。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ Program to count positions such that all
// elements before it are greater

#include <bits/stdc++.h>
using namespace std;

// Function to count positions such that all
// elements before it are greater
int getPositionCount(int a[], int n)
{  
    // Count is initially 1 for the first element
    int count = 1;

    // Initial Minimum
    int min = a[0];

    // Traverse the array
    for(int i=1; i<n; i++)
    {  
        // If current element is new minimum
        if(a[i] <= min)
        {
            // Update minimum
            min = a[i];

            // Increment count
            count++;
        }
    }

    return count;
}

// Driver Code
int main()
{
    int a[] = { 5, 4, 6, 1, 3, 1 };
    int n = sizeof(a) / sizeof(a[0]);

    cout<<getPositionCount(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to count positions such that all
// elements before it are greater
class GFG
{

// Function to count positions such that all
// elements before it are greater
static int getPositionCount(int a[], int n)
{
    // Count is initially 1 for the first element
    int count = 1;

    // Initial Minimum
    int min = a[0];

    // Traverse the array
    for(int i = 1; i < n; i++)
    {
        // If current element is new minimum
        if(a[i] <= min)
        {
            // Update minimum
            min = a[i];

            // Increment count
            count++;
        }
    }

    return count;
}

// Driver Code
public static void main(String[] args)
{
    int a[] = { 5, 4, 6, 1, 3, 1 };
    int n = a.length;

    System.out.print(getPositionCount(a, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 Program to count positions such that all
# elements before it are greater

# Function to count positions such that all
# elements before it are greater
def getPositionCount(a, n) :

    # Count is initially 1 for the first element
    count = 1;

    # Initial Minimum
    min = a[0];

    # Traverse the array
    for i in range(1, n) :

        # If current element is new minimum
        if(a[i] <= min) :

            # Update minimum
            min = a[i];

            # Increment count
            count += 1;

    return count;

# Driver Code
if __name__ == "__main__" :

    a = [ 5, 4, 6, 1, 3, 1 ];
    n = len(a);

    print(getPositionCount(a, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# Program to count positions such that all
// elements before it are greater
using System;

class GFG
{

    // Function to count positions such that all
    // elements before it are greater
    static int getPositionCount(int []a, int n)
    {
        // Count is initially 1 for the first element
        int count = 1;

        // Initial Minimum
        int min = a[0];

        // Traverse the array
        for(int i = 1; i < n; i++)
        {
            // If current element is new minimum
            if(a[i] <= min)
            {
                // Update minimum
                min = a[i];

                // Increment count
                count++;
            }
        }

        return count;
    }

    // Driver Code
    public static void Main()
    {
        int []a = { 5, 4, 6, 1, 3, 1 };
        int n = a.Length;

        Console.WriteLine(getPositionCount(a, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript Program to count positions such that all
// elements before it are greater

// Function to count positions such that all
// elements before it are greater
function getPositionCount(a, n)
{  
    // Count is initially 1 for the first element
    var count = 1;

    // Initial Minimum
    var min = a[0];

    // Traverse the array
    for(var i = 1; i < n; i++)
    {  
        // If current element is new minimum
        if(a[i] <= min)
        {
            // Update minimum
            min = a[i];

            // Increment count
            count++;
        }
    }

    return count;
}

// Driver Code
var a = [5, 4, 6, 1, 3, 1];
var n = a.length;
document.write( getPositionCount(a, n));

// This code is contributed by itsok.
</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(N)