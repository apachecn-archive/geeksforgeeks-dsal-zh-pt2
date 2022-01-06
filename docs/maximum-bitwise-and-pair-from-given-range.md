# 给定范围内的最大位“与”对

> 原文:[https://www . geeksforgeeks . org/给定范围的最大位对/](https://www.geeksforgeeks.org/maximum-bitwise-and-pair-from-given-range/)

给定范围**【L，R】**，任务是找到一对 **(X，Y)** 使得 **L ≤ X < Y ≤ R** 和 **X & Y** 在所有可能的对中最大，然后打印找到的对的位“与”。
**举例:**

> **输入:** L = 1，R = 9
> **输出:** 8
> 在所有可能的对中，对 **(8，9)** 给出了按位“与”的最大值。
> **输入:** L = 523641，R = 985624
> **输出:** 985622

**天真方法:**从 **L** 迭代到 **R** 并检查每个可能对的按位“与”，最后打印最大值。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum bitwise AND
// possible among all the possible pairs
int maxAND(int L, int R)
{
    int maximum = L & R;

    for (int i = L; i < R; i++)
        for (int j = i + 1; j <= R; j++)

            // Maximum among all (i, j) pairs
            maximum = max(maximum, (i & j));

    return maximum;
}

// Driver code
int main()
{
    int L = 1, R = 632;
    cout << maxAND(L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the maximum bitwise AND
// possible among all the possible pairs
static int maxAND(int L, int R)
{
    int maximum = L & R;

    for (int i = L; i < R; i++)
        for (int j = i + 1; j <= R; j++)

            // Maximum among all (i, j) pairs
            maximum = Math.max(maximum, (i & j));

    return maximum;
}

// Driver code
public static void main(String[] args)
{
    int L = 1, R = 632;
    System.out.println(maxAND(L, R));
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the maximum bitwise AND
# possible among all the possible pairs
def maxAND(L, R):
    maximum = L & R

    for i in range(L, R, 1):
        for j in range(i + 1, R + 1, 1):

            # Maximum among all (i, j) pairs
            maximum = max(maximum, (i & j))

    return maximum

# Driver code
if __name__ == '__main__':
    L = 1
    R = 632
    print(maxAND(L, R))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the maximum bitwise AND
// possible among all the possible pairs
static int maxAND(int L, int R)
{
    int maximum = L & R;

    for (int i = L; i < R; i++)
        for (int j = i + 1; j <= R; j++)

            // Maximum among all (i, j) pairs
            maximum = Math.Max(maximum, (i & j));

    return maximum;
}

// Driver code
public static void Main(String[] args)
{
    int L = 1, R = 632;
    Console.WriteLine(maxAND(L, R));
}
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the maximum bitwise AND
// possible among all the possible pairs
function maxAND($L, $R)
{
    $maximum = $L & $R;

    for ($i = $L; $i < $R; $i++)
        for ($j = $i + 1; $j <= $R; $j++)

            // Maximum among all (i, j) pairs
            $maximum = max($maximum, ($i & $j));

    return $maximum;
}

// Driver code
$L = 1; $R = 632;
echo(maxAND($L, $R));

// This code contributed by Code_Mech.
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the maximum bitwise AND
// possible among all the possible pairs
function maxAND(L, R)
{
    var maximum = L & R;

    for (var i = L; i < R; i++)
        for (var j = i + 1; j <= R; j++)

            // Maximum among all (i, j) pairs
            maximum = Math.max(maximum, (i & j));

    return maximum;
}

// Driver code
var L = 1, R = 632;
document.write( maxAND(L, R));

</script>
```

**Output:** 

```
630
```

**时间复杂度:** O(n <sup>2</sup> )
**有效途径:**如果我们仔细观察[L，R]范围，最大 AND 可能在(R)和(R–1)的 **AND 或(R–1)和(R–2)**的 **AND 之间。
以下是上述方法的实施:** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum bitwise AND
// possible among all the possible pairs
int maxAND(int L, int R)
{

    // If there is only a single value
    // in the range [L, R]
    if (L == R)
        return L;

    // If there are only two values
    // in the range [L, R]
    else if ((R - L) == 1)
        return (R & L);
    else {
        if (((R - 1) & R) > ((R - 2) & (R - 1)))
            return ((R - 1) & R);
        else
            return ((R - 2) & (R - 1));
    }
}

// Driver code
int main()
{
    int L = 1, R = 632;
    cout << maxAND(L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GfG
{

// Function to return the maximum bitwise AND
// possible among all the possible pairs
static int maxAND(int L, int R)
{

    // If there is only a single value
    // in the range [L, R]
    if (L == R)
        return L;

    // If there are only two values
    // in the range [L, R]
    else if ((R - L) == 1)
        return (R & L);
    else {
        if (((R - 1) & R) > ((R - 2) & (R - 1)))
            return ((R - 1) & R);
        else
            return ((R - 2) & (R - 1));
    }
}

// Driver code
public static void main(String[] args)
{
    int L = 1, R = 632;
    System.out.println(maxAND(L, R));
}
}

// This code is contributed by
// Prerna Saini
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum bitwise AND
# possible among all the possible pairs
def maxAND(L, R):

    # If there is only a single value
    # in the range [L, R]
    if (L == R):
        return L;

    # If there are only two values
    # in the range [L, R]
    elif ((R - L) == 1):
        return (R & L);
    else:
        if (((R - 1) & R) >
            ((R - 2) & (R - 1))):
            return ((R - 1) & R);
        else:
            return ((R - 2) & (R - 1));

# Driver code
L = 1;
R = 632;
print(maxAND(L, R));

# This code contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;

class GfG
{

    // Function to return the maximum bitwise AND
    // possible among all the possible pairs
    static int maxAND(int L, int R)
    {

        // If there is only a single value
        // in the range [L, R]
        if (L == R)
            return L;

        // If there are only two values
        // in the range [L, R]
        else if ((R - L) == 1)
            return (R & L);
        else
        {
            if (((R - 1) & R) > ((R - 2) & (R - 1)))
                return ((R - 1) & R);
            else
                return ((R - 2) & (R - 1));
        }
    }

    // Driver code
    public static void Main()
    {
        int L = 1, R = 632;
        Console.WriteLine(maxAND(L, R));
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the maximum bitwise AND
// possible among all the possible pairs
function maxAND($L, $R)
{

    // If there is only a single value
    // in the range [L, R]
    if ($L == $R)
        return $L;

    // If there are only two values
    // in the range [L, R]
    else if (($R - $L) == 1)
        return ($R & $L);
    else
    {
        if ((($R - 1) & $R) > (($R - 2) & ($R - 1)))
            return (($R - 1) & $R);
        else
            return (($R - 2) & ($R - 1));
    }
}

// Driver code
$L = 1;
$R = 632;
echo maxAND($L, $R);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Function to return the maximum bitwise AND
    // possible among all the possible pairs
    function maxAND(L, R)
    {

        // If there is only a single value
        // in the range [L, R]
        if (L == R)
            return L;

        // If there are only two values
        // in the range [L, R]
        else if ((R - L) == 1)
            return (R & L);
        else
        {
            if (((R - 1) & R) > ((R - 2) & (R - 1)))
                return ((R - 1) & R);
            else
                return ((R - 2) & (R - 1));
        }
    }

    let L = 1, R = 632;
      document.write(maxAND(L, R));

</script>
```

**Output:** 

```
630
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)