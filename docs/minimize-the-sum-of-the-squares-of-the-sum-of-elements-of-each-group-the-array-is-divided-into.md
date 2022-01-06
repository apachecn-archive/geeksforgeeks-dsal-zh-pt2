# 最小化数组分成的每组元素之和的平方和

> 原文:[https://www . geesforgeks . org/最小化数组被分成的每个组的元素的平方和/](https://www.geeksforgeeks.org/minimize-the-sum-of-the-squares-of-the-sum-of-elements-of-each-group-the-array-is-divided-into/)

给定一个由**偶数**个元素组成的数组，任务是将该数组分成 **M** 个元素组(每个组必须至少包含 2 个元素)，使得每个组的和的平方和最小化，即
(组 1 的 _ 元素的和) <sup>2</sup> +(组 2 的 _ 元素的和) <sup>2</sup> +(组 3 的 _ 元素的和) <sup>2..+(sum _ of _ elements _ of _ groupM)<sup>2</sup>
**示例:**</sup> 

> **输入:** arr[] = {5，8，13，45，6，3}
> **输出:** 2824
> 组可以是(3，45)、(5，13)和(6，8)
> (3+45)<sup>2</sup>+(5+13)<sup>2</sup>+(6+8)<sup>2</sup>= 48<sup>2</sup>+18

**方法:**我们的最终总和取决于两个因素:

1.  每组元素的总和。
2.  所有这些组的平方和。

如果我们把上面提到的两个因素都最小化，我们就能把结果最小化。为了最小化第二个因素，我们应该制作最小尺寸的组，即只有两个元素。为了最小化第一个因素，我们可以将最小的数与最大的数配对，将第二个最小的数与第二个最大的数配对，以此类推。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimized sum
unsigned long long findAnswer(int n,
                       vector<int>& arr)
{

    // Sort the array to pair the elements
    sort(arr.begin(), arr.end());

    // Variable to hold the answer
    unsigned long long sum = 0;

    // Pair smallest with largest, second
    // smallest with second largest, and
    // so on
    for (int i = 0; i < n / 2; ++i) {
        sum += (arr[i] + arr[n - i - 1])
               * (arr[i] + arr[n - i - 1]);
    }

    return sum;
}

// Driver code
int main()
{
    std::vector<int> arr = { 53, 28, 143, 5 };
    int n = arr.size();
    cout << findAnswer(n, arr);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return the minimized sum
    static int findAnswer(int n, int[] arr)
    {

        // Sort the array to pair the elements
        Arrays.sort(arr);

        // Variable to hold the answer
        int sum = 0;

        // Pair smallest with largest, second
        // smallest with second largest, and
        // so on
        for (int i = 0; i < n / 2; ++i)
        {
            sum += (arr[i] + arr[n - i - 1])
                    * (arr[i] + arr[n - i - 1]);
        }

        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = {53, 28, 143, 5};
        int n = arr.length;
        System.out.println(findAnswer(n, arr));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the minimized sum
def findAnswer(n, arr):

    # Sort the array to pair the elements
    arr.sort(reverse = False)

    # Variable to hold the answer
    sum = 0

    # Pair smallest with largest, second
    # smallest with second largest, and
    # so on
    for i in range(int(n / 2)):
        sum += ((arr[i] + arr[n - i - 1]) *
                (arr[i] + arr[n - i - 1]))

    return sum

# Driver code
if __name__ == '__main__':
    arr = [53, 28, 143, 5]
    n = len(arr)
    print(findAnswer(n, arr))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the minimized sum
static int findAnswer(int n, int []arr)
{

    // Sort the array to pair the elements
    Array.Sort(arr);

    // Variable to hold the answer
    int sum = 0;

    // Pair smallest with largest, second
    // smallest with second largest, and
    // so on
    for (int i = 0; i < n / 2; ++i)
    {
        sum += (arr[i] + arr[n - i - 1])
            * (arr[i] + arr[n - i - 1]);
    }

    return sum;
}

// Driver code
static void Main()
{
    int []arr = { 53, 28, 143, 5 };
    int n = arr.Length;
    Console.WriteLine(findAnswer(n, arr));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the minimized sum
function findAnswer($n, $arr)
{

    // Sort the array to pair the elements
    sort($arr);

    // Variable to hold the answer
    $sum = 0;

    // Pair smallest with largest, second
    // smallest with second largest, and
    // so on
    for ($i = 0; $i < $n / 2; ++$i)
    {
        $sum += ($arr[$i] + $arr[$n - $i - 1]) *
                ($arr[$i] + $arr[$n - $i - 1]);
    }

    return $sum;
}

// Driver code
$arr = array( 53, 28, 143, 5);
$n = count($arr);
echo findAnswer($n, $arr);

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
// Javascript implementation of the approach

// Function to return the minimized sum
function findAnswer(n, arr)
{

    // Sort the array to pair the elements
    arr.sort((a, b) => a - b);

    // Variable to hold the answer
    let sum = 0;

    // Pair smallest with largest, second
    // smallest with second largest, and
    // so on
    for (let i = 0; i < Math.floor(n / 2); ++i)
    {
        sum += (arr[i] + arr[n - i - 1]) *
                (arr[i] + arr[n - i - 1]);
    }

    return sum;
}

// Driver code
let arr = new Array( 53, 28, 143, 5);
let n = arr.length;
document.write(findAnswer(n, arr));

// This code is contributed by _saurabh_jaiswal
```

**Output:** 

```
28465
```