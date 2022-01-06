# 给定 N 个立方体的边时每个人立方体的最大体积

> 原文:[https://www . geeksforgeeks . org/给定 n 个立方体边缘时每个人的立方体最大体积/](https://www.geeksforgeeks.org/maximum-volume-of-cube-for-every-person-when-edge-of-n-cubes-are-given/)

给定一组分别表示 N 个立方体结构的边的 **N 个**整数。还给出了表示人数的整数 **M** 。任务是找到每个人可以得到的立方体的最大体积。
**注**:立方体可以从 N 个立方体中任意一个切割出任意形状。
**示例:**

> **输入:** a[] = {1，1，1，2，2}，m = 3
> **输出:** 4
> 三个人每人获得一片体积 4
> 人 1 从最后一个立方体获得一片体积 4。
> 第二个人从最后一个立方体中获得第四个体积的切片。
> 人物 3 从倒数第二个立方体中获得体积 4 的切片。
> **输入:** a[] = {2，2，2，2，2}，m = 4
> **输出:** 8

**天真法**:天真法是先计算所有立方体的体积，然后线性检查每个体积是否可以分布在所有 M 个人中，并在所有这些体积中找到最大体积。
T3】时间复杂度: O(N <sup>2</sup>

**高效的方法**:高效的方法就是用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来寻找答案。因为数组中给出了边长，所以将它们转换为相应立方体的体积。在所有立方体的体积中找出最大体积。说起来，最大音量是**最大音量**。现在，在范围[0，最大音量]上执行**二分搜索法**。

*   计算范围的中间值，比如说中间。
*   现在，计算体积*中间*的所有立方体中可切割的立方体总数。
*   如果可以切割的立方体总数超过了人数，那么可以为每个人切割立方体的体积量，因此我们检查范围**【mid+1，maxVolume】**中的较大值。
*   如果立方体总数不超过人数，那么我们检查范围**【低，中 1】**内的答案。

以下是上述方法的实现:

## C++

```
// C++ program to implement the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to get the maximum volume that
// every person can get
int getMaximumVloume(int a[], int n, int m)
{
    int maxVolume = 0;

    // Convert the length to respective volumes
    // and find the maximum volumes
    for (int i = 0; i < n; i++) {
        a[i] = a[i] * a[i] * a[i];

        maxVolume = max(a[i], maxVolume);
    }

    // Apply binary search with initial
    // low as 0 and high as the maximum most
    int low = 0, high = maxVolume;

    // Initial answer is 0 slices
    int maxVol = 0;

    // Apply binary search
    while (low <= high) {

        // Get the mid element
        int mid = (low + high) >> 1;

        // Count the slices of volume mid
        int cnt = 0;
        for (int i = 0; i < n; i++) {
            cnt += a[i] / mid;
        }

        // If the slices of volume
        // exceeds the number of persons
        // then every person can get volume mid
        if (cnt >= m) {

            // Then check for larger in the right half
            low = mid + 1;

            // Replace tbe answer with
            // current maximum i.e., mid
            maxVol = max(maxVol, mid);
        }

        // else traverse in the left half
        else
            high = mid - 1;
    }

    return maxVol;
}

// Driver code
int main()
{
    int a[] = { 1, 1, 1, 2, 2 };
    int n = sizeof(a) / sizeof(a[0]);
    int m = 3;

    cout << getMaximumVloume(a, n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the above approach
class GFG
{

    // Function to get the maximum volume that
    // every person can get
    static int getMaximumVloume(int a[], int n, int m)
    {
        int maxVolume = 0;

        // Convert the length to respective volumes
        // and find the maximum volumes
        for (int i = 0; i < n; i++)
        {
            a[i] = a[i] * a[i] * a[i];

            maxVolume = Math.max(a[i], maxVolume);
        }

        // Apply binary search with initial
        // low as 0 and high as the maximum most
        int low = 0, high = maxVolume;

        // Initial answer is 0 slices
        int maxVol = 0;

        // Apply binary search
        while (low <= high)
        {

            // Get the mid element
            int mid = (low + high) >> 1;

            // Count the slices of volume mid
            int cnt = 0;
            for (int i = 0; i < n; i++)
            {
                cnt += a[i] / mid;
            }

            // If the slices of volume
            // exceeds the number of persons
            // then every person can get volume mid
            if (cnt >= m)
            {

                // Then check for larger in the right half
                low = mid + 1;

                // Replace tbe answer with
                // current maximum i.e., mid
                maxVol = Math.max(maxVol, mid);
            }

            // else traverse in the left half
            else
            {
                high = mid - 1;
            }
        }

        return maxVol;
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = {1, 1, 1, 2, 2};
        int n = a.length;
        int m = 3;

        System.out.println(getMaximumVloume(a, n, m));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to implement
# the above approach

# Function to get the maximum volume
# that every person can get
def getMaximumVloume(a, n, m):
    maxVolume = 0

    # Convert the length to respective
    # volumes and find the maximum volumes
    for i in range(n):
        a[i] = a[i] * a[i] * a[i]

        maxVolume = max(a[i], maxVolume)

    # Apply binary search with initial
    # low as 0 and high as the maximum most
    low = 0
    high = maxVolume

    # Initial answer is 0 slices
    maxVol = 0

    # Apply binary search
    while (low <= high):

        # Get the mid element
        mid = (low + high) >> 1

        # Count the slices of volume mid
        cnt = 0
        for i in range(n):
            cnt += int(a[i] / mid)

        # If the slices of volume
        # exceeds the number of persons
        # then every person can get volume mid
        if (cnt >= m):

            # Then check for larger in the right half
            low = mid + 1

            # Replace tbe answer with
            # current maximum i.e., mid
            maxVol = max(maxVol, mid)

        # else traverse in the left half
        else:
            high = mid - 1

    return maxVol

# Driver code
if __name__ == '__main__':
    a = [1, 1, 1, 2, 2]
    n = len(a)
    m = 3

    print(getMaximumVloume(a, n, m))

# This code is contributed
# by Surendra_Gangwar
```

## C#

```
// C# program to implement the above approach
using System;

class GFG
{

    // Function to get the maximum volume that
    // every person can get
    static int getMaximumVloume(int []a, int n, int m)
    {
        int maxVolume = 0;

        // Convert the length to respective volumes
        // and find the maximum volumes
        for (int i = 0; i < n; i++)
        {
            a[i] = a[i] * a[i] * a[i];

            maxVolume = Math.Max(a[i], maxVolume);
        }

        // Apply binary search with initial
        // low as 0 and high as the maximum most
        int low = 0, high = maxVolume;

        // Initial answer is 0 slices
        int maxVol = 0;

        // Apply binary search
        while (low <= high)
        {

            // Get the mid element
            int mid = (low + high) >> 1;

            // Count the slices of volume mid
            int cnt = 0;
            for (int i = 0; i < n; i++)
            {
                cnt += a[i] / mid;
            }

            // If the slices of volume
            // exceeds the number of persons
            // then every person can get volume mid
            if (cnt >= m)
            {

                // Then check for larger in the right half
                low = mid + 1;

                // Replace tbe answer with
                // current maximum i.e., mid
                maxVol = Math.Max(maxVol, mid);
            }

            // else traverse in the left half
            else
            {
                high = mid - 1;
            }
        }

        return maxVol;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []a = {1, 1, 1, 2, 2};
        int n = a.Length;
        int m = 3;

        Console.WriteLine(getMaximumVloume(a, n, m));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement the above approach

// Function to get the maximum volume that
// every person can get
function getMaximumVloume($a, $n, $m)
{
    $maxVolume = 0;

    // Convert the length to respective volumes
    // and find the maximum volumes
    for ($i = 0; $i < $n; $i++)
    {
        $a[$i] = $a[$i] * $a[$i] * $a[$i];

        $maxVolume = max($a[$i], $maxVolume);
    }

    // Apply binary search with initial
    // low as 0 and high as the maximum most
    $low = 0; $high = $maxVolume;

    // Initial answer is 0 slices
    $maxVol = 0;

    // Apply binary search
    while ($low <= $high)
    {

        // Get the mid element
        $mid = ($low + $high) >> 1;

        // Count the slices of volume mid
        $cnt = 0;
        for ($i = 0; $i < $n; $i++)
        {
            $cnt += (int)($a[$i] / $mid);
        }

        // If the slices of volume
        // exceeds the number of persons
        // then every person can get volume mid
        if ($cnt >= $m)
        {

            // Then check for larger in the right half
            $low = $mid + 1;

            // Replace tbe answer with
            // current maximum i.e., mid
            $maxVol = max($maxVol, $mid);
        }

        // else traverse in the left half
        else
            $high = $mid - 1;
    }

    return $maxVol;
}

// Driver code
$a = array(1, 1, 1, 2, 2);
$n = sizeof($a);
$m = 3;

echo getMaximumVloume($a, $n, $m);

// This code is contributed by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// javascript program to implement the above approach    
// Function to get the maximum volume that
    // every person can get
    function getMaximumVloume(a , n , m) {
        var maxVolume = 0;

        // Convert the length to respective volumes
        // and find the maximum volumes
        for (i = 0; i < n; i++) {
            a[i] = a[i] * a[i] * a[i];

            maxVolume = Math.max(a[i], maxVolume);
        }

        // Apply binary search with initial
        // low as 0 and high as the maximum most
        var low = 0, high = maxVolume;

        // Initial answer is 0 slices
        var maxVol = 0;

        // Apply binary search
        while (low <= high) {

            // Get the mid element
            var mid = (low + high) >> 1;

            // Count the slices of volume mid
            var cnt = 0;
            for (i = 0; i < n; i++) {
                cnt += parseInt(a[i] / mid);
            }

            // If the slices of volume
            // exceeds the number of persons
            // then every person can get volume mid
            if (cnt >= m) {

                // Then check for larger in the right half
                low = mid + 1;

                // Replace tbe answer with
                // current maximum i.e., mid
                maxVol = Math.max(maxVol, mid);
            }

            // else traverse in the left half
            else {
                high = mid - 1;
            }
        }

        return maxVol;
    }

    // Driver code

        var a = [ 1, 1, 1, 2, 2 ];
        var n = a.length;
        var m = 3;

        document.write(getMaximumVloume(a, n, m));

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(N * log (maxVolume))