# 计算对(I，j)的数量，使得 arr[i]可以被 arr[j]整除，或者 arr[j]可以被 arr[i]整除

> 原文:[https://www . geeksforgeeks . org/count-对-I-j-so-arri 可被 arrj 整除或-arrj 可被 arri 整除/](https://www.geeksforgeeks.org/count-the-number-of-pairs-i-j-such-that-either-arri-is-divisible-by-arrj-or-arrj-is-divisible-by-arri/)

给定一个 N 个整数的数组 **arr[]** ，任务是找到无序索引对的计数 **(i，j)** ，这样 **i！= j** 和 **0 < =i < j < N** 并且 **arr[i]** 可以被 **arr[j]** 整除或者 **arr[j]** 可以被 **arr[i]** 整除。
**举例:**

> **输入:** arr[] = {2，4}
> **输出:** 1
> (0，1)是唯一可能的索引对。
> **输入:** arr[] = {3，2，4，2，6}
> **输出:** 6
> 可能的对是(0，4)，(1，2)，(1，3)，(1，4)，(2，3)和(3，4)。

**方法:**思路是从数组中找到最大元素，用变量**计数**存储无序对的个数，数组 **freq[]** 存储数组元素的频率。现在遍历数组，为每个元素找到可被数组中的**和**除尽且小于或等于数组中最大值的数。如果数组中存在该数字，则更新变量**计数**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find number of unordered pairs
int freqPairs(int arr[], int n)
{

    // Maximum element from the array
    int max = *(std::max_element(arr, arr + n));

    // Array to store the frequency of each
    // element
    int freq[max + 1] = { 0 };

    // Stores the number of unordered pairs
    int count = 0;

    // Store the frequency of each element
    for (int i = 0; i < n; i++)
        freq[arr[i]]++;

    // Find the number of unordered pairs
    for (int i = 0; i < n; i++) {
        for (int j = 2 * arr[i]; j <= max; j += arr[i]) {

            // If the number j divisible by ith element
            // is present in the array
            if (freq[j] >= 1)
                count += freq[j];
        }

        // If the ith element of the array
        // has frequency more than one
        if (freq[arr[i]] > 1) {
            count += freq[arr[i]] - 1;
            freq[arr[i]]--;
        }
    }

    return count;
}

// Driver code
int main()
{

    int arr[] = { 3, 2, 4, 2, 6 };
    int n = (sizeof(arr) / sizeof(arr[0]));

    cout << freqPairs(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;

// Java implementation of the approach
class GFG
{

    // Function to find number of unordered pairs
    static int freqPairs(int arr[], int n)
    {

        // Maximum element from the array
        int max = Arrays.stream(arr).max().getAsInt();

        // Array to store the frequency of each
        // element
        int freq[] = new int[max + 1];

        // Stores the number of unordered pairs
        int count = 0;

        // Store the frequency of each element
        for (int i = 0; i < n; i++)
        {
            freq[arr[i]]++;
        }

        // Find the number of unordered pairs
        for (int i = 0; i < n; i++)
        {
            for (int j = 2 * arr[i]; j <= max; j += arr[i])
            {

                // If the number j divisible by ith element
                // is present in the array
                if (freq[j] >= 1)
                {
                    count += freq[j];
                }
            }

            // If the ith element of the array
            // has frequency more than one
            if (freq[arr[i]] > 1)
            {
                count += freq[arr[i]] - 1;
                freq[arr[i]]--;
            }
        }

        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {3, 2, 4, 2, 6};
        int n = arr.length;

        System.out.println(freqPairs(arr, n));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to find number of unordered pairs
def freqPairs(arr, n):

    # Maximum element from the array
    max = arr[0]
    for i in range(len(arr)):
        if arr[i] > max:
            max = arr[i]

    # Array to store the frequency of
    # each element
    freq = [0 for i in range(max + 1)]

    # Stores the number of unordered pairs
    count = 0

    # Store the frequency of each element
    for i in range(n):
        freq[arr[i]] += 1

    # Find the number of unordered pairs
    for i in range(n):
        for j in range(2 * arr[i],
                           max + 1, arr[i]):

            # If the number j divisible by ith
            # element is present in the array
            if (freq[j] >= 1):
                count += freq[j]

        # If the ith element of the array
        # has frequency more than one
        if (freq[arr[i]] > 1):
            count += freq[arr[i]] - 1
            freq[arr[i]] -= 1

    return count

# Driver code
if __name__ == '__main__':
    arr = [3, 2, 4, 2, 6]
    n = len(arr)

    print(freqPairs(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Linq;

class GFG
{

    // Function to find number of unordered pairs
    static int freqPairs(int []arr, int n)
    {

        // Maximum element from the array
        int max = arr.Max();

        // Array to store the frequency of each
        // element
        int []freq = new int[max + 1];

        // Stores the number of unordered pairs
        int count = 0;

        // Store the frequency of each element
        for (int i = 0; i < n; i++)
        {
            freq[arr[i]]++;
        }

        // Find the number of unordered pairs
        for (int i = 0; i < n; i++)
        {
            for (int j = 2 * arr[i]; j <= max; j += arr[i])
            {

                // If the number j divisible by ith element
                // is present in the array
                if (freq[j] >= 1)
                {
                    count += freq[j];
                }
            }

            // If the ith element of the array
            // has frequency more than one
            if (freq[arr[i]] > 1)
            {
                count += freq[arr[i]] - 1;
                freq[arr[i]]--;
            }
        }

        return count;
    }

    // Driver code
    public static void Main(String []args)
    {
        int []arr = {3, 2, 4, 2, 6};
        int n = arr.Length;

        Console.WriteLine(freqPairs(arr, n));
    }
}

// This code has been contributed by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to find number of unordered pairs
function freqPairs($arr, $n)
{

    // Maximum element from the array
    $max = max($arr);

    // Array to store the frequency of
    // each element
    $freq = array_fill(0, $max + 1, 0);

    // Stores the number of unordered pairs
    $count = 0;

    // Store the frequency of each element
    for ($i = 0; $i < $n; $i++)
        $freq[$arr[$i]]++;

    // Find the number of unordered pairs
    for ($i = 0; $i < $n; $i++)
    {
        for ($j = 2 * $arr[$i];
             $j <= $max; $j += $arr[$i])
        {

            // If the number j divisible by ith
            // element is present in the array
            if ($freq[$j] >= 1)
                $count += $freq[$j];
        }

        // If the ith element of the array
        // has frequency more than one
        if ($freq[$arr[$i]] > 1)
        {
            $count += $freq[$arr[$i]] - 1;
            $freq[$arr[$i]]--;
        }
    }

    return $count;
}

// Driver code
$arr = array(3, 2, 4, 2, 6);
$n = count($arr);

echo freqPairs($arr, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to find number of unordered pairs
function freqPairs(arr, n)
{

    // Maximum element from the array
    let max = Math.max(...arr);

    // Array to store the frequency of each
    // element
    let freq = new Array(max + 1).fill(0);

    // Stores the number of unordered pairs
    let count = 0;

    // Store the frequency of each element
    for (let i = 0; i < n; i++)
        freq[arr[i]]++;

    // Find the number of unordered pairs
    for (let i = 0; i < n; i++) {
        for (let j = 2 * arr[i]; j <= max; j += arr[i]) {

            // If the number j divisible by ith element
            // is present in the array
            if (freq[j] >= 1)
                count += freq[j];
        }

        // If the ith element of the array
        // has frequency more than one
        if (freq[arr[i]] > 1) {
            count += freq[arr[i]] - 1;
            freq[arr[i]]--;
        }
    }

    return count;
}

// Driver code

    let arr = [ 3, 2, 4, 2, 6 ];
    let n = arr.length;

    document.write(freqPairs(arr, n));

</script>
```

**Output:** 

```
6
```