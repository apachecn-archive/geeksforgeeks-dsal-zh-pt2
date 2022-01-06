# 对八进制表示中有数字 D 的数字进行最多 N 次计数

> 原文:[https://www . geesforgeks . org/count-numbers-up-n-with-digit-d-in-it-octal-presentation/](https://www.geeksforgeeks.org/count-numbers-up-to-n-having-digit-d-in-its-octal-representation/)

给定一个正整数 **N** 和一个代表一个数字的整数 **D** ，任务是对范围**【1，N】**内的数字进行计数，使得该数字的[八进制表示](https://www.geeksforgeeks.org/octal-numbers-c/)中至少有一个数字是 **d** 。

**示例:**

> **输入:** N = 20，D = 7
> **输出:** 2
> **说明:**
> 八进制表示中数字 7 的[1，20]范围内的数字是 7 和 15。
> 因此，要求的输出为 2。
> 
> **输入:** N = 40，D = 5
> **输出:** 6
> **解释:**
> 八进制表示中有数字 5 的[1，40]范围内的数字是 5，13，21，29，37 和 40。
> 因此，所需输出为 6

**方法:**按照以下步骤解决问题:

*   迭代范围**【1，N】**。对于每一个**I<sup>th</sup>T5【数字】检查[数字的八进制表示中至少有一个数字是](https://www.geeksforgeeks.org/octal-numbers-c/)还是 **d** 。如果发现为真，则增加计数。**
*   最后，打印获得的计数。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the numbers in given
// range whose octal representation
// contains atleast digit, d
void countNumbers(int n, int d)
{
    // Store count of numbers up to n
    // whose octal representation
    // contains digit d
    int total = 0;

    // Iterate over the range[1, n]
    for (int i = 1; i <= n; i++) {

        int x = i;

        // Calculate digit of i in
        // octal representation
        while (x > 0) {

            // Check if octal representation
            // of x contains digit d
            if (x % 8 == d) {

                // Update total
                total++;
                break;
            }

            // Update x
            x = x / 8;
        }
    }

    // Print the answer
    cout << total;
}

// Driver Code
int main()
{
    // Given N and D
    int n = 20, d = 7;

    // Counts and prints numbers
// up to N having D as a digit
// in its octal representation
    countNumbers(n, d);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to count the numbers in given
// range whose octal representation
// contains atleast digit, d
static void countNumbers(int n, int d)
{

    // Store count of numbers up to n
    // whose octal representation
    // contains digit d
    int total = 0;

    // Iterate over the range[1, n]
    for(int i = 1; i <= n; i++)
    {
        int x = i;

        // Calculate digit of i in
        // octal representation
        while (x > 0)
        {

            // Check if octal representation
            // of x contains digit d
            if (x % 8 == d)
            {

                // Update total
                total++;
                break;
            }

            // Update x
            x = x / 8;
        }
    }

    // Print the answer
    System.out.println(total);
}

// Driver code
public static void main(String[] args)
{

    // Given N and D
    int n = 20, d = 7;

    // Counts and prints numbers
    // up to N having D as a digit
    // in its octal representation
    countNumbers(n, d);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count the numbers in given
# range whose octal representation
# contains atleast digit, d
def countNumbers(n, d):

    # Store count of numbers up to n
    # whose octal representation
    # contains digit d
    total = 0

    # Iterate over the range[1, n]
    for i in range(1, n + 1):
        x = i

        # Calculate digit of i in
        # octal representation
        while (x > 0):

            # Check if octal representation
            # of x contains digit d
            if (x % 8 == d):

                # Update total
                total += 1
                break

            # Update x
            x = x // 8

    # Prthe answer
    print (total)

# Driver Code
if __name__ == '__main__':

    # Given N and D
    n , d = 20, 7

    # Counts and prints numbers
    # up to N having D as a digit
    # in its octal representation
    countNumbers(n, d)

# This code is contributed by mohit kumr 29
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to count the numbers in given
// range whose octal representation
// contains atleast digit, d
static void countNumbers(int n, int d)
{

    // Store count of numbers up to n
    // whose octal representation
    // contains digit d
    int total = 0;

    // Iterate over the range[1, n]
    for(int i = 1; i <= n; i++)
    {
        int x = i;

        // Calculate digit of i in
        // octal representation
        while (x > 0)
        {

            // Check if octal representation
            // of x contains digit d
            if (x % 8 == d)
            {

                // Update total
                total++;
                break;
            }

            // Update x
            x = x / 8;
        }
    }

    // Print the answer
    Console.WriteLine(total);
}

// Driver Code
static void Main()
{

    // Given N and D
    int n = 20, d = 7;

    // Counts and prints numbers
    // up to N having D as a digit
    // in its octal representation
    countNumbers(n, d);
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to count the numbers in given
// range whose octal representation
// contains atleast digit, d
function countNumbers(n, d)
{

    // Store count of numbers up to n
    // whose octal representation
    // contains digit d
    let total = 0;

    // Iterate over the range[1, n]
    for(let i = 1; i <= n; i++)
    {
        let x = i;

        // Calculate digit of i in
        // octal representation
        while (x > 0)
        {

            // Check if octal representation
            // of x contains digit d
            if (x % 8 == d)
            {

                // Update total
                total++;
                break;
            }

            // Update x
            x = x / 8;
        }
    }

    // Print the answer
    document.write(total);
}

// Driver Code

    // Given N and D
    let n = 20, d = 7;

    // Counts and prlets numbers
    // up to N having D as a digit
    // in its octal representation
    countNumbers(n, d);

    // This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N * log<sub>8</sub>N)*
***辅助空间:** O(1)*