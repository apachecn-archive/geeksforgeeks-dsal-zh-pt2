# 总和等于给定数 N 的最小立方体数

> 原文:[https://www . geesforgeks . org/最小立方数-其和等于给定数-n/](https://www.geeksforgeeks.org/minimum-number-of-cubes-whose-sum-equals-to-given-number-n/)

给定一个整数 **n** ，任务是找到最小数量的立方体，其和等于 **N** 。
**例:**

> **输入:** N = 496
> **输出:**3
> 4<sup>3</sup>+6<sup>3</sup>+6<sup>3</sup>= 496
> 注意 1<sup>3</sup>+3<sup>3</sup>+5<sup>3</sup>+7<sup>3</sup>= 496 但需要 4 个立方体。
> **输入:** N = 15
> **输出:** 8

**天真的方法:**编写一个递归方法，将每个小于 **N** 的完美立方体作为求和的一部分，然后对剩余求和所需的立方体数量进行递归**N–X**。这个解的时间复杂度是指数级的。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the minimum
// number of cubes whose sum is k
int MinOfCubed(int k)
{
    // If k is less than the 2^3
    if (k < 8)
        return k;

    // Initialize with the maximum
    // number of cubes required
    int res = k;
    for (int i = 1; i <= k; i++) {
        if ((i * i * i) > k)
            return res;
        res = min(res, MinOfCubed(k - (i * i * i)) + 1);
    }
    return res;
}

// Driver code
int main()
{
    int num = 15;
    cout << MinOfCubed(num);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the minimum
    // number of cubes whose sum is k
    static int MinOfCubed(int k)
    {
        // If k is less than the 2^3
        if (k < 8)
            return k;

        // Initialize with the maximum
        // number of cubes required
        int res = k;
        for (int i = 1; i <= k; i++) {
            if ((i * i * i) > k)
                return res;
            res = Math.min(res, MinOfCubed(k - (i * i * i)) + 1);
        }
        return res;
    }

    // Driver code
    public static void main(String[] args)
    {
        int num = 15;
        System.out.println(MinOfCubed(num));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum
# number of cubes whose sum is k
def MinOfCubed(k):

    # If k is less than the 2 ^ 3
    if (k < 8):
        return k;

    # Initialize with the maximum
    # number of cubes required
    res = k;
    for i in range(1, k + 1):
        if ((i * i * i) > k):
            return res;
        res = min(res, MinOfCubed(k - (i * i * i)) + 1);
    return res;

# Driver code
num = 15;
print(MinOfCubed(num));

# This code contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function to return the minimum
    // number of cubes whose sum is k
    static int MinOfCubed(int k)
    {
        // If k is less than the 2^3
        if (k < 8)
            return k;

        // Initialize with the maximum
        // number of cubes required
        int res = k;
        for (int i = 1; i <= k; i++) {
            if ((i * i * i) > k)
                return res;
            res = Math.Min(res, MinOfCubed(k - (i * i * i)) + 1);
        }
        return res;
    }

    // Driver code
    static public void Main()
    {
        int num = 15;
        Console.WriteLine(MinOfCubed(num));
    }
}

// This code has been contributed by ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the minimum
// number of cubes whose sum is k
function MinOfCubed($k)
{
    // If k is less than the 2^3
    if ($k < 8)
        return $k;

    // Initialize with the maximum
    // number of cubes required
    $res = $k;
    for ($i = 1; $i <= $k; $i++)
    {
        if (($i * $i * $i) > $k)
            return $res;
        $res = min($res, MinOfCubed($k - ($i *$i * $i)) + 1);
    }
    return $res;
}

    // Driver code
    $num = 15;
    echo MinOfCubed($num);

    // This code is contributed by Ryuga

?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the minimum
    // number of cubes whose sum is k
    function MinOfCubed(k)
    {
        // If k is less than the 2^3
        if (k < 8)
            return k;

        // Initialize with the maximum
        // number of cubes required
        let res = k;
        for (let i = 1; i <= k; i++) {
            if ((i * i * i) > k)
                return res;
            res = Math.min(res, MinOfCubed(k - (i * i * i)) + 1);
        }
        return res;
    }

    let num = 15;
      document.write(MinOfCubed(num));

</script>
```

**Output:** 

```
8
```

**高效的方法:**如果我们为上面的解画出完整的递归树，我们可以看到很多子问题被一次又一次地解决，所以我们可以看到这个问题具有重叠子问题的性质。这引导我们使用动态编程范式来解决问题。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum
// number of cubes whose sum is k
int MinOfCubedDP(int k)
{
    vector<int> DP(k+1);
    int j = 1, t = 1;
    DP[0] = 0;
    for (int i = 1; i <= k; i++) {
        DP[i] = INT_MAX;

        // While current perfect cube
        // is less than current element
        while (j <= i) {

            // If i is a perfect cube
            if (j == i)
                DP[i] = 1;

            // i = (i - 1) + 1^3
            else if (DP[i] > DP[i - j])
                DP[i] = DP[i - j] + 1;

            // Next perfect cube
            t++;
            j = t * t * t;
        }

        // Re-initialization for next element
        t = j = 1;
    }
    return DP[k];
}

// Driver code
int main()
{
    int num = 15;
    cout << MinOfCubedDP(num);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the minimum
    // number of cubes whose sum is k
    static int MinOfCubedDP(int k)
    {
        int[] DP = new int[k + 1];
        int j = 1, t = 1;
        DP[0] = 0;
        for (int i = 1; i <= k; i++) {
            DP[i] = Integer.MAX_VALUE;

            // While current perfect cube
            // is less than current element
            while (j <= i) {

                // If i is a perfect cube
                if (j == i)
                    DP[i] = 1;

                // i = (i - 1) + 1^3
                else if (DP[i] > DP[i - j])
                    DP[i] = DP[i - j] + 1;

                // Next perfect cube
                t++;
                j = t * t * t;
            }

            // Re-initialization for next element
            t = j = 1;
        }
        return DP[k];
    }

    // Driver code
    public static void main(String[] args)
    {
        int num = 15;
        System.out.println(MinOfCubedDP(num));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python implementation of the approach
import sys

# Function to return the minimum
# number of cubes whose sum is k
def MinOfCubedDP(k):
    DP = [0] * (k + 1);
    j = 1;
    t = 1;
    DP[0] = 0;
    for i in range(1, k + 1):
        DP[i] = sys.maxsize;

        # While current perfect cube
        # is less than current element
        while (j <= i):

            # If i is a perfect cube
            if (j == i):
                DP[i] = 1;

            # i = (i - 1) + 1^3
            elif (DP[i] > DP[i - j]):
                DP[i] = DP[i - j] + 1;

            # Next perfect cube
            t += 1;
            j = t * t * t;

        # Re-initialization for next element
        t = j = 1;
    return DP[k];

# Driver code
num = 15;
print(MinOfCubedDP(num));

# This code contributed by Rajput-Ji
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function to return the minimum
    // number of cubes whose sum is k
    static int MinOfCubedDP(int k)
    {
        int[] DP = new int[k + 1];
        int j = 1, t = 1;
        DP[0] = 0;
        for (int i = 1; i <= k; i++) {
            DP[i] = int.MaxValue;

            // While current perfect cube
            // is less than current element
            while (j <= i) {

                // If i is a perfect cube
                if (j == i)
                    DP[i] = 1;

                // i = (i - 1) + 1^3
                else if (DP[i] > DP[i - j])
                    DP[i] = DP[i - j] + 1;

                // Next perfect cube
                t++;
                j = t * t * t;
            }

            // Re-initialization for next element
            t = j = 1;
        }
        return DP[k];
    }

    // Driver code
    public static void Main()
    {
        int num = 15;
        Console.WriteLine(MinOfCubedDP(num));
    }
}

/* This code contributed by Code_Mech */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the minimum
// number of cubes whose sum is k
function MinOfCubedDP($k)
{
    $DP = array($k + 1);
    $j = 1; $t = 1;
    $DP[0] = 0;
    for ($i = 1; $i <= $k; $i++)
    {
        $DP[$i] = PHP_INT_MAX;

        // While current perfect cube
        // is less than current element
        while ($j <= $i)
        {

            // If i is a perfect cube
            if ($j == $i)
                $DP[$i] = 1;

            // i = (i - 1) + 1^3
            else if ($DP[$i] > $DP[$i - $j])
                $DP[$i] = $DP[$i - $j] + 1;

            // Next perfect cube
            $t++;
            $j = $t * $t * $t;
        }

        // Re-initialization for next element
        $t = $j = 1;
    }
    return $DP[$k];
}

// Driver code
$num = 15;
echo(MinOfCubedDP($num));

// This code contributed by Code_Mech
?>
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Function to return the minimum
    // number of cubes whose sum is k
    function MinOfCubedDP(k)
    {
        let DP = new Array(k + 1);
        DP.fill(0);
        let j = 1, t = 1;
        DP[0] = 0;
        for (let i = 1; i <= k; i++) {
            DP[i] = Number.MAX_VALUE;

            // While current perfect cube
            // is less than current element
            while (j <= i) {

                // If i is a perfect cube
                if (j == i)
                    DP[i] = 1;

                // i = (i - 1) + 1^3
                else if (DP[i] > DP[i - j])
                    DP[i] = DP[i - j] + 1;

                // Next perfect cube
                t++;
                j = t * t * t;
            }

            // Re-initialization for next element
            t = j = 1;
        }
        return DP[k];
    }

    let num = 15;
    document.write(MinOfCubedDP(num));

</script>
```

**Output:** 

```
8
```

乍一看，该算法似乎在多项式时间内工作，因为我们有两个嵌套循环，外部循环采用 O(n)，内部循环采用 O(n^(1/3)).所以整个算法采用 O(n*n^(1/3)).但是复杂度作为输入长度的函数是什么呢？要表示 n 大小的数字，我们需要 m = log(n)–(基数为 2 的对数)位。在这种情况下，n=2^m.如果我们在公式 O(n*n^(1/3)中将 2^m 设置为 n，我们看到时间复杂度仍然是指数的。这种算法被称为伪多项式。