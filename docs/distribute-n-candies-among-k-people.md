# 在 K 人中分发 N 颗糖果

> 原文:[https://www . geesforgeks . org/distribute-n-candes-in-k-people/](https://www.geeksforgeeks.org/distribute-n-candies-among-k-people/)

给了 N 个糖果和 K 个人。在第一轮中，第一个人得到 1 颗糖果，第二个人得到 2 颗糖果，以此类推，直到 K 个人。在下一轮，第一个人得到 K+1 颗糖果，第二个人得到 k+2 颗糖果，以此类推。如果糖果的数量少于每次转动所需的糖果数量，则该人收到剩余数量的糖果。
任务是找到每个人最后拥有的糖果总数。
**例:**

> **输入:** N = 7，K = 4
> **输出:** 1 2 3 1
> 第一个转弯，第四个人要给 4 颗糖果，但是还有
> 只剩下 1 颗，因此他只拿了一颗。
> **输入:** N = 10，K = 3
> **输出:** 5 2 3
> 在第二个转弯处，第一个人收到 4 个，然后我们就没有糖果了。

一种**天真的方法**是每次循环迭代，并相应地分发糖果，直到糖果完成。
**时间复杂度:** O(分配数)
A **更好的方法**是在 O(1)中执行每一个回合，计算自然数的和，直到系列的最后一项为**(回合*k)** ，减去自然数的和，直到前一系列的最后一项为**(回合-1)*k.** 继续这样做，直到和小于 N，一旦超过，则以给定的方式分配糖果，直到可能。如果每个人在一个回合中得到他想要得到的糖果数量，我们称这个回合结束。
以下是上述方法的实施:

## C++

```
// C++ code for better approach
// to distribute candies
#include <bits/stdc++.h>
using namespace std;

// Function to find out the number of
// candies every person received
void candies(int n, int k)
{

    // Count number of complete turns
    int count = 0;

    // Get the last term
    int ind = 1;

    // Stores the number of candies
    int arr[k];

    memset(arr, 0, sizeof(arr));

    while (n) {

        // Last term of last and
        // current series
        int f1 = (ind - 1) * k;
        int f2 = ind * k;

        // Sum of current and last  series
        int sum1 = (f1 * (f1 + 1)) / 2;
        int sum2 = (f2 * (f2 + 1)) / 2;

        // Sum of current series only
        int res = sum2 - sum1;

        // If sum of current is less than N
        if (res <= n) {
            count++;
            n -= res;
            ind++;
        }
        else // Individually distribute
        {
            int i = 0;

            // First term
            int term = ((ind - 1) * k) + 1;

            // Distribute candies till there
            while (n > 0) {

                // Candies available
                if (term <= n) {
                    arr[i++] = term;
                    n -= term;
                    term++;
                }
                else // Not available
                {
                    arr[i++] = n;
                    n = 0;
                }
            }
        }
    }

    // Count the total candies
    for (int i = 0; i < k; i++)
        arr[i] += (count * (i + 1))
                + (k * (count * (count - 1)) / 2);

    // Print the total candies
    for (int i = 0; i < k; i++)
        cout << arr[i] << " ";
}

// Driver Code
int main()
{
    int n = 10, k = 3;
    candies(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  code for better approach
// to distribute candies

class GFG {
    // Function to find out the number of
    // candies every person received
    static void candies(int n, int k){
        int[] arr = new int[k];
        int j = 0;
        while(n>0){

            for(int i =0;i<k;i++){
                j++;
                if(n<=0){
                    break;
                }
                else{
                    if(j<n){
                        arr[i] = arr[i]+j;
                    }
                    else{
                        arr[i] = arr[i]+n;
                    }
                    n = n-j;
                }

            }
        }
        for(int i:arr){
            System.out.print(i+" ");
        }
    }
            // Driver Code
      public static void main(String[] args)
      {
        int n = 10, k = 3;
        candies(n, k);
      }
    }

        // This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 code for better approach
# to distribute candies
import math as mt

# Function to find out the number of
# candies every person received
def candies(n, k):

    # Count number of complete turns
    count = 0

    # Get the last term
    ind = 1

    # Stores the number of candies
    arr = [0 for i in range(k)]

    while n > 0:

        # Last term of last and
        # current series
        f1 = (ind - 1) * k
        f2 = ind * k

        # Sum of current and last series
        sum1 = (f1 * (f1 + 1)) // 2
        sum2 = (f2 * (f2 + 1)) //2

        # Sum of current series only
        res = sum2 - sum1

        # If sum of current is less than N
        if (res <= n):
            count += 1
            n -= res
            ind += 1
        else: # Individually distribute
            i = 0

            # First term
            term = ((ind - 1) * k) + 1

            # Distribute candies till there
            while (n > 0):

                # Candies available
                if (term <= n):
                    arr[i] = term
                    i += 1
                    n -= term
                    term += 1
                else:
                    arr[i] = n
                    i += 1
                    n = 0

    # Count the total candies
    for i in range(k):
        arr[i] += ((count * (i + 1)) +
                   (k * (count * (count - 1)) // 2))

    # Print the total candies
    for i in range(k):
        print(arr[i], end = " ")

# Driver Code
n, k = 10, 3
candies(n, k)

# This code is contributed by Mohit kumar
```

## C#

```
// C# code for better approach
// to distribute candies

using System;
class GFG
{
    // Function to find out the number of
    // candies every person received
    static void candies(int n, int k)
    {

        // Count number of complete turns
        int count = 0;

        // Get the last term
        int ind = 1;

        // Stores the number of candies
        int []arr=new int[k];

        for(int i=0;i<k;i++)
         arr[i]=0;

        while (n>0) {

            // Last term of last and
            // current series
            int f1 = (ind - 1) * k;
            int f2 = ind * k;

            // Sum of current and last series
            int sum1 = (f1 * (f1 + 1)) / 2;
            int sum2 = (f2 * (f2 + 1)) / 2;

            // Sum of current series only
            int res = sum2 - sum1;

            // If sum of current is less than N
            if (res <= n) {
                count++;
                n -= res;
                ind++;
            }
            else // Individually distribute
            {
                int i = 0;

                // First term
                int term = ((ind - 1) * k) + 1;

                // Distribute candies till there
                while (n > 0) {

                    // Candies available
                    if (term <= n) {
                        arr[i++] = term;
                        n -= term;
                        term++;
                    }
                    else // Not available
                    {
                        arr[i++] = n;
                        n = 0;
                    }
                }
            }
        }

        // Count the total candies
        for (int i = 0; i < k; i++)
            arr[i] += (count * (i + 1))
                    + (k * (count * (count - 1)) / 2);

        // Print the total candies
        for (int i = 0; i < k; i++)
            Console.Write( arr[i] + " ");
    }

    // Driver Code
    public static void Main()
    {
        int n = 10, k = 3;
        candies(n, k);

    }
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code for better approach
// to distribute candies

// Function to find out the number of
// candies every person received
function candies($n, $k)
{

    // Count number of complete turns
    $count = 0;

    // Get the last term
    $ind = 1;

    // Stores the number of candies
    $arr = array_fill(0, $k, 0) ;

    while ($n)
    {

        // Last term of last and
        // current series
        $f1 = ($ind - 1) * $k;
        $f2 = $ind * $k;

        // Sum of current and last series
        $sum1 = floor(($f1 * ($f1 + 1)) / 2);
        $sum2 = floor(($f2 * ($f2 + 1)) / 2);

        // Sum of current series only
        $res = $sum2 - $sum1;

        // If sum of current is less than N
        if ($res <= $n)
        {
            $count++;
            $n -= $res;
            $ind++;
        }
        else // Individually distribute
        {
            $i = 0;

            // First term
            $term = (($ind - 1) * $k) + 1;

            // Distribute candies till there
            while ($n > 0)
            {

                // Candies available
                if ($term <= $n)
                {
                    $arr[$i++] = $term;
                    $n -= $term;
                    $term++;
                }
                else // Not available
                {
                    $arr[$i++] = $n;
                    $n = 0;
                }
            }
        }
    }

    // Count the total candies
    for ($i = 0; $i < $k; $i++)
        $arr[$i] += floor(($count * ($i + 1)) + ($k *
                          ($count * ($count - 1)) / 2));

    // Print the total candies
    for ($i = 0; $i < $k; $i++)
        echo $arr[$i], " ";
}

// Driver Code
$n = 10;
$k = 3;
candies($n, $k);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// JavaScript  code for better approach
// to distribute candies

    // Function to find out the number of
    // candies every person received
    function candies(n , k) {

        // Count number of complete turns
        var count = 0;

        // Get the last term
        var ind = 1;

        // Stores the number of candies
        var arr = Array(k);

        for (i = 0; i < k; i++)
            arr[i] = 0;

        while (n > 0) {

            // Last term of last and
            // current series
            var f1 = (ind - 1) * k;
            var f2 = ind * k;

            // Sum of current and last series
            var sum1 = (f1 * (f1 + 1)) / 2;
            var sum2 = (f2 * (f2 + 1)) / 2;

            // Sum of current series only
            var res = sum2 - sum1;

            // If sum of current is less than N
            if (res <= n) {
                count++;
                n -= res;
                ind++;
            } else // Individually distribute
            {
                var i = 0;

                // First term
                var term = ((ind - 1) * k) + 1;

                // Distribute candies till there
                while (n > 0) {

                    // Candies available
                    if (term <= n) {
                        arr[i++] = term;
                        n -= term;
                        term++;
                    } else // Not available
                    {
                        arr[i++] = n;
                        n = 0;
                    }
                }
            }
        }

        // Count the total candies
        for (i = 0; i < k; i++)
            arr[i] += (count * (i + 1)) +
            (k * (count * (count - 1)) / 2);

        // Print the total candies
        for (i = 0; i < k; i++)
            document.write(arr[i] + " ");
    }

    // Driver Code

        var n = 10, k = 3;
        candies(n, k);

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
5 2 3
```

**时间复杂度:** O(圈数+ K)
一种**有效的方法**是利用二分搜索法找到自然数之和小于 N 的最大数(比如 MAXI)。因为最后一个数总是 K 的倍数，所以我们得到最后一个完整圈数。从 n 中减去到那时的总和。通过遍历数组来分配剩余的糖果。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find out the number of
// candies every person received
void candies(int n, int k)
{

    // Count number of complete turns
    int count = 0;

    // Get the last term
    int ind = 1;

    // Stores the number of candies
    int arr[k];

    memset(arr, 0, sizeof(arr));

    int low = 0, high = n;

    // Do a binary search to find the number whose
    // sum is less than N.
    while (low <= high) {

        // Get mide
        int mid = (low + high) >> 1;
        int sum = (mid * (mid + 1)) >> 1;

        // If sum is below N
        if (sum <= n) {

            // Find number of complete turns
            count = mid / k;

            // Right halve
            low = mid + 1;
        }
        else {

            // Left halve
            high = mid - 1;
        }
    }

    // Last term of last complete series
    int last = (count * k);

    // Subtract the sum till
    n -= (last * (last + 1)) / 2;

    int i = 0;

    // First term of incomplete series
    int term = (count * k) + 1;

    while (n) {
        if (term <= n) {
            arr[i++] = term;
            n -= term;
            term++;
        }
        else {
            arr[i] += n;
            n = 0;
        }
    }

    // Count the total candies
    for (int i = 0; i < k; i++)
        arr[i] += (count * (i + 1))
               + (k * (count * (count - 1)) / 2);

    // Print the total candies
    for (int i = 0; i < k; i++)
        cout << arr[i] << " ";
}

// Driver Code
int main()
{
    int n = 7, k = 4;
    candies(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

class GFG
{
    // Function to find out the number of
    // candies every person received
    static void candies(int n, int k)
    {

        // Count number of complete turns
        int count = 0;

        // Get the last term
        int ind = 1;

        // Stores the number of candies
        int []arr=new int[k];

        for(int i=0;i<k;i++)
         arr[i]=0;

        int low = 0, high = n;

        // Do a binary search to find the number whose
        // sum is less than N.
        while (low <= high) {

            // Get mide
            int mid = (low + high) >> 1;
            int sum = (mid * (mid + 1)) >> 1;

            // If sum is below N
            if (sum <= n) {

                // Find number of complete turns
                count = mid / k;

                // Right halve
                low = mid + 1;
            }
            else {

                // Left halve
                high = mid - 1;
            }
        }

        // Last term of last complete series
        int last = (count * k);

        // Subtract the sum till
        n -= (last * (last + 1)) / 2;

        int j = 0;

        // First term of incomplete series
        int term = (count * k) + 1;

        while (n > 0) {
            if (term <= n) {
                arr[j++] = term;
                n -= term;
                term++;
            }
            else {
                arr[j] += n;
                n = 0;
            }
        }

        // Count the total candies
        for (int i = 0; i < k; i++)
            arr[i] += (count * (i + 1))
                + (k * (count * (count - 1)) / 2);

        // Print the total candies
        for (int i = 0; i < k; i++)
            System.out.print( arr[i] + " " );
    }

    // Driver Code
    public static void main(String []args)
    {
        int n = 7, k = 4;
        candies(n, k);

    }

}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to find out the number of
# candies every person received
def candies(n, k):

    # Count number of complete turns
    count = 0;

    # Get the last term
    ind = 1;

    # Stores the number of candies
    arr = [0] * k;

    low = 0;
    high = n;

    # Do a binary search to find the
    # number whose sum is less than N.
    while (low <= high):

        # Get mide
        mid = (low + high) >> 1;
        sum = (mid * (mid + 1)) >> 1;

        # If sum is below N
        if (sum <= n):

            # Find number of complete turns
            count = int(mid / k);

            # Right halve
            low = mid + 1;
        else:

            # Left halve
            high = mid - 1;

    # Last term of last complete series
    last = (count * k);

    # Subtract the sum till
    n -= int((last * (last + 1)) / 2);

    i = 0;

    # First term of incomplete series
    term = (count * k) + 1;

    while (n):
        if (term <= n):
            arr[i] = term;
            i += 1;
            n -= term;
            term += 1;
        else:
            arr[i] += n;
            n = 0;

    # Count the total candies
    for i in range(k):
        arr[i] += ((count * (i + 1)) +
                int(k * (count * (count - 1)) / 2));

    # Print the total candies
    for i in range(k):
        print(arr[i], end = " ");

# Driver Code
n = 7;
k = 4;
candies(n, k);

# This code is contributed by chandan_jnu
```

## C#

```
// C# implementation of the above approach

using System;
class GFG
{
    // Function to find out the number of
    // candies every person received
    static void candies(int n, int k)
    {

        // Count number of complete turns
        int count = 0;

        // Get the last term
        int ind = 1;

        // Stores the number of candies
        int []arr=new int[k];

        for(int i=0;i<k;i++)
         arr[i]=0;

        int low = 0, high = n;

        // Do a binary search to find the number whose
        // sum is less than N.
        while (low <= high) {

            // Get mide
            int mid = (low + high) >> 1;
            int sum = (mid * (mid + 1)) >> 1;

            // If sum is below N
            if (sum <= n) {

                // Find number of complete turns
                count = mid / k;

                // Right halve
                low = mid + 1;
            }
            else {

                // Left halve
                high = mid - 1;
            }
        }

        // Last term of last complete series
        int last = (count * k);

        // Subtract the sum till
        n -= (last * (last + 1)) / 2;

        int j = 0;

        // First term of incomplete series
        int term = (count * k) + 1;

        while (n > 0) {
            if (term <= n) {
                arr[j++] = term;
                n -= term;
                term++;
            }
            else {
                arr[j] += n;
                n = 0;
            }
        }

        // Count the total candies
        for (int i = 0; i < k; i++)
            arr[i] += (count * (i + 1))
                + (k * (count * (count - 1)) / 2);

        // Print the total candies
        for (int i = 0; i < k; i++)
            Console.Write( arr[i] + " " );
    }

    // Driver Code
    public static void Main()
    {
        int n = 7, k = 4;
        candies(n, k);

    }

}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to find out the number of
// candies every person received
function candies($n, $k)
{

    // Count number of complete turns
    $count = 0;

    // Get the last term
    $ind = 1;

    // Stores the number of candies
    $arr = array_fill(0, $k, 0);

    $low = 0;
    $high = $n;

    // Do a binary search to find the
    // number whose sum is less than N.
    while ($low <= $high)
    {

        // Get mide
        $mid = ($low + $high) >> 1;
        $sum = ($mid * ($mid + 1)) >> 1;

        // If sum is below N
        if ($sum <= $n)
        {

            // Find number of complete turns
            $count = (int)($mid / $k);

            // Right halve
            $low = $mid + 1;
        }
        else
        {

            // Left halve
            $high = $mid - 1;
        }
    }

    // Last term of last complete series
    $last = ($count * $k);

    // Subtract the sum till
    $n -= (int)(($last * ($last + 1)) / 2);

    $i = 0;

    // First term of incomplete series
    $term = ($count * $k) + 1;

    while ($n)
    {
        if ($term <= $n)
        {
            $arr[$i++] = $term;
            $n -= $term;
            $term++;
        }
        else
        {
            $arr[$i] += $n;
            $n = 0;
        }
    }

    // Count the total candies
    for ($i = 0; $i < $k; $i++)
        $arr[$i] += ($count * ($i + 1)) +
         (int)($k * ($count * ($count - 1)) / 2);

    // Print the total candies
    for ($i = 0; $i < $k; $i++)
        echo $arr[$i] . " ";
}

// Driver Code
$n = 7;
$k = 4;
candies($n, $k);

// This code is contributed
// by chandan_jnu
?>
```

## java 描述语言

```
<script>
// javascript implementation of the above approach   
// Function to find out the number of
    // candies every person received
    function candies(n , k) {

        // Count number of complete turns
        var count = 0;

        // Get the last term
        var ind = 1;

        // Stores the number of candies
        var arr = Array(k).fill(0);

        for (i = 0; i < k; i++)
            arr[i] = 0;

        var low = 0, high = n;

        // Do a binary search to find the number whose
        // sum is less than N.
        while (low <= high) {

            // Get mide
            var mid = parseInt((low + high) /2);
            var sum = parseInt((mid * (mid + 1)) / 2);

            // If sum is below N
            if (sum <= n) {

                // Find number of complete turns
                count = parseInt(mid / k);

                // Right halve
                low = mid + 1;
            } else {

                // Left halve
                high = mid - 1;
            }
        }

        // Last term of last complete series
        var last = (count * k);

        // Subtract the sum till
        n -= (last * (last + 1)) / 2;

        var j = 0;

        // First term of incomplete series
        var term = (count * k) + 1;

        while (n > 0) {
            if (term <= n) {
                arr[j++] = term;
                n -= term;
                term++;
            } else {
                arr[j] += n;
                n = 0;
            }
        }

        // Count the total candies
        for (i = 0; i < k; i++)
            arr[i] += (count * (i + 1)) + (k * (count * (count - 1)) / 2);

        // Print the total candies
        for (i = 0; i < k; i++)
            document.write(arr[i] + " ");
    }

    // Driver Code

        var n = 7, k = 4;
        candies(n, k);

// This code contributed by aashish1995
</script>
```

**Output:** 

```
1 2 3 1
```

**时间复杂度:** O(log N + K)