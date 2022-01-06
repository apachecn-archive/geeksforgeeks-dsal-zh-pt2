# 三个数的等和异或

> 原文:[https://www . geeksforgeeks . org/三个数的等和异或/](https://www.geeksforgeeks.org/equal-sum-and-xor-of-three-numbers/)

给定一个整数 **N** 。任务是计算整数对 **A** 和 **B** 的数量，使得 **A + B + N = A ^ B ^ N** 和 a 与 b 小于 n。
T9】示例:

> **输入:**N = 2
> T3】输出: 3
> 解释:-
> 为 N = 2
> 2 XOR 0 XOR 0 = 2+0+0
> 2 XOR 0 XOR 1 = 2+0+1
> 2 XOR 0 XOR 2！= 2+0+2
> 2 异或 1 异或 0 = 2+1+0
> 2 异或 1 异或 1！= 2+1+1
> 2 异或 1 异或 2！= 2+1+2
> 2 异或 2 异或 0！= 2+2+0
> 2 异或 2 异或 1！= 2+2+1
> 2 异或 2 异或 2！= 2+2+2
> 所以(0，0)、(0，1)和(1，0)是必需的对。所以输出是 3。
> **输入:** N = 4
> **输出:** 9

**逼近** :
要使三个数的**和**等于三个数的**与给定数之一的**异或，我们可以做以下操作:-

1.  用二进制形式表示定数。
2.  遍历定数的二进制扩展。
    *   如果你找到一个 1，只有一个条件，也就是说，你把另外两个数字的二进制位作为 0 和 0。
    *   如果你找到一个 0，将有三个条件，即你可以有二进制位作为(0，0)，(1，0)
        或(0，1)。
3.  下面的三位组永远不会进位，所以它们是有效的。
4.  所以答案会是 **3^(** [**二进制表示中的零数**](https://www.geeksforgeeks.org/xor-counts-0s-1s-binary-representation/) **)** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Defining ull to unsigned long long int
typedef unsigned long long int ull;

// Function to calculate power of 3
ull calculate(int bit_cnt)
{
    ull res = 1;
    while (bit_cnt--) {
        res = res * 3;
    }

    return res;
}

// Function to return the count of the
// unset bit ( zeros )
int unset_bit_count(ull n)
{
    int count = 0;
    while (n) {

        // Check the bit is 0 or not
        if ((n & 1) == 0)
            count++;
        // Right shifting ( dividing by 2 )
        n = n >> 1;
    }
    return count;
}

// Driver Code
int main()
{
    ull n;
    n = 2;

    int count = unset_bit_count(n);

    ull ans = calculate(count);

    cout << ans << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to calculate power of 3
static long calculate(int bit_cnt)
{
    long res = 1;
    while (bit_cnt-- > 0)
    {
        res = res * 3;
    }

    return res;
}

// Function to return the count of the
// unset bit ( zeros )
static int unset_bit_count(long n)
{
    int count = 0;
    while (n > 0)
    {

        // Check the bit is 0 or not
        if ((n & 1) == 0)
            count++;

        // Right shifting ( dividing by 2 )
        n = n >> 1;
    }
    return count;
}

// Driver Code
public static void main(String[] args)
{
    long n;
    n = 2;

    int count = unset_bit_count(n);

    long ans = calculate(count);

    System.out.println(ans);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to calculate power of 3
def calculate(bit_cnt):

    res = 1;
    while (bit_cnt > 0):
        bit_cnt -= 1;
        res = res * 3;
    return res;

# Function to return the count of the
# unset bit ( zeros )
def unset_bit_count(n):

    count = 0;
    while (n > 0):

        # Check the bit is 0 or not
        if ((n & 1) == 0):
            count += 1;

        # Right shifting ( dividing by 2 )
        n = n >> 1;

    return count;

# Driver Code
if __name__ == '__main__':

    n = 2;

    count = unset_bit_count(n);

    ans = calculate(count);

    print(ans);

# This code contributed by Rajput-Ji
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to calculate power of 3
static long calculate(int bit_cnt)
{
    long res = 1;
    while (bit_cnt-- > 0)
    {
        res = res * 3;
    }

    return res;
}

// Function to return the count of the
// unset bit (zeros)
static int unset_bit_count(long n)
{
    int count = 0;
    while (n > 0)
    {

        // Check the bit is 0 or not
        if ((n & 1) == 0)
            count++;

        // Right shifting ( dividing by 2 )
        n = n >> 1;
    }
    return count;
}

// Driver Code
public static void Main(String[] args)
{
    long n;
    n = 2;

    int count = unset_bit_count(n);

    long ans = calculate(count);

    Console.WriteLine(ans);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of
// the above approach

// Function to calculate power of 3
function calculate(bit_cnt)
{
    let res = 1;
    while (bit_cnt--) {
        res = res * 3;
    }

    return res;
}

// Function to return the count of the
// unset bit ( zeros )
function unset_bit_count(n)
{
    let count = 0;
    while (n) {

        // Check the bit is 0 or not
        if ((n & 1) == 0)
            count++;
        // Right shifting ( dividing by 2 )
        n = n >> 1;
    }
    return count;
}

// Driver Code
    let n;
    n = 2;

    let count = unset_bit_count(n);

    let ans = calculate(count);

    document.write(ans);

</script>
```

**Output:** 

```
3
```

**时间复杂度**:0(未设置的位数)。
**辅助空间** : O(1)。