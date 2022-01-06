# 清点需要的纸币数量

> 原文:[https://www . geeksforgeeks . org/count-所需纸币数量/](https://www.geeksforgeeks.org/count-the-number-of-currency-notes-needed/)

你有无限量的钞票价值 **A** 和 **B** 美元 **(A 不等于 B)** 。您想使用精确的 **N** 纸币支付总共 **S** 美元。任务是找到你需要的价值 **A** 美元的纸币数量。如果没有解决方案返回 **-1** 。

**示例:**

> **输入:** A = 1，B = 2，S = 7，N = 5
> **输出:** 3
> 3 * A + 2 * B = S
> 3 * 1 + 2 * 2 = 7
> 
> **输入:** A = 2，B = 1，S = 7，N = 5
> T3】输出: 2
> 
> **输入:** A = 2，B = 1，S = 4，N = 5
> **输出:** -1
> 
> **输入:** A = 2，B = 3，S = 20，N = 8
> T3】输出: 4

**方法:**让 **x** 为所需的有价票据数量 **A** ，则其余票据即**N–x**必须为有价票据 **B** 。由于要求它们的总和为 **S** ，因此必须满足以下等式:

> S =(A * x)+(B *(N–x))
> 进一步求解方程，
> S =(A * x)+(B * N)–(B * x)
> S–(B * N)=(A–B)* x
> **x =(S–(B * N))/(A–B)**
> 求解 **x** 后，只有当
> 的

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the amount of notes
// with value A required
int bankNotes(int A, int B, int S, int N)
{
    int numerator = S - (B * N);
    int denominator = A - B;

    // If possible
    if (numerator % denominator == 0)
        return (numerator / denominator);
    return -1;
}

// Driver code
int main()
{
    int A = 1, B = 2, S = 7, N = 5;
    cout << bankNotes(A, B, S, N) << endl;
}

// This code is contributed by mits
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the amount of notes
    // with value A required
    static int bankNotes(int A, int B, int S, int N)
    {
        int numerator = S - (B * N);
        int denominator = A - B;

        // If possible
        if (numerator % denominator == 0)
            return (numerator / denominator);
        return -1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int A = 1, B = 2, S = 7, N = 5;
        System.out.print(bankNotes(A, B, S, N));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the amount of notes
# with value A required
def bankNotes(A, B, S, N):

    numerator = S - (B * N)
    denominator = A - B

    # If possible
    if (numerator % denominator == 0):
        return (numerator // denominator)
    return -1

# Driver code
A, B, S, N = 1, 2, 7, 5
print(bankNotes(A, B, S, N))

# This code is contributed
# by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the amount of notes
    // with value A required
    static int bankNotes(int A, int B,
                         int S, int N)
    {
        int numerator = S - (B * N);
        int denominator = A - B;

        // If possible
        if (numerator % denominator == 0)
            return (numerator / denominator);
        return -1;
    }

    // Driver code
    public static void Main()
    {
        int A = 1, B = 2, S = 7, N = 5;
        Console.Write(bankNotes(A, B, S, N));
    }
}

// This code is contributed by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the amount of notes
// with value A required
function bankNotes($A, $B, $S, $N)
{
    $numerator = $S - ($B * $N);
    $denominator = $A - $B;

    // If possible
    if ($numerator % $denominator == 0)
        return ($numerator / $denominator);
    return -1;
}

// Driver code
$A = 1; $B= 2; $S = 7; $N = 5;
echo(bankNotes($A, $B, $S, $N));

// This code is contributed by Code_Mech
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the amount of notes
// with value A required
function bankNotes(A, B, S, N)
{
    let numerator = S - (B * N);
    let denominator = A - B;

    // If possible
    if (numerator % denominator == 0)
        return (Math.floor(numerator /
                           denominator));
    return -1;
}

// Driver Code
let A = 1, B = 2, S = 7, N = 5;

document.write(bankNotes(A, B, S, N) + "</br>");

// This code is contributed by jana_sayantan

</script>
```

**Output:** 

```
3
```