# 在数组中找到一个分割点

> 原文:[https://www . geesforgeks . org/find-a-partition-in-point array/](https://www.geeksforgeeks.org/find-a-partition-point-in-array/)

给定一个未排序的整数数组。找到一个元素，使它左边的所有元素都变小，右边的元素变大。如果不存在这样的元素，则打印-1。
注意，这样的元素可以不止一个。例如，按递增顺序排序的数组，所有元素都遵循属性。我们只需要找到一个这样的元素。
**例:**

```
Input :  A[] = {4, 3, 2, 5, 8, 6, 7}  
Output : 5 

Input : A[] = {5, 6, 2, 8, 10, 9, 8} 
Output : -1
```

**简单解**取 O(n <sup>2</sup> )。想法是一个接一个地挑选每个数组元素，对于每个元素，我们必须检查它是大于它左边的所有元素，还是小于它右边的所有元素。
以下是以上想法的实现:

## C++

```
// Simple C++ program to find a partition point in
// an array
#include <bits/stdc++.h>
using namespace std;

// Prints an element such than all elements on left
// are smaller and all elements on right are greater.
int FindElement(int A[], int n)
{
    // traverse array elements
    for (int i = 0; i < n; i++) {
        // If we found that such number
        int flag = 0;

        // check All the elements on its left are smaller
        for (int j = 0; j < i; j++)
            if (A[j] >= A[i]) {
                flag = 1;
                break;
            }

        // check All the elements on its right are Greater
        for (int j = i + 1; j < n; j++)
            if (A[j] <= A[i]) {
                flag = 1;
                break;
            }

        // If flag == 0 indicates we found that number
        if (flag == 0)
            return A[i];
    }
    return -1;
}

// driver program to test above function
int main()
{
    int A[] = { 4, 3, 2, 5, 8, 6, 7 };
    int n = sizeof(A) / sizeof(A[0]);
    cout << FindElement(A, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Simple Java program to find
// a partition point in an array
import java.io.*;

class GFG {

    // Prints an element such than all elements
    // on left are smaller and all elements on
    // right are greater.
    static int FindElement(int[] A, int n)
    {
        // traverse array elements
        for (int i = 0; i < n; i++) {

            // If we found that such number
            int flag = 0;

            // check All the elements on
            // its left are smaller
            for (int j = 0; j < i; j++)
                if (A[j] >= A[i]) {
                    flag = 1;
                    break;
                }

            // check All the elements on
            // its right are Greater
            for (int j = i + 1; j < n; j++)
                if (A[j] <= A[i]) {
                    flag = 1;
                    break;
                }

            // If flag == 0 indicates we
            // found that number
            if (flag == 0)
                return A[i];
        }
        return -1;
    }

    // Driver code
    static public void main(String[] args)
    {
        int[] A = {4, 3, 2, 5, 8, 6, 7};
        int n = A.length;
        System.out.println(FindElement(A, n));
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Simple python 3 program to find a
# partition point in an array

# Prints an element such than all
# elements on left are smaller and
# all elements on right are greater.
def FindElement(A, n):

    # traverse array elements
    for i in range(0, n, 1):

        # If we found that such number
        flag = 0

        # check All the elements on its
        # left are smaller
        for j in range(0, i, 1):
            if (A[j] >= A[i]):
                flag = 1
                break

        # check All the elements on its
        # right are Greater
        for j in range(i + 1, n, 1):
            if (A[j] <= A[i]):
                flag = 1
                break

        # If flag == 0 indicates we found
        # that number
        if (flag == 0):
            return A[i]

    return -1

# Driver Code
if __name__ == '__main__':
    A = [4, 3, 2, 5, 8, 6, 7]
    n = len(A)
    print(FindElement(A, n))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// Simple C# program to find a
// partition point in an array
using System;

class GFG {

    // Prints an element such than all
    // elements on left are smaller and all
    // elements on right are greater.
    static int FindElement(int[] A, int n)
    {
        // traverse array elements
        for (int i = 0; i < n; i++) {

            // If we found that such number
            int flag = 0;

            // check All the elements on
            // its left are smaller
            for (int j = 0; j < i; j++)
                if (A[j] >= A[i]) {
                    flag = 1;
                    break;
                }

            // check All the elements on
            // its right are Greater
            for (int j = i + 1; j < n; j++)
                if (A[j] <= A[i]) {
                    flag = 1;
                    break;
                }

            // If flag == 0 indicates we
            // found that number
            if (flag == 0)
                return A[i];
        }
        return -1;
    }

    // Driver code
    static public void Main()
    {
        int[] A = { 4, 3, 2, 5, 8, 6, 7 };
        int n = A.Length;
        Console.WriteLine(FindElement(A, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Simple PHP program to find a partition
// point in an array

// Prints an element such than all elements
// on left are smaller and all elements on
// right are greater.
function FindElement($A, $n)
{
    // traverse array elements
    for ($i = 0; $i < $n; $i++)
    {
        // If we found that such number
        $flag = 0;

        // check All the elements on its
        // left are smaller
        for ( $j = 0; $j < $i; $j++)
            if ($A[$j] >= $A[$i])
            {
                $flag = 1;
                break;
            }

        // check All the elements on its
        // right are Greater
        for ( $j = $i + 1; $j < $n; $j++)
            if ($A[$j] <= $A[$i])
            {
                $flag = 1;
                break;
            }

        // If flag == 0 indicates we found
        // that number
        if ($flag == 0)
            return $A[$i];
    }
    return -1;
}

// Driver Code
$A = array( 4, 3, 2, 5, 8, 6, 7 );
$n = count($A);
echo FindElement($A, $n);

// This code is contributed by
// Rajput-Ji
?>
```

## java 描述语言

```
<script>

// Simple JavaScript program to find
// a partition point in an array

// Prints an element such than all elements
// on left are smaller and all elements on
// right are greater.
function FindElement(A , n)
{
    // traverse array elements
    for (i = 0; i < n; i++) {

        // If we found that such number
        var flag = 0;

        // check All the elements on
        // its left are smaller
        for (j = 0; j < i; j++)
            if (A[j] >= A[i]) {
                flag = 1;
                break;
            }

        // check All the elements on
        // its right are Greater
        for (j = i + 1; j < n; j++)
            if (A[j] <= A[i]) {
                flag = 1;
                break;
            }

        // If flag == 0 indicates we
        // found that number
        if (flag == 0)
            return A[i];
    }
    return -1;
}

// Driver code
var A = [4, 3, 2, 5, 8, 6, 7];
var n = A.length;
document.write(FindElement(A, n));

// This code contributed by shikhasingrajput

</script>
```

**输出:**

```
5
```

**时间复杂度:**O(n)<sup>2</sup>)
**高效解**取 O(n)时间。

1.  创建一个辅助数组“GE[]”。GE[]应该存储大于 A[i]且位于 A[i]左侧的元素。
2.  创建另一个辅助数组“SE[]”。SE[i]应存储小于 A[i]且位于 A[i]右侧的元素。
3.  查找数组中保持条件 GE[i-1] < A[i] < SE[i+1]的元素。

以下是上述思路的实现:

## C++

```
// Simple C++ program to find
// a partition point in an array
#include <bits/stdc++.h>
using namespace std;

// Returns an element that has all
// the element to its left smaller and
// to its right greater
int FindElement(int A[], int n)
{
    // Create an array 'SE[]' that will
    // store smaller element on right side.
    int SE[n];

    // Create an another array 'GE[]' that will
    // store greatest element on left side.
    int GE[n];

    // initialize first and last index of SE[], GE[]
    GE[0] = A[0];
    SE[n - 1] = A[n - 1];

    // store greatest element from left to right
    for (int i = 1; i < n; i++) {
        if (GE[i - 1] < A[i])
            GE[i] = A[i];
        else
            GE[i] = GE[i - 1];
    }

    // store smallest element from right to left
    for (int i = n - 2; i >= 0; i--) {
        if (A[i] < SE[i + 1])
            SE[i] = A[i];
        else
            SE[i] = SE[i + 1];
    }

    // Now find a number which is greater then all
    // elements at it's left and smaller the all
    // then elements to it's right
    for (int j = 0; j < n; j++)
    {
        if ((j == 0 && A[j] < SE[j + 1]) ||
            (j == n - 1 && A[j] > GE[j - 1]) ||
            (A[j] < SE[j + 1] && A[j] > GE[j - 1]))
            return A[j];
    }

    return -1;
}

// Driver code
int main()
{
    int A[] = {4, 3, 2, 5, 8, 6, 7};
    int n = sizeof(A) / sizeof(A[0]);
    cout << FindElement(A, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Simple java program to find a
// partition point in an array
import java.io.*;

class GFG {

    // Returns an element that has all
    // the element to its left smaller
    // and to its right greater
    static int FindElement(int[] A, int n)
    {
        // Create an array 'SE[]' that will
        // store smaller element on right side.
        int[] SE = new int[n];

        // Create an another array 'GE[]' that
        // will store greatest element on left side.
        int[] GE = new int[n];

        // initialize first and last index of SE[], GE[]
        GE[0] = A[0];
        SE[n - 1] = A[n - 1];

        // store greatest element from left to right
        for (int i = 1; i < n; i++)
        {
            if (GE[i - 1] < A[i])
                GE[i] = A[i];
            else
                GE[i] = GE[i - 1];
        }

        // store smallest element from right to left
        for (int i = n - 2; i >= 0; i--)
        {
            if (A[i] < SE[i + 1])
                SE[i] = A[i];
            else
                SE[i] = SE[i + 1];
        }

        // Now find a number which is greater then all
        // elements at it's left and smaller the all
        // then elements to it's right
        for (int j = 0; j < n; j++)
        {
            if ((j == 0 && A[j] < SE[j + 1]) ||
                (j == n - 1 && A[j] > GE[j - 1]) ||
                (A[j] < SE[j + 1] && A[j] > GE[j - 1]))
                return A[j];
        }

        return -1;
    }

    // Driver code
    static public void main(String[] args)
    {
        int[] A = {4, 3, 2, 5, 8, 6, 7};
        int n = A.length;
        System.out.println(FindElement(A, n));
    }
}

// This code is contributed by vt_m.
```

## C#

```
// Simple C# program to find
// a partition point in an array
using System;

class GFG {

    // Returns an element that has all
    // the element to its left smaller
    // and to its right greater
    static int FindElement(int[] A, int n)
    {
        // Create an array 'SE[]' that will
        // store smaller element on right side.
        int[] SE = new int[n];

        // Create an another array 'GE[]' that will
        // store greatest element on left side.
        int[] GE = new int[n];

        // initialize first and last index of SE[], GE[]
        GE[0] = A[0];
        SE[n - 1] = A[n - 1];

        // store greatest element from left to right
        for (int i = 1; i < n; i++)
        {
            if (GE[i - 1] < A[i])
                GE[i] = A[i];
            else
                GE[i] = GE[i - 1];
        }

        // store smallest element from right to left
        for (int i = n - 2; i >= 0; i--)
        {
            if (A[i] < SE[i + 1])
                SE[i] = A[i];
            else
                SE[i] = SE[i + 1];
        }

        // Now find a number which is greater then all
        // elements at it's left and smaller the all
        // then elements to it's right
        for (int j = 0; j < n; j++)
        {
            if ((j == 0 && A[j] < SE[j + 1]) ||
                (j == n - 1 && A[j] > GE[j - 1]) ||
                (A[j] < SE[j + 1] && A[j] > GE[j - 1]))
                return A[j];
        }

        return -1;
    }

    // Driver code
    static public void Main()
    {
        int[] A = {4, 3, 2, 5, 8, 6, 7};
        int n = A.Length;
        Console.WriteLine(FindElement(A, n));
    }
}

// This code is contributed by vt_m .
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find a partition point
// in an array

// Prints an element such than all elements
// on left are smaller and all elements on
// right are greater.
function FindElement($A, $n)
{
    // traverse array elements
    for ($i = 0; $i < $n; $i++)
    {

        // If we found that such number
        $flag = 0;

        // check All the elements on
        // its left are smaller
        for ($j = 0; $j < $i; $j++)
            if ($A[$j] >= $A[$i])
            {
                $flag = 1;
                break;
            }

        // check All the elements on
        // its right are Greater
        for ($j = $i + 1; $j < $n; $j++)
            if ($A[$j] <= $A[$i])
            {
                $flag = 1;
                break;
            }

        // If flag == 0 indicates we
        // found that number
        if ($flag == 0)
            return $A[$i];
    }
    return -1;
}

// Driver code
$A = array(4, 3, 2, 5, 8, 6, 7);
$n = sizeof($A);
echo(FindElement($A, $n));

// This code is contributed
// by Mukul Singh
?>
```

## java 描述语言

```
<script>
    // Simple Javascript program to find
    // a partition point in an array

    // Returns an element that has all
    // the element to its left smaller
    // and to its right greater
    function FindElement(A, n)
    {
        // Create an array 'SE[]' that will
        // store smaller element on right side.
        let SE = new Array(n);

        // Create an another array 'GE[]' that will
        // store greatest element on left side.
        let GE = new Array(n);

        // initialize first and last index of SE[], GE[]
        GE[0] = A[0];
        SE[n - 1] = A[n - 1];

        // store greatest element from left to right
        for (let i = 1; i < n; i++)
        {
            if (GE[i - 1] < A[i])
                GE[i] = A[i];
            else
                GE[i] = GE[i - 1];
        }

        // store smallest element from right to left
        for (let i = n - 2; i >= 0; i--)
        {
            if (A[i] < SE[i + 1])
                SE[i] = A[i];
            else
                SE[i] = SE[i + 1];
        }

        // Now find a number which is greater then all
        // elements at it's left and smaller the all
        // then elements to it's right
        for (let j = 0; j < n; j++)
        {
            if ((j == 0 && A[j] < SE[j + 1]) ||
                (j == n - 1 && A[j] > GE[j - 1]) ||
                (A[j] < SE[j + 1] && A[j] > GE[j - 1]))
                return A[j];
        }

        return -1;
    }

    let A = [4, 3, 2, 5, 8, 6, 7];
    let n = A.length;
    document.write(FindElement(A, n));

</script>
```

**输出:**

```
5
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)
本文由**尼尚辛格**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。