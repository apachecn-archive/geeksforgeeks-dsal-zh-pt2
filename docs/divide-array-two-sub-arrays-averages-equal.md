# 将数组分成两个子数组，使它们的平均值相等

> 原文:[https://www . geesforgeks . org/divide-array-two-sub array-average-equal/](https://www.geeksforgeeks.org/divide-array-two-sub-arrays-averages-equal/)

给定一个整数数组，任务是将一个整数数组分成两个子数组，尽可能使它们的平均值相等。
**例:**

```
Input : arr[] = {1, 5, 7, 2, 0};    
Output : (0  1) and (2  4) 
Subarrays arr[0..1] and arr[2..4] have
same average.

Input : arr[] = {4, 3, 5, 9, 11};
Output : Not possible
```

[问于微软](https://www.careercup.com/question?id=2622)

一种**天真的方法**是运行两个循环，找到平均值相等的子阵列。

## C++

```
// Simple C++ program to find subarrays
// whose averages are equal
#include<bits/stdc++.h>
using namespace std;

// Finding two subarrays
// with equal average.
void findSubarrays(int arr[], int n)
{
    bool found = false;
    int lsum = 0;
    for (int i = 0; i < n - 1; i++)
    {
        lsum += arr[i];
        int rsum = 0;
        for (int j = i + 1; j < n; j++)
            rsum += arr[j];

        // If averages of arr[0...i] and
        // arr[i+1..n-1] are same. To avoid
        // floating point problems we compare
        // "lsum*(n-i+1)" and "rsum*(i+1)"
        // instead of "lsum/(i+1)" and
        // "rsum/(n-i+1)"
        if (lsum * (n - i - 1) ==
               rsum * (i + 1))
        {
            printf("From (%d %d) to (%d %d)\n",
                           0, i, i + 1, n - 1);
            found = true;
        }
    }

    // If no subarrays found
    if (found == false)
        cout << "Subarrays not found"
             << endl;
}

// Driver code
int main()
{
    int arr[] = {1, 5, 7, 2, 0};
    int n = sizeof(arr) / sizeof(arr[0]);
    findSubarrays(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Simple Java program to find subarrays
// whose averages are equal

public class GFG {

    // Finding two subarrays
    // with equal average.
    static void findSubarrays(int[] arr, int n)
    {
        boolean found = false;
        int lsum = 0;

        for (int i = 0; i < n - 1; i++)
        {
            lsum += arr[i];
            int rsum = 0;

            for (int j = i + 1; j < n; j++)
                rsum += arr[j];

            // If averages of arr[0...i] and
            // arr[i+1..n-1] are same. To avoid
            // floating point problems we compare
            // "lsum*(n-i+1)" and "rsum*(i+1)"
            // instead of "lsum/(i+1)" and
            // "rsum/(n-i+1)"
            if (lsum * (n - i - 1) ==
                                rsum * (i + 1))
            {
                System.out.println("From (0 " + i
                        + ") to (" +(i + 1) + " "
                                + (n - 1)+ ")");

                found = true;
            }
        }

        // If no subarrays found
        if (found == false)
            System.out.println( "Subarrays not "
                                    + "found");
    }

    // Driver code
    static public void main (String[] args)
    {
        int[] arr = {1, 5, 7, 2, 0};
        int n = arr.length;
        findSubarrays(arr, n);
    }
}

// This code is contributed by Mukul Singh.
```

## 蟒蛇 3

```
# Simple Python 3 program to find subarrays
# whose averages are equal

# Finding two subarrays with equal average.
def findSubarrays(arr, n):

    found = False
    lsum = 0
    for i in range(n - 1):

        lsum += arr[i]
        rsum = 0
        for j in range(i + 1, n):
            rsum += arr[j]

        # If averages of arr[0...i] and
        # arr[i+1..n-1] are same. To avoid
        # floating point problems we compare
        # "lsum*(n-i+1)" and "rsum*(i+1)"
        # instead of "lsum/(i+1)" and
        # "rsum/(n-i+1)"
        if (lsum * (n - i - 1) == rsum * (i + 1)):
            print("From", "(", 0, i, ")",
                  "to", "(", i + 1, n - 1, ")")
            found = True

    # If no subarrays found
    if (found == False):
        print("Subarrays not found")

# Driver code
if __name__ == "__main__":

    arr = [1, 5, 7, 2, 0]
    n = len(arr)
    findSubarrays(arr, n)

# This code is contributed by ita_c
```

## C#

```
// Simple C# program to find subarrays
// whose averages are equal
using System;

public class GFG {

    // Finding two subarrays
    // with equal average.
    static void findSubarrays(int []arr, int n)
    {
        bool found = false;
        int lsum = 0;

        for (int i = 0; i < n - 1; i++)
        {
            lsum += arr[i];
            int rsum = 0;

            for (int j = i + 1; j < n; j++)
                rsum += arr[j];

            // If averages of arr[0...i] and
            // arr[i+1..n-1] are same. To avoid
            // floating point problems we compare
            // "lsum*(n-i+1)" and "rsum*(i+1)"
            // instead of "lsum/(i+1)" and
            // "rsum/(n-i+1)"
            if (lsum * (n - i - 1) ==
                                  rsum * (i + 1))
            {
                Console.WriteLine("From ( 0 " + i
                        + ") to(" + (i + 1) + " "
                                + (n - 1) + ")");

                found = true;
            }
        }

        // If no subarrays found
        if (found == false)
            Console.WriteLine( "Subarrays not "
                                    + "found");
    }

    // Driver code
    static public void Main ()
    {
        int []arr = {1, 5, 7, 2, 0};
        int n = arr.Length;
        findSubarrays(arr, n);
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Simple PHP program to find subarrays
// whose averages are equal

// Finding two subarrays
// with equal average.
function findSubarrays( $arr, $n)
{
    $found = false;
    $lsum = 0;
    for ( $i = 0; $i < $n - 1; $i++)
    {
        $lsum += $arr[$i];
        $rsum = 0;
        for ( $j = $i + 1; $j < $n; $j++)
            $rsum += $arr[$j];

        // If averages of arr[0...i] and
        // arr[i+1..n-1] are same. To avoid
        // floating point problems we compare
        // "lsum*(n-i+1)" and "rsum*(i+1)"
        // instead of "lsum/(i+1)" and "rsum/(n-i+1)"
        if ($lsum * ($n - $i - 1) ==
                $rsum * ($i + 1))
        {
        echo "From ( 0 ", $i," )".
             " to (", $i + 1," ", $n - 1,")\n";

            $found = true;
        }
    }

    // If no subarrays found
    if ($found == false)
        echo "Subarrays not found" ;
}

// Driver code
$arr = array(1, 5, 7, 2, 0);
$n = count($arr);
findSubarrays($arr, $n);

// This code is contributed by vt_m
?>
```

## java 描述语言

```
<script>

// Simple Javascript program to find subarrays
// whose averages are equal

    // Finding two subarrays
    // with equal average.
    function findSubarrays(arr,n)
    {
        let found = false;
        let lsum = 0;

        for (let i = 0; i < n - 1; i++)
        {
            lsum += arr[i];
            let rsum = 0;

            for (let j = i + 1; j < n; j++)
                rsum += arr[j];

            // If averages of arr[0...i] and
            // arr[i+1..n-1] are same. To avoid
            // floating point problems we compare
            // "lsum*(n-i+1)" and "rsum*(i+1)"
            // instead of "lsum/(i+1)" and
            // "rsum/(n-i+1)"
            if (lsum * (n - i - 1) ==
                                rsum * (i + 1))
            {
                document.write("From (0 " + i
                        + ") to (" +(i + 1) + " "
                                + (n - 1)+ ")");

                found = true;
            }
        }

        // If no subarrays found
        if (found == false)
            document.write( "Subarrays not "
                                    + "found");
    }

    // Driver code
    let arr=[1, 5, 7, 2, 0];
    let n = arr.length;
    findSubarrays(arr, n);

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
From (0  1) to (2  4)
```

**时间复杂度:**O(n<sup>2</sup>)
T5】辅助空间: O(1)
一个**高效的解决方案**就是求数组元素的和。将 leftsum 初始化为零。运行一个循环，通过添加数组元素找到 leftsum。对于右和，我们从总和中减去左和，然后求出右和，并根据它们的指数求出左和右和的平均值。

```
1) Compute sum of all array elements. Let this 
   sum be "sum"
2) Initialize leftsum = 0.
3) Run a loop for i=0 to n-1.
    a) leftsum  = leftsum + arr[i]
    b) rightsum = sum - leftsum
    c) If average of left and right are same, 
       print current index as output.
```

以下是上述方法的实现:

## C++

```
// Efficient C++ program for
// dividing array to make
// average equal
#include<bits/stdc++.h>
using namespace std;

void findSubarrays(int arr[], int n)
{
    // Find array sum
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    bool found = false;
    int lsum = 0;
    for (int i = 0; i < n - 1; i++)
    {
        lsum += arr[i];
        int rsum = sum - lsum;

        // If averages of arr[0...i]
        // and arr[i+1..n-1] are same.
        // To avoid floating point problems
        // we compare "lsum*(n-i+1)"
        // and "rsum*(i+1)" instead of
        // "lsum/(i+1)" and "rsum/(n-i+1)"
        if (lsum * (n - i - 1) == rsum * (i + 1))
        {
            printf("From (%d %d) to (%d %d)\n",
                               0, i, i+1, n-1);
            found = true;
        }
    }

    // If no subarrays found
    if (found == false)
        cout << "Subarrays not found"
             << endl;
}

// Driver code
int main()
{
    int arr[] = {1, 5, 7, 2, 0};
    int n = sizeof(arr) / sizeof(arr[0]);
    findSubarrays(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java program for
// dividing array to make
// average equal
import java.util.*;

class GFG
{
static void findSubarrays(int arr[], int n)
{
    // Find array sum
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    boolean found = false;
    int lsum = 0;
    for (int i = 0; i < n - 1; i++)
    {
        lsum += arr[i];
        int rsum = sum - lsum;

        // If averages of arr[0...i]
        // and arr[i+1..n-1] are same.
        // To avoid floating point problems
        // we compare "lsum*(n-i+1)"
        // and "rsum*(i+1)" instead of
        // "lsum/(i+1)" and "rsum/(n-i+1)"
        if (lsum * (n - i - 1) == rsum * (i + 1))
        {
            System.out.printf("From (%d %d) to (%d %d)\n",
                                      0, i, i + 1, n - 1);
            found = true;
        }
    }

    // If no subarrays found
    if (found == false)
        System.out.println("Subarrays not found");
}

// Driver code
static public void main ( String []arg)
{
    int arr[] = {1, 5, 7, 2, 0};
    int n = arr.length;
    findSubarrays(arr, n);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Efficient Python program for
# dividing array to make
# average equal

def findSubarrays(arr, n):

    # Find array sum
    sum = 0;
    for i in range(n):
        sum += arr[i];

    found = False;
    lsum = 0;
    for i in range(n - 1):
        lsum += arr[i];
        rsum = sum - lsum;

        # If averages of arr[0...i]
        # and arr[i + 1..n - 1] are same.
        # To avoid floating poproblems
        # we compare "lsum*(n - i + 1)"
        # and "rsum*(i + 1)" instead of
        # "lsum / (i + 1)" and "rsum/(n - i + 1)"
        if (lsum * (n - i - 1) == rsum * (i + 1)):
            print("From (%d %d) to (%d %d)\n"%
                   (0, i, i + 1, n - 1));
            found = True;

    # If no subarrays found
    if (found == False):
        print("Subarrays not found");

# Driver code
if __name__ == '__main__':
    arr = [ 1, 5, 7, 2, 0 ];
    n = len(arr);
    findSubarrays(arr, n);

# This code is contributed by Rajput-Ji
```

## C#

```
// Efficient C# program for
// dividing array to make
// average equal
using System;

class GFG
{
static void findSubarrays(int []arr, int n)
{
    // Find array sum
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    bool found = false;
    int lsum = 0;
    for (int i = 0; i < n - 1; i++)
    {
        lsum += arr[i];
        int rsum = sum - lsum;

        // If averages of arr[0...i]
        // and arr[i+1..n-1] are same.
        // To avoid floating point problems
        // we compare "lsum*(n-i+1)"
        // and "rsum*(i+1)" instead of
        // "lsum/(i+1)" and "rsum/(n-i+1)"
        if (lsum * (n - i - 1) == rsum * (i + 1))
        {
            Console.Write("From ({0} {1}) to ({2} {3})\n",
                                      0, i, i + 1, n - 1);
            found = true;
        }
    }

    // If no subarrays found
    if (found == false)
        Console.WriteLine("Subarrays not found");
}

// Driver code
static public void Main ( String []arg)
{
    int []arr = {1, 5, 7, 2, 0};
    int n = arr.Length;
    findSubarrays(arr, n);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Efficient Javascript program for
// dividing array to make
// average equal

    function findSubarrays(arr,n)
    {
    // Find array sum
    let sum = 0;
    for (let i = 0; i < n; i++)
        sum += arr[i];

    let found = false;
    let lsum = 0;
    for (let i = 0; i < n - 1; i++)
    {
        lsum += arr[i];
        let rsum = sum - lsum;

        // If averages of arr[0...i]
        // and arr[i+1..n-1] are same.
        // To avoid floating point problems
        // we compare "lsum*(n-i+1)"
        // and "rsum*(i+1)" instead of
        // "lsum/(i+1)" and "rsum/(n-i+1)"
        if (lsum * (n - i - 1) == rsum * (i + 1))
        {
            document.write(
       "From (0 "+i+") to ("+(i+1)+" "+(n-1)+")\n"
      );

            found = true;
        }
    }

    // If no subarrays found
    if (found == false)
        document.write("Subarrays not found");
    }
    // Driver code
    let arr=[1, 5, 7, 2, 0];
    let n = arr.length;
    findSubarrays(arr, n);

    // This code is contributed by rag2127

</script>
```

**输出:**

```
From (0  1) to (2  4)
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)
本文由**丹麦语 _RAZA** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。