# 满足给定条件的最大长度子阵列

> 原文:[https://www . geesforgeks . org/最大长度-满足给定条件的子数组/](https://www.geeksforgeeks.org/maximum-length-sub-array-which-satisfies-the-given-conditions/)

给定一个二进制数组 **arr[]** ，任务是找到给定数组中最长的子数组的长度，这样如果子数组被分成两个大小相等的子数组，那么这两个子数组要么包含所有**0**要么包含所有**1**。例如，两个子阵列的形式必须是 **{0，0，0，0}** 和 **{1，1，1，1}** 或 **{1，1，1}** 和 **{0，0，0}** ，而不是 **{0，0，0}** 和 **{0，0，0}**

**示例:**

> **输入:** arr[] = {1，1，1，0，0，1，1}
> **输出:** 4
> {1，1，0，0}和{0，0，1，1}是最大长度有效子数组。
> 
> **输入:** arr[] = {1，1，0，0，0，1，1，1}
> **输出:** 6
> {0，0，0，1，1，1}是唯一有效的最大长度子数组。

**方法:**对于数组中每两个连续的元素，说**arr【I】**和**arr【j】**，其中 **j = i + 1** ，将它们视为所需子数组的中间两个元素。为了使该子阵列成为有效的子阵列 **arr[i]** 必须不等于 **arr[j]** 。如果它可以是一个有效的子阵列，那么它的大小是 **2** 。现在，尝试通过同时递减 **i** 和递增 **j** 来将该子数组扩展到更大的大小，并且索引 i 之前的所有元素**和索引 j** 之后的所有元素**必须分别等于**arr【I】**和**arr【j】**。打印到目前为止找到的最长的子阵列的大小。**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum length
// of the required sub-array
int maxLength(int arr[], int n)
{
    int maxLen = 0;

    // For the first consecutive
    // pair of elements
    int i = 0;
    int j = i + 1;

    // While a consecutive pair
    // can be selected
    while (j < n) {

        // If current pair forms a
        // valid sub-array
        if (arr[i] != arr[j]) {

            // 2 is the length of the
            // current sub-array
            maxLen = max(maxLen, 2);

            // To extend the sub-array both ways
            int l = i - 1;
            int r = j + 1;

            // While elements at indices l and r
            // are part of a valid sub-array
            while (l >= 0 && r < n && arr[l] == arr[i]
                   && arr[r] == arr[j]) {
                l--;
                r++;
            }

            // Update the maximum length so far
            maxLen = max(maxLen, 2 * (r - j));
        }

        // Select the next consecutive pair
        i++;
        j = i + 1;
    }

    // Return the maximum length
    return maxLen;
}

// Driver code
int main()
{
    int arr[] = { 1, 1, 1, 0, 0, 1, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << maxLength(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the maximum length
    // of the required sub-array
    static int maxLength(int arr[], int n)
    {
        int maxLen = 0;

        // For the first consecutive
        // pair of elements
        int i = 0;
        int j = i + 1;

        // While a consecutive pair
        // can be selected
        while (j < n) {

            // If current pair forms a
            // valid sub-array
            if (arr[i] != arr[j]) {

                // 2 is the length of the
                // current sub-array
                maxLen = Math.max(maxLen, 2);

                // To extend the sub-array both ways
                int l = i - 1;
                int r = j + 1;

                // While elements at indices l and r
                // are part of a valid sub-array
                while (l >= 0 && r < n && arr[l] == arr[i] && arr[r] == arr[j]) {
                    l--;
                    r++;
                }

                // Update the maximum length so far
                maxLen = Math.max(maxLen, 2 * (r - j));
            }

            // Select the next consecutive pair
            i++;
            j = i + 1;
        }

        // Return the maximum length
        return maxLen;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 1, 1, 0, 0, 1, 1 };
        int n = arr.length;

        System.out.println(maxLength(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum length
# of the required sub-array
def maxLength(arr, n):
    maxLen = 0

    # For the first consecutive
    # pair of elements
    i = 0
    j = i + 1

    # While a consecutive pair
    # can be selected
    while (j < n):

        # If current pair forms a
        # valid sub-array
        if (arr[i] != arr[j]):

            # 2 is the length of the
            # current sub-array
            maxLen = max(maxLen, 2)

            # To extend the sub-array both ways
            l = i - 1
            r = j + 1

            # While elements at indices l and r
            # are part of a valid sub-array
            while (l >= 0 and r < n and arr[l] == arr[i]
                and arr[r] == arr[j]):
                l-= 1
                r+= 1

            # Update the maximum length so far
            maxLen = max(maxLen, 2 * (r - j))

        # Select the next consecutive pair
        i+= 1
        j = i + 1

    # Return the maximum length
    return maxLen

# Driver code

arr =[1, 1, 1, 0, 0, 1, 1]
n = len(arr)

print(maxLength(arr, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function to return the maximum length
    // of the required sub-array
    static int maxLength(int[] arr, int n)
    {
        int maxLen = 0;

        // For the first consecutive
        // pair of elements
        int i = 0;
        int j = i + 1;

        // While a consecutive pair
        // can be selected
        while (j < n) {

            // If current pair forms a
            // valid sub-array
            if (arr[i] != arr[j]) {

                // 2 is the length of the
                // current sub-array
                maxLen = Math.Max(maxLen, 2);

                // To extend the sub-array both ways
                int l = i - 1;
                int r = j + 1;

                // While elements at indices l and r
                // are part of a valid sub-array
                while (l >= 0 && r < n && arr[l] == arr[i] && arr[r] == arr[j]) {
                    l--;
                    r++;
                }

                // Update the maximum length so far
                maxLen = Math.Max(maxLen, 2 * (r - j));
            }

            // Select the next consecutive pair
            i++;
            j = i + 1;
        }

        // Return the maximum length
        return maxLen;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr = { 1, 1, 1, 0, 0, 1, 1 };
        int n = arr.Length;

        Console.WriteLine(maxLength(arr, n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the maximum length
// of the required sub-array
function maxLength(arr, n)
{
    let maxLen = 0;

    // For the first consecutive
    // pair of elements
    let i = 0;
    let j = i + 1;

    // While a consecutive pair
    // can be selected
    while (j < n) {

        // If current pair forms a
        // valid sub-array
        if (arr[i] != arr[j]) {

            // 2 is the length of the
            // current sub-array
            maxLen = Math.max(maxLen, 2);

            // To extend the sub-array both ways
            let l = i - 1;
            let r = j + 1;

            // While elements at indices l and r
            // are part of a valid sub-array
            while (l >= 0 && r < n && arr[l] == arr[i]
                   && arr[r] == arr[j]) {
                l--;
                r++;
            }

            // Update the maximum length so far
            maxLen = Math.max(maxLen, 2 * (r - j));
        }

        // Select the next consecutive pair
        i++;
        j = i + 1;
    }

    // Return the maximum length
    return maxLen;
}

// Driver code
    let arr = [ 1, 1, 1, 0, 0, 1, 1 ];
    let n = arr.length;

    document.write(maxLength(arr, n));

</script>
```

**Output:** 

```
4
```

**交替法:**我们可以保持之前相似元素的最大长度，尝试与下一个不同的邻接元素组成子阵列，最大化子阵列长度。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the maximum length
// of the required sub-array
int maxLength(int a[], int n)
{

    // To store the maximum length
    // for a valid subarray
    int maxLen = 0;

    // To store the count of contiguous
    // similar elements for previous
    // group and the current group
    int prev_cnt = 0, curr_cnt = 1;
    for (int i = 1; i < n; i++) {

        // If current element is equal to
        // the previous element then it is
        // a part of the same group
        if (a[i] == a[i - 1])
            curr_cnt++;

        // Else update the previous group
        // and start counting elements
        // for the new group
        else {
            prev_cnt = curr_cnt;
            curr_cnt = 1;
        }

        // Update the maximum possible length for a group
        maxLen = max(maxLen, min(prev_cnt, curr_cnt));
    }

    // Return the maximum length of the valid subarray
    return (2 * maxLen);
}

// Driver code
int main()
{
    int arr[] = { 1, 1, 1, 0, 0, 1, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << maxLength(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the maximum length
// of the required sub-array
static int maxLength(int a[], int n)
{

    // To store the maximum length
    // for a valid subarray
    int maxLen = 0;

    // To store the count of contiguous
    // similar elements for previous
    // group and the current group
    int prev_cnt = 0, curr_cnt = 1;
    for (int i = 1; i < n; i++)
    {

        // If current element is equal to
        // the previous element then it is
        // a part of the same group
        if (a[i] == a[i - 1])
            curr_cnt++;

        // Else update the previous group
        // and start counting elements
        // for the new group
        else
        {
            prev_cnt = curr_cnt;
            curr_cnt = 1;
        }

        // Update the maximum possible length for a group
        maxLen = Math.max(maxLen,
                 Math.min(prev_cnt, curr_cnt));
    }

    // Return the maximum length
    // of the valid subarray
    return (2 * maxLen);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 1, 1, 0, 0, 1, 1 };
    int n = arr.length;

    System.out.println(maxLength(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
# Function to return the maximum length
# of the required sub-array
def maxLength(a, n):

    # To store the maximum length
    # for a valid subarray
    maxLen = 0;

    # To store the count of contiguous
    # similar elements for previous
    # group and the current group
    prev_cnt = 0; curr_cnt = 1;
    for i in range(1, n):

        # If current element is equal to
        # the previous element then it is
        # a part of the same group
        if (a[i] == a[i - 1]):
            curr_cnt += 1;

        # Else update the previous group
        # and start counting elements
        # for the new group
        else:
            prev_cnt = curr_cnt;
            curr_cnt = 1;

        # Update the maximum possible
        # length for a group
        maxLen = max(maxLen, min(prev_cnt,
                                 curr_cnt));

    # Return the maximum length
    # of the valid subarray
    return (2 * maxLen);

# Driver code
arr = [ 1, 1, 1, 0, 0, 1, 1 ];
n = len(arr);

print(maxLength(arr, n));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the maximum length
// of the required sub-array
static int maxLength(int[] a, int n)
{

    // To store the maximum length
    // for a valid subarray
    int maxLen = 0;

    // To store the count of contiguous
    // similar elements for previous
    // group and the current group
    int prev_cnt = 0, curr_cnt = 1;
    for (int i = 1; i < n; i++)
    {

        // If current element is equal to
        // the previous element then it is
        // a part of the same group
        if (a[i] == a[i - 1])
            curr_cnt++;

        // Else update the previous group
        // and start counting elements
        // for the new group
        else
        {
            prev_cnt = curr_cnt;
            curr_cnt = 1;
        }

        // Update the maximum possible length for a group
        maxLen = Math.Max(maxLen,
                 Math.Min(prev_cnt, curr_cnt));
    }

    // Return the maximum length
    // of the valid subarray
    return (2 * maxLen);
}

// Driver code
public static void Main()
{
    int[] arr = { 1, 1, 1, 0, 0, 1, 1 };
    int n = arr.Length;

    Console.WriteLine(maxLength(arr, n));
}
}

// This code is contributed by Code_Mech.
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the maximum length
// of the required sub-array
function maxLength(a, n)
{

    // To store the maximum length
    // for a valid subarray
    let maxLen = 0;

    // To store the count of contiguous
    // similar elements for previous
    // group and the current group
    let prev_cnt = 0, curr_cnt = 1;
    for (let i = 1; i < n; i++) {

        // If current element is equal to
        // the previous element then it is
        // a part of the same group
        if (a[i] == a[i - 1])
            curr_cnt++;

        // Else update the previous group
        // and start counting elements
        // for the new group
        else {
            prev_cnt = curr_cnt;
            curr_cnt = 1;
        }

        // Update the maximum possible length for a group
        maxLen = Math.max(maxLen, Math.min(prev_cnt, curr_cnt));
    }

    // Return the maximum length of the valid subarray
    return (2 * maxLen);
}

// Driver code
    let arr = [ 1, 1, 1, 0, 0, 1, 1 ];
    let n = arr.length;

    document.write(maxLength(arr, n));

</script>
```

**Output:** 

```
4
```