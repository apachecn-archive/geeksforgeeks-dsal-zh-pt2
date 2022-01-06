# 二进制圆形数组中最大连续 1(或 0)

> 原文:[https://www . geesforgeks . org/二进制循环数组中最大连续 1 或 0 数/](https://www.geeksforgeeks.org/maximum-consecutive-ones-or-zeros-in-a-binary-circular-array/)

给定一个大小为 N 的二进制[圆形数组](https://www.geeksforgeeks.org/circular-array/)，任务是找出圆形数组中出现的连续 1 的计数最大数量。
**例:**

> **输入:** arr[] = {1，1，0，0，1，0，1，0，1，1，1}
> **输出:** 6
> 后 4 位和前 2 位有 6 个连续的 1。
> **输入:** a[] = {0，1，0，1，0，1，0，1，0，1}
> **输出:** 1

一个简单的解决方案是创建一个大小为 2*N 的数组，其中 N 是输入数组的大小。我们在这个数组中复制输入数组两次。现在我们需要在一次遍历中找到这个二进制数组中[最长的连续 1。
**高效解决方案:**可以按照以下步骤解决上述问题:](https://www.geeksforgeeks.org/maximum-consecutive-ones-or-zeros-in-a-binary-array/) 

1.  我们可以使用模数运算符循环遍历数组，而不是创建大小为 2*N 的数组来实现循环数组。
2.  从 0 迭代到 2*N，并将 1 的连续数计算为:
    *   从左到右遍历数组。
    *   每次遍历时，计算当前索引为 **(i%N)** ，以便当 **i > N** 时循环遍历数组。
    *   如果我们看到一个 1，我们增加计数，并将其与最大值进行比较。如果我们看到一个 0，我们重置计数为 0。
3.  当 a[i]==0 和 i>=n 时脱离循环，以降低某些情况下的时间复杂度。

以下是上述方法的实现:

## C++

```
// C++ program to count maximum consecutive
// 1's in a binary circular array
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of maximum
// consecutive 1's in a binary circular array
int getMaxLength(bool arr[], int n)
{

    // Starting index
    int start = 0;

    // To store the maximum length of the
    // prefix of the given array with all 1s
    int preCnt = 0;
    while (start < n && arr[start] == 1) {
        preCnt++;
        start++;
    }

    // Ending index
    int end = n - 1;

    // To store the maximum length of the
    // suffix of the given array with all 1s
    int suffCnt = 0;
    while (end >= 0 && arr[end] == 1) {
        suffCnt++;
        end--;
    }

    // The array contains all 1s
    if (start > end)
        return n;

    // Find the maximum length subarray
    // with all 1s from the remaining not
    // yet traversed subarray
    int midCnt = 0;

    // To store the result for middle 1s
    int result = 0;

    for (int i = start; i <= end; i++) {
        if (arr[i] == 1) {
            midCnt++;
            result = max(result, midCnt);
        }
        else {
            midCnt = 0;
        }
    }

    // (preCnt + suffCnt) is the subarray when
    // the given array is assumed to be circular
    return max(result, preCnt + suffCnt);
}

// Driver code
int main()
{
    bool arr[] = { 1, 1, 0, 0, 1, 0, 1,
                   0, 1, 1, 1, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << getMaxLength(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count maximum consecutive
// 1's in a binary circular array
class GfG {

    // Function to return the count of maximum
    // consecutive 1's in a binary circular array
    static int getMaxLength(int arr[], int n)
    {
        // Starting index
        int start = 0;

        // To store the maximum length of the
        // prefix of the given array with all 1s
        int preCnt = 0;
        while (start < n && arr[start] == 1) {
            preCnt++;
            start++;
        }

        // Ending index
        int end = n - 1;

        // To store the maximum length of the
        // suffix of the given array with all 1s
        int suffCnt = 0;
        while (end >= 0 && arr[end] == 1) {
            suffCnt++;
            end--;
        }

        // The array contains all 1s
        if (start > end)
            return n;

        // Find the maximum length subarray
        // with all 1s from the remaining not
        // yet traversed subarray
        int midCnt = 0;

        // To store the result for middle 1s
        int result = 0;

        for (int i = start; i <= end; i++) {
            if (arr[i] == 1) {
                midCnt++;
                result = Math.max(result, midCnt);
            }
            else {
                midCnt = 0;
            }
        }

        // (preCnt + suffCnt) is the subarray when
        // the given array is assumed to be circular
        return Math.max(result, preCnt + suffCnt);
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = new int[] { 1, 1, 0, 0, 1, 0,
                                1, 0, 1, 1, 1, 1 };
        int n = arr.length;
        System.out.println(getMaxLength(arr, n));
    }
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python 3 program to count maximum consecutive
# 1's in a binary circular array

# Function to return the count of
# maximum consecutive 1's in a
# binary circular array
def getMaxLength(arr, n):

    # Starting index
    start = 0

    # To store the maximum length of the
    # prefix of the given array with all 1s
    preCnt = 0
    while(start < n and arr[start] == 1):
        preCnt = preCnt + 1
        start = start + 1

    # Ending index
    end = n - 1

    # To store the maximum length of the
    # suffix of the given array with all 1s
    suffCnt = 0
    while(end >= 0 and arr[end] == 1):
        suffCnt = suffCnt + 1
        end = end - 1

    # The array contains all 1s
    if(start > end):
        return n

    # Find the maximum length subarray
    # with all 1s from the remaining not
    # yet traversed subarray
    midCnt = 0

    i = start

    # To store the result for middle 1s
    result = 0

    while(i <= end):
        if(arr[i] == 1):
            midCnt = midCnt + 1
            result = max(result, midCnt)
        else:
            midCnt = 0
        i = i + 1

    # (preCnt + suffCnt) is the subarray when
    # the given array is assumed to be circular
    return max(result, preCnt + suffCnt)

# Driver code
if __name__ == '__main__':
    arr = [1, 1, 0, 0, 1, 0,
        1, 0, 1, 1, 1, 1]
    n = len(arr)
    print(getMaxLength(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to count maximum consecutive
// 1's in a binary circular array
using System;

class GFG {

    // Function to return the count of maximum
    // consecutive 1's in a binary circular array
    static int getMaxLength(int[] arr, int n)
    {

        // Starting index
        int start = 0;

        // To store the maximum length of the
        // prefix of the given array with all 1s
        int preCnt = 0;
        while (start < n && arr[start] == 1) {
            preCnt++;
            start++;
        }

        // Ending index
        int end = n - 1;

        // To store the maximum length of the
        // suffix of the given array with all 1s
        int suffCnt = 0;
        while (end >= 0 && arr[end] == 1) {
            suffCnt++;
            end--;
        }

        // The array contains all 1s
        if (start > end)
            return n;

        // Find the maximum length subarray
        // with all 1s from the remaining not
        // yet traversed subarray
        int midCnt = 0;

        // To store the result for middle 1s
        int result = 0;

        for (int i = start; i <= end; i++) {
            if (arr[i] == 1) {
                midCnt++;
                result = Math.Max(result, midCnt);
            }
            else {
                midCnt = 0;
            }
        }

        // (preCnt + suffCnt) is the subarray when
        // the given array is assumed to be circular
        return Math.Max(result, preCnt + suffCnt);
    }

    // Driver code
    public static void Main()
    {
        int[] arr = new int[] { 1, 1, 0, 0, 1, 0,
                                1, 0, 1, 1, 1, 0 };
        int n = arr.Length;
        Console.WriteLine(getMaxLength(arr, n));
    }
}

// This code is contributed by Code_Mech.
```

## java 描述语言

```
<script>
// javascript program to count maximum consecutive
// 1's in a binary circular array

    // Function to return the count of maximum
    // consecutive 1's in a binary circular array
    function getMaxLength(arr , n)
    {

        // Starting index
        var start = 0;

        // To store the maximum length of the
        // prefix of the given array with all 1s
        var preCnt = 0;
        while (start < n && arr[start] == 1) {
            preCnt++;
            start++;
        }

        // Ending index
        var end = n - 1;

        // To store the maximum length of the
        // suffix of the given array with all 1s
        var suffCnt = 0;
        while (end >= 0 && arr[end] == 1) {
            suffCnt++;
            end--;
        }

        // The array contains all 1s
        if (start > end)
            return n;

        // Find the maximum length subarray
        // with all 1s from the remaining not
        // yet traversed subarray
        var midCnt = 0;

        // To store the result for middle 1s
        var result = 0;

        for (i = start; i <= end; i++) {
            if (arr[i] == 1) {
                midCnt++;
                result = Math.max(result, midCnt);
            } else {
                midCnt = 0;
            }
        }

        // (preCnt + suffCnt) is the subarray when
        // the given array is assumed to be circular
        return Math.max(result, preCnt + suffCnt);
    }

    // Driver code
        var arr = [ 1, 1, 0, 0, 1, 0, 1, 0, 1, 1, 1, 1 ];
        var n = arr.length;
        document.write(getMaxLength(arr, n));

// This code is contributed by umadevi9616
</script>
```

**Output**

```
6
```