# 最长增加子阵列

> 原文:[https://www.geeksforgeeks.org/longest-increasing-subarray/](https://www.geeksforgeeks.org/longest-increasing-subarray/)

给定一个包含 **n 个**数字的数组。问题是找到最长的连续子阵列的长度，使得子阵列中的每个元素都严格大于它在同一子阵列中的前一个元素。时间复杂度应为 0(n)。

**示例:**

```
Input : arr[] = {5, 6, 3, 5, 7, 8, 9, 1, 2}
Output : 5
The subarray is {3, 5, 7, 8, 9}

Input : arr[] = {12, 13, 1, 5, 4, 7, 8, 10, 10, 11}
Output : 4
The subarray is {4, 7, 8, 10} 
```

**算法:**

```
lenOfLongIncSubArr(arr, n)
    Declare max = 1, len = 1
    for i = 1 to n-1
    if arr[i] > arr[i-1]
        len++
    else
        if max < len
            max = len
        len = 1
    if max < len
        max = len
    return max 
```

## C++

```
// C++ implementation to find the length of
// longest increasing contiguous subarray
#include <bits/stdc++.h>

using namespace std;

// function to find the length of longest increasing
// contiguous subarray
int lenOfLongIncSubArr(int arr[], int n)
{
    // 'max' to store the length of longest
    // increasing subarray
    // 'len' to store the lengths of longest
    // increasing subarray at diiferent
    // instants of time
    int max = 1, len = 1;

    // traverse the array from the 2nd element
    for (int i=1; i<n; i++)
    {
        // if current element if greater than previous
        // element, then this element helps in building
        // up the previous increasing subarray encountered
        // so far
        if (arr[i] > arr[i-1])
            len++;
        else
        {
            // check if 'max' length is less than the length
            // of the current increasing subarray. If true,
            // then update 'max'
            if (max < len)   
                max = len;

            // reset 'len' to 1 as from this element
            // again the length of the new increasing
            // subarray is being calculated   
            len = 1;   
        }   
    }

    // comparing the length of the last
    // increasing subarray with 'max'
    if (max < len)
        max = len;

    // required maximum length
    return max;
}

// Driver program to test above
int main()
{
    int arr[] = {5, 6, 3, 5, 7, 8, 9, 1, 2};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Length = "
         << lenOfLongIncSubArr(arr, n);
    return 0;    
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code to find length of
// Longest increasing subarray
import java.util.*;

class GFG {

    // function to find the length of longest
    // increasing contiguous subarray
    public static int lenOfLongIncSubArr(int arr[],
                                            int n)
    {
        // 'max' to store the length of longest
        // increasing subarray
        // 'len' to store the lengths of longest
        // increasing subarray at diiferent
        // instants of time
        int max = 1, len = 1;

        // traverse the array from the 2nd element
        for (int i=1; i<n; i++)
        {
            // if current element if greater than
            // previous element, then this element
            // helps in building up the previous
            // increasing subarray encountered
            // so far
            if (arr[i] > arr[i-1])
                len++;
            else
            {
                // check if 'max' length is less
                // than the length of the current
                // increasing subarray. If true,
                // than update 'max'
                if (max < len)   
                    max = len;

                // reset 'len' to 1 as from this
                // element again the length of the
                // new increasing subarray is being
                // calculated   
                len = 1;   
            }   
        }

        // comparing the length of the last
        // increasing subarray with 'max'
        if (max < len)
            max = len;

        // required maximum length
        return max;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
         int arr[] = {5, 6, 3, 5, 7, 8, 9, 1, 2};
            int n = arr.length;
            System.out.println("Length = " +
                      lenOfLongIncSubArr(arr, n));

        }
    }

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python 3 implementation to find the length of
# longest increasing contiguous subarray

# function to find the length of longest
# increasing contiguous subarray
def lenOfLongIncSubArr(arr, n) :

    # 'max' to store the length of longest
    # increasing subarray
    # 'len' to store the lengths of longest
    # increasing subarray at diiferent
    # instants of time
    m = 1
    l = 1

    # traverse the array from the 2nd element
    for i in range(1, n) :

        # if current element if greater than previous
        # element, then this element helps in building
        # up the previous increasing subarray encountered
        # so far
        if (arr[i] > arr[i-1]) :
            l =l + 1
        else :

            # check if 'max' length is less than the length
            # of the current increasing subarray. If true,
            # then update 'max'
            if (m < l)  :
                m = l

            # reset 'len' to 1 as from this element
            # again the length of the new increasing
            # subarray is being calculated   
            l = 1

    # comparing the length of the last
    # increasing subarray with 'max'
    if (m < l) :
        m = l

    # required maximum length
    return m

# Driver program to test above

arr = [5, 6, 3, 5, 7, 8, 9, 1, 2]
n = len(arr)
print("Length = ", lenOfLongIncSubArr(arr, n))

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// C# Code to find length of
// Longest increasing subarray
using System;

class GFG {

    // function to find the length of longest
    // increasing contiguous subarray
    public static int lenOfLongIncSubArr(int[] arr,
                                             int n)
    {
        // 'max' to store the length of longest
        // increasing subarray
        // 'len' to store the lengths of longest
        // increasing subarray at diiferent
        // instants of time
        int max = 1, len = 1;

        // traverse the array from the 2nd element
        for (int i = 1; i < n; i++) {

            // if current element if greater than
            // previous element, then this element
            // helps in building up the previous
            // increasing subarray encountered
            // so far
            if (arr[i] > arr[i - 1])
                len++;
            else {

                // check if 'max' length is less
                // than the length of the current
                // increasing subarray. If true,
                // than update 'max'
                if (max < len)
                    max = len;

                // reset 'len' to 1 as from this
                // element again the length of the
                // new increasing subarray is being
                // calculated
                len = 1;
            }
        }

        // comparing the length of the last
        // increasing subarray with 'max'
        if (max < len)
            max = len;

        // required maximum length
        return max;
    }

    /* Driver program to test above function */
    public static void Main()
    {
        int[] arr = { 5, 6, 3, 5, 7, 8, 9, 1, 2 };
        int n = arr.Length;
        Console.WriteLine("Length = " +
                           lenOfLongIncSubArr(arr, n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find the length of
// longest increasing contiguous subarray

// function to find the length of
// longest increasing contiguous
// subarray
function lenOfLongIncSubArr($arr, $n)
{

    // 'max' to store the length of longest
    // increasing subarray
    // 'len' to store the lengths of longest
    // increasing subarray at diiferent
    // instants of time
    $max = 1;
    $len = 1;

    // traverse the array from
    // the 2nd element
    for ($i = 1; $i < $n; $i++)
    {

        // if current element if
        // greater than previous
        // element, then this element
        // helps in building up the
        // previous increasing subarray
        // encountered so far
        if ($arr[$i] > $arr[$i-1])
            $len++;
        else
        {

            // check if 'max' length is
            // less than the length
            // of the current increasing
            // subarray. If true,
            // then update 'max'
            if ($max < $len)
                $max = $len;

            // reset 'len' to 1 as
            // from this element
            // again the length of
            // the new increasing
            // subarray is being
            // calculated
            $len = 1;
        }
    }

    // comparing the length of the last
    // increasing subarray with 'max'
    if ($max < $len)
        $max = $len;

    // required maximum length
    return $max;
}

    // Driver Code
    $arr = array(5, 6, 3, 5, 7, 8, 9, 1, 2);
    $n = sizeof($arr);
    echo "Length = ", lenOfLongIncSubArr($arr, $n);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript implementation to find the length of
// longest increasing contiguous subarray

// function to find the length of longest increasing
// contiguous subarray
function lenOfLongIncSubArr(arr, n)
{
    // 'max' to store the length of longest
    // increasing subarray
    // 'len' to store the lengths of longest
    // increasing subarray at diiferent
    // instants of time
    var max = 1, len = 1;

    // traverse the array from the 2nd element
    for (var i=1; i<n; i++)
    {
        // if current element if greater than previous
        // element, then this element helps in building
        // up the previous increasing subarray encountered
        // so far
        if (arr[i] > arr[i-1])
            len++;
        else
        {
            // check if 'max' length is less than the length
            // of the current increasing subarray. If true,
            // then update 'max'
            if (max < len)  
            {
                max = len;
            }

            // reset 'len' to 1 as from this element
            // again the length of the new increasing
            // subarray is being calculated  
            len = 1;  
        }  
    }

    // comparing the length of the last
    // increasing subarray with 'max'
    if (max < len)
    {
        max = len;
    }

    // required maximum length
    return max;
}

// Driver program to test above
var arr = [5, 6, 3, 5, 7, 8, 9, 1, 2];
var n = arr.length;
document.write("Length = " + lenOfLongIncSubArr(arr, n));
// This code is contributed by shivani.
</script>
```

**输出:**

```
Length = 5
```

**时间复杂度:** O(n)

**如何打印子阵列？**
我们可以通过跟踪最大长度的索引来打印子阵列。

## C++

```
// C++ implementation to find the length of
// longest increasing contiguous subarray
#include <bits/stdc++.h>
using namespace std;

// function to find the length of longest increasing
// contiguous subarray
void printLogestIncSubArr(int arr[], int n)
{
    // 'max' to store the length of longest
    // increasing subarray
    // 'len' to store the lengths of longest
    // increasing subarray at diiferent
    // instants of time
    int max = 1, len = 1, maxIndex = 0;

    // traverse the array from the 2nd element
    for (int i=1; i<n; i++)
    {
        // if current element if greater than previous
        // element, then this element helps in building
        // up the previous increasing subarray encountered
        // so far
        if (arr[i] > arr[i-1])
            len++;
        else
        {
            // check if 'max' length is less than the length
            // of the current increasing subarray. If true,
            // then update 'max'
            if (max < len)   
            {
                max = len;

                // index assign the starting index of
                // longest increasing contiguous subarray.  
                maxIndex = i - max;
            }

            // reset 'len' to 1 as from this element
            // again the length of the new increasing
            // subarray is being calculated   
            len = 1;   
        }   
    }

    // comparing the length of the last
    // increasing subarray with 'max'
    if (max < len)
    {
        max = len;
        maxIndex = n - max;
    }

    // Print the elements of longest increasing
    // contiguous subarray.
    for (int i=maxIndex; i<max+maxIndex; i++)
        cout << arr[i] << " ";
}

// Driver program to test above
int main()
{
    int arr[] = {5, 6, 3, 5, 7, 8, 9, 1, 2};
    int n = sizeof(arr) / sizeof(arr[0]);
    printLogestIncSubArr(arr, n);
    return 0;    
}
// This code is contributed by Dharmendra kumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code For Longest increasing subarray
import java.util.*;

class GFG {

    // function to find the length of longest
    // increasing contiguous subarray
    public static void printLogestIncSubArr(int arr[],
                                              int n)
    {
        // 'max' to store the length of longest
        // increasing subarray
        // 'len' to store the lengths of longest
        // increasing subarray at diiferent
        // instants of time
        int max = 1, len = 1, maxIndex = 0;

        // traverse the array from the 2nd element
        for (int i = 1; i < n; i++)
        {
            // if current element if greater than
            // previous element, then this element
            // helps in building up the previous
            // increasing subarray encountered
            // so far
            if (arr[i] > arr[i-1])
                len++;
            else
            {
                // check if 'max' length is less
                // than the length of the current
                // increasing subarray. If true,
                // then update 'max'
                if (max < len)   
                {
                    max = len;

                    // index assign the starting
                    // index of longest increasing
                    // contiguous subarray.  
                    maxIndex = i - max;
                }

                // reset 'len' to 1 as from this
                // element again the length of the
                // new increasing subarray is
                // being calculated   
                len = 1;   
            }   
        }

        // comparing the length of the last
        // increasing subarray with 'max'
        if (max < len)
        {
            max = len;
            maxIndex = n - max;
        }

        // Print the elements of longest
        // increasing contiguous subarray.
        for (int i = maxIndex; i < max+maxIndex; i++)
            System.out.print(arr[i] + " ");
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr[] = {5, 6, 3, 5, 7, 8, 9, 1, 2};
        int n = arr.length;
        printLogestIncSubArr(arr, n);

    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python 3 implementation to find the length of
# longest increasing contiguous subarray

# function to find the length of longest increasing
# contiguous subarray
def printLogestIncSubArr( arr, n) :

    # 'max' to store the length of longest
    # increasing subarray
    # 'len' to store the lengths of longest
    # increasing subarray at diiferent
    # instants of time
    m = 1
    l = 1
    maxIndex = 0

    # traverse the array from the 2nd element
    for i in range(1, n) :

        # if current element if greater than previous
        # element, then this element helps in building
        # up the previous increasing subarray
        # encountered so far
        if (arr[i] > arr[i-1]) :
            l =l + 1
        else :

            # check if 'max' length is less than the length
            # of the current increasing subarray. If true,
            # then update 'max'
            if (m < l)  :
                m = l

                # index assign the starting index of
                # longest increasing contiguous subarray.  
                maxIndex = i - m

            # reset 'len' to 1 as from this element
            # again the length of the new increasing
            # subarray is being calculated   
            l = 1   

    # comparing the length of the last
    # increasing subarray with 'max'
    if (m < l) :
        m = l
        maxIndex = n - m

    # Print the elements of longest
    # increasing contiguous subarray.
    for i in range(maxIndex, (m+maxIndex)) :
        print(arr[i] , end=" ")

# Driver program to test above
arr = [5, 6, 3, 5, 7, 8, 9, 1, 2]
n = len(arr)
printLogestIncSubArr(arr, n)

# This code is contributed
# by Nikita Tiwari
```

## C#

```
// C# Code to print
// Longest increasing subarray
using System;

class GFG {

    // function to find the length of longest
    // increasing contiguous subarray
    public static void printLogestIncSubArr(int[] arr,
                                                int n)
    {
        // 'max' to store the length of longest
        // increasing subarray
        // 'len' to store the lengths of longest
        // increasing subarray at diiferent
        // instants of time
        int max = 1, len = 1, maxIndex = 0;

        // traverse the array from the 2nd element
        for (int i = 1; i < n; i++) {

            // if current element if greater than
            // previous element, then this element
            // helps in building up the previous
            // increasing subarray encountered
            // so far
            if (arr[i] > arr[i - 1])
                len++;
            else
            {
                // check if 'max' length is less
                // than the length of the current
                // increasing subarray. If true,
                // then update 'max'
                if (max < len) {
                    max = len;

                    // index assign the starting
                    // index of longest increasing
                    // contiguous subarray.
                    maxIndex = i - max;
                }

                // reset 'len' to 1 as from this
                // element again the length of the
                // new increasing subarray is
                // being calculated
                len = 1;
            }
        }

        // comparing the length of the last
        // increasing subarray with 'max'
        if (max < len) {
            max = len;
            maxIndex = n - max;
        }

        // Print the elements of longest
        // increasing contiguous subarray.
        for (int i = maxIndex; i < max + maxIndex; i++)
            Console.Write(arr[i] + " ");
    }

    /* Driver program to test above function */
    public static void Main()
    {
        int[] arr = { 5, 6, 3, 5, 7, 8, 9, 1, 2 };
        int n = arr.Length;
        printLogestIncSubArr(arr, n);
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find
// the length of longest increasing
// contiguous subarray

// function to find the length of
// longest increasing contiguous subarray
function printLogestIncSubArr(&$arr, $n)
{
    // 'max' to store the length of
    // longest increasing subarray
    // 'len' to store the lengths of
    // longest increasing subarray at
    // diiferent instants of time
    $max = 1;
    $len = 1;
    $maxIndex = 0;

    // traverse the array from
    // the 2nd element
    for ($i = 1; $i < $n; $i++)
    {
        // if current element if greater
        // than previous element, then
        // this element helps in building
        // up the previous increasing
        // subarray encountered so far
        if ($arr[$i] > $arr[$i - 1])
            $len++;
        else
        {
            // check if 'max' length is less
            // than the length of the current
            // increasing subarray. If true,
            // then update 'max'
            if ($max < $len)
            {
                $max = $len;

                // index assign the starting
                // index of longest increasing
                // contiguous subarray.
                $maxIndex = $i - $max;
            }

            // reset 'len' to 1 as from this
            // element again the length of
            // the new increasing subarray
            // is being calculated
            $len = 1;
        }
    }

    // comparing the length of
    // the last increasing
    // subarray with 'max'
    if ($max < $len)
    {
        $max = $len;
        $maxIndex = $n - $max;
    }

    // Print the elements of
    // longest increasing
    // contiguous subarray.
    for ($i = $maxIndex;
         $i < ($max + $maxIndex); $i++)
        echo($arr[$i] . " ") ;

}

// Driver Code
$arr = array(5, 6, 3, 5, 7,
             8, 9, 1, 2);
$n = sizeof($arr);
printLogestIncSubArr($arr, $n);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript implementation to find the length of
// longest increasing contiguous subarray

// function to find the length of longest increasing
// contiguous subarray
function printLogestIncSubArr(arr, n)
{
    // 'max' to store the length of longest
    // increasing subarray
    // 'len' to store the lengths of longest
    // increasing subarray at diiferent
    // instants of time
    var max = 1, len = 1, maxIndex = 0;

    // traverse the array from the 2nd element
    for (var i=1; i<n; i++)
    {
        // if current element if greater than previous
        // element, then this element helps in building
        // up the previous increasing subarray encountered
        // so far
        if (arr[i] > arr[i-1])
            len++;
        else
        {
            // check if 'max' length is less than the length
            // of the current increasing subarray. If true,
            // then update 'max'
            if (max < len)   
            {
                max = len;

                // index assign the starting index of
                // longest increasing contiguous subarray.  
                maxIndex = i - max;
            }

            // reset 'len' to 1 as from this element
            // again the length of the new increasing
            // subarray is being calculated   
            len = 1;   
        }   
    }

    // comparing the length of the last
    // increasing subarray with 'max'
    if (max < len)
    {
        max = len;
        maxIndex = n - max;
    }

    // Print the elements of longest increasing
    // contiguous subarray.
    for (var i=maxIndex; i<max+maxIndex; i++)
        document.write( arr[i] + " ");
}

// Driver program to test above
var arr = [5, 6, 3, 5, 7, 8, 9, 1, 2];
var n = arr.length;
printLogestIncSubArr(arr, n);

// This code is contributed by rrrtnx.
</script>
```

**输出:**

```
3 5 7 8 9 
```

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。