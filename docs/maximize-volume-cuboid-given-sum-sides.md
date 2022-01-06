# 给定边数和的长方体体积最大化

> 原文:[https://www . geesforgeks . org/maximum-volume-长方体-给定-和-sides/](https://www.geeksforgeeks.org/maximize-volume-cuboid-given-sum-sides/)

给我们一个长方体的长度**，宽度**和高度**之和，比如说 S。任务是找到能达到的最大体积，使边的总和为 S.
长方体的体积=长*宽*高
**例:**** 

```
Input : s  = 4
Output : 2
Only possible dimensions are some combination of 1, 1, 2.

Input : s = 8
Output : 18
All possible edge dimensions:
[1, 1, 6], volume = 6
[1, 2, 5], volume = 10
[1, 3, 4], volume = 12
[2, 2, 4], volume = 16
[2, 3, 3], volume = 18
```

**方法一:(蛮力)**
跑三个嵌套的思路，一个为长，一个为宽，一个为高。对于每次迭代，计算体积并与最大体积进行比较。
以下是本办法的实施:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Return the maximum volume.
int maxvolume(int s)
{
    int maxvalue = 0;

    // for length
    for (int i = 1; i <= s - 2; i++) {

        // for breadth
        for (int j = 1; j <= s - 1; j++) {

            // for height
            int k = s - i - j;

            // calculating maximum volume.
            maxvalue = max(maxvalue, i * j * k);
        }
    }

    return maxvalue;
}

// Driven Program
int main()
{
    int s = 8;
    cout << maxvolume(s) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to Maximize volume of
// cuboid with given sum of sides

class GFG
{

    // Return the maximum volume.
    static int maxvolume(int s)
    {
        int maxvalue = 0;

        // for length
        for (int i = 1; i <= s - 2; i++)
        {

            // for breadth
            for (int j = 1; j <= s - 1; j++)
            {

                // for height
                int k = s - i - j;

                // calculating maximum volume.
                maxvalue = Math.max(maxvalue, i * j * k);
            }
        }

        return maxvalue;
    }
    // Driver function
    public static void main (String[] args)
    {
        int s = 8;
        System.out.println(maxvolume(s));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 code to Maximize volume of
# cuboid with given sum of sides

# Return the maximum volume.
def maxvolume (s):
    maxvalue = 0

    # for length
    i = 1
    for i in range(s - 1):
        j = 1

        # for breadth
        for j in range(s):

            # for height
            k = s - i - j

            # calculating maximum volume.
            maxvalue = max(maxvalue, i * j * k)

    return maxvalue

# Driven Program
s = 8
print(maxvolume(s))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# code to Maximize volume of
// cuboid with given sum of sides
using System;

class GFG
{

    // Return the maximum volume.
    static int maxvolume(int s)
    {
        int maxvalue = 0;

        // for length
        for (int i = 1; i <= s - 2; i++)
        {

            // for breadth
            for (int j = 1; j <= s - 1; j++)
            {

                // for height
                int k = s - i - j;

                // calculating maximum volume.
                maxvalue = Math.Max(maxvalue, i * j * k);
            }
        }

        return maxvalue;
    }

    // Driver function
    public static void Main ()
    {
        int s = 8;
        Console.WriteLine(maxvolume(s));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to Maximize volume of
// cuboid with given sum of sides

// Return the maximum volume.
function maxvolume( $s)
{
    $maxvalue = 0;

    // for length
    for ( $i = 1; $i <= $s - 2; $i++)
    {

        // for breadth
        for ( $j = 1; $j <= $s - 1; $j++)
        {

            // for height
            $k = $s - $i - $j;

            // calculating maximum volume.
            $maxvalue = max($maxvalue,
                            $i * $j * $k);
        }
    }

    return $maxvalue;
}

// Driver Code
$s = 8;
echo(maxvolume($s));

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>
// javascript code to Maximize volume of
// cuboid with given sum of sides

// Return the maximum volume.
function maxvolume( s)
{
    let maxvalue = 0;

    // for length
    for (let i = 1; i <= s - 2; i++)
    {

        // for breadth
        for (let j = 1; j <= s - 1; j++)
        {

            // for height
            let k = s - i - j;

            // calculating maximum volume.
            maxvalue = Math.max(maxvalue, i * j * k);
        }
    }
    return maxvalue;
}

// Driver code
    let s = 8;
   document.write(maxvolume(s));

    // This code is contributed by gauravrajput1
</script>
```

**输出:**

```
18
```

**时间复杂度:** O(n <sup>2</sup> )

**方法 2:(高效方法)**
思路是尽可能平均划分边。
因此，
长度=地板(s/3)
宽度=地板((s–地板(s/3))/2)=地板((s–地板(s/3)/2)
高度= s–长度–宽度= s–地板(s/3)–地板((s–地板(s/3))/2)
以下是该方法的实施:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Return the maximum volume.
int maxvolume(int s)
{
    // finding length
    int length = s / 3;

    s -= length;

    // finding breadth
    int breadth = s / 2;

    // finding height
    int height = s - breadth;

    return length * breadth * height;
}

// Driven Program
int main()
{
    int s = 8;
    cout << maxvolume(s) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to Maximize volume of
// cuboid with given sum of sides
import java.io.*;

class GFG
{
    // Return the maximum volume.
    static int maxvolume(int s)
    {
        // finding length
        int length = s / 3;

        s -= length;

        // finding breadth
        int breadth = s / 2;

        // finding height
        int height = s - breadth;

        return length * breadth * height;
    }

    // Driven Program
    public static void main (String[] args)
    {
        int s = 8;
        System.out.println ( maxvolume(s));

    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 code to Maximize volume of
# cuboid with given sum of sides

# Return the maximum volume.
def maxvolume( s ):

    # finding length
    length = int(s / 3)

    s -= length

    # finding breadth
    breadth = s / 2

    # finding height
    height = s - breadth

    return int(length * breadth * height)

# Driven Program
s = 8
print( maxvolume(s) )

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# code to Maximize volume of
// cuboid with given sum of sides
using System;

class GFG
{
    // Return the maximum volume.
    static int maxvolume(int s)
    {
        // finding length
        int length = s / 3;

        s -= length;

        // finding breadth
        int breadth = s / 2;

        // finding height
        int height = s - breadth;

        return length * breadth * height;
    }

    // Driven Program
    public static void Main ()
    {
        int s = 8;
        Console.WriteLine( maxvolume(s));

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Return the maximum volume.
function maxvolume($s)
{
    // finding length
    $length = (int)($s / 3);

    $s -= $length;

    // finding breadth
    $breadth = (int)($s / 2);

    // finding height
    $height = $s - $breadth;

    return $length * $breadth * $height;
}

// Driven Code
$s = 8;
echo(maxvolume($s));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Return the maximum volume.
function maxvolume( s)
{

    // finding length
    let length = parseInt(s / 3);
    s -= length;

    // finding breadth
    let breadth = parseInt(s / 2);

    // finding height
    let height = s - breadth;
    return length * breadth * height;
}

// Driven Program
let s = 8;
    document.write(maxvolume(s));

// This code is contributed by aashish1995

</script>
```

**输出:**

```
18
```

**时间复杂度:** O(1)
**这是怎么工作的？**

> 我们基本上需要最大化
> 三个数的乘积，x，y，z，其和是给定的。
> 给定 s = x + y + z
> 最大化 P = x * y * z
> = x * y *(s–x–y)
> = x * y * s–x * x * s–x * y–x * y
> 我们得到 DP/dx = sy–2xy–y * y
> 和 DP/dy = sx–2xy–x * x
> 当
> x = s/3，y = s/3 时，我们得到 dp/dx = 0 和 dp/dy = 0