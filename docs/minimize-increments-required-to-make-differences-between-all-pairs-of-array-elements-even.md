# 最小化所有阵列元素对之间的差异所需的增量，甚至

> 原文:[https://www . geeksforgeeks . org/最小化增量-所有数组元素对之间的差异-偶数/](https://www.geeksforgeeks.org/minimize-increments-required-to-make-differences-between-all-pairs-of-array-elements-even/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)、 **arr[]** ，任务是最小化使数组元素的所有差异对相等所需的数组元素增量数。

**示例:**

> **输入:** arr[] = {4，1，2}
> **输出:** 1
> **解释:**
> 
> 操作 1:将 arr[1]增加 1。数组 arr[]修改为{4，2，2}。
> 所有对:(4，2) →差= 2
> (4，2) →差= 2
> (2，2) →差= 0
> 现在，数组元素之间的成对差是偶数。因此，答案是 1。
> 
> **输入:** arr[] = {2，4}
> **输出:** 0
> **说明:**所有数组元素对之间的差异已经是偶数了。因此，答案是 0。

**方法:**给定的问题可以通过观察以下事实来解决:为了使所有数组元素对之间的差异均匀，两个元素必须具有相同的奇偶性。因此，想法是将所有数组元素转换为**偶数**或**奇数**。最小增量数等于偶数和奇数阵列元素的[计数的最小值。](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/) 

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum increments
// required to difference between all
// pairs of array elements even
void minimumOperations(int arr[], int N)
{
    // Store the count of odd
    // and even numbers
    int oddCnt = 0, evenCnt = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        if (arr[i] % 2 == 0) {

            // Increment evenCnt by 1
            evenCnt++;
        }
        else {

            // Increment eveCnt by 1
            oddCnt++;
        }
    }

    // Print the minimum of oddCnt
    // and eveCnt
    cout << min(oddCnt, evenCnt);
}

// Driver Code
int main()
{
    int arr[] = { 4, 1, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);
    minimumOperations(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG
{

  // Function to find the minimum increments
  // required to difference between all
  // pairs of array elements even
  static void minimumOperations(int[] arr, int N)
  {

    // Store the count of odd
    // and even numbers
    int oddCnt = 0, evenCnt = 0;

    // Traverse the array
    for (int i = 0; i < N; i++)
    {
      if (arr[i] % 2 == 0)
      {

        // Increment evenCnt by 1
        evenCnt++;
      }
      else
      {

        // Increment oddCnt by 1
        oddCnt++;
      }
    }

    // Print the minimum of oddCnt
    // and eveCnt
    System.out.print(Math.min(oddCnt, evenCnt));
  }  

  // Driver code
  public static void main(String args[])
  {
    int[] arr = { 4, 1, 2 };
    int N = arr.length;
    minimumOperations(arr, N);
  }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the minimum increments
# required to difference between all
# pairs of array elements even
def minimumOperations(arr, N) :

    # Store the count of odd
    # and even numbers
    oddCnt = 0
    evenCnt = 0

    # Traverse the array
    for i in range(N):
        if (arr[i] % 2 == 0) :

            # Increment evenCnt by 1
            evenCnt += 1

        else :

            # Increment eveCnt by 1
            oddCnt += 1

    # Prthe minimum of oddCnt
    # and eveCnt
    print(min(oddCnt, evenCnt))

# Driver Code
arr = [ 4, 1, 2 ]
N = len(arr)
minimumOperations(arr, N)

# This code is contributed by sanjoy_62.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to find the minimum increments
    // required to difference between all
    // pairs of array elements even
    static void minimumOperations(int[] arr, int N)
    {

        // Store the count of odd
        // and even numbers
        int oddCnt = 0, evenCnt = 0;

        // Traverse the array
        for (int i = 0; i < N; i++)
        {
            if (arr[i] % 2 == 0)
            {

                // Increment evenCnt by 1
                evenCnt++;
            }
            else
            {

                // Increment eveCnt by 1
                oddCnt++;
            }
        }

        // Print the minimum of oddCnt
        // and eveCnt
        Console.Write(Math.Min(oddCnt, evenCnt));
    }  

  // Driver code
  static void Main()
  {
    int[] arr = { 4, 1, 2 };
    int N = arr.Length;
    minimumOperations(arr, N);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
// Java script program for the above approach

// Function to find the minimum increments
// required to difference between all
// pairs of array elements even
function minimumOperations(arr,N)
{

    // Store the count of odd
    // and even numbers
    let oddCnt = 0, evenCnt = 0;

    // Traverse the array
    for (let i = 0; i < N; i++)
    {
    if (arr[i] % 2 == 0)
    {

        // Increment evenCnt by 1
        evenCnt++;
    }
    else
    {

        // Increment oddCnt by 1
        oddCnt++;
    }
    }

    // Print the minimum of oddCnt
    // and eveCnt
    document.write(Math.min(oddCnt, evenCnt));
}

// Driver code

    let arr = [ 4, 1, 2 ];
    let N = arr.length;
    minimumOperations(arr, N);

// This code is contributed by Bobby
</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)