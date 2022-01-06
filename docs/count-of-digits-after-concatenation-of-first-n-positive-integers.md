# 前 N 个正整数串联后的位数

> 原文:[https://www . geesforgeks . org/前 n 个正整数串联后的位数/](https://www.geeksforgeeks.org/count-of-digits-after-concatenation-of-first-n-positive-integers/)

给定一个正整数 **N** ，任务是找出前 N 个正整数串联的总位数。
**例:**

> **输入:** N = 10
> **输出:** 11
> 说明:
> 形成的数字是 12345678910。
> 因此，总位数= 11
> **输入:** N = 20
> **输出:** 31
> **解释:**
> 形成的数字为 1234567891011121314151617181920
> 因此，总位数= 31

**方法:**我们用例子来观察一下。

*   设 N = 13。所以，在 1 到 13 之间的所有数字中，出现在某个位置的数字是 1，2，3，4，5，6，7，8，9，0，1，2，3。
*   同样，十位数是 1，1，1，1。
*   所以，1 到 13 的总位数是 13(13–0)。
*   同样，总的十位数是 4(13–9)。
*   现在，让我们看另一个数字来理解这个模式。设 N = 234。所以，单位处的数字是 1(24 次)、2(24 次)、3(24 次)、4(24 次)、5(23 次)、6(23 次)、7(23 次)、8(23 次)、9(23 次)、0(23 次)。因此，23 * 6 + 24 * 4 = 234。
*   同样，十位数是 234–9 = 225，因为从 1 到 234，只有 1–9 是一位数。
*   最后，第一百位的位数是 234–99 = 225，因为从 1 到 234，只有 1–9 是一位数，1–99 是两位数。
*   因此，串联时形成的总位数是 234(234–1+1)+225(234–10+1)+135(234–100+1)= 594。
*   因此，想法是减去 0，9，99，999 …从 N 开始，得到每个地方的位数，所有这些的总和就是需要的答案。

以下是上述方法的实现:

## C++

```
// C++ program to find the number of
// digits after concatenating the
// first N positive integers

#include <iostream>
#include <math.h>
using namespace std;

// Function to find the number of
// digits after concatenating the
// first N positive integers
void numberOfDigits(int N)
{
    int nod = floor(log10(N) + 1);
    int toDecrease
        = (pow(10, nod) - 1) / 9;
    cout << (N + 1) * nod - toDecrease
         << endl;
}

// Driver code
int main()
{
    int N = 13;
    numberOfDigits(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number of
// digits after concatenating the
// first N positive integers
class GFG{

// Function to find the number of
// digits after concatenating the
// first N positive integers
static void numberOfDigits(int N)
{
    int nod = (int)Math.floor(Math.log10(N) + 1);
    int toDecrease = (int)(Math.pow(10, nod) - 1) / 9;

    System.out.print((N + 1) * nod - toDecrease);
}

// Driver code
public static void main(String[] args)
{
    int N = 13;
    numberOfDigits(N);
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 program to find the number
# of digits after concatenating the
# first N positive integers
from math import log10, floor

# Function to find the number of
# digits after concatenating the
# first N positive integers
def numberOfDigits(N):

    nod = floor(log10(N) + 1);
    toDecrease = (pow(10, nod) - 1) // 9

    print((N + 1) * nod - toDecrease)

# Driver code
if __name__ == '__main__':

    N = 13

    numberOfDigits(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find the number of
// digits after concatenating the
// first N positive integers
using System;
class GFG{

// Function to find the number of
// digits after concatenating the
// first N positive integers
static void numberOfDigits(int N)
{
    int nod = (int)Math.Floor(Math.Log10(N) + 1);
    int toDecrease = (int)(Math.Pow(10, nod) - 1) / 9;

    Console.Write((N + 1) * nod - toDecrease);
}

// Driver code
public static void Main()
{
    int N = 13;
    numberOfDigits(N);
}
}

// This code is contributed by Nidhi_Biet
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the number of
// digits after concatenating the
// first N positive integers
function numberOfDigits(N)
{
    let nod = Math.floor(Math.log10(N) + 1);
    let toDecrease = (Math.pow(10, nod) - 1) / 9;

    document.write((N + 1) * nod - toDecrease);
}

// Driver code

    let N = 13;
    numberOfDigits(N);

 // This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
17
```

***时间复杂度:**O(log<sub>10</sub>N)*
***辅助空间:** O(1)*