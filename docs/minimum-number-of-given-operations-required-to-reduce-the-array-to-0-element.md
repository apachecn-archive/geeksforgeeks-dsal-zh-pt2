# 将数组简化为 0 元素所需的最小给定操作数

> 原文:[https://www . geesforgeks . org/最小给定操作数-将数组缩减为 0 元素所需的操作数/](https://www.geeksforgeeks.org/minimum-number-of-given-operations-required-to-reduce-the-array-to-0-element/)

给定一个由 **N** 个整数组成的数组 **arr[]** 。任务是找到将数组减少到 0 个元素所需的最小给定操作数。在一次操作中，可以从数组中选择任何元素，并移除它的所有倍数，包括它自己。
**例:**

> **输入:** arr[] = {2，4，6，3，4，6，8}
> **输出:** 2
> 操作 1:选择 2 并删除所有倍数，arr[] = {3}
> 操作 3:选择 3，数组变为 0 元素。
> **输入:** arr[] = {2，4，2，4，4，4}
> **输出:** 1

**天真的方法:**在每一步从数组中找到最小值，遍历整个数组找到这些元素的倍数并删除它们。
**高效进场:**

*   创建一个计数数组，存储数组中每个数字的计数。
*   因为我们知道对于一个数 x，满足条件(A % x == 0)的元素实际上是 x 的倍数，因此我们需要找到每个数的倍数，并将它们的频率设置为 0，包括所选元素本身。
*   现在对于每个数，我们遍历它的倍数一次，然后从它的所有倍数中减去这个数的计数值。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum
// operations required
int minOperations(int* arr, int n)
{
    int maxi, result = 0;

    // Count the frequency of each element
    vector<int> freq(1000001, 0);
    for (int i = 0; i < n; i++) {
        int x = arr[i];
        freq[x]++;
    }

    // Maximum element from the array
    maxi = *(max_element(arr, arr + n));
    for (int i = 1; i <= maxi; i++) {
        if (freq[i] != 0) {

            // Find all the multiples of i
            for (int j = i * 2; j <= maxi; j = j + i) {

                // Delete the multiples
                freq[j] = 0;
            }

            // Increment the operations
            result++;
        }
    }
    return result;
}

// Driver code
int main()
{
    int arr[] = { 2, 4, 2, 4, 4, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << minOperations(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;

class GFG
{

    // Function to return the minimum
    // operations required
    static int minOperations(int[] arr, int n)
    {
        int maxi, result = 0;

        // Count the frequency of each element
        int[] freq = new int[1000001];
        for (int i = 0; i < n; i++)
        {
            int x = arr[i];
            freq[x]++;
        }

        // Maximum element from the array
        maxi = Arrays.stream(arr).max().getAsInt();
        for (int i = 1; i <= maxi; i++)
        {
            if (freq[i] != 0)
            {

                // Find all the multiples of i
                for (int j = i * 2; j <= maxi; j = j + i)
                {

                    // Delete the multiples
                    freq[j] = 0;
                }

                // Increment the operations
                result++;
            }
        }
        return result;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {2, 4, 2, 4, 4, 4};
        int n = arr.length;

        System.out.println(minOperations(arr, n));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum
# operations required
def minOperations(arr, n):

    result = 0

    # Count the frequency of each element
    freq = [0] * 1000001

    for i in range(0, n):
        freq[arr[i]] += 1

    # Maximum element from the array
    maxi = max(arr)
    for i in range(1, maxi+1):
        if freq[i] != 0:

            # Find all the multiples of i
            for j in range(i * 2, maxi+1, i):

                # Delete the multiples
                freq[j] = 0

            # Increment the operations
            result += 1

    return result

# Driver code
if __name__ == "__main__":

    arr = [2, 4, 2, 4, 4, 4]
    n = len(arr)

    print(minOperations(arr, n))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of above approach
using System;
using System.Linq;

class GFG
{

    // Function to return the minimum
    // operations required
    static int minOperations(int[] arr, int n)
    {
        int maxi, result = 0;

        // Count the frequency of each element
        int[] freq = new int[1000001];
        for (int i = 0; i < n; i++)
        {
            int x = arr[i];
            freq[x]++;
        }

        // Maximum element from the array
        maxi = arr.Max();
        for (int i = 1; i <= maxi; i++)
        {
            if (freq[i] != 0)
            {

                // Find all the multiples of i
                for (int j = i * 2; j <= maxi; j = j + i)
                {

                    // Delete the multiples
                    freq[j] = 0;
                }

                // Increment the operations
                result++;
            }
        }
        return result;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {2, 4, 2, 4, 4, 4};
        int n = arr.Length;

        Console.WriteLine(minOperations(arr, n));
    }
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the minimum
// operations required
function minOperations($arr, $n)
{
    $result = 0;

    $freq = array();

    // Count the frequency of each element
    for($i = 0; $i < $n; $i++)
    {
        $freq[$arr[$i]] = 0;
    }

    for ($i = 0; $i < $n; $i++)
    {
        $x = $arr[$i];
        $freq[$x]++;
    }

    // Maximum element from the array
    $maxi = max($arr);
    for ($i = 1; $i <= $maxi; $i++)
    {
        if ($freq[$i] != 0)
        {

            // Find all the multiples of i
            for ($j = $i * 2;
                 $j <= $maxi; $j = $j + $i)
            {

                // Delete the multiples
                $freq[$j] = 0;
            }

            // Increment the operations
            $result++;
        }
    }
    return $result;
}

// Driver code
$arr = array( 2, 4, 2, 4, 4, 4 );
$n = count($arr);

echo minOperations($arr, $n);

// This code is contributed by AnkitRai01
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the minimum
// operations required
function minOperations(arr, n)
{
    let maxi, result = 0;

    // Count the frequency of each element
    let freq = new Array(1000001).fill(0);
    for (let i = 0; i < n; i++) {
        let x = arr[i];
        freq[x]++;
    }

    // Maximum element from the array
    maxi = Math.max(...arr);
    for (let i = 1; i <= maxi; i++) {
        if (freq[i] != 0) {

            // Find all the multiples of i
            for (let j = i * 2; j <= maxi; j = j + i) {

                // Delete the multiples
                freq[j] = 0;
            }

            // Increment the operations
            result++;
        }
    }
    return result;
}

// Driver code
    let arr = [ 2, 4, 2, 4, 4, 4 ];
    let n = arr.length;

    document.write(minOperations(arr, n));

</script>
```

**Output:** 

```
1
```