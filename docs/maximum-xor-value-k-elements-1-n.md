# 从 1 到 n 的最多 k 个元素的最大异或值

> 原文:[https://www . geesforgeks . org/maximum-xor-value-k-elements-1-n/](https://www.geeksforgeeks.org/maximum-xor-value-k-elements-1-n/)

给你两个正整数 n 和 k，你要计算从 1 到 n 最多 k 个元素的最大可能 XOR 值
**注:** k > 1
**例:**

```
Input : n = 7, k = 3
Output : 7
Explanation : You can select 1, 2, 4 for maximum XOR-value

Input : n = 7, k = 2
Output : 7
Explanation : You can select 3 and 4 for maximum value.
```

对于 k 的任何值，我们可以从 1 到 n 中选择至少两个数字，对于所需的结果，我们必须更仔细地观察 n 的位表示。因此，让我们通过一个例子来理解它。假设 n = 6，k = 2:
6 = 110 的位表示
5 = 101 的位表示
4 = 100 的位表示
3 = 011 的位表示
2 = 010 的位表示
1 = 001 的位表示
现在，您可以看到，在选择了您想要的数量并选择了其中任何一个之后，您都无法获得大于 111 的异或值，即 7。因此，对于给定的 n 和 k > 1，最大可能的异或值是 **2 <sup>log2(n)+1</sup> -1** (即 n 的所有位都变为 1 时的值)。

## C++

```
// Program to obtain maximum XOR value sub-array
#include <bits/stdc++.h>
using namespace std;

// function to calculate maximum XOR value
int maxXOR(int n, int k) {
  int c = log2(n) + 1;

  // Return (2^c - 1)
  return ((1 << c) - 1);
}

// driver program
int main() {
  int n = 12;
  int k = 3;
  cout << maxXOR(n, k);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to obtain maximum
// XOR value sub-array
import java.lang.*;

class GFG
{
// function to calculate
// maximum XOR value
static int maxXOR(int n, int k)
{
int c = (int) (Math.log(n) /
               Math.log(2)) + 1;

// Return (2^c - 1)
return ((1 << c) - 1);
}

// Driver Code
public static void main(String[] args)
{
int n = 12;
int k = 3;
System.out.println(maxXOR(n, k));
}
}

// This code is contributed by Smitha
```

## 蟒蛇 3

```
# Python3 program to obtain maximum
# XOR value sub-array
import math

# Function to calculate maximum XOR value
def maxXOR(n, k):
    c = int(math.log(n, 2)) + 1

    # Return (2^c - 1)
    return ((1 << c) - 1)

# Driver Code
n = 12; k = 3
print (maxXOR(n, k))

# This code is contributed by shreyanshi_arun.
```

## C#

```
// Program to obtain maximum
// XOR value sub-array
using System;

class GFG
{
// function to calculate
// maximum XOR value
static int maxXOR(int n, int k)
{
int c = (int) (Math.Log(n) /
               Math.Log(2)) + 1;

// Return (2^c - 1)
return ((1 << c) - 1);
}

// Driver Code
public static void Main(String[] args)
{
int n = 12;
int k = 3;
Console.Write(maxXOR(n, k)) ;
}
}

// This code is contributed by Smitha
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to obtain maximum
// XOR value sub-array

// function to calculate
// maximum XOR value
function maxXOR($n, $k)
{
    $c = log($n, 2) + 1;

    // Return (2^c - 1)
    return ((1 << $c) - 1);
}

// Driver Code
$n = 12;
$k = 3;
echo maxXOR($n, $k);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// JavaScript program to obtain maximum
// XOR value sub-array

// function to calculate
// maximum XOR value
function maxXOR(n, k)
{
let c = (Math.log(n) /
               Math.log(2)) + 1;

// Return (2^c - 1)
return ((1 << c) - 1);
}   

// Driver code

        let n = 12;
        let k = 3;
        document.write(maxXOR(n, k));

</script>
```

**Output:** 

```
15
```