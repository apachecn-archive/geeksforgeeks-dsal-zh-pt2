# 可以包含给定点的最大线段数

> 原文:[https://www . geeksforgeeks . org/最多可包含给定点数的段数/](https://www.geeksforgeeks.org/maximum-number-of-segments-that-can-contain-the-given-points/)

给定一个包含 **N** 整数和两个整数 **X** 和 **Y** 的数组 **arr[]** 。考虑 **N** 条线段，其中每条线段的起点和终点分别为**arr[I]–X**和 **arr[i] + Y** 。
给定另一个数组 **b[]** 的 **M** 点。任务是将这些点分配给线段，以使已分配给点的线段数最大。请注意，一个点最多可以分配给 1 个线段。
**例:**

> **输入:** arr[] = {1，5}，b = {1，1，2}，X = 1，Y = 4
> **输出:** 1
> 线段为【1-X，1+Y】，【5-X，5+Y】即【0，5】和【4，9】
> 点 1 可以分配给第一段【0，5】
> 点不能分配给第二段。
> So 2 也可以分配给第一个段，但不会最大化段的数量。
> 所以答案是 1。
> **输入:** arr[] = {1，2，3，4}，b = {1，3，5}，X = 0，Y = 0
> **输出:** 2

**方法:**对两个输入数组进行排序。现在，对于每个片段，我们尝试为其分配第一个可能的未分配点。如果当前线段在当前点之前结束，这意味着我们无法为其指定任何点，因为它前面的所有点都大于当前点，并且线段已经结束。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum number of segments
int countPoints(int n, int m, vector<int> a,
                vector<int> b, int x, int y)
{
    // Sort both the vectors
    sort(a.begin(), a.end());
    sort(b.begin(), b.end());

    // Initially pointing to the first element of b[]
    int j = 0;
    int count = 0;
    for (int i = 0; i < n; i++) {

        // Try to find a match in b[]
        while (j < m) {

            // The segment ends before b[j]
            if (a[i] + y < b[j])
                break;

            // The point lies within the segment
            if (b[j] >= a[i] - x && b[j] <= a[i] + y) {
                count++;
                j++;
                break;
            }

            // The segment starts after b[j]
            else
                j++;
        }
    }

    // Return the required count
    return count;
}

// Driver code
int main()
{
    int x = 1, y = 4;
    vector<int> a = { 1, 5 };
    int n = a.size();
    vector<int> b = { 1, 1, 2 };
    int m = a.size();
    cout << countPoints(n, m, a, b, x, y);

   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the
// maximum number of segments
static int countPoints(int n, int m, int a[],
                        int[] b, int x, int y)
{
    // Sort both the vectors
    Arrays.sort(a);
    Arrays.sort(b);

    // Initially pointing to the first element of b[]
    int j = 0;
    int count = 0;
    for (int i = 0; i < n; i++)
    {

        // Try to find a match in b[]
        while (j < m)
        {

            // The segment ends before b[j]
            if (a[i] + y < b[j])
                break;

            // The point lies within the segment
            if (b[j] >= a[i] - x && b[j] <= a[i] + y)
            {
                count++;
                j++;
                break;
            }

            // The segment starts after b[j]
            else
                j++;
        }
    }

    // Return the required count
    return count;
}

// Driver code
public static void main(String args[])
{
    int x = 1, y = 4;
    int[] a = { 1, 5 };
    int n = a.length;
    int[] b = { 1, 1, 2 };
    int m = a.length;
    System.out.println(countPoints(n, m, a, b, x, y));
}
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum
# number of segments
def countPoints(n, m, a, b, x, y):

    # Sort both the vectors
    a.sort()
    b.sort()

    # Initially pointing to the first
    # element of b[]
    j, count = 0, 0
    for i in range(0, n):

        # Try to find a match in b[]
        while j < m:

            # The segment ends before b[j]
            if a[i] + y < b[j]:
                break

            # The point lies within the segment
            if (b[j] >= a[i] - x and
                b[j] <= a[i] + y):
                count += 1
                j += 1
                break

            # The segment starts after b[j]
            else:
                j += 1

    # Return the required count
    return count

# Driver code
if __name__ == "__main__":

    x, y = 1, 4
    a = [1, 5]
    n = len(a)
    b = [1, 1, 2]
    m = len(b)
    print(countPoints(n, m, a, b, x, y))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the
    // maximum number of segments
    static int countPoints(int n, int m, int []a,
                            int []b, int x, int y)
    {
        // Sort both the vectors
        Array.Sort(a);
        Array.Sort(b);

        // Initially pointing to the
        // first element of b[]
        int j = 0;
        int count = 0;
        for (int i = 0; i < n; i++)
        {

            // Try to find a match in b[]
            while (j < m)
            {

                // The segment ends before b[j]
                if (a[i] + y < b[j])
                    break;

                // The point lies within the segment
                if (b[j] >= a[i] - x && b[j] <= a[i] + y)
                {
                    count++;
                    j++;
                    break;
                }

                // The segment starts after b[j]
                else
                    j++;
            }
        }

        // Return the required count
        return count;
    }

    // Driver code
    public static void Main()
    {
        int x = 1, y = 4;
        int[] a = {1, 5};
        int n = a.Length;
        int[] b = {1, 1, 2};
        int m = a.Length;
        Console.WriteLine(countPoints(n, m, a, b, x, y));
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the maximum number of segments
function countPoints($n, $m, $a, $b, $x, $y)
{
    // Sort both the vectors
    sort($a);
    sort($b);

    // Initially pointing to the first element of b[]
    $j = 0;
    $count = 0;
    for ($i = 0; $i < $n; $i++)
    {

        // Try to find a match in b[]
        while ($j < $m)
        {

            // The segment ends before b[j]
            if ($a[$i] + $y < $b[$j])
                break;

            // The point lies within the segment
            if ($b[$j] >= $a[$i] - $x &&
                $b[$j] <= $a[$i] + $y)
            {
                $count++;
                $j++;
                break;
            }

            // The segment starts after b[j]
            else
                $j++;
        }
    }

    // Return the required count
    return $count;
}

    // Driver code
    $x = 1;
    $y = 4;
    $a = array( 1, 5 );
    $n = count($a);
    $b = array( 1, 1, 2 );
    $m = count($b);
    echo countPoints($n, $m, $a, $b, $x, $y);

// This code is contributed by Arnab Kundu
?>
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Function to return the
    // maximum number of segments
    function countPoints(n, m, a, b, x, y)
    {
        // Sort both the vectors
        a.sort(function(a, b){return a - b});
        b.sort(function(a, b){return a - b});

        // Initially pointing to the
        // first element of b[]
        let j = 0;
        let count = 0;
        for (let i = 0; i < n; i++)
        {

            // Try to find a match in b[]
            while (j < m)
            {

                // The segment ends before b[j]
                if (a[i] + y < b[j])
                    break;

                // The point lies within the segment
                if (b[j] >= a[i] - x && b[j] <= a[i] + y)
                {
                    count++;
                    j++;
                    break;
                }

                // The segment starts after b[j]
                else
                    j++;
            }
        }

        // Return the required count
        return count;
    }

    let x = 1, y = 4;
    let a = [1, 5];
    let n = a.length;
    let b = [1, 1, 2];
    let m = a.length;
    document.write(countPoints(n, m, a, b, x, y));

</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(N * log(N))
**辅助空间:** O(1)