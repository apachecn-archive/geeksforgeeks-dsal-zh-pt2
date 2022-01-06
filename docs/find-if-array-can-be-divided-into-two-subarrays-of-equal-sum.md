# 求数组是否可以分成两个和相等的子数组

> 原文:[https://www . geesforgeks . org/find-if-array-can-divide-two-subarray-of-equal-sum/](https://www.geeksforgeeks.org/find-if-array-can-be-divided-into-two-subarrays-of-equal-sum/)

给定一个整数数组，找出是否有可能从数组中恰好移除一个整数，该整数将数组分成两个具有相同和的子数组。
示例:

```
Input:  arr = [6, 2, 3, 2, 1]
Output:  true
Explanation:  On removing element 2 at index 1,
the array gets divided into two subarrays [6]
 and [3, 2, 1] having equal sum

Input:  arr = [6, 1, 3, 2, 5]
Output:  true
Explanation:  On removing element 3 at index 2,
the array gets divided into two subarrays [6, 1]
and [2, 5] having equal sum.

Input:  arr = [6, -2, -3, 2, 3]
Output: true
Explanation:  On removing element 6 at index 0, 
the array gets divided into two sets [] 
and [-2, -3, 2, 3] having equal sum

Input:  arr = [6, -2, 3, 2, 3]
Output: false
```

一个简单的解决方案是考虑数组的所有元素，计算它们的左右和，如果发现左右和相等，则返回真。该解决方案的时间复杂度为 0(n<sup>2</sup>)。
高效解决方案**包括提前计算数组中所有元素的和。然后对于数组的每个元素，我们可以通过使用数组元素的总和减去到目前为止找到的元素总和来计算它在 O(1)时间内的右总和。该解决方案的时间复杂度为 O(n)，其使用的辅助空间为 O(1)。
以下是上述方法的实施:** 

## C++

```
// C++ program to divide the array into two
// subarrays with the same sum on removing
// exactly one integer from the array
#include <iostream>
using namespace std;

// Utility function to print the sub-array
void printSubArray(int arr[], int start, int end)
{
    cout << "[ ";
    for (int i = start; i <= end; i++)
        cout << arr[i] << " ";
    cout << "] ";
}

// Function that divides the array into two subarrays
// with the same sum
bool divideArray(int arr[], int n)
{
    // sum stores sum of all elements of the array
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // sum stores sum till previous index of the array
    int sum_so_far = 0;

    for (int i = 0; i < n; i++)
    {
        // If on removing arr[i], we get equals left
        // and right half
        if (2 * sum_so_far + arr[i] == sum)
        {
            cout << "The array can be divided into
                    "two subarrays with equal sum\nThe"
                    " two subarrays are - ";
            printSubArray(arr, 0, i - 1);
            printSubArray(arr, i + 1, n - 1);

            return true;
        }
        // add current element to sum_so_far
        sum_so_far += arr[i];
    }

    // The array cannot be divided
    cout << "The array cannot be divided into two "
         "subarrays with equal sum";

    return false;
}

// Driver code
int main()
{
    int arr[] = {6, 2, 3, 2, 1};
    int n = sizeof(arr)/sizeof(arr[0]);

    divideArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to divide the array into two
// subarrays with the same sum on removing
// exactly one integer from the array
import java.io.*;

class GFG
{
    // Utility function to print the sub-array
    static void printSubArray(int arr[], int start, int end)
    {
        System.out.print("[ ");
        for (int i = start; i <= end; i++)
            System.out.print(arr[i] +" ");
        System.out.print("] ");
    }

    // Function that divides the array into two subarrays
    // with the same sum
    static boolean divideArray(int arr[], int n)
    {
        // sum stores sum of all elements of the array
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];

        // sum stores sum till previous index of the array
        int sum_so_far = 0;

        for (int i = 0; i < n; i++)
        {
            // If on removing arr[i], we get equals left
            // and right half
            if (2 * sum_so_far + arr[i] == sum)
            {
                System.out.print("The array can be divided into "
                    +"two subarrays with equal sum\nThe"
                    +" two subarrays are - ");
                printSubArray(arr, 0, i - 1);
                printSubArray(arr, i + 1, n - 1);

                return true;
            }
            // add current element to sum_so_far
            sum_so_far += arr[i];
        }

        // The array cannot be divided
        System.out.println("The array cannot be divided into two "
                +"subarrays with equal sum");

        return false;
    }

    // Driver program
    public static void main (String[] args)
    {
        int arr[] = {6, 2, 3, 2, 1};
        int n = arr.length;

        divideArray(arr, n);
    }
}

// This code is contributed by Pramod Kumar
```

## 蟒蛇 3

```
''' Python3 program to divide the array
into two subarrays with the same sum on
removing exactly one integer from the array'''

# Utility function to print the sub-array
def printSubArray(arr, start, end):
    print ("[ ", end = "")
    for i in range(start, end+1):
        print (arr[i], end =" ")
    print ("]", end ="")

# Function that divides the array into
# two subarrays with the same sum
def divideArray(arr, n):

    # sum stores sum of all
    # elements of the array
    sum = 0
    for i in range(0, n):
        sum += arr[i]

    # sum stores sum till previous
    # index of the array
    sum_so_far = 0
    for i in range(0, n):

        # If on removing arr[i], we get
        # equals left and right half
        if 2 * sum_so_far + arr[i] == sum:
            print ("The array can be divided into",
                    "two subarrays with equal sum")
            print ("two subarrays are -", end = "")
            printSubArray(arr, 0, i - 1)
            printSubArray(arr, i + 1, n - 1)
            return True

        # add current element to sum_so_far
        sum_so_far += arr[i]

    # The array cannot be divided
    print ("The array cannot be divided into"
           "two subarrays with equal sum", end = "")

    return False

# Driver code
arr = [6, 2, 3, 2, 1]
n = len(arr)
divideArray(arr, n)

# This code is contributed by Shreyanshi Arun
```

## C#

```
// C# program to divide the array into two
// subarrays with the same sum on removing
// exactly one integer from the array
using System;

class GFG {

    // Utility function to print the sub-array
    static void printSubArray(int []arr,
                           int start, int end)
    {
        Console.Write("[ ");
        for (int i = start; i <= end; i++)
            Console.Write(arr[i] +" ");
        Console.Write("] ");
    }

    // Function that divides the array into
    // two subarrays with the same sum
    static bool divideArray(int []arr, int n)
    {

        // sum stores sum of all elements of
        // the array
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];

        // sum stores sum till previous index
        // of the array
        int sum_so_far = 0;

        for (int i = 0; i < n; i++)
        {

            // If on removing arr[i], we get
            // equals left and right half
            if (2 * sum_so_far + arr[i] == sum)
            {
                Console.Write("The array can be"
                 + " divided into two subarrays"
                 + " with equal sum\nThe two"
                 + " subarrays are - ");
                printSubArray(arr, 0, i - 1);
                printSubArray(arr, i + 1, n - 1);

                return true;
            }
            // add current element to sum_so_far
            sum_so_far += arr[i];
        }

        // The array cannot be divided
        Console.WriteLine("The array cannot be"
          + " divided into two subarrays with "
                                + "equal sum");

        return false;
    }

    // Driver program
    public static void Main ()
    {
        int []arr = {6, 2, 3, 2, 1};
        int n = arr.Length;

        divideArray(arr, n);
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to divide the array into two
// subarrays with the same sum on removing
// exactly one integer from the array

// Utility function to print the sub-array
function printSubArray($arr, $start, $end)
{
    echo "[ ";
    for ($i = $start; $i <= $end; $i++)
        echo $arr[$i] . " ";
    echo "] ";
}

// Function that divides the
// array into two subarrays
// with the same sum
function divideArray($arr, $n)
{

    // sum stores sum of all
    // elements of the array
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        $sum += $arr[$i];

    // sum stores sum till previous
    // index of the array
    $sum_so_far = 0;

    for ($i = 0; $i < $n; $i++)
    {

        // If on removing arr[i],
        // we get equals left
        // and right half
        if (2 * $sum_so_far + $arr[$i] == $sum)
        {
            echo "The array can be divided into" .
                 "two subarrays with equal sum\nThe".
                 " two subarrays are - ";
            printSubArray($arr, 0, $i - 1);
            printSubArray($arr, $i + 1, $n - 1);

            return true;
        }

        // add current element
        // to sum_so_far
        $sum_so_far += $arr[$i];
    }

    // The array cannot be divided
    echo "The array cannot be divided into two ".
         "subarrays with equal sum";

    return false;
}

    // Driver code
    $arr = array(6, 2, 3, 2, 1);
    $n = sizeof($arr);

    divideArray($arr, $n);

// This code is contributed by Anuj_67
?>
```

## java 描述语言

```
<script>

    // JavaScript program to divide the array into two
    // subarrays with the same sum on removing
    // exactly one integer from the array

    // Utility function to print the sub-array
    function printSubArray(arr, start, end)
    {
        document.write("[ ");
        for (let i = start; i <= end; i++)
            document.write(arr[i] +" ");
        document.write("] ");
    }

    // Function that divides the array into
    // two subarrays with the same sum
    function divideArray(arr, n)
    {

        // sum stores sum of all elements of
        // the array
        let sum = 0;
        for (let i = 0; i < n; i++)
            sum += arr[i];

        // sum stores sum till previous index
        // of the array
        let sum_so_far = 0;

        for (let i = 0; i < n; i++)
        {

            // If on removing arr[i], we get
            // equals left and right half
            if (2 * sum_so_far + arr[i] == sum)
            {
                document.write("The array can be"
                 + " divided into two subarrays"
                 + " with equal sum " + "</br>" + "The two"
                 + " sets are - ");
                printSubArray(arr, 0, i - 1);
                printSubArray(arr, i + 1, n - 1);

                return true;
            }
            // add current element to sum_so_far
            sum_so_far += arr[i];
        }

        // The array cannot be divided
        document.write("The array cannot be"
          + " divided into two subarrays with "
                                + "equal sum" + "</br>");

        return false;
    }

    let arr = [6, 2, 3, 2, 1];
    let n = arr.length;

    divideArray(arr, n);

</script>
```

**输出:**

```
The array can be divided into two subarrays with equal sum
The two sets are - [6] [3 2 1]
```

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。