# 使用填充邻居的最小迭代次数用 1 填充数组

> 原文:[https://www . geesforgeks . org/fill-array-1s-minimum-iterations-fill-neighbors/](https://www.geeksforgeeks.org/fill-array-1s-minimum-iterations-filling-neighbors/)

给定一个 0 和 1 的数组，如果在一次迭代中 1 的近邻可以被填充，那么在多少次迭代中整个数组可以被 1 填充。
注:如果不能用 1 填充数组，则打印“-1”。
**例:**

```
Input : arr[] = {1, 0, 1, 0, 0, 1, 0, 1, 
                     1, 0, 1, 1, 0, 0, 1}
Output : 1
To convert the whole array into 1s, one iteration
is required. Between indexes i=2 and i=5, the zero 
at i=3 would be converted to '1' due to its neighbours
at i=2 similarly the zero at i=4 would be converted 
into '1' due to its neighbor at i=5, all this can 
be done in a single iteration. Similarly all 0's can
be converted to 1 in single iteration.

Input : arr[] = {0, 0, 1, 1, 0, 0, 1, 1, 0, 
                    1, 1, 1, 1, 0, 0, 0, 1}
Output : 2
```

问于:亚马逊

假设单个 1 可以将它的 0 个邻居都转换为 1。这个问题归结为三种情况:

```
Case 1 : A block of 0s has 1s on both sides

Let count_zero be the count of zeros in the block.

Number of iterations are always equal to : 
              count_zero/2   if (count_zero is even)
              count_zero+1)/2    if(count_zero is odd).

Case 2 : Either single 1 at the end or in 
         the starting. For example 0 0 0 0 1 and 
         1 0 0 0 0
In this case the number of iterations required will 
always be equal to number of zeros.

Case 3 : There are no 1s (Array has only 0s)
In this case array can't be filled with all 1's. 
So print -1.
```

算法:

```
1-Start traversing the array.
  (a) Traverse until a 0 is found.
     while (i < n && a[i] == 1)
     {
        i++;
        flag=true;
     }
   Flag is set to true just to check at 
   the last if array contains any 1 or not.

  (b) Traverse until a 1 is found and Count 
     contiguous 0 .
     while (i < n && a[i] == 0)
     {
         count_zero++;
         i++;
     }

  (c) Now check which case is satisfied by 
     current subarray. And update iterations 
     using count and update max iterations.    
```

## C++

```
// C++ program to find number of iterations
// to fill with all 1s
#include<bits/stdc++.h>
using namespace std;

// Returns count of iterations to fill arr[]
// with 1s.
int countIterations(int arr[], int n)
{
    bool oneFound = false;
    int res = 0;
    // Start traversing the array
    for (int i=0; i<n; )
    {
        if (arr[i] == 1)
          oneFound = true;

        // Traverse until a 0 is found
        while (i<n && arr[i]==1)
            i++;

        // Count contiguous 0s
        int count_zero = 0;
        while (i<n && arr[i]==0)
        {
            count_zero++;
            i++;
        }

        // Condition for Case 3
        if (oneFound == false && i == n)
            return -1;

        // Condition to check if Case 1 satisfies:
        int curr_count;
        if (i < n && oneFound == true)
        {
            // If count_zero is even
            if (count_zero & 1 == 0)
                curr_count = count_zero/2;

            // If count_zero is odd
            else
                curr_count = (count_zero+1)/2;

            // Reset count_zero
            count_zero = 0;
        }

        // Case 2
        else
        {
            curr_count = count_zero;
            count_zero = 0;
        }

        // Update res
        res = max(res, curr_count);
    }

    return res;
}

// Driver code
int main()
{
    int arr[] = {0, 1, 0, 0, 1, 0, 0,
                 0, 0, 0, 0, 0, 1, 0};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countIterations(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of iterations
// to fill with all 1s

class Test
{
    // Returns count of iterations to fill arr[]
    // with 1s.
    static int countIterations(int arr[], int n)
    {
        boolean oneFound = false;
        int res = 0;

        // Start traversing the array
        for (int i=0; i<n; )
        {
            if (arr[i] == 1)
              oneFound = true;

            // Traverse until a 0 is found
            while (i<n && arr[i]==1)
                i++;

            // Count contiguous 0s
            int count_zero = 0;
            while (i<n && arr[i]==0)
            {
                count_zero++;
                i++;
            }

            // Condition for Case 3
            if (oneFound == false && i == n)
                return -1;

            // Condition to check if Case 1 satisfies:
            int curr_count;
            if (i < n && oneFound == true)
            {
                // If count_zero is even
                if ((count_zero & 1) == 0)
                    curr_count = count_zero/2;

                // If count_zero is odd
                else
                    curr_count = (count_zero+1)/2;

                // Reset count_zero
                count_zero = 0;
            }

            // Case 2
            else
            {
                curr_count = count_zero;
                count_zero = 0;
            }

            // Update res
            res = Math.max(res, curr_count);
        }

        return res;
    }

    // Driver method
    public static void main(String[] args)
    {
        int arr[] = {0, 1, 0, 0, 1, 0, 0,
                0, 0, 0, 0, 0, 1, 0};

        System.out.println(countIterations(arr, arr.length));

    }
}
```

## 蟒蛇 3

```
# Python3 program to find number
# of iterations to fill with all 1s

# Returns count of iterations
# to fill arr[] with 1s.
def countIterations(arr, n):

    oneFound = False;
    res = 0;
    i = 0;

    # Start traversing the array
    while (i < n):
        if (arr[i] == 1):
            oneFound = True;

        # Traverse until a 0 is found
        while (i < n and arr[i] == 1):
            i += 1;

        # Count contiguous 0s
        count_zero = 0;
        while (i < n and arr[i] == 0):
            count_zero += 1;
            i += 1;

        # Condition for Case 3
        if (oneFound == False and i == n):
            return -1;

        # Condition to check
        # if Case 1 satisfies:
        curr_count = 0;
        if (i < n and oneFound == True):

            # If count_zero is even
            if ((count_zero & 1) == 0):
                curr_count = count_zero // 2;

            # If count_zero is odd
            else:
                curr_count = (count_zero + 1) // 2;

            # Reset count_zero
            count_zero = 0;

        # Case 2
        else:
            curr_count = count_zero;
            count_zero = 0;

        # Update res
        res = max(res, curr_count);

    return res;

# Driver code
arr = [0, 1, 0, 0, 1, 0, 0,
       0, 0, 0, 0, 0, 1, 0];
n = len(arr);
print(countIterations(arr, n));

# This code is contributed by mits
```

## C#

```
// C# program to find number of
// iterations to fill with all 1s
using System;

class Test {

    // Returns count of iterations
    // to fill arr[] with 1s.
    static int countIterations(int []arr, int n)
    {
        bool oneFound = false;
        int res = 0;

        // Start traversing the array
        for (int i = 0; i < n; )
        {
            if (arr[i] == 1)
            oneFound = true;

            // Traverse until a 0 is found
            while (i < n && arr[i] == 1)
                i++;

            // Count contiguous 0s
            int count_zero = 0;
            while (i < n && arr[i] == 0)
            {
                count_zero++;
                i++;
            }

            // Condition for Case 3
            if (oneFound == false && i == n)
                return -1;

            // Condition to check if
            // Case 1 satisfies:
            int curr_count;
            if (i < n && oneFound == true)
            {

                // If count_zero is even
                if ((count_zero & 1) == 0)
                    curr_count = count_zero / 2;

                // If count_zero is odd
                else
                    curr_count = (count_zero + 1) / 2;

                // Reset count_zero
                count_zero = 0;
            }

            // Case 2
            else
            {
                curr_count = count_zero;
                count_zero = 0;
            }

            // Update res
            res = Math.Max(res, curr_count);
        }

        return res;
    }

    // Driver code
    public static void Main()
    {
        int []arr = {0, 1, 0, 0, 1, 0, 0,
                0, 0, 0, 0, 0, 1, 0};

        Console.Write(countIterations(arr, arr.Length));

    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number
// of iterations to fill with all 1s

// Returns count of iterations
// to fill arr[] with 1s.
function countIterations($arr, $n)
{
    $oneFound = false;
    $res = 0;
    // Start traversing the array
    for ( $i = 0; $i < $n; )
    {
        if ($arr[$i] == 1)
        $oneFound = true;

        // Traverse until a 0 is found
        while ($i < $n && $arr[$i] == 1)
            $i++;

        // Count contiguous 0s
        $count_zero = 0;
        while ($i < $n && $arr[$i] == 0)
        {
            $count_zero++;
            $i++;
        }

        // Condition for Case 3
        if ($oneFound == false && $i == $n)
            return -1;

        // Condition to check
        // if Case 1 satisfies:
        $curr_count;
        if ($i < $n && $oneFound == true)
        {
            // If count_zero is even
            if ($count_zero & 1 == 0)
                $curr_count = $count_zero / 2;

            // If count_zero is odd
            else
                $curr_count = ($count_zero + 1) / 2;

            // Reset count_zero
            $count_zero = 0;
        }

        // Case 2
        else
        {
            $curr_count = $count_zero;
            $count_zero = 0;
        }

        // Update res
        $res = max($res, $curr_count);
    }

    return $res;
}

// Driver code
$arr = array(0, 1, 0, 0, 1, 0, 0,
            0, 0, 0, 0, 0, 1, 0);
$n = sizeof($arr) / sizeof($arr[0]);
echo countIterations($arr, $n);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript program to find number of
// iterations to fill with all 1s

// Returns count of iterations to fill arr[]
// with 1s.
function countIterations(arr, n)
{
    var oneFound = false;
    var res = 0;

    // Start traversing the array
    for(var i = 0; i < n; )
    {
        if (arr[i] == 1)
          oneFound = true;

        // Traverse until a 0 is found
        while (i < n && arr[i] == 1)
            i++;

        // Count contiguous 0s
        var count_zero = 0;
        while (i < n && arr[i] == 0)
        {
            count_zero++;
            i++;
        }

        // Condition for Case 3
        if (oneFound == false && i == n)
            return -1;

        // Condition to check if Case 1 satisfies:
        var curr_count;
        if (i < n && oneFound == true)
        {

            // If count_zero is even
            if ((count_zero & 1) == 0)
                curr_count = count_zero / 2;

            // If count_zero is odd
            else
                curr_count = (count_zero + 1) / 2;

            // Reset count_zero
            count_zero = 0;
        }

        // Case 2
        else
        {
            curr_count = count_zero;
            count_zero = 0;
        }

        // Update res
        res = Math.max(res, curr_count);
    }

    return res;
}

// Driver Code
var arr = [ 0, 1, 0, 0, 1, 0, 0,
            0, 0, 0, 0, 0, 1, 0 ];

document.write(countIterations(arr, arr.length));

// This code is contributed by Ankita saini

</script>
```

**输出:**

```
4
```

**时间复杂度:** O(n)
本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。