# 计算可被 10 整除的转数

> 原文:[https://www . geeksforgeeks . org/count-rotations-可被 10 整除/](https://www.geeksforgeeks.org/count-rotations-which-are-divisible-by-10/)

给定一个数 **N** ，任务是计算给定数的所有可被 10 整除的旋转。
**例:**

> **输入:** N = 10203
> **输出:** 2
> **说明:**
> 给定的数字可能有 5 次旋转。它们是:02031、20310、03102、31020、10203
> 在这些旋转中，只有 20310 和 31020 可以被 10 整除。所以 2 是输出。
> **输入:** N = 135
> **输出:** 0

**天真方法:**这个问题的天真方法是[形成所有可能的旋转](https://www.geeksforgeeks.org/generate-all-rotations-of-a-number/)。众所周知，对于多个尺寸 **K** ，该数量 **N** 的可能转数为 **K** 。因此，找出所有的旋转，对于每个旋转，检查这个数是否能被 10 整除。这种方法的时间复杂度是二次的。
**高效方法:**高效方法背后的概念是，为了检查一个数是否能被 10 整除，我们只需检查最后一位数字是否为 0。所以思路就是简单的迭代给定的数，求 0 的个数，如果 0 的个数是 **F** ，那么很明显 **K** 旋转中的 **F** 在给定的数 **N** 的末尾会有 0。
以下是上述办法的实施:

## C++

```
// C++ implementation to find the
// count of rotations which are
// divisible by 10

#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// all the rotations which are
// divisible by 10.
int countRotation(int n)
{
    int count = 0;

    // Loop to iterate through the
    // number
    do {
        int digit = n % 10;

        // If the last digit is 0,
        // then increment the count
        if (digit == 0)
            count++;
        n = n / 10;
    } while (n != 0);

    return count;
}

// Driver code
int main()
{
    int n = 10203;
    cout << countRotation(n);
}
```

## C#

```
// CSharp implementation to find the
// count of rotations which are
// divisible by 10

using System;
class Solution {

    // Function to return the count
    // of all rotations which are
    // divisible by 10.
    static int countRotation(int n)
    {
        int count = 0;

        // Loop to iterate through the
        // number
        do {
            int digit = n % 10;

            // If the last digit is 0,
            // then increment the count
            if (digit % 2 == 0)
                count++;
            n = n / 10;
        } while (n != 0);

        return count;
    }

    // Driver code
    public static void Main()
    {
        int n = 10203;
        Console.Write(countRotation(n));
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// count of rotations which are
// divisible by 10

class GFG {

    // Function to return the count
    // of all rotations which are
    // divisible by 10.
    static int countRotation(int n)
    {
        int count = 0;

        // Loop to iterate through the
        // number
        do {
            int digit = n % 10;

            // If the last digit is 0,
            // then increment the count
            if (digit == 0)
                count++;
            n = n / 10;
        } while (n != 0);

        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 10203;

        System.out.println(countRotation(n));
    }
}
```

## 计算机编程语言

```
# Python3 implementation to find the
# count of rotations which are
# divisible by 10

# Function to return the count of
# all rotations which are divisible
# by 10.
def countRotation(n):
    count = 0;

    # Loop to iterate through the
    # number
    while n > 0:
        digit = n % 10

        # If the last digit is 0,
        # then increment the count
        if(digit % 2 == 0):
            count = count + 1
        n = int(n / 10)

    return count;   

# Driver code 
if __name__ == "__main__" :

    n = 10203; 
    print(countRotation(n)); 
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// count of rotations which are
// divisible by 10

// Function to return the count of
// all the rotations which are
// divisible by 10.
function countRotation(n)
{
    let count = 0;

    // Loop to iterate through the
    // number
    do {
        let digit = n % 10;

        // If the last digit is 0,
        // then increment the count
        if (digit == 0)
            count++;
        n = parseInt(n / 10);
    } while (n != 0);

    return count;
}

// Driver code
let n = 10203;
document.write(countRotation(n));

</script>
```

**Output:** 

```
2
```

**时间复杂度:** *O(log <sub>10</sub> N)* ，其中 N 为数字的长度。

**辅助空间:** O(1)