# 找到 2^(2^A) % B

> 原文:[https://www.geeksforgeeks.org/find-22a-b/](https://www.geeksforgeeks.org/find-22a-b/)

给定两个整数 **A** 和 **B** ，任务是计算 **2 <sup>2A</sup> % B** 。

**示例:**

> **输入:** A = 3，B = 5
> **输出:**1
> 2<sup>23</sup>% 5 = 2<sup>8</sup>% 5 = 256% 5 = 1。
> 
> **输入:** A = 10，B = 13
> T3】输出: 3

**方法:**利用递归将问题分解为子问题，不溢出整数，可以高效地解决问题。

> 让 **F(A，B) = 2 <sup>2A</sup> % B** 。
> 现在，F(A，B)= 2<sup>2A</sup>% B
> = 2<sup>2 * 2A–1</sup>% B
> =(2<sup>2A–1+2A–1</sup>)% B
> =(2<sup>2A–1</sup>* 2<sup>2A–1</sup>)% B
> =(F(A–1，B)* F(A–1，B)) % B
> 底壳为 F(1，B) = 2 <sup>21</sup> % B = 4 % B.

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long

// Function to return 2^(2^A) % B
ll F(ll A, ll B)
{

    // Base case, 2^(2^1) % B = 4 % B
    if (A == 1)
        return (4 % B);
    else
    {
        ll temp =  F(A - 1, B);
        return (temp * temp) % B;
    }
}

// Driver code
int main()
{
    ll A = 25, B = 50;

    // Print 2^(2^A) % B
    cout << F(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{
    // Function to return 2^(2^A) % B
    static long F(long A, long B)
    {

        // Base case, 2^(2^1) % B = 4 % B
        if (A == 1)
            return (4 % B);
        else
        {
            long temp = F(A - 1, B);
            return (temp * temp) % B;
        }
    }

    // Driver code
    public static void main(String args[])
    {
        long A = 25, B = 50;

        // Print 2^(2^A) % B
        System.out.println(F(A, B));
    }
}

// This code is contributed by Ryuga
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return 2^(2^A) % B
def F(A, B):

    # Base case, 2^(2^1) % B = 4 % B
    if (A == 1):
        return (4 % B);
    else:
        temp = F(A - 1, B);
        return (temp * temp) % B;

# Driver code
A = 25;
B = 50;

# Print 2^(2^A) % B
print(F(A, B));

# This code is contributed by mits
```

## C#

```
// C# implementation of the approach
class GFG
{

// Function to return 2^(2^A) % B
static long F(long A, long B)
{

    // Base case, 2^(2^1) % B = 4 % B
    if (A == 1)
        return (4 % B);
    else
    {
        long temp = F(A - 1, B);
        return (temp * temp) % B;
    }
}

// Driver code
static void Main()
{
    long A = 25, B = 50;

    // Print 2^(2^A) % B
    System.Console.WriteLine(F(A, B));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return 2^(2^A) % B
function F($A, $B)
{

    // $Base case, 2^(2^1) % B = 4 % B
    if ($A == 1)
        return (4 % $B);
    else
    {
        $temp =  F($A - 1, $B);
        return ($temp * $temp) % $B;
    }
}

// Driver code
$A = 25;
$B = 50;

 // Print 2^(2^$A) % $B
echo F($A, $B);

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return 2^(2^A) % B
function F(A, B)
{

    // Base case, 2^(2^1) % B = 4 % B
    if (A == 1)
        return (4 % B);
    else
    {
        var temp =  F(A - 1, B);
        return (temp * temp) % B;
    }
}

// Driver code
var A = 25, B = 50;

// Print 2^(2^A) % B
document.write( F(A, B));

// This code is contributed by noob2000

</script>
```

**Output:** 

```
46
```