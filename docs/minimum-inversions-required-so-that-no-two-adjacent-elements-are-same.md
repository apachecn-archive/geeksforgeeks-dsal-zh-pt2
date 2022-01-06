# 为使相邻元素不相同所需的最小反转

> 原文:[https://www . geeksforgeeks . org/minimum-inversion-required-so-no-两个相邻元素-相同/](https://www.geeksforgeeks.org/minimum-inversions-required-so-that-no-two-adjacent-elements-are-same/)

给定大小为 **N** 的二进制数组 **arr[]** 。任务是找到所需的最小反转数，这样就不会有两个相邻的元素相同。单次反转后，元素可能会从 **0** 变为 **1** 或从 **1** 变为 **0** 。
**示例:**

> **输入:** arr[] = {1，1，1}
> **输出:** 1
> 将 arr[1]从 1 更改为 0，
> 数组变为{1，0，1}。
> **输入:** arr[] = {1，0，0，1，0，0，1，0}
> **输出:** 3

**方法:**制作数组{1，0，1，0，1，0，1，…}或{0，1，0，1，0，1，0，0，0，1，0，…}只有两种可能。让 **ans_a** 和 **ans_b** 分别为获取这些数组所需的更改计数。现在，最终答案将是 **min(ans_a，ans_b)** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum
// inversions required so that no
// two adjacent elements are same
int min_changes(int a[], int n)
{
    // To store the inversions required
    // to make the array {1, 0, 1, 0, 1, 0, 1, ...}
    // and {0, 1, 0, 1, 0, 1, 0, ...} respectively
    int ans_a = 0, ans_b = 0;

    // Find all the changes required
    for (int i = 0; i < n; i++) {
        if (i % 2 == 0) {
            if (a[i] == 0)
                ans_a++;
            else
                ans_b++;
        }
        else {
            if (a[i] == 0)
                ans_b++;
            else
                ans_a++;
        }
    }

    // Return the required answer
    return min(ans_a, ans_b);
}

// Driver code
int main()
{
    int a[] = { 1, 0, 0, 1, 0, 0, 1, 0 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << min_changes(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the minimum
// inversions required so that no
// two adjacent elements are same
static int min_changes(int a[], int n)
{
    // To store the inversions required
    // to make the array {1, 0, 1, 0, 1, 0, 1, ...}
    // and {0, 1, 0, 1, 0, 1, 0, ...} respectively
    int ans_a = 0, ans_b = 0;

    // Find all the changes required
    for (int i = 0; i < n; i++)
    {
        if (i % 2 == 0)
        {
            if (a[i] == 0)
                ans_a++;
            else
                ans_b++;
        }
        else
        {
            if (a[i] == 0)
                ans_b++;
            else
                ans_a++;
        }
    }

    // Return the required answer
    return Math.min(ans_a, ans_b);
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 1, 0, 0, 1, 0, 0, 1, 0 };
    int n = a.length;

    System.out.println(min_changes(a, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum
# inversions required so that no
# two adjacent elements are same
def min_changes(a, n):

    # To store the inversions required
    # to make the array {1, 0, 1, 0, 1, 0, 1, ...}
    # and {0, 1, 0, 1, 0, 1, 0, ...} respectively
    ans_a = 0;
    ans_b = 0;

    # Find all the changes required
    for i in range(n):
        if (i % 2 == 0):
            if (a[i] == 0):
                ans_a += 1;
            else:
                ans_b += 1;

        else:
            if (a[i] == 0):
                ans_b += 1;
            else:
                ans_a += 1;

    # Return the required answer
    return min(ans_a, ans_b);

# Driver code
if __name__ == '__main__':

    a = [ 1, 0, 0, 1, 0, 0, 1, 0 ];
    n = len(a);

    print(min_changes(a, n));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the minimum
// inversions required so that no
// two adjacent elements are same
static int min_changes(int []a, int n)
{
    // To store the inversions required
    // to make the array {1, 0, 1, 0, 1, 0, 1, ...}
    // and {0, 1, 0, 1, 0, 1, 0, ...} respectively
    int ans_a = 0, ans_b = 0;

    // Find all the changes required
    for (int i = 0; i < n; i++)
    {
        if (i % 2 == 0)
        {
            if (a[i] == 0)
                ans_a++;
            else
                ans_b++;
        }
        else
        {
            if (a[i] == 0)
                ans_b++;
            else
                ans_a++;
        }
    }

    // Return the required answer
    return Math.Min(ans_a, ans_b);
}

// Driver code
public static void Main(String[] args)
{
    int []a = { 1, 0, 0, 1, 0, 0, 1, 0 };
    int n = a.Length;

    Console.WriteLine(min_changes(a, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the minimum
// inversions required so that no
// two adjacent elements are same
function min_changes(a, n) {
    // To store the inversions required
    // to make the array {1, 0, 1, 0, 1, 0, 1, ...}
    // and {0, 1, 0, 1, 0, 1, 0, ...} respectively
    let ans_a = 0, ans_b = 0;

    // Find all the changes required
    for (let i = 0; i < n; i++) {
        if (i % 2 == 0) {
            if (a[i] == 0)
                ans_a++;
            else
                ans_b++;
        }
        else {
            if (a[i] == 0)
                ans_b++;
            else
                ans_a++;
        }
    }

    // Return the required answer
    return Math.min(ans_a, ans_b);
}

// Driver code
let a = [1, 0, 0, 1, 0, 0, 1, 0];
let n = a.length;

document.write(min_changes(a, n));

</script>
```

**Output:** 

```
3
```