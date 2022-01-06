# 计算序列中连续递增和递减子序列的数量

> 原文:[https://www . geeksforgeeks . org/count-序列中连续递增和递减子序列的数量/](https://www.geeksforgeeks.org/count-the-number-of-contiguous-increasing-and-decreasing-subsequences-in-a-sequence/)

对于给定的大小为 **N** 的不同整数序列，任务是计算该序列中连续递增子序列和连续递减子序列的数量。
**例:**

> **输入:** arr[] = { 80，50，60，70，40 }
> **输出:** 1 2
> **解释:**
> 唯一一个递增的子序列是(50，60，70)
> 两个递减的子序列是(80，50)和(70，40)。
> **输入:** arr[] = { 10，20，23，12，5，4，61，67，87，9 }
> **输出:** 2 2
> **解释:**
> 递增的子序列是(10，20，23)和(4，61，67，87)
> ，而递减的子序列是(23，12，5，4)和(25，4)

**方法:**解决这个问题背后的想法是使用两个数组来跟踪基于下一个元素的索引的增加或减少。

1.  定义两个数组 max 和 min，以便存储数组元素的索引。对于数组的第一个元素，如果它大于它的下一个元素，它的索引存储在 max 数组中，否则它存储在 min 数组中，以此类推。
2.  对于数组的最后一个元素，如果它大于前一个元素，它的索引存储在 max 数组中，否则它存储在 min 数组中。
3.  此后，所有最大连续递增子序列从( **min 到 max** 匹配，而所有最大连续递减子序列从( **max 到 min** 匹配。
4.  最后，如果数组的第一个元素的索引存储在最小数组的第一个索引中，那么最大连续递增子序列的可能数量是最小数组的**大小**，最大连续递减子序列的可能数量是**(最大数组的大小–1)**。
5.  如果数组的第一个元素的索引存储在 max 数组的第一个索引中，那么最大连续递增子序列的可能数量是**(max 数组-1 的大小)**，最大连续递减子序列的可能数量是 min 数组的**大小**。

下面是上述方法的实现。

## C++

```
// C++ implementation of the above approach.

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of maximal contiguous
// increasing and decreasing subsequences
void numOfSubseq(int arr[], int n)

{

    int i, inc_count, dec_count;
    int max[n], min[n];

    // k2, k1 are used to store the
    // count of max and min array

    int k1 = 0, k2 = 0;

    // Comparison to store the index of
    // first element of array
    if (arr[0] < arr[1])
        min[k1++] = 0;
    else
        max[k2++] = 0;

    // Comparison to store the index
    // from second to second last
    // index of array
    for (i = 1; i < n - 1; i++) {
        if (arr[i] < arr[i - 1]
            && arr[i] < arr[i + 1])
            min[k1++] = i;

        if (arr[i] > arr[i - 1]
            && arr[i] > arr[i + 1])
            max[k2++] = i;
    }

    // Comparison to store the index
    // of last element of array
    if (arr[n - 1] < arr[n - 2])
        min[k1++] = n - 1;
    else
        max[k2++] = n - 1;

    // Count of number of maximal contiguous
    // increasing and decreasing subsequences
    if (min[0] == 0) {
        inc_count = k2;
        dec_count = k1 - 1;
    }
    else {
        inc_count = k2 - 1;
        dec_count = k1;
    }

    cout << "Increasing Subsequence Count: "
         << inc_count << "\n";
    cout << "Decreasing Subsequence Count: "
         << dec_count << "\n";
}

// Driver program to test above
int main()
{
    int arr[] = { 12, 8, 11, 13, 10, 15, 14, 16, 20 };
    int n = sizeof(arr) / sizeof(arr[0]);
    numOfSubseq(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach.
class GFG
{

    // Function to count the number of maximal contiguous
    // increasing and decreasing subsequences
    static void numOfSubseq(int arr[], int n)

    {

        int i, inc_count, dec_count;
        int max[] = new int[n];
        int min[] = new int[n];

        // k2, k1 are used to store the
        // count of max and min array

        int k1 = 0, k2 = 0;

        // Comparison to store the index of
        // first element of array
        if (arr[0] < arr[1])
            min[k1++] = 0;
        else
            max[k2++] = 0;

        // Comparison to store the index
        // from second to second last
        // index of array
        for (i = 1; i < n - 1; i++)
        {
            if (arr[i] < arr[i - 1]
                && arr[i] < arr[i + 1])
                min[k1++] = i;

            if (arr[i] > arr[i - 1]
                && arr[i] > arr[i + 1])
                max[k2++] = i;
        }

        // Comparison to store the index
        // of last element of array
        if (arr[n - 1] < arr[n - 2])
            min[k1++] = n - 1;
        else
            max[k2++] = n - 1;

        // Count of number of maximal contiguous
        // increasing and decreasing subsequences
        if (min[0] == 0)
        {
            inc_count = k2;
            dec_count = k1 - 1;
        }
        else
        {
            inc_count = k2 - 1;
            dec_count = k1;
        }

        System.out.println("Increasing Subsequence" +
                            " Count: " + inc_count) ;
        System.out.println("Decreasing Subsequence" +
                            " Count: " + dec_count) ;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 12, 8, 11, 13, 10, 15, 14, 16, 20 };
        int n = arr.length;
        numOfSubseq(arr, n);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the above approach.

# Function to count the number of maximal contiguous
# increasing and decreasing subsequences
def numOfSubseq(arr, n):
    i, inc_count, dec_count = 0, 0, 0;
    max = [0]*n;
    min = [0]*n;

    # k2, k1 are used to store the
    # count of max and min array
    k1 = 0;
    k2 = 0;

    # Comparison to store the index of
    # first element of array
    if (arr[0] < arr[1]):
        min[k1] = 0;
        k1 += 1;
    else:
        max[k2] = 0;
        k2 += 1;

    # Comparison to store the index
    # from second to second last
    # index of array
    for i in range(1, n-1):
        if (arr[i] < arr[i - 1] and arr[i] < arr[i + 1]):
            min[k1] = i;
            k1 += 1;

        if (arr[i] > arr[i - 1] and arr[i] > arr[i + 1]):
            max[k2] = i;
            k2 += 1;

    # Comparison to store the index
    # of last element of array
    if (arr[n - 1] < arr[n - 2]):
        min[k1] = n - 1;
        k1 += 1;
    else:
        max[k2] = n - 1;
        k2 += 1;

    # Count of number of maximal contiguous
    # increasing and decreasing subsequences
    if (min[0] == 0):
        inc_count = k2;
        dec_count = k1 - 1;
    else:
        inc_count = k2 - 1;
        dec_count = k1;

    print("Increasing Subsequence Count: " , inc_count);
    print("Decreasing Subsequence Count: " , dec_count);

# Driver code
if __name__ == '__main__':
    arr = [ 12, 8, 11, 13, 10, 15, 14, 16, 20 ];
    n = len(arr);
    numOfSubseq(arr, n);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the above approach.
using System;

class GFG
{

// Function to count the number of maximal contiguous
// increasing and decreasing subsequences
static void numOfSubseq(int []arr, int n)

{

    int i, inc_count, dec_count;
    int []max = new int[n];
    int []min = new int[n];

    // k2, k1 are used to store the
    // count of max and min array
    int k1 = 0, k2 = 0;

    // Comparison to store the index of
    // first element of array
    if (arr[0] < arr[1])
        min[k1++] = 0;
    else
        max[k2++] = 0;

    // Comparison to store the index
    // from second to second last
    // index of array
    for (i = 1; i < n - 1; i++)
    {
        if (arr[i] < arr[i - 1]
            && arr[i] < arr[i + 1])
            min[k1++] = i;

        if (arr[i] > arr[i - 1]
            && arr[i] > arr[i + 1])
            max[k2++] = i;
    }

    // Comparison to store the index
    // of last element of array
    if (arr[n - 1] < arr[n - 2])
        min[k1++] = n - 1;
    else
        max[k2++] = n - 1;

    // Count of number of maximal contiguous
    // increasing and decreasing subsequences
    if (min[0] == 0)
    {
        inc_count = k2;
        dec_count = k1 - 1;
    }
    else
    {
        inc_count = k2 - 1;
        dec_count = k1;
    }

    Console.WriteLine("Increasing Subsequence" +
                        " Count: " + inc_count) ;
    Console.WriteLine("Decreasing Subsequence" +
                        " Count: " + dec_count) ;
}

// Driver code
static public void Main ()
{
    int []arr = { 12, 8, 11, 13, 10, 15, 14, 16, 20 };
    int n = arr.Length;
    numOfSubseq(arr, n);
}
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach.

    // Function to count the number of maximal contiguous
    // increasing and decreasing subsequences
    function numOfSubseq(arr, n)

    {

        let i, inc_count, dec_count;
        let max = new Array(n);
        max.fill(0);
        let min = new Array(n);
        min.fill(0);

        // k2, k1 are used to store the
        // count of max and min array
        let k1 = 0, k2 = 0;

        // Comparison to store the index of
        // first element of array
        if (arr[0] < arr[1])
            min[k1++] = 0;
        else
            max[k2++] = 0;

        // Comparison to store the index
        // from second to second last
        // index of array
        for (i = 1; i < n - 1; i++)
        {
            if (arr[i] < arr[i - 1]
                && arr[i] < arr[i + 1])
                min[k1++] = i;

            if (arr[i] > arr[i - 1]
                && arr[i] > arr[i + 1])
                max[k2++] = i;
        }

        // Comparison to store the index
        // of last element of array
        if (arr[n - 1] < arr[n - 2])
            min[k1++] = n - 1;
        else
            max[k2++] = n - 1;

        // Count of number of maximal contiguous
        // increasing and decreasing subsequences
        if (min[0] == 0)
        {
            inc_count = k2;
            dec_count = k1 - 1;
        }
        else
        {
            inc_count = k2 - 1;
            dec_count = k1;
        }

        document.write("Increasing Subsequence" +
                            " Count: " + inc_count + "</br>") ;
        document.write("Decreasing Subsequence" +
                            " Count: " + dec_count + "</br>") ;
    }

    let arr = [ 12, 8, 11, 13, 10, 15, 14, 16, 20 ];
    let n = arr.length;
    numOfSubseq(arr, n);

// This code is contributed by suresh07.
</script>
```

**Output:** 

```
Increasing Subsequence Count: 3
Decreasing Subsequence Count: 3
```

**时间复杂度:** O(N)