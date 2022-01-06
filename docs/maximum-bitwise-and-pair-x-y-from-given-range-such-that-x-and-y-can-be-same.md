# 给定范围内的最大位“与”对(X，Y)，使得 X 和 Y 可以相同

> 原文:[https://www . geesforgeks . org/max-bitwise-and-pair-x-y-from-给定范围-so-x-and-y-可以相同/](https://www.geeksforgeeks.org/maximum-bitwise-and-pair-x-y-from-given-range-such-that-x-and-y-can-be-same/)

给定一个**范围【L，R】**，任务是找到一对(X，Y)**不一定是截然不同的**。找到所选整数的按位“与”的最大可能值。
**例:**

> **输入:** L = 3，R = 7
> **输出:** 7
> **解释:**
> 在所有可能的对中，对(7，7)给出了按位 AND 的最大值。
> **输入:** L = 54，R = 55
> **输出:** 55
> **解释:**
> 在所有可能的对中，对(55，55)给出了按位 AND 的最大值。

**朴素方法:**解决上述问题的朴素方法是从 L 到 R 进行迭代，并检查每个可能对的按位 and，最后打印最大值。
***时间复杂度:** O(N <sup>2</sup> )*
**高效方法:**
为了优化上述方法，我们必须观察到这里我们必须要有整数 L 和 R，我们必须从区间[L，R]中选择两个整数，这样它们的按位 and 应该是最大的。L 和 R 之间任意两个数字的按位“与”将始终仅小于或等于 R。所以如果我们必须从区间中选择两个整数，我们可以选择整数为 R，这是按位 and 最大化的唯一方法。
以下是上述方法的实施:

## C

```
// C implementation to find the
// Maximum Bitwise AND pair (X, Y)
// from given range such that
// X and Y can be same

#include <stdio.h>

// Function to return the
// maximum bitwise AND
int maximumAND(int L, int R)
{
    return R;
}

// Driver code
int main()
{
    int l = 3;
    int r = 7;

    printf("%d", maximumAND(l, r));

    return 0;
}
```

## C++

```
// C++ implementation to find the
// Maximum Bitwise AND pair (X, Y)
// from given range such that
// X and Y can be same

#include <bits/stdc++.h>
using namespace std;

// Function to return the
// maximum bitwise AND
int maximumAND(int L, int R)
{
    return R;
}

// Driver code
int main()
{
    int l = 3;
    int r = 7;

    cout << maximumAND(l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// Maximum Bitwise AND pair (X, Y)
// from given range such that
// X and Y can be same

class GFG {

    // Function to return the
    // maximum bitwise AND
    static int maximumAND(int L, int R)
    {
        return R;
    }

    // Driver code
    public static void main(String[] args)
    {
        int l = 3;
        int r = 7;
        System.out.print(maximumAND(l, r));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation to find the
# Maximum Bitwise AND pair (X, Y)
# from given range such that
# X and Y can be same

# Function to return the
# maximum bitwise AND
def maximumAND(L, R):
    return R

# Driver code
if __name__ == '__main__':
    l = 3
    r = 7
    print(maximumAND(l, r))
```

## C#

```
// C# implementation to find the
// maximum Bitwise AND pair (X, Y)
// from given range such that
// X and Y can be same
using System;

class GFG{

// Function to return the
// maximum bitwise AND
static int maximumAND(int L, int R)
{
    return R;
}

// Driver code
public static void Main(String[] args)
{
    int l = 3;
    int r = 7;

    Console.Write(maximumAND(l, r));
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// JavaScript implementation to find the
// Maximum Bitwise AND pair (X, Y)
// from given range such that
// X and Y can be same

// Function to return the
    // maximum bitwise AND
    function maximumAND(L, R)
    {
        return R;
    }

// Driver Code

        let l = 3;
        let r = 7;
        document.write(maximumAND(l, r));

</script>
```

**Output:** 

```
7
```

***时间复杂度:** O(1)*