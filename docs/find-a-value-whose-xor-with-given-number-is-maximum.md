# 求一个与给定数异或最大的值

> 原文:[https://www . geesforgeks . org/find-a-value-with-xor-to-number-max/](https://www.geeksforgeeks.org/find-a-value-whose-xor-with-given-number-is-maximum/)

给定一个值 X，任务是找到数字 Y，当与 X 进行异或运算时，该数字将给出最大可能值。
(假设 X 为 8 位)X 和 Y 的最大可能值为 255。
**例:**

```
Input:  X = 2
Output: 253
Binary Representation of X = 00000010
Binary Representation of Y = 11111101
Maximum XOR value: 11111111

Input:  X = 200
Output: 55
```

**方法:**为了确保 XOR 的最大值，我们需要将 x 中的所有开位设置为关，因此，y 应该将 x 中的所有开位设置为关，x 中的所有关位设置为开(0^1 = 1，1^0 = 1)。所以 Y 应该是 x 的 1 的补码表示。
下面是上面方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function To Calculate Answer
int calculate(int X)
{
    // Find number of bits in the given integer
    int number_of_bits = 8;

    // XOR the given integer with poe(2,
    // number_of_bits-1 and print the result
    return ((1 << number_of_bits) - 1) ^ X;
}

// Driver Code
int main()
{
    int X = 4;

    cout << "Required Number is : "
         << calculate(X) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

import java.io.*;

class GFG {

// Function To Calculate Answer
static int calculate(int X)
{
    // Find number of bits in the given integer
    int number_of_bits = 8;

    // XOR the given integer with poe(2,
    // number_of_bits-1 and print the result
    return ((1 << number_of_bits) - 1) ^ X;
}

// Driver Code

    public static void main (String[] args) {
        int X = 4;

    System.out.println( "Required Number is : "
        +calculate(X));
    }
}
// This code is contributed by shs..
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function To Calculate Answer
def calculate(X):

    # Find number of bits in the given integer
    number_of_bits = 8

    # XOR the given integer with poe(2,
    # number_of_bits-1 and print the result
    return ((1 << number_of_bits) - 1) ^ X

# Driver Code
if __name__ == "__main__":

    X = 4
    print("Required Number is:", calculate(X))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function To Calculate Answer
static int calculate(int X)
{
    // Find number of bits in
    // the given integer
    int number_of_bits = 8;

    // XOR the given integer with poe(2,
    // number_of_bits-1 and print the result
    return ((1 << number_of_bits) - 1) ^ X;
}

// Driver Code
public static void Main ()
{
    int X = 4;

    Console.WriteLine("Required Number is : " +
                                 calculate(X));
}
}

// This code is contributed by shs..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the
// above approach

// Function To Calculate Answer
function calculate($X)
{
    // Find number of bits in
    // the given integer
    $number_of_bits = 8;

    // XOR the given integer with
    // poe(2, number_of_bits-1 and
    // print the result
    return ((1 << $number_of_bits) - 1) ^ $X;
}

// Driver Code
$X = 4;

echo "Required Number is : " .
      calculate($X) . "\n";

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function To Calculate Answer
function calculate(X)
{
    // Find number of bits in the given integer
    let number_of_bits = 8;

    // XOR the given integer with poe(2,
    // number_of_bits-1 and print the result
    return ((1 << number_of_bits) - 1) ^ X;
}

// Driver Code
    let X = 4;

    document.write("Required Number is : "
         + calculate(X) + "<br>");

</script>
```

**Output:** 

```
Required Number is : 251
```