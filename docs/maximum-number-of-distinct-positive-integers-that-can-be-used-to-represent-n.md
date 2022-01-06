# 可用于表示 N 的不同正整数的最大数量

> 原文:[https://www . geesforgeks . org/可用于表示 n 的最大非重复正整数数/](https://www.geeksforgeeks.org/maximum-number-of-distinct-positive-integers-that-can-be-used-to-represent-n/)

给定一个整数 **N** ，任务是找出可以用来表示 **N** 的不同正整数的最大个数。

**示例:**

> **输入:** N = 5
> **输出:** 2
> 5 可以表示为 1 + 4、2 + 3、3 + 2、4 + 1 和 5。
> 所以在表示中可以使用的最大整数是 2。
> 
> **输入:**N = 10
> T3】输出: 4

**方法:**我们总是可以贪婪地选择不同的整数尽可能小，以最大化可以使用的不同整数的数量。如果我们使用前 x 个自然数，让它们的和为 f(x)。
所以我们需要找到一个最大值 x，这样 f(x) < = n。

> 1+2+3+…n< = n 
> x *(x+1)/2<= n
> x^2+x-2n<= 0
> 我们可以用二次公式 X = (-1 + sqrt(1+8*n))/2 求解上述方程。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the required count
int count(int n)
{
    return int((-1 + sqrt(1 + 8 * n)) / 2);
}

// Driver code
int main()
{
    int n = 10;

    cout << count(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    // Function to return the required count
    static int count(int n)
    {
        return (int)(-1 + Math.sqrt(1 + 8 * n)) / 2;

    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 10;

        System.out.println(count(n));
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import sqrt

# Function to return the required count
def count(n) :

    return (-1 + sqrt(1 + 8 * n)) // 2;

# Driver code
if __name__ == "__main__" :

    n = 10;

    print(count(n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of approach
using System;

class GFG
{

    // Function to return the required count
    public static int count(int n)
    {
        return (-1 + (int)Math.Sqrt(1 + 8 * n)) / 2;
    }

    // Driver Code
    public static void Main()
    {
        int n = 10;

        Console.Write(count(n));
    }
}

// This code is contributed by Mohit Kumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the required count
function count(n)
{
    return parseInt((-1 + Math.sqrt(1 + 8 * n)) / 2);
}

// Driver code
var n = 10;

document.write(count(n));

// This code is contributed by rutvik_56

</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(1)