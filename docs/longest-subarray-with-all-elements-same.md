# 所有元素相同的最长子阵列

> 原文:[https://www . geeksforgeeks . org/最长-包含所有元素的子阵列-相同/](https://www.geeksforgeeks.org/longest-subarray-with-all-elements-same/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是找到由所有相等元素组成的最大子数组。
**例:**

> **输入:** arr[] = {1，1，2，2，2，3，3 }；
> **输出:** 3
> **说明:**
> 等元素最长的子阵为{2，2，2}
> **输入:** arr[] = {1，1，2，2，2，3，3，3，3 }；
> **输出:** 4
> **说明:**
> 元素相等的最长子阵列为{3，3，3，3}

**方法:**思路是遍历数组，检查当前元素是否等于上一个元素。如果是，则将最长子阵列的长度增加 1。否则，当前最长的子阵列等于 1。此外，在迭代的每一步用相等的元素更新最长的子阵列。
以下是上述办法的实施情况:

## C++

```
// C++ program to find largest
// subarray with all equal elements.

#include <bits/stdc++.h>
using namespace std;

// Function to find largest sub
// array with all equal elements.
int subarray(int arr[], int n)
{

    int ans = 1, temp = 1;

    // Traverse the array
    for (int i = 1; i < n; i++) {

        // If element is same as
        // previous increment temp value
        if (arr[i] == arr[i - 1]) {
            ++temp;
        }
        else {
            ans = max(ans, temp);
            temp = 1;
        }
    }
    ans = max(ans, temp);

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 2, 2, 1, 1,
                  2, 2, 2, 3, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << subarray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find largest
// subarray with all equal elements.
import java.util.*;

class GFG{

// Function to find largest sub
// array with all equal elements.
static int subarray(int arr[], int n)
{
    int ans = 1, temp = 1;

    // Traverse the array
    for(int i = 1; i < n; i++)
    {

       // If element is same as
       // previous increment temp value
       if (arr[i] == arr[i - 1])
       {
           ++temp;
       }
       else
       {
           ans = Math.max(ans, temp);
           temp = 1;
       }
    }
    ans = Math.max(ans, temp);

    // Return the required answer
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 2, 1, 1, 2,
                  2, 2, 3, 3 };
    int n = arr.length;

    // Function call
    System.out.print(subarray(arr, n));
}
}

// This code is contributed by AbhiThakur
```

## 蟒蛇 3

```
# Python3 program to find largest
# subarray with all equal elements.

# Function to find largest sub
# array with all equal elements.
def subarray(arr, n):

    ans, temp = 1, 1

    # Traverse the array
    for i in range(1, n):

        # If element is same as previous
        # increment temp value
        if arr[i] == arr[i - 1]:
            temp = temp + 1
        else:
            ans = max(ans, temp)
            temp = 1

    ans = max(ans, temp)

    # Return the required answer
    return ans

# Driver code
arr = [ 2, 2, 1, 1, 2,
        2, 2, 3, 3 ]
n = len(arr)

# Function call
print(subarray(arr, n))

# This code is contributed by jrishabh99
```

## C#

```
// C# program to find largest
// subarray with all equal elements.
using System;
class GFG{

// Function to find largest sub
// array with all equal elements.
static int subarray(int[] arr, int n)
{
    int ans = 1, temp = 1;

    // Traverse the array
    for(int i = 1; i < n; i++)
    {

       // If element is same as
       // previous increment temp value
       if (arr[i] == arr[i - 1])
       {
           ++temp;
       }
       else
       {
           ans = Math.Max(ans, temp);
           temp = 1;
       }
    }
    ans = Math.Max(ans, temp);

    // Return the required answer
    return ans;
}

// Driver code
public static void Main()
{
    int[] arr = { 2, 2, 1, 1, 2,
                  2, 2, 3, 3 };
    int n = arr.Length;

    // Function call
    Console.Write(subarray(arr, n));
}
}

// This code is contributed by Nidhi_biet
```

## java 描述语言

```
<script>

// Javascript program to find largest
// subarray with all equal elements.

// Function to find largest sub
// array with all equal elements.
function subarray(arr, n)
{

    var ans = 1, temp = 1;

    // Traverse the array
    for (var i = 1; i < n; i++) {

        // If element is same as
        // previous increment temp value
        if (arr[i] == arr[i - 1]) {
            ++temp;
        }
        else {
            ans = Math.max(ans, temp);
            temp = 1;
        }
    }
    ans = Math.max(ans, temp);

    // Return the required answer
    return ans;
}

// Driver code
var arr = [ 2, 2, 1, 1,
              2, 2, 2, 3, 3 ];
var n = arr.length;

// Function call
document.write( subarray(arr, n));

</script>
```

**Output:** 

```
3
```

***时间复杂度**:O(N)*T4】