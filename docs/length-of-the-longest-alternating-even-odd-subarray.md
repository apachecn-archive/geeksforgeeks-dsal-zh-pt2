# 最长交替偶奇子阵列的长度

> 原文:[https://www . geesforgeks . org/最长交替偶奇子阵长度/](https://www.geeksforgeeks.org/length-of-the-longest-alternating-even-odd-subarray/)

给定一个由 N 个整数组成的**数组，任务是找出数组中最长的交替偶奇子数组的长度。
**例:**** 

> **输入:** a[] = {1，2，3，4，5，7，9}
> **输出:** 5
> **解释:**
> 子阵列{1，2，3，4，5}具有交替的偶、奇元素。
> **输入:** a[] = {1，3，5}
> **输出:** 0
> **解释:**
> 不可能有这样的交替顺序。

**方法:**幼稚方法

**说明:**考虑每个子阵，求偶、奇子阵的长度

## C++

```
#include <iostream>
using namespace std;

// Function to find the longest subarray
int longestEvenOddSubarray(int a[], int n)
{
    // Length of longest
    // alternating subarray
    int ans = 0;

    // Iterate in the array
    for (int i = 0; i < n ; i++) {
        int cnt = 1;
        // Iterate for every  subarray
        for (int j = i + 1; j < n; j++) {
            if ((a[j - 1] % 2 == 0 && a[j] % 2 != 0)
                || (a[j - 1] % 2 != 0 && a[j] % 2 == 0))
                cnt++;
            else
                break;
        }
        // store max count
        ans = max(ans, cnt);
    }

    return ans;
}

/* Driver code*/
int main()
{
    int a[] = { 1, 2, 3, 4, 5, 7, 8 };

    int n = sizeof(a) / sizeof(a[0]);

    cout << longestEvenOddSubarray(a, n);
    return 0;
}
```

**Output**

```
5
```

方法 2:

**方法:**要解决上面提到的问题，我们必须观察到两个偶数的**和是偶数，**两个奇数**的和是偶数，但是一个偶数和一个奇数**的和是奇数。

*   初始初始化 *cnt* 一个计数器，将长度存储为 1。
*   迭代数组元素，检查连续元素是否有奇数和。
*   如果 cnt 有一个奇数和，则将它增加 1。
*   如果它没有奇数和，则用 1 重新初始化 cnt。

以下是上述方法的实现:

## C++

```
// C++ program to find the Length of the
// longest alternating even odd subarray

#include <bits/stdc++.h>
using namespace std;

// Function to find the longest subarray
int longestEvenOddSubarray(int a[], int n)
{
    // Length of longest
    // alternating subarray
    int longest = 1;
    int cnt = 1;

    // Iterate in the array
    for (int i = 0; i < n - 1; i++) {

        // increment count if consecutive
        // elements has an odd sum
        if ((a[i] + a[i + 1]) % 2 == 1) {
            cnt++;
        }
        else {
            // Store maximum count in longest
            longest = max(longest, cnt);

            // Reinitialize cnt as 1 consecutive
            // elements does not have an odd sum
            cnt = 1;
        }
    }

    // Length of 'longest' can never be 1
    // since even odd has to occur in pair or more
    // so return 0 if longest = 1
    if (longest == 1)
        return 0;

    return max(cnt, longest);
}

/* Driver code*/
int main()
{
    int a[] = { 1, 2, 3, 4, 5, 7, 8 };

    int n = sizeof(a) / sizeof(a[0]);

    cout << longestEvenOddSubarray(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the Length of the
// longest alternating even odd subarray
import java.util.*;
class GFG{

// Function to find the longest subarray
static int longestEvenOddSubarray(int a[], int n)
{
    // Length of longest
    // alternating subarray
    int longest = 1;
    int cnt = 1;

    // Iterate in the array
    for (int i = 0; i < n - 1; i++)
    {

        // increment count if consecutive
        // elements has an odd sum
        if ((a[i] + a[i + 1]) % 2 == 1)
        {
            cnt++;
        }
        else
        {
            // Store maximum count in longest
            longest = Math.max(longest, cnt);

            // Reinitialize cnt as 1 consecutive
            // elements does not have an odd sum
            cnt = 1;
        }
    }

    // Length of 'longest' can never be 1
    // since even odd has to occur in pair or more
    // so return 0 if longest = 1
    if (longest == 1)
        return 0;

    return Math.max(cnt, longest);
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 1, 2, 3, 4, 5, 7, 8 };

    int n = a.length;

    System.out.println(longestEvenOddSubarray(a, n));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to find the length of the
# longest alternating even odd subarray

# Function to find the longest subarray
def longestEvenOddSubarray(arr, n):

    # Length of longest
    # alternating subarray
    longest = 1
    cnt = 1

    # Iterate in the array
    for i in range(n - 1):

        # Increment count if consecutive
        # elements has an odd sum
        if((arr[i] + arr[i + 1]) % 2 == 1):
            cnt = cnt + 1
        else:

            # Store maximum count in longest
            longest = max(longest, cnt)

            # Reinitialize cnt as 1 consecutive
            # elements does not have an odd sum
            cnt = 1

    # Length of 'longest' can never be 1 since
    # even odd has to occur in pair or more
    # so return 0 if longest = 1
    if(longest == 1):
       return 0

    return max(cnt, longest)

# Driver Code
arr = [ 1, 2, 3, 4, 5, 7, 8 ]
n = len(arr)

print(longestEvenOddSubarray(arr, n))

# This code is contributed by skylags
```

## C#

```
// C# program to find the Length of the
// longest alternating even odd subarray
using System;

class GFG{

// Function to find the longest subarray
static int longestEvenOddSubarray(int[] a, int n)
{

    // Length of longest
    // alternating subarray
    int longest = 1;
    int cnt = 1;

    // Iterate in the array
    for(int i = 0; i < n - 1; i++)
    {

       // Increment count if consecutive
       // elements has an odd sum
       if ((a[i] + a[i + 1]) % 2 == 1)
       {
           cnt++;
       }
       else
       {

           // Store maximum count in longest
           longest = Math.Max(longest, cnt);

           // Reinitialize cnt as 1 consecutive
           // elements does not have an odd sum
           cnt = 1;
       }
    }

    // Length of 'longest' can never be 1
    // since even odd has to occur in pair
    // or more so return 0 if longest = 1
    if (longest == 1)
        return 0;
    return Math.Max(cnt, longest);
}

// Driver code
static void Main()
{

    int[] a = { 1, 2, 3, 4, 5, 7, 8 };
    int n = a.Length;

    Console.WriteLine(longestEvenOddSubarray(a, n));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
// JavaScript program to find the Length of the
// longest alternating even odd subarray

// Function to find the longest subarray
function longestEvenOddSubarray(a, n)
{

    // Length of longest
    // alternating subarray
    let longest = 1;
    let cnt = 1;

    // Iterate in the array
    for (let i = 0; i < n - 1; i++) {

        // increment count if consecutive
        // elements has an odd sum
        if ((a[i] + a[i + 1]) % 2 == 1)
        {
            cnt++;
        }
        else
        {

            // Store maximum count in longest
            longest = Math.max(longest, cnt);

            // Reinitialize cnt as 1 consecutive
            // elements does not have an odd sum
            cnt = 1;
        }
    }

    // Length of 'longest' can never be 1
    // since even odd has to occur in pair or more
    // so return 0 if longest = 1
    if (longest == 1)
        return 0;

    return Math.max(cnt, longest);
}

/* Driver code*/
    let a = [ 1, 2, 3, 4, 5, 7, 8 ];
    let n = a.length;
    document.write(longestEvenOddSubarray(a, n));

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
5
```