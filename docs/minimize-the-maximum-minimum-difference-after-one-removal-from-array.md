# 从阵列中移除一次后，最小化最大最小差异

> 原文:[https://www . geeksforgeeks . org/从阵列中一次移除后最小化最大最小差异/](https://www.geeksforgeeks.org/minimize-the-maximum-minimum-difference-after-one-removal-from-array/)

给定一个大小为 **n ≥ 3** 的数组 **arr[]** ，任务是在移除一个元素后，从数组中找到最大和最小元素之间的最小可能差异。
**例:**

> **输入:** arr[] = {1，2，3}
> **输出:** 1
> 移除 1 将给出 3–2 = 1
> 移除 2，3–1 = 2
> 和移除 3 将导致 2–1 = 1
> **输入:** arr[] = {1，2，4，3，4}
> **输出:** 2

**天真方法:**很明显，要对差异产生影响，只需移除最小或最大元素。

*   对数组排序。
*   去掉最小值，存储**diff 1 = arr[n–1]–arr[1]**。
*   去掉最大值，**diff 2 = arr[n–2]–arr[0]**。
*   最后打印 **min(diff1，diff2)** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum required difference
int findMinDifference(int arr[], int n)
{
    // Sort the given array
    sort(arr, arr + n);

    // When minimum element is removed
    int diff1 = arr[n - 1] - arr[1];

    // When maximum element is removed
    int diff2 = arr[n - 2] - arr[0];

    // Return the minimum of diff1 and diff2
    return min(diff1, diff2);
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 4, 3, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << findMinDifference(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class solution
{

// Function to return the minimum required difference
static int findMinDifference(int arr[], int n)
{
    // Sort the given array
    Arrays.sort(arr);

    // When minimum element is removed
    int diff1 = arr[n - 1] - arr[1];

    // When maximum element is removed
    int diff2 = arr[n - 2] - arr[0];

    // Return the minimum of diff1 and diff2
    return Math.min(diff1, diff2);
}

// Driver Code
public static void  main(String args[])
{
    int arr[] = { 1, 2, 4, 3, 4 };
    int n = arr.length;

    System.out.print(findMinDifference(arr, n));

}
}
// This code is contributed by
// Sanjit_Prasad
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum
# required difference
def findMinDifference(arr, n) :

    # Sort the given array
    arr.sort()

    # When minimum element is removed
    diff1 = arr[n - 1] - arr[1]

    # When maximum element is removed
    diff2 = arr[n - 2] - arr[0]

    # Return the minimum of diff1 and diff2
    return min(diff1, diff2)

# Driver Code
if __name__ == "__main__" :

    arr = [ 1, 2, 4, 3, 4 ]
    n = len(arr)

    print(findMinDifference(arr, n))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

public class GFG{

// Function to return the minimum required difference
static int findMinDifference(int []arr, int n)
{
    // Sort the given array
    Array.Sort(arr);

    // When minimum element is removed
    int diff1 = arr[n - 1] - arr[1];

    // When maximum element is removed
    int diff2 = arr[n - 2] - arr[0];

    // Return the minimum of diff1 and diff2
    return Math.Min(diff1, diff2);
}

// Driver Code
    static public void Main (){

    int []arr = { 1, 2, 4, 3, 4 };
    int n = arr.Length;

    Console.Write(findMinDifference(arr, n));

}
}
// This code is contributed by Sachin..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the minimum
// required difference
function findMinDifference($arr, $n)
{
    // Sort the given array
    sort($arr, 0);

    // When minimum element is removed
    $diff1 = $arr[$n - 1] - $arr[1];

    // When maximum element is removed
    $diff2 = $arr[$n - 2] - $arr[0];

    // Return the minimum of diff1 and diff2
    return min($diff1, $diff2);
}

// Driver Code
$arr = array(1, 2, 4, 3, 4);
$n = sizeof($arr);

echo findMinDifference($arr, $n);

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the minimum required difference
    function findMinDifference(arr, n)
    {
        // Sort the given array
        arr.sort();

        // When minimum element is removed
        let diff1 = arr[n - 1] - arr[1];

        // When maximum element is removed
        let diff2 = arr[n - 2] - arr[0];

        // Return the minimum of diff1 and diff2
        return Math.min(diff1, diff2);
    }

    let arr = [ 1, 2, 4, 3, 4 ];
    let n = arr.length;

    document.write(findMinDifference(arr, n));

</script>
```

**Output:** 

```
2
```

**高效方法:**为了从数组中找到 **min** 、 **secondMin** 、 **max** 和 **secondMax** 元素。我们不需要对数组进行排序，它可以在单个数组遍历中完成。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the minimum required difference
int findMinDifference(int arr[], int n)
{
    int min__, secondMin, max__, secondMax;

    min__ = secondMax = (arr[0] < arr[1]) ? arr[0] : arr[1];
    max__ = secondMin = (arr[0] < arr[1]) ? arr[1] : arr[0];

    for (int i = 2; i < n; i++)
    {
        // If current element is greater than max
        if (arr[i] > max__)
        {
            // max will become secondMax
            secondMax = max__;

            // Update the max
            max__ = arr[i];
        }

        // If current element is greater than secondMax
        // but smaller than max
        else if (arr[i] > secondMax)
        {

            // Update the secondMax
            secondMax = arr[i];
        }

        // If current element is smaller than min
        else if (arr[i] < min__)
        {

            // min will become secondMin
            secondMin = min__;

            // Update the min
            min__ = arr[i];
        }

        // If current element is smaller than secondMin
        // but greater than min
        else if (arr[i] < secondMin) {

            // Update the secondMin
            secondMin = arr[i];
        }
    }

    // Minimum of the two possible differences
    int diff = min(max__ - secondMin, secondMax - min__);
    return diff;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 4, 3, 4 };
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << (findMinDifference(arr, n));
}

// This code is contributed by
// Shashank_Sharma
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG {

    // Function to return the minimum required difference
    static int findMinDifference(int arr[], int n)
    {
        int min, secondMin, max, secondMax;

        min = secondMax = (arr[0] < arr[1]) ? arr[0] : arr[1];
        max = secondMin = (arr[0] < arr[1]) ? arr[1] : arr[0];

        for (int i = 2; i < n; i++) {

            // If current element is greater than max
            if (arr[i] > max) {

                // max will become secondMax
                secondMax = max;

                // Update the max
                max = arr[i];
            }

            // If current element is greater than secondMax
            // but smaller than max
            else if (arr[i] > secondMax) {

                // Update the secondMax
                secondMax = arr[i];
            }

            // If current element is smaller than min
            else if (arr[i] < min) {

                // min will become secondMin
                secondMin = min;

                // Update the min
                min = arr[i];
            }

            // If current element is smaller than secondMin
            // but greater than min
            else if (arr[i] < secondMin) {

                // Update the secondMin
                secondMin = arr[i];
            }
        }

        // Minimum of the two possible differences
        int diff = Math.min(max - secondMin, secondMax - min);

        return diff;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 4, 3, 4 };
        int n = arr.length;

        System.out.println(findMinDifference(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the minimum
# required difference
def findMinDifference(arr, n):

    if(arr[0] < arr[1]):
        min__ = secondMax = arr[0]
    else:
        min__ = secondMax = arr[1]

    if(arr[0] < arr[1]):
        max__ = secondMin = arr[1]
    else:
        max__ = secondMin = arr[0]

    for i in range(2, n):

        # If current element is greater
        # than max
        if (arr[i] > max__):

            # max will become secondMax
            secondMax = max__

            # Update the max
            max__ = arr[i]

        # If current element is greater than
        # secondMax but smaller than max
        elif (arr[i] > secondMax):

            # Update the secondMax
            secondMax = arr[i]

        # If current element is smaller than min
        elif(arr[i] < min__):

            # min will become secondMin
            secondMin = min__

            # Update the min
            min__ = arr[i]

        # If current element is smaller than
        # secondMin but greater than min
        elif(arr[i] < secondMin):

            # Update the secondMin
            secondMin = arr[i]

    # Minimum of the two possible
    # differences
    diff = min(max__ - secondMin,
                       secondMax - min__)
    return diff

# Driver code
if __name__ == '__main__':
    arr = [1, 2, 4, 3, 4]
    n = len(arr)
    print(findMinDifference(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
using System;

// C# implementation of the approach
public class GFG {

    // Function to return the minimum required difference
    static int findMinDifference(int []arr, int n)
    {
        int min, secondMin, max, secondMax;

        min = secondMax = (arr[0] < arr[1]) ? arr[0] : arr[1];
        max = secondMin = (arr[0] < arr[1]) ? arr[1] : arr[0];

        for (int i = 2; i < n; i++) {

            // If current element is greater than max
            if (arr[i] > max) {

                // max will become secondMax
                secondMax = max;

                // Update the max
                max = arr[i];
            }

            // If current element is greater than secondMax
            // but smaller than max
            else if (arr[i] > secondMax) {

                // Update the secondMax
                secondMax = arr[i];
            }

            // If current element is smaller than min
            else if (arr[i] < min) {

                // min will become secondMin
                secondMin = min;

                // Update the min
                min = arr[i];
            }

            // If current element is smaller than secondMin
            // but greater than min
            else if (arr[i] < secondMin) {

                // Update the secondMin
                secondMin = arr[i];
            }
        }

        // Minimum of the two possible differences
        int diff = Math.Min(max - secondMin, secondMax - min);

        return diff;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 1, 2, 4, 3, 4 };
        int n = arr.Length;

        Console.WriteLine(findMinDifference(arr, n));
    }
}
// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the minimum
// required difference
function findMinDifference($arr, $n)
{

    $min__ = $secondMax = ($arr[0] < $arr[1]) ?
                           $arr[0] : $arr[1];
    $max__ = $secondMin = ($arr[0] < $arr[1]) ?
                           $arr[1] : $arr[0];

    for ($i = 2; $i < $n; $i++)
    {
        // If current element is greater than max
        if ($arr[$i] > $max__)
        {
            // max will become secondMax
            $secondMax = $max__;

            // Update the max
            $max__ = $arr[$i];
        }

        // If current element is greater than secondMax
        // but smaller than max
        else if ($arr[$i] > $secondMax)
        {

            // Update the secondMax
            $secondMax = $arr[$i];
        }

        // If current element is smaller than min
        else if ($arr[$i] < $min__)
        {

            // min will become secondMin
            $secondMin = $min__;

            // Update the min
            $min__ = $arr[$i];
        }

        // If current element is smaller than secondMin
        // but greater than min
        else if ($arr[$i] < $secondMin)
        {

            // Update the secondMin
            $secondMin = $arr[$i];
        }
    }

    // Minimum of the two possible differences
    $diff = min($max__ - $secondMin,
                         $secondMax - $min__);
    return $diff;
}

// Driver code
$arr = array( 1, 2, 4, 3, 4 );
$n = count($arr);
print(findMinDifference($arr, $n));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Function to return the minimum required difference
    function findMinDifference(arr, n)
    {
        let min__, secondMin, max__, secondMax;

        min__ = secondMax = (arr[0] < arr[1]) ? arr[0] : arr[1];
        max__ = secondMin = (arr[0] < arr[1]) ? arr[1] : arr[0];

        for (let i = 2; i < n; i++)
        {
            // If current element is greater than max
            if (arr[i] > max__)
            {
                // max will become secondMax
                secondMax = max__;

                // Update the max
                max__ = arr[i];
            }

            // If current element is greater than secondMax
            // but smaller than max
            else if (arr[i] > secondMax)
            {

                // Update the secondMax
                secondMax = arr[i];
            }

            // If current element is smaller than min
            else if (arr[i] < min__)
            {

                // min will become secondMin
                secondMin = min__;

                // Update the min
                min__ = arr[i];
            }

            // If current element is smaller than secondMin
            // but greater than min
            else if (arr[i] < secondMin) {

                // Update the secondMin
                secondMin = arr[i];
            }
        }

        // Minimum of the two possible differences
        let diff = Math.min(max__ - secondMin, secondMax - min__);
        return diff;
    }  

    let arr = [ 1, 2, 4, 3, 4 ];
    let n = arr.length;
    document.write(findMinDifference(arr, n));

</script>
```

**Output:** 

```
2
```