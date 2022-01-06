# 一个数的第五根

> 原文:[https://www.geeksforgeeks.org/fifth-root-of-a-number/](https://www.geeksforgeeks.org/fifth-root-of-a-number/)

给定一个数字，打印该数字 5 '根的楼层。
**例:**

```
Input  : n = 32
Output : 2
2 raise to power 5 is 32

Input  : n = 250
Output : 3
Fifth square root of 250 is between 3 and 4
So floor value is 3.
```

**方法 1(简单)**
一个简单的解决方法是将结果初始化为 0，当结果 <sup>5</sup> 小于或等于 n 时，继续递增结果，最后返回结果–1。

## C++14

```
// A C++ program to find floor of 5th root
#include<bits/stdc++.h>
using namespace std;

// Returns floor of 5th root of n
int floorRoot5(int n)
{
    // Base cases
    if (n == 0 || n == 1)
        return n;

    // Initialize result
    int res = 0;

    // Keep incrementing res while res^5 is
    // smaller than or equal to n
    while (res*res*res*res*res <= n)
        res++;

    // Return floor of 5'th root
    return res-1;
}

// Driver program
int main()
{
    int n = 250;
    cout << "Floor of 5'th root is "
         << floorRoot5(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find floor of 5th root

class GFG {

// Returns floor of 5th root of n
static int floorRoot5(int n)
{

    // Base cases
    if (n == 0 || n == 1)
        return n;

    // Initialize result
    int res = 0;

    // Keep incrementing res while res^5
    // is smaller than or equal to n
    while (res * res * res * res * res <= n)
        res++;

    // Return floor of 5'th root
    return res-1;
}

    // Driver Code
    public static void main(String []args)
    {
        int n = 250;
        System.out.println("Floor of 5'th root is "
                            + floorRoot5(n));
    }
}

// This code is contributed by Anshul Aggarwal.
```

## 蟒蛇 3

```
# A Python3 program to find the floor
# of the 5th root

# Returns floor of 5th root of n
def floorRoot5(n):

    # Base cases
    if n == 0 and n == 1:
        return n

    # Initialize result
    res = 0

    # Keep incrementing res while res^5
    # is smaller than or equal to n
    while res * res * res * res * res <= n:
        res += 1

    # Return floor of 5'th root
    return res-1

# Driver Code
if __name__ == "__main__":

    n = 250
    print("Floor of 5'th root is",
                    floorRoot5(n))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find floor of 5th root
using System;

class GFG {

// Returns floor of 5th root of n
static int floorRoot5(int n)
{

    // Base cases
    if (n == 0 || n == 1)
        return n;

    // Initialize result
    int res = 0;

    // Keep incrementing res while res^5
    // is smaller than or equal to n
    while (res * res * res * res * res <= n)
        res++;

    // Return floor of 5'th root
    return res-1;
}

    // Driver Code
    public static void Main()
    {
        int n = 250;
        Console.Write("Floor of 5'th root is "
                       + floorRoot5(n));
    }
}

// This code is contributed by Sumit Sudhakar.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// floor of 5th root

// Returns floor of
// 5th root of n
function floorRoot5($n)
{

    // Base cases
    if ($n == 0 || $n == 1)
        return $n;

    // Initialize result
    $res = 0;

    // Keep incrementing res while
    // res^5 is smaller than or
    // equal to n
    while ($res * $res * $res *
           $res * $res <= $n)
        $res++;

    // Return floor
    // of 5'th root
    return $res - 1;
}

    // Driver Code
    $n = 250;
    echo "Floor of 5'th root is "
                , floorRoot5($n);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find floor of 5th root

// Returns floor of 5th root of n
function floorRoot5(n)
{

    // Base cases
    if (n == 0 || n == 1)
        return n;

    // Initialize result
    let res = 0;

    // Keep incrementing res while res^5
    // is smaller than or equal to n
    while (res * res * res * res * res <= n)
        res++;

    // Return floor of 5'th root
    return res-1;
}

// Driver Code

        let n = 250;
       document.write("Floor of 5'th root is "
                            + floorRoot5(n));

</script>
```

**输出:**

```
Floor of 5'th root is 3
```

上述解的时间复杂度为 **O(n <sup>1/5</sup> )** 。我们可以做得更好。参见下面的解决方案。
**方法二(二分搜索法)**
思路是做[二分搜索法](http://geeksquiz.com/binary-search/)。我们从 n/2 开始，如果它的 5 次幂大于 n，我们重复从 n/2+1 到 n 的区间，否则如果幂小于 n，我们重复从 0 到 n/2-1 的区间

## C++

```
// A C++ program to find floor of 5'th root
#include<bits/stdc++.h>
using namespace std;

// Returns floor of 5'th root of n
int floorRoot5(int n)
{
    // Base cases
    if (n == 0 || n == 1)
       return n;

    // Do Binary Search for floor of 5th square root
    int low = 1, high = n, ans = 0;
    while (low <= high)
    {
        // Find the middle point and its power 5
        int mid = (low + high) / 2;
        long int mid5 = mid*mid*mid*mid*mid;

        // If mid is the required root
        if (mid5 == n)
            return mid;

        // Since we need floor, we update answer when
        // mid5 is smaller than n, and move closer to
        // 5'th root
        if (mid5 < n)
        {
            low = mid + 1;
            ans = mid;
        }
        else // If mid^5 is greater than n
            high = mid - 1;
    }
    return ans;
}

// Driver program
int main()
{
    int n = 250;
    cout << "Floor of 5'th root is "
         << floorRoot5(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to find
// floor of 5'th root

class GFG {

    // Returns floor of 5'th
    // root of n
    static int floorRoot5(int n)
    {

        // Base cases
        if (n == 0 || n == 1)
        return n;

        // Do Binary Search for
        // floor of 5th square root
        int low = 1, high = n, ans = 0;
        while (low <= high)
        {

            // Find the middle point
            // and its power 5
            int mid = (low + high) / 2;
            long mid5 = mid * mid * mid *
                            mid * mid;

            // If mid is the required root
            if (mid5 == n)
                return mid;

            // Since we need floor,
            // we update answer when
            // mid5 is smaller than n,
            // and move closer to
            // 5'th root
            if (mid5 < n)
            {
                low = mid + 1;
                ans = mid;
            }

            // If mid^5 is greater
            // than n
            else
                high = mid - 1;
        }
        return ans;
    }

    // Driver Code
    public static void main(String []args)
    {
        int n = 250;
        System.out.println("Floor of 5'th root is " +
                                     floorRoot5(n));
    }
}

// This code is contributed by Anshul Aggarwal.
```

## 蟒蛇 3

```
# A Python3 program to find the floor
# of 5'th root

# Returns floor of 5'th root of n
def floorRoot5(n):

    # Base cases
    if n == 0 or n == 1:
        return n

    # Do Binary Search for floor of
    # 5th square root
    low, high, ans = 1, n, 0
    while low <= high:

        # Find the middle point and its power 5
        mid = (low + high) // 2
        mid5 = mid * mid * mid * mid * mid

        # If mid is the required root
        if mid5 == n:
            return mid

        # Since we need floor, we update answer
        # when mid5 is smaller than n, and move
        # closer to 5'th root
        if mid5 < n:

            low = mid + 1
            ans = mid

        else: # If mid^5 is greater than n
            high = mid - 1

    return ans

# Driver Code
if __name__ == "__main__":

    n = 250
    print("Floor of 5'th root is", floorRoot5(n))

# This code is contributed by Rituraj Jain
```

## C#

```
// A C# program to find
// floor of 5'th root
using System;

class GFG {

    // Returns floor of 5'th
    // root of n
    static int floorRoot5(int n)
    {

        // Base cases
        if (n == 0 || n == 1)
        return n;

        // Do Binary Search for
        // floor of 5th square root
        int low = 1, high = n, ans = 0;
        while (low <= high)
        {

            // Find the middle point
            // and its power 5
            int mid = (low + high) / 2;
            long mid5 = mid * mid * mid *
                            mid * mid;

            // If mid is the required root
            if (mid5 == n)
                return mid;

            // Since we need floor,
            // we update answer when
            // mid5 is smaller than n,
            // and move closer to
            // 5'th root
            if (mid5 < n)
            {
                low = mid + 1;
                ans = mid;
            }

            // If mid^5 is greater
            // than n
            else
                high = mid - 1;
        }
        return ans;
    }

    // Driver Code
    public static void Main(String []args)
    {
        int n = 250;
        Console.WriteLine("Floor of 5'th root is " +
                                     floorRoot5(n));
    }
}

// This code is contributed by Anshul Aggarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A PHP program to find floor of 5'th root

// Returns floor of 5'th root of n
function floorRoot5($n)
{
    // Base cases
    if ($n == 0 || $n == 1)
    return $n;

    // Do Binary Search for floor of 5th square root
    $low = 1;
    $high = $n;
    $ans = 0;
    while ($low <= $high)
    {
        // Find the middle point and its power 5
        $mid = (int)(($low + $high) / 2);
        $mid5 = $mid*$mid*$mid*$mid*$mid;

        // If mid is the required root
        if ($mid5 == $n)
            return $mid;

        // Since we need floor, we update answer when
        // mid5 is smaller than n, and move closer to
        // 5'th root
        if ($mid5 < $n)
        {
            $low = $mid + 1;
            $ans = $mid;
        }
        else // If mid^5 is greater than n
            $high = $mid - 1;
    }
    return $ans;
}

    // Driver code
    $n = 250;
    echo "Floor of 5'th root is ".floorRoot5($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// A javascript program to find
// floor of 5'th root  
// Returns floor of 5'th
// root of n
function floorRoot5(n)
{

    // Base cases
    if (n == 0 || n == 1)
    return n;

    // Do Binary Search for
    // floor of 5th square root
    var low = 1, high = n, ans = 0;
    while (low <= high)
    {

        // Find the middle point
        // and its power 5
        var mid = parseInt((low + high) / 2);
        var mid5 = mid * mid * mid *
                        mid * mid;

        // If mid is the required root
        if (mid5 == n)
            return mid;

        // Since we need floor,
        // we update answer when
        // mid5 is smaller than n,
        // and move closer to
        // 5'th root
        if (mid5 < n)
        {
            low = mid + 1;
            ans = mid;
        }

        // If mid^5 is greater
        // than n
        else
            high = mid - 1;
    }
    return ans;
}

// Driver Code
var n = 250;
document.write("Floor of 5'th root is " +
                             floorRoot5(n));

// This code contributed by Princi Singh

</script>
```

**输出:**

```
Floor of 5'th root is 3
```

**时间复杂度:**O(logN)
T3】辅助空间: O(1)
我们也可以用[牛顿拉夫森法](https://www.geeksforgeeks.org/solution-algebraic-transcendental-equations-set-3-newton-raphson-method/)来求精确根。实施见[本](http://qa.geeksforgeeks.org/7487/program-calculate-fifth-without-using-mathematical-operators)。
来源:[http://QA . geeksforgeeks . org/7487/program-calculate-first-不使用数学运算符](http://qa.geeksforgeeks.org/7487/program-calculate-fifth-without-using-mathematical-operators)
如发现有不正确的地方，请写评论，或者想分享更多以上讨论话题的信息