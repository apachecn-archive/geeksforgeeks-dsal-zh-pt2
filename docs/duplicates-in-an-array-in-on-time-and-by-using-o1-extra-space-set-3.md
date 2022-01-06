# 在 O(n)个时间内通过使用 O(1)个额外空间在数组中复制| Set-3

> 原文:[https://www . geesforgeks . org/time-on-use-O1-extra-space-set-3 阵列中的重复项/](https://www.geeksforgeeks.org/duplicates-in-an-array-in-on-time-and-by-using-o1-extra-space-set-3/)

给定 n 个元素的数组，其中包含从 0 到 n-1 的元素，这些数字中的任何一个出现任意次。在 O(n)中找到这些重复的数字，并且只使用恒定的内存空间。要求保持元素重复的顺序。如果不存在重复元素，则打印-1。
**例:**

```
Input : arr[] = {1, 2, 3, 1, 3, 6, 6}
Output : 1, 3, 6
Elements 1, 3 and 6 are repeating.
Second occurrence of 1 is found
first followed by repeated occurrence
of 3 and 6.

Input : arr[] = {0, 3, 1, 3, 0}
Output : 3, 0
Second occurrence of 3 is found
first followed by second occurrence 
of 0.
```

[Recommended: Please solve it on *“PRACTICE”* first, before moving on to the solution.](https://practice.geeksforgeeks.org/problems/find-duplicates-in-an-array/1)

我们在下面的帖子中讨论了这个问题的两种方法:
[在 O(n)时间和 O(1)额外空间中查找重复项|集合 1](https://www.geeksforgeeks.org/find-duplicates-in-on-time-and-constant-extra-space/)
[在 O(n)时间和通过使用 O(1)额外空间在数组中查找重复项|集合-2](https://www.geeksforgeeks.org/duplicates-array-using-o1-extra-space-set-2/)
第一种方法有一个问题。它会多次打印重复的数字。例如:{1，6，3，1，3，6，6}它将输出为:3 6 6。在第二种方法中，虽然每个重复的项目只打印一次，但是它们重复出现的顺序没有被保持。为了按重复的顺序打印元素，修改了第二种方法。为了标记数组元素大小的存在，n 被添加到对应于数组元素 arr[i]的索引位置 arr[i]。在添加 n 之前，检查索引 arr[i]处的值是否大于或等于 n。如果它大于或等于，那么这意味着元素 arr[i]正在重复。为了避免多次打印重复元素，请检查它是否是 arr[i]的第一次重复。如果索引位置 arr[i]处的值小于 2*n，则这是第一次重复。这是因为，如果元素 arr[i]之前只出现过一次，则 n 只被添加到索引 arr[i]一次，因此索引 arr[i]处的值小于 2*n。将 n 添加到索引 arr[i]中，使得该值变得大于或等于 2*n，这将阻止当前重复元素的进一步打印。此外，如果索引 arr[i]处的值小于 n，则它是元素 arr[i]的第一次出现(而不是重复)。所以为了标记这个，在索引 arr[i]处给元素添加 n。
以下是上述方法的实施:

## C++

```
// C++ program to print all elements that
// appear more than once.
#include <bits/stdc++.h>
using namespace std;

// Function to find repeating elements
void printDuplicates(int arr[], int n)
{
    int i;

    // Flag variable used to
    // represent whether repeating
    // element is found or not.
    int fl = 0;

    for (i = 0; i < n; i++) {

        // Check if current element is
        // repeating or not. If it is
        // repeating then value will
        // be greater than or equal to n.
        if (arr[arr[i] % n] >= n) {

            // Check if it is first
            // repetition or not. If it is
            // first repetition then value
            // at index arr[i] is less than
            // 2*n. Print arr[i] if it is
            // first repetition.
            if (arr[arr[i] % n] < 2 * n) {
                cout << arr[i] % n << " ";
                fl = 1;
            }
        }

        // Add n to index arr[i] to mark
        // presence of arr[i] or to
        // mark repetition of arr[i].
        arr[arr[i] % n] += n;
    }

    // If flag variable is not set
    // then no repeating element is
    // found. So print -1.
    if (!fl)
        cout << "-1";
}

// Driver Function
int main()
{
    int arr[] = { 1, 6, 3, 1, 3, 6, 6 };
    int arr_size = sizeof(arr) / sizeof(arr[0]);
    printDuplicates(arr, arr_size);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all elements
// that appear more than once.
import java.io.*;

class GFG
{

// Function to find repeating elements
static void printDuplicates(int arr[], int n)
{
    int i;

    // Flag variable used to
    // represent whether repeating
    // element is found or not.
    int fl = 0;

    for (i = 0; i < n; i++)
    {

        // Check if current element is
        // repeating or not. If it is
        // repeating then value will
        // be greater than or equal to n.
        if (arr[arr[i] % n] >= n)
        {

            // Check if it is first
            // repetition or not. If it is
            // first repetition then value
            // at index arr[i] is less than
            // 2*n. Print arr[i] if it is
            // first repetition.
            if (arr[arr[i] % n] < 2 * n)
            {
                System.out.print( arr[i] % n + " ");
                fl = 1;
            }
        }

        // Add n to index arr[i] to mark
        // presence of arr[i] or to
        // mark repetition of arr[i].
        arr[arr[i] % n] += n;
    }

    // If flag variable is not set
    // then no repeating element is
    // found. So print -1.
    if (!(fl > 0))
        System.out.println("-1");
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = { 1, 6, 3, 1, 3, 6, 6 };
    int arr_size = arr.length;
    printDuplicates(arr, arr_size);
}
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python 3 program to print all elements that
# appear more than once.

# Function to find repeating elements
def printDuplicates(arr, n):

    # Flag variable used to
    # represent whether repeating
    # element is found or not.
    fl = 0;

    for i in range (0, n):

        # Check if current element is
        # repeating or not. If it is
        # repeating then value will
        # be greater than or equal to n.
        if (arr[arr[i] % n] >= n):

            # Check if it is first
            # repetition or not. If it is
            # first repetition then value
            # at index arr[i] is less than
            # 2*n. Print arr[i] if it is
            # first repetition.
            if (arr[arr[i] % n] < 2 * n):
                print(arr[i] % n, end = " ")
                fl = 1;

        # Add n to index arr[i] to mark
        # presence of arr[i] or to
        # mark repetition of arr[i].
        arr[arr[i] % n] += n;

    # If flag variable is not set
    # then no repeating element is
    # found. So print -1.
    if (fl == 0):
        print("-1")

# Driver Function
arr = [ 1, 6, 3, 1, 3, 6, 6 ];
arr_size = len(arr);
printDuplicates(arr, arr_size);

# This code is contributed
# by Akanksha Rai
```

## C#

```
// C# program to print all elements
// that appear more than once.
using System;

class GFG
{

// Function to find repeating elements
static void printDuplicates(int []arr, int n)
{
    int i;

    // Flag variable used to
    // represent whether repeating
    // element is found or not.
    int fl = 0;

    for (i = 0; i < n; i++)
    {

        // Check if current element is
        // repeating or not. If it is
        // repeating then value will
        // be greater than or equal to n.
        if (arr[arr[i] % n] >= n)
        {

            // Check if it is first
            // repetition or not. If it is
            // first repetition then value
            // at index arr[i] is less than
            // 2*n. Print arr[i] if it is
            // first repetition.
            if (arr[arr[i] % n] < 2 * n)
            {
                Console.Write( arr[i] % n + " ");
                fl = 1;
            }
        }

        // Add n to index arr[i] to mark
        // presence of arr[i] or to
        // mark repetition of arr[i].
        arr[arr[i] % n] += n;
    }

    // If flag variable is not set
    // then no repeating element is
    // found. So print -1.
    if (!(fl > 0))
        Console.Write("-1");
}

// Driver Code
public static void Main ()
{
    int []arr = { 1, 6, 3, 1, 3, 6, 6 };
    int arr_size = arr.Length;
    printDuplicates(arr, arr_size);
}
}

// This code is contributed
// by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print all elements that
// appear more than once.

// Function to find repeating elements
function printDuplicates($arr, $n)
{
    $i;

    // Flag variable used to
    // represent whether repeating
    // element is found or not.
    $fl = 0;

    for ($i = 0; $i < $n; $i++)
    {

        // Check if current element is
        // repeating or not. If it is
        // repeating then value will
        // be greater than or equal to n.
        if ($arr[$arr[$i] % $n] >= $n)
        {

            // Check if it is first
            // repetition or not. If it is
            // first repetition then value
            // at index arr[i] is less than
            // 2*n. Print arr[i] if it is
            // first repetition.
            if ($arr[$arr[$i] % $n] < 2 * $n)
            {
                echo $arr[$i] % $n . " ";
                $fl = 1;
            }
        }

        // Add n to index arr[i] to mark
        // presence of arr[i] or to
        // mark repetition of arr[i].
        $arr[$arr[$i] % $n] += $n;
    }

    // If flag variable is not set
    // then no repeating element is
    // found. So print -1.
    if (!$fl)
        echo "-1";
}

// Driver Function
$arr = array(1, 6, 3, 1, 3, 6, 6);
$arr_size = sizeof($arr);
printDuplicates($arr, $arr_size);

// This code is contributed
// by Mukul Singh
```

## java 描述语言

```
<script>

// JavaScript program to print all elements that
// appear more than once.

// Function to find repeating elements
function printDuplicates(arr, n)
{
    let i;

    // Flag variable used to
    // represent whether repeating
    // element is found or not.
    let fl = 0;

    for (i = 0; i < n; i++) {

        // Check if current element is
        // repeating or not. If it is
        // repeating then value will
        // be greater than or equal to n.
        if (arr[arr[i] % n] >= n) {

            // Check if it is first
            // repetition or not. If it is
            // first repetition then value
            // at index arr[i] is less than
            // 2*n. Print arr[i] if it is
            // first repetition.
            if (arr[arr[i] % n] < 2 * n) {
                document.write(arr[i] % n + " ");
                fl = 1;
            }
        }

        // Add n to index arr[i] to mark
        // presence of arr[i] or to
        // mark repetition of arr[i].
        arr[arr[i] % n] += n;
    }

    // If flag variable is not set
    // then no repeating element is
    // found. So print -1.
    if (!fl)
        document.write("-1");
}

// Driver Function

    let arr = [ 1, 6, 3, 1, 3, 6, 6 ];
    let arr_size = arr.length;
    printDuplicates(arr, arr_size);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
1 3 6
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)