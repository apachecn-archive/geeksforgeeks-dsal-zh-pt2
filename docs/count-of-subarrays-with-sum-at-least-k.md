# 总和至少为 K 的子阵列计数

> 原文:[https://www . geesforgeks . org/subarray-count-with-sum-at-k/](https://www.geeksforgeeks.org/count-of-subarrays-with-sum-at-least-k/)

给定一个大小为 **N** 的数组 **arr[]** 和一个整数 **K > 0** 。任务是找到和至少 **K** 的子阵个数。
**举例:**

> **输入:** arr[] = {6，1，2，7}，K = 10
> **输出:** 2
> {6，1，2，7}和{1，2，7}是唯一有效的子阵。
> **输入:** arr[] = {3，3，3}，K = 5
> **输出:** 3

**方法:**对于一个固定的左索引(比如说 **l** ，试着在 **l** (比如说 **r** )的右边找到第一个索引，这样**(arr[l]+arr[l+1]+…+arr[r])≥K**。然后在要求的答案上加上**N–r+1**。对所有左侧索引重复此过程。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number of
// subarrays with sum atleast k
int k_sum(int a[], int n, int k)
{
    // To store the right index
    // and the current sum
    int r = 0, sum = 0;

    // To store the number of sub-arrays
    int ans = 0;

    // For all left indexes
    for (int l = 0; l < n; l++) {

        // Get elements till current sum
        // is less than k
        while (sum < k) {
            if (r == n)
                break;
            else {
                sum += a[r];
                r++;
            }
        }

        // No such subarray is possible
        if (sum < k)
            break;

        // Add all possible subarrays
        ans += n - r + 1;

        // Remove the left most element
        sum -= a[l];
    }

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    int a[] = { 6, 1, 2, 7 }, k = 10;
    int n = sizeof(a) / sizeof(a[0]);

    cout << k_sum(a, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the number of
    // subarrays with sum atleast k
    static int k_sum(int a[], int n, int k)
    {
        // To store the right index
        // and the current sum
        int r = 0, sum = 0;

        // To store the number of sub-arrays
        int ans = 0;

        // For all left indexes
        for (int l = 0; l < n; l++)
        {

            // Get elements till current sum
            // is less than k
            while (sum < k)
            {
                if (r == n)
                    break;
                else
                {
                    sum += a[r];
                    r++;
                }
            }

            // No such subarray is possible
            if (sum < k)
                break;

            // Add all possible subarrays
            ans += n - r + 1;

            // Remove the left most element
            sum -= a[l];
        }

        // Return the required answer
        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        int a[] = { 6, 1, 2, 7 }, k = 10;
        int n = a.length;

        System.out.println(k_sum(a, n, k));
    }
}

// This code is contributed by kanugargng
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the number of
# subarrays with sum atleast k
def k_sum(a, n, k):

    # To store the right index
    # and the current sum
    r, sum = 0, 0;

    # To store the number of sub-arrays
    ans = 0;

    # For all left indexes
    for l in range(n):

        # Get elements till current sum
        # is less than k
        while (sum < k):
            if (r == n):
                break;
            else:
                sum += a[r];
                r += 1;

        # No such subarray is possible
        if (sum < k):
            break;

        # Add all possible subarrays
        ans += n - r + 1;

        # Remove the left most element
        sum -= a[l];
    # Return the required answer
    return ans;

# Driver code
a = [ 6, 1, 2, 7 ]; k = 10;
n = len(a);

print(k_sum(a, n, k));

# This code contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the number of
    // subarrays with sum atleast k
    static int k_sum(int []a, int n, int k)
    {
        // To store the right index
        // and the current sum
        int r = 0, sum = 0;

        // To store the number of sub-arrays
        int ans = 0;

        // For all left indexes
        for (int l = 0; l < n; l++)
        {

            // Get elements till current sum
            // is less than k
            while (sum < k)
            {
                if (r == n)
                    break;
                else
                {
                    sum += a[r];
                    r++;
                }
            }

            // No such subarray is possible
            if (sum < k)
                break;

            // Add all possible subarrays
            ans += n - r + 1;

            // Remove the left most element
            sum -= a[l];
        }

        // Return the required answer
        return ans;
    }

    // Driver code
    public static void Main()
    {
        int []a = { 6, 1, 2, 7 };
        int k = 10;
        int n = a.Length;

        Console.WriteLine(k_sum(a, n, k));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the number of
// subarrays with sum atleast k
function k_sum(a, n, k)
{

    // To store the right index
    // and the current sum
    let r = 0, sum = 0;

    // To store the number of sub-arrays
    let ans = 0;

    // For all left indexes
    for (let l = 0; l < n; l++) {

        // Get elements till current sum
        // is less than k
        while (sum < k) {
            if (r == n)
                break;
            else {
                sum += a[r];
                r++;
            }
        }

        // No such subarray is possible
        if (sum < k)
            break;

        // Add all possible subarrays
        ans += n - r + 1;

        // Remove the left most element
        sum -= a[l];
    }

    // Return the required answer
    return ans;
}

// Driver code
let a = [6, 1, 2, 7], k = 10;
let n = a.length;

document.write(k_sum(a, n, k));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
2
```