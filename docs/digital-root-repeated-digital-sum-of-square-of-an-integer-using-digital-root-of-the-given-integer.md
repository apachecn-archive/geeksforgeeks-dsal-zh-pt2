# 使用给定整数的数字根的整数平方的数字根(重复数字和)

> 原文:[https://www . geesforgeks . org/digital-root-repeated-digital-使用给定整数的数字根的整数平方和/](https://www.geeksforgeeks.org/digital-root-repeated-digital-sum-of-square-of-an-integer-using-digital-root-of-the-given-integer/)

给定一个整数 **N** ，任务是使用 **N** 的[数字根找到**N<sup>2</sup>T5。**](https://www.geeksforgeeks.org/digital-rootrepeated-digital-sum-given-integer/)

> [**正整数的数字根**](https://www.geeksforgeeks.org/digital-rootrepeated-digital-sum-given-integer/) 是通过将整数的数字相加计算出来的。如果结果值是个位数，那么这个位数就是数字根。如果结果值包含两位或两位以上的数字，则将这些数字相加，并重复该过程，直到获得一位数。

**示例:**

> **输入:** N = 15
> **输出:** 9
> **解释:**
> 15 <sup>2</sup> = 225，2+2+5 = 9
> 
> **输入:**N = 9
> T3】输出: 9

**途径:**思路是找到 **N** 的。现在我们可以通过观察以下几点，利用 **N** 的数字根找到 **N <sup>2</sup>** 的数字根:

*   如果 **N** 的数字根是 1 或 8，那么**N<sup>2</sup>T5】的数字根总是 1；**
*   如果 **N** 的数字根是 2 或 7，那么**N<sup>2</sup>T5】的数字根总是 4；**
*   如果 **N** 的数字根是 3 或 6 或 9，那么**N<sup>2</sup>T5】的数字根总是 9；**
*   如果 **N** 的数字根是 4 或 5，那么**N<sup>2</sup>T5】的数字根总是 7；**

下面是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the digital
// root of the number
int digitalRootofN(string num)
{
    // If num is 0
    if (num.compare("0") == 0)
        return 0;

    // Count sum of digits under mod 9
    int ans = 0;
    for (int i = 0; i < num.length(); i++)
        ans = (ans + num[i] - '0') % 9;

    // If digit sum is multiple of 9,
    // 9, else remainder with 9.
    return (ans == 0) ? 9 : ans % 9;
}

// Returns digital root of N * N
int digitalRootofNSquare(string N)
{
    // finding digital root of N
    int NDigRoot = digitalRootofN(N);

    if (NDigRoot == 1 || NDigRoot == 8)
        return 1;

    if (NDigRoot == 2 || NDigRoot == 7)
        return 4;

    if (NDigRoot == 3 || NDigRoot == 6)
        return 9;

    if (NDigRoot == 4 || NDigRoot == 5)
        return 7;
}

// Driver Code
int main()
{
    string num = "15";
    cout << digitalRootofNSquare(num);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
import java.io.*;

class GFG{

// Function to find the digital
// root of the number
static int digitalRootofN(String num)
{

    // If num is 0
    if (num.compareTo("0") == 0)
        return 0;

    // Count sum of digits under mod 9
    int ans = 0;
    for(int i = 0; i < num.length(); i++)
        ans = (ans + num.charAt(i) - '0') % 9;

    // If digit sum is multiple of 9,
    // 9, else remainder with 9.
    return (ans == 0) ? 9 : ans % 9;
}

// Returns digital root of N * N
static int digitalRootofNSquare(String N)
{

    // Finding digital root of N
    int NDigRoot = digitalRootofN(N);

    if (NDigRoot == 1 || NDigRoot == 8)
        return 1;

    else if (NDigRoot == 2 || NDigRoot == 7)
        return 4;

    else if (NDigRoot == 3 || NDigRoot == 6)
        return 9;
    else
        return 7;
}

// Driver Code
public static void main (String[] args)
{
    String num = "15";

    // Function call
    System.out.print(digitalRootofNSquare(num));
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to find the digital
# root of the number
def digitalRootofN(num):

    # If num is 0
    if (num == ("0")):
        return 0;

    # Count sum of digits
    # under mod 9
    ans = 0;
    for i in range(0, len(num)):
        ans = (ans + ord(num[i]) - ord('0')) % 9;

    # If digit sum is multiple of 9,
    # 9, else remainder with 9.
    return 9 if (ans == 0) else ans % 9;

# Returns digital root of N * N
def digitalRootofNSquare(N):

    # Finding digital root of N
    NDigRoot = digitalRootofN(N);
    if (NDigRoot == 1 or NDigRoot == 8):
        return 1;
    elif(NDigRoot == 2 or NDigRoot == 7):
        return 4;
    elif(NDigRoot == 3 or NDigRoot == 6):
        return 9;
    else:
        return 7;

# Driver Code
if __name__ == '__main__':

    num = "15";

    # Function call
    print(digitalRootofNSquare(num));

# This code is contributed by shikhasingrajput
```

## C#

```
// C# implementation of the
// above approach
using System;

class GFG{

// Function to find the digital
// root of the number
static int digitalRootofN(string num)
{

    // If num is 0
    if (num.CompareTo("0") == 0)
        return 0;

    // Count sum of digits under mod 9
    int ans = 0;
    for(int i = 0; i < num.Length; i++)
        ans = (ans + num[i] - '0') % 9;

    // If digit sum is multiple of 9,
    // 9, else remainder with 9.
    return (ans == 0) ? 9 : ans % 9;
}

// Returns digital root of N * N
static int digitalRootofNSquare(string N)
{

    // Finding digital root of N
    int NDigRoot = digitalRootofN(N);

    if (NDigRoot == 1 || NDigRoot == 8)
        return 1;

    else if (NDigRoot == 2 || NDigRoot == 7)
        return 4;

    else if (NDigRoot == 3 || NDigRoot == 6)
        return 9;

    else
        return 7;
}

// Driver Code
public static void Main ()
{
    string num = "15";

    // Function call
    Console.Write(digitalRootofNSquare(num));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// Javascript implementation of the
// above approach

// Function to find the digital
// root of the number
function digitalRootofN(num)
{
    // If num is 0
    if (num == "0")
        return 0;

    // Count sum of digits under mod 9
    var ans = 0;
    for (var i = 0; i < num.length; i++)
        ans = (ans + num[i] - '0') % 9;

    // If digit sum is multiple of 9,
    // 9, else remainder with 9.
    return (ans == 0) ? 9 : ans % 9;
}

// Returns digital root of N * N
function digitalRootofNSquare(N)
{
    // finding digital root of N
    var NDigRoot = digitalRootofN(N);

    if (NDigRoot == 1 || NDigRoot == 8)
        return 1;

    if (NDigRoot == 2 || NDigRoot == 7)
        return 4;

    if (NDigRoot == 3 || NDigRoot == 6)
        return 9;

    if (NDigRoot == 4 || NDigRoot == 5)
        return 7;
}

// Driver Code
var num = "15";
document.write( digitalRootofNSquare(num));

</script>
```

**Output:** 

```
9
```

**时间复杂度:***O(N)*
T5**辅助空间:** O(1)