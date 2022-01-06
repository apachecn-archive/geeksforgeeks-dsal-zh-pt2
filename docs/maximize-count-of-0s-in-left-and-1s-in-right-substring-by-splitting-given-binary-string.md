# 通过拆分给定的二进制字符串

，最大化左子串中的 0 和右子串中的 1 的数量

> 原文:[https://www . geesforgeks . org/通过拆分给定二进制字符串来最大化左 0 中 0 和右 1 中 1 的计数/](https://www.geeksforgeeks.org/maximize-count-of-0s-in-left-and-1s-in-right-substring-by-splitting-given-binary-string/)

给定[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **字符串**，任务是通过在任意索引处拆分给定的二进制字符串，最大化左子字符串中 0 的计数和右子字符串中 1 的计数。最后打印这样的 0 和 1 的和。

**示例:**

> **输入:** str = "0011110011"
> **输出:** 8
> **解释:**
> 如果一个字符串在索引 2 处被拆分，那么 Left substring = "00 "和 Right substring = "11110011 "。
> 因此，左子串的 0 和右子串的 1 的计数之和为 2 + 6 = 8。
> 
> **输入:** str = "0001101111011"
> **输出:** 11
> **解释:**
> 如果字符串在索引 3 处拆分，那么左子字符串为“000”，右子字符串为“1101111011”。
> 因此，左子串的 0 和右子串的 1 的计数之和为 3 + 8 = 11。

**进场:**

1.  [计算给定二进制字符串](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)中的 1 的数量(比如**total one**)。
2.  遍历给定的字符串，保持 0(比如说**零**)和 1(比如说**一**)的计数。
3.  在字符串遍历期间，将最大和更新为:

> maxSum = max(maxSum，零+(总计–1))

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to maximize the sum of the count
// of zeros and ones in the left and right
// substring
int maxSum(string& str)
{

    int maximumSum = 0;

    // To store the total ones
    int totalOnes;

    // Count the total numbers of ones
    // in string str
    totalOnes = count(str.begin(),
                      str.end(), '1');

    // To store the count of zeros and
    // ones while traversing string
    int zero = 0, ones = 0;

    // Iterate the given string and
    // update the maximum sum
    for (int i = 0; str[i]; i++) {

        if (str[i] == '0') {
            zero++;
        }
        else {
            ones++;
        }

        // Update the maximum Sum
        maximumSum
            = max(
                maximumSum,
                zero + (totalOnes - ones));
    }

    return maximumSum;
}

// Driver Code
int main()
{
    // Given binary string
    string str = "011101";

    // Function call
    cout << maxSum(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

// Function to maximize the sum 
// of the count of zeros and ones 
// in the left and right substring
static int maxSum(String str)
{
    int maximumSum = 0;

    // To store the total ones
    int totalOnes = 0;

    // Count the total numbers of ones
    // in string str
    for(int i = 0; i < str.length(); i++)
    {
       if (str.charAt(i) == '1')
       {
           totalOnes++;
       }
    }

    // To store the count of zeros and
    // ones while traversing string
    int zero = 0, ones = 0;

    // Iterate the given string and
    // update the maximum sum
    for(int i = 0; i < str.length(); i++)
    {
       if (str.charAt(i) == '0')
       {
           zero++;
       }
       else
       {
           ones++;
       }

       // Update the maximum Sum
       maximumSum = Math.max(maximumSum,
                            zero + (totalOnes - ones));
    }

    return maximumSum;
}

// Driver Code
public static void main(String args[])
{

    // Given binary string
    String str = "011101";

    // Function call
    System.out.println(maxSum(str));
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to maximize the sum of the count
# of zeros and ones in the left and right
# substring
def maxSum(str):

    maximumSum = 0

    # To store the total ones

    # Count the total numbers of ones
    # in str
    totalOnes = 0
    for i in str:
        if i == '1':
            totalOnes += 1

    # To store the count of zeros and
    # ones while traversing string
    zero = 0
    ones = 0

    # Iterate the given and
    # update the maximum sum
    i = 0
    while i < len(str):

        if (str[i] == '0'):
            zero += 1
        else:
            ones += 1

        # Update the maximum Sum
        maximumSum= max(maximumSum,zero + (totalOnes - ones))
        i += 1

    return maximumSum

# Driver Code
if __name__ == '__main__':
    # Given binary string
    str = "011101"

    # Function call
    print(maxSum(str))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to maximize the sum
// of the count of zeros and ones
// in the left and right substring
static int maxSum(string str)
{
    int maximumSum = 0;

    // To store the total ones
    int totalOnes = 0;

    // Count the total numbers of ones
    // in string str
    for(int i = 0; i < str.Length; i++)
    {
       if (str[i] == '1')
       {
           totalOnes++;
       }
    }

    // To store the count of zeros and
    // ones while traversing string
    int zero = 0, ones = 0;

    // Iterate the given string and
    // update the maximum sum
    for(int i = 0; i < str.Length; i++)
    {
       if (str[i] == '0')
       {
           zero++;
       }
       else
       {
           ones++;
       }

       // Update the maximum Sum
       maximumSum = Math.Max(maximumSum, zero +
                                   (totalOnes -
                                    ones));
    }
    return maximumSum;
}

// Driver Code
public static void Main(string []args)
{

    // Given binary string
    string str = "011101";

    // Function call
    Console.Write(maxSum(str));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to maximize the sum of the count
// of zeros and ones in the left and right
// substring
function maxSum(str)
{

    var maximumSum = 0;

    // To store the total ones
    var totalOnes = 0;

    // Count the total numbers of ones
    // in string str
    str.split('').forEach(c => {

        if(c == '1')
            totalOnes++;
    });

    // To store the count of zeros and
    // ones while traversing string
    var zero = 0, ones = 0;

    // Iterate the given string and
    // update the maximum sum
    for (var i = 0; str[i]; i++) {

        if (str[i] == '0') {
            zero++;
        }
        else {
            ones++;
        }

        // Update the maximum Sum
        maximumSum
            = Math.max(
                maximumSum,
                zero + (totalOnes - ones));
    }

    return maximumSum;
}

// Driver Code
// Given binary string
var str = "011101";
// Function call
document.write( maxSum(str));

</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N)* ，其中 N 是字符串的长度。

***辅助空间:**O(1)*T4】