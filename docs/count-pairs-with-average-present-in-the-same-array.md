# 对同一阵列中存在平均值的对进行计数

> 原文:[https://www . geesforgeks . org/count-pairs-with-average-present-in-the-at-in-the-the-in-the-the-in-the-in-the-in-the-in-the-in-the-in-the-the-in-the-the-in-the-](https://www.geeksforgeeks.org/count-pairs-with-average-present-in-the-same-array/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，其中 **|arr[i] ≤ 1000|** 为所有有效的 **i** 。任务是计算数组中的整数对，其平均值也存在于同一数组中，即 **(arr[i]，arr[j])** 必须是有效的整数对 **(arr[i] + arr[j]) / 2** 也必须存在于数组中。

**示例:**

> **输入:** arr[] = {2，1，3}
> **输出:** 1
> 只有有效的对是(1，3)，因为数组中还存在(1 + 3) / 2 = 2。
> **输入:** arr[] = {4，2，5，1，3，5}
> **输出:** 7

**方法:**制作一个频率数组，存储每个数组元素的频率。请记住，如果数组也包含负数，那么我们必须将频率数组的大小设为原始大小的两倍。更新频率阵列后，有两种情况:

1.  如果 **freq[i] > 0** ，则所需配对的总数将为**计数=(freq[I]*(freq[I]–1))/2**。
2.  对于每一对 **(freq[i]，freq[j])** ，其中 **freq[i] > 0** 、 **freq[j] > 0** 和 **freq[(i + j) / 2] > 0** ，则所需对的总数将为 **count = (freq[i] * freq[j])** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
const int N = 1000;

// Function to return the count
// of valid pairs
int countPairs(int arr[], int n)
{

    // Frequency array
    // Twice the original size to hold
    // negative elements as well
    int size = (2 * N) + 1;
    int freq[size] = { 0 };

    // Update the frequency of each
    // of the array element
    for (int i = 0; i < n; i++) {
        int x = arr[i];

        // If say x = -1000 then we will place
        // the frequency of -1000 at
        // (-1000 + 1000 = 0) a[0] index
        freq[x + N]++;
    }

    // To store the count of valid pairs
    int ans = 0;

    // Remember we will check only for (even, even)
    // or (odd, odd) pairs of indexes as the average
    // of two consecutive elements is
    // a floating point number
    for (int i = 0; i < size; i++) {

        if (freq[i] > 0) {

            ans += ((freq[i]) * (freq[i] - 1)) / 2;

            for (int j = i + 2; j < 2001; j += 2) {
                if (freq[j] > 0 && (freq[(i + j) / 2] > 0)) {
                    ans += (freq[i] * freq[j]);
                }
            }
        }
    }
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 4, 2, 5, 1, 3, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << countPairs(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

    static int N = 1000;

    // Function to return the count
    // of valid pairs
    static int countPairs(int arr[], int n)
    {

        // Frequency array
        // Twice the original size to hold
        // negative elements as well
        int size = (2 * N) + 1;
        int freq[] = new int[size];

        // Update the frequency of each
        // of the array element
        for (int i = 0; i < n; i++)
        {
            int x = arr[i];

            // If say x = -1000 then we will place
            // the frequency of -1000 at
            // (-1000 + 1000 = 0) a[0] index
            freq[x + N]++;
        }

        // To store the count of valid pairs
        int ans = 0;

        // Remember we will check only for (even, even)
        // or (odd, odd) pairs of indexes as the average
        // of two consecutive elements is
        // a floating point number
        for (int i = 0; i < size; i++)
        {

            if (freq[i] > 0)
            {

                ans += ((freq[i]) * (freq[i] - 1)) / 2;

                for (int j = i + 2; j < 2001; j += 2)
                {
                    if (freq[j] > 0 && (freq[(i + j) / 2] > 0))
                    {
                        ans += (freq[i] * freq[j]);
                    }
                }
            }
        }
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {4, 2, 5, 1, 3, 5};
        int n = arr.length;

        System.out.println(countPairs(arr, n));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
N = 1000

# Function to return the count
# of valid pairs
def countPairs(arr, n):

    # Frequency array
    # Twice the original size to hold
    # negative elements as well
    size = (2 * N) + 1
    freq = [0 for i in range(size)]

    # Update the frequency of each
    # of the array element
    for i in range(n):
        x = arr[i]

        # If say x = -1000 then we will place
        # the frequency of -1000 at
        # (-1000 + 1000 = 0) a[0] index
        freq[x + N] += 1

    # To store the count of valid pairs
    ans = 0

    # Remember we will check only for (even, even)
    # or (odd, odd) pairs of indexes as the average
    # of two consecutive elements is
    # a floating point number
    for i in range(size):
        if (freq[i] > 0):
            ans += int(((freq[i]) * (freq[i] - 1)) / 2)

            for j in range(i + 2, 2001, 2):
                if (freq[j] > 0 and
                   (freq[int((i + j) / 2)] > 0)):
                    ans += (freq[i] * freq[j])

    return ans

# Driver code
if __name__ == '__main__':
    arr = [4, 2, 5, 1, 3, 5]
    n = len(arr)

    print(countPairs(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static int N = 1000;

    // Function to return the count
    // of valid pairs
    static int countPairs(int []arr, int n)
    {

        // Frequency array
        // Twice the original size to hold
        // negative elements as well
        int size = (2 * N) + 1;
        int []freq = new int[size];

        // Update the frequency of each
        // of the array element
        for (int i = 0; i < n; i++)
        {
            int x = arr[i];

            // If say x = -1000 then we will place
            // the frequency of -1000 at
            // (-1000 + 1000 = 0) a[0] index
            freq[x + N]++;
        }

        // To store the count of valid pairs
        int ans = 0;

        // Remember we will check only for (even, even)
        // or (odd, odd) pairs of indexes as the average
        // of two consecutive elements is
        // a floating point number
        for (int i = 0; i < size; i++)
        {

            if (freq[i] > 0)
            {

                ans += ((freq[i]) * (freq[i] - 1)) / 2;

                for (int j = i + 2; j < 2001; j += 2)
                {
                    if (freq[j] > 0 && (freq[(i + j) / 2] > 0))
                    {
                        ans += (freq[i] * freq[j]);
                    }
                }
            }
        }
        return ans;
    }

    // Driver code
    public static void Main()
    {
        int []arr = {4, 2, 5, 1, 3, 5};
        int n = arr.Length;

        Console.WriteLine(countPairs(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// javascript implementation of the approach
    var N = 1000;

    // Function to return the count
    // of valid pairs
    function countPairs(arr , n) {

        // Frequency array
        // Twice the original size to hold
        // negative elements as well
        var size = (2 * N) + 1;
        var freq = Array(size).fill(0);

        // Update the frequency of each
        // of the array element
        for (i = 0; i < n; i++) {
            var x = arr[i];

            // If say x = -1000 then we will place
            // the frequency of -1000 at
            // (-1000 + 1000 = 0) a[0] index
            freq[x + N]++;
        }

        // To store the count of valid pairs
        var ans = 0;

        // Remember we will check only for (even, even)
        // or (odd, odd) pairs of indexes as the average
        // of two consecutive elements is
        // a floating point number
        for (i = 0; i < size; i++) {

            if (freq[i] > 0) {

                ans += ((freq[i]) * (freq[i] - 1)) / 2;

                for (j = i + 2; j < 2001; j += 2) {
                    if (freq[j] > 0 && (freq[(i + j) / 2] > 0)) {
                        ans += (freq[i] * freq[j]);
                    }
                }
            }
        }
        return ans;
    }

    // Driver code

        var arr = [ 4, 2, 5, 1, 3, 5 ];
        var n = arr.length;

        document.write(countPairs(arr, n));

// This code contributed by Rajput-Ji
</script>
```

**Output:** 

```
7
```