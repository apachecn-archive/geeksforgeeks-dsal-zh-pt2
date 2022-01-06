# 给定数组的 arr[i] % arr[j]的最大值

> 原文:[https://www . geeksforgeeks . org/给定数组的最大 arri-arrj 值/](https://www.geeksforgeeks.org/maximum-value-of-arri-arrj-for-a-given-array/)

给定一个数组 **arr[]** ，任务是为所有可能的对找到 **arr[i] % arr[j]** 的最大值。
**例:**

> **输入:** arr[] = { 2，3 }
> **输出:** 2
> 2 % 3 = 2
> 3 % 2 = 1
> **输入:** arr[] = { 2，2，2，2 }
> **输出:** 0

**天真方法:**运行两个嵌套循环，计算每对循环的 **arr[i] % arr[j]** 的值。根据计算值更新答案。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return maximum value of
// arr[i] % arr[j]
int computeMaxValue(const int* arr, int n)
{
    int ans = 0;
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {

            // Check pair (x, y) as well as
            // (y, x) for maximum value
            int val = max(arr[i] % arr[j],
                          arr[j] % arr[i]);

            // Update the answer
            ans = max(ans, val);
        }
    }
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 2, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << computeMaxValue(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

import java.util.*;
class GFG
{

    // Function to return maximum value of
    // arr[i] % arr[j]
    static int computeMaxValue(int []arr, int n)
    {
        int ans = 0;
        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {

                // Check pair (x, y) as well as
                // (y, x) for maximum value
                int val = Math.max(arr[i] % arr[j],
                            arr[j] % arr[i]);

                // Update the answer
                ans = Math.max(ans, val);
            }
        }
        return ans;
    }

    // Driver code
    public static void main(String []args)
    {
        int []arr = { 2, 3 };
        int n = arr.length;
        System.out.println(computeMaxValue(arr, n));

    }

}

// This code is contributed
// by ihritik
```

## 蟒蛇 3

```
# Python3  implementation of the above approach

# Function to return maximum value of
# arr[i] % arr[j]
def computeMaxValue(arr, n):

    ans = 0
    for i in range(0, n-1):
        for j in range( i+1, n):

            # Check pair (x, y) as well as
            # (y, x) for maximum value
            val = max(arr[i] % arr[j], arr[j] % arr[i])

            # Update the answer
            ans = max(ans, val)

    return ans

# Driver code
arr = [ 2, 3 ]
n = len(arr)
print(computeMaxValue(arr, n))

# This code is contributed
# by ihritik
```

## C#

```
// C# implementation of the above approach

using System;
class GFG
{

    // Function to return maximum value of
    // arr[i] % arr[j]
    static int computeMaxValue(int []arr, int n)
    {
        int ans = 0;
        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {

                // Check pair (x, y) as well as
                // (y, x) for maximum value
                int val = Math.Max(arr[i] % arr[j],
                            arr[j] % arr[i]);

                // Update the answer
                ans = Math.Max(ans, val);
            }
        }
        return ans;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 2, 3 };
        int n = arr.Length;
        Console.WriteLine(computeMaxValue(arr, n));

    }

}

// This code is contributed
// by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to return maximum value of
// arr[i] % arr[j]
function computeMaxValue($arr, $n)
{
    $ans = 0;
    for ($i = 0; $i < $n - 1; $i++) {
        for ($j = $i + 1; $j < $n; $j++) {

            // Check pair (x, y) as well as
            // (y, x) for maximum value
            $val = max($arr[$i] % $arr[$j],
                        $arr[$j] % $arr[$i]);

            // Update the answer
            $ans = max($ans, $val);
        }
    }
    return $ans;
}

// Driver code
$arr = array( 2, 3 );
$n = sizeof($arr);
echo computeMaxValue($arr, $n);

// This code is contributed
// by ihritik

?>
```

## java 描述语言

```
<script>

    // Javascript implementation of
    // the above approach

    // Function to return maximum value of
    // arr[i] % arr[j]
    function computeMaxValue(arr, n)
    {
        let ans = 0;
        for (let i = 0; i < n - 1; i++) {
            for (let j = i + 1; j < n; j++) {

                // Check pair (x, y) as well as
                // (y, x) for maximum value
                let val = Math.max(arr[i] % arr[j],
                            arr[j] % arr[i]);

                // Update the answer
                ans = Math.max(ans, val);
            }
        }
        return ans;
    }

    let arr = [ 2, 3 ];
    let n = arr.length;
    document.write(computeMaxValue(arr, n));

</script>
```

**Output:** 

```
2
```

**有效途径:**当 **A < B** 和 **A 和 B 最大可能**时， **A % B** 的最大值产生。换句话说，结果将是数组中第二大的元素，除了数组中所有元素都相同的情况(在这种情况下，结果将是 **0** )。

> A =数组的第二大元素。
> B =数组的最大元素和 A<B .
> A % B 的最大值= A.
> **角例:**如果数组的所有元素都相同，说 **arr[] = {x，x，x，x}** 那么结果就是 x % x = **0** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return maximum value of
// arr[i] % arr[j]
int computeMaxValue(const int* arr, int n)
{
    bool allSame = true;
    int i = 1;
    while (i < n) {

        // If current element is different
        // from the previous element
        if (arr[i] != arr[i - 1]) {
            allSame = false;
            break;
        }
        i++;
    }

    // If all the elements of the array are equal
    if (allSame)
        return 0;

    // Maximum element from the array
    int max = *std::max_element(arr, arr + n);
    int secondMax = 0;
    for (i = 0; i < n; i++) {
        if (arr[i] < max && arr[i] > secondMax)
            secondMax = arr[i];
    }

    // Return the second maximum element
    // from the array
    return secondMax;
}

// Driver code
int main()
{
    int arr[] = { 2, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << computeMaxValue(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

// Function to return maximum value of
// arr[i] % arr[j]
static int computeMaxValue(int arr[], int n)
{
    boolean allSame = true;
    int i = 1;
    while (i < n)
    {

        // If current element is different
        // from the previous element
        if (arr[i] != arr[i - 1])
        {
            allSame = false;
            break;
        }
        i++;
    }

    // If all the elements of the
    // array are equal
    if (allSame)
        return 0;

    // Maximum element from the array
    int max = -1;
    for(i = 0; i < n; i++)
    {
        if(max < arr[i])
        max = arr[i];
    }
    int secondMax = 0;
    for (i = 0; i < n; i++)
    {
        if (arr[i] < max && arr[i] > secondMax)
            secondMax = arr[i];
    }

    // Return the second maximum element
    // from the array
    return secondMax;
}

// Driver code
public static void main(String[] args)
{
    int []arr = { 2, 3 };
    int n = arr.length;
    System.out.println(computeMaxValue(arr, n));
}
}

// This code is contributed
// by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to return maximum value
# of arr[i] % arr[j]
def computeMaxValue(arr, n) :

    allSame = True;
    i = 1;
    while (i < n) :

        # If current element is different
        # from the previous element
        if (arr[i] != arr[i - 1]) :
            allSame = False
            break

        i += 1

    # If all the elements of the
    # array are equal
    if (allSame) :
        return 0

    # Maximum element from the array
    max_element = max(arr)

    secondMax = 0
    for i in range(n) :
        if (arr[i] < max_element and
            arr[i] > secondMax) :
            secondMax = arr[i]

    # Return the second maximum element
    # from the array
    return secondMax

# Driver code
if __name__ == "__main__" :
    arr = [ 2, 3 ]
    n = len(arr)

    print(computeMaxValue(arr, n))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function to return maximum value of
// arr[i] % arr[j]
static int computeMaxValue(int[] arr, int n)
{
    bool allSame = true;
    int i = 1;
    while (i < n)
    {

        // If current element is different
        // from the previous element
        if (arr[i] != arr[i - 1])
        {
            allSame = false;
            break;
        }
        i++;
    }

    // If all the elements of the
    // array are equal
    if (allSame)
        return 0;

    // Maximum element from the array
    int max = -1;
    for(i = 0; i < n; i++)
    {
        if(max < arr[i])
        max = arr[i];
    }
    int secondMax = 0;
    for (i = 0; i < n; i++)
    {
        if (arr[i] < max && arr[i] > secondMax)
            secondMax = arr[i];
    }

    // Return the second maximum element
    // from the array
    return secondMax;
}

// Driver code
public static void Main()
{
    int[] arr = { 2, 3 };
    int n = arr.Length;
    Console.Write(computeMaxValue(arr, n));
}
}

// This code is contributed by Ita_c.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to return maximum value of
// arr[i] % arr[j]
function computeMaxValue($arr, $n)
{
    $allSame = true;
    $i = 1;
    while ($i < $n)
    {

        // If current element is different
        // from the previous element
        if ($arr[$i] != $arr[$i - 1])
        {
            $allSame = false;
            break;
        }
        $i++;
    }

    // If all the elements of the
    // array are equal
    if ($allSame)
        return 0;

    // Maximum element from the array
    $max = max($arr);
    $secondMax = 0;
    for ($i = 0; $i < $n; $i++)
    {
        if ($arr[$i] < $max &&
            $arr[$i] > $secondMax)
            $secondMax = $arr[$i];
    }

    // Return the second maximum
    // element from the array
    return $secondMax;
}

// Driver code
$arr = array(2, 3);
$n = sizeof($arr);
echo computeMaxValue($arr, $n);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>   
    // Javascript implementation of the above approach

    // Function to return maximum value of
    // arr[i] % arr[j]
    function computeMaxValue(arr, n)
    {
        let allSame = true;
        let i = 1;
        while (i < n)
        {

            // If current element is different
            // from the previous element
            if (arr[i] != arr[i - 1])
            {
                allSame = false;
                break;
            }
            i++;
        }

        // If all the elements of the
        // array are equal
        if (allSame)
            return 0;

        // Maximum element from the array
        let max = -1;
        for(i = 0; i < n; i++)
        {
            if(max < arr[i])
                max = arr[i];
        }
        let secondMax = 0;
        for (i = 0; i < n; i++)
        {
            if (arr[i] < max && arr[i] > secondMax)
                secondMax = arr[i];
        }

        // Return the second maximum element
        // from the array
        return secondMax;
    }

    let arr = [ 2, 3 ];
    let n = arr.length;
    document.write(computeMaxValue(arr, n));

</script>
```

**Output:** 

```
2
```