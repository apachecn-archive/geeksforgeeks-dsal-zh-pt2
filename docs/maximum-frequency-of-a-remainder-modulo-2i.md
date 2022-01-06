# 余数模 2i 的最大频率

> 原文:[https://www . geesforgeks . org/最大余数频率模 2i/](https://www.geeksforgeeks.org/maximum-frequency-of-a-remainder-modulo-2i/)

给定一个八进制数 **N** ，任务是将该数转换为十进制，然后用 **2** 即**2<sup>I</sup>T7】的每次方求模，使得 **i > 0** 和**2<sup>I</sup>T19】N**并打印模的最大频率。
**举例:**** 

> **输入:** N = 13
> **输出:** 2
> 八进制(13) =十进制(11)
> 11% 2 = 1
> 11% 4 = 3
> 11% 8 = 3
> 3 出现次数最多，即 2 次。
> **输入:** N = 21
> **输出:** 4

**方法:**用数字的二进制表示代替数字，找到数字的二进制表示。众所周知，二进制表示中的每一个数字都以递增的顺序表示 2 的幂。所以 2 次方数的模是由它前面的位的二进制表示形成的数。例如

> 八进制(13) =十进制(11) =二进制(1011)
> 所以，
> 11(1011)% 2(10)= 1(1)
> 11(1011)% 4(100)= 3(11)
> 11(1011)% 8(1000)= 3(011)

这里，可以观察到，当模的二进制表示中有一个零时，该数保持不变。所以模的最大频率将是 1 +该数的二进制表示中连续 0 的个数(不是前导零)。由于模从 2 开始，移除数字的最低有效位。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Binary representation of the digits
const string bin[] = { "000", "001", "010", "011",
                       "100", "101", "110", "111" };

// Function to return the maximum frequency
// of s modulo with a power of 2
int maxFreq(string s)
{

    // Store the binary representation
    string binary = "";

    // Convert the octal to binary
    for (int i = 0; i < s.length(); i++) {
        binary += bin[s[i] - '0'];
    }

    // Remove the LSB
    binary = binary.substr(0, binary.length() - 1);

    int count = 1, prev = -1, i, j = 0;

    for (i = binary.length() - 1; i >= 0; i--, j++)

        // If there is 1 in the binary representation
        if (binary[i] == '1') {

            // Find the number of zeroes in between
            // two 1's in the binary representation
            count = max(count, j - prev);
            prev = j;
        }

    return count;
}

// Driver code
int main()
{
    string octal = "13";

    cout << maxFreq(octal);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Binary representation of the digits
static String bin[] = { "000", "001", "010", "011",
                        "100", "101", "110", "111" };

// Function to return the maximum frequency
// of s modulo with a power of 2
static int maxFreq(String s)
{

    // Store the binary representation
    String binary = "";

    // Convert the octal to binary
    for (int i = 0; i < s.length(); i++)
    {
        binary += bin[s.charAt(i) - '0'];
    }

    // Remove the LSB
    binary = binary.substring(0,
             binary.length() - 1);

    int count = 1, prev = -1, i, j = 0;

    for (i = binary.length() - 1;
         i >= 0; i--, j++)

        // If there is 1 in the binary representation
        if (binary.charAt(i) == '1')
        {

            // Find the number of zeroes in between
            // two 1's in the binary representation
            count = Math.max(count, j - prev);
            prev = j;
        }
    return count;
}

// Driver code
public static void main(String []args)
{
    String octal = "13";

    System.out.println(maxFreq(octal));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Binary representation of the digits
bin = [ "000", "001", "010", "011",
        "100", "101", "110", "111" ];

# Function to return the maximum frequency
# of s modulo with a power of 2
def maxFreq(s) :

    # Store the binary representation
    binary = "";

    # Convert the octal to binary
    for i in range(len(s)) :
        binary += bin[ord(s[i]) - ord('0')];

    # Remove the LSB
    binary = binary[0 : len(binary) - 1];

    count = 1; prev = -1;j = 0;

    for i in range(len(binary) - 1, -1, -1) :

        # If there is 1 in the binary representation
        if (binary[i] == '1') :

            # Find the number of zeroes in between
            # two 1's in the binary representation
            count = max(count, j - prev);
            prev = j;

        j += 1;

    return count;

# Driver code
if __name__ == "__main__" :

    octal = "13";

    print(maxFreq(octal));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Binary representation of the digits
static String []bin = { "000", "001", "010", "011",
                        "100", "101", "110", "111" };

// Function to return the maximum frequency
// of s modulo with a power of 2
static int maxFreq(String s)
{

    // Store the binary representation
    String binary = "";

    // Convert the octal to binary
    for (int K = 0; K < s.Length; K++)
    {
        binary += bin[s[K] - '0'];
    }

    // Remove the LSB
    binary = binary.Substring(0,
             binary.Length - 1);

    int count = 1, prev = -1, i, j = 0;

    for (i = binary.Length - 1;
         i >= 0; i--, j++)

        // If there is 1 in the binary representation
        if (binary[i] == '1')
        {

            // Find the number of zeroes in between
            // two 1's in the binary representation
            count = Math.Max(count, j - prev);
            prev = j;
        }
    return count;
}

// Driver code
public static void Main(String []args)
{
    String octal = "13";

    Console.WriteLine(maxFreq(octal));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Binary representation of the digits
bin = [ "000", "001", "010", "011",
            "100", "101", "110", "111" ];

// Function to return the maximum frequency
// of s modulo with a power of 2
function maxFreq( s )
{

    // Store the binary representation
    var binary = "";

    // Convert the octal to binary
    for (var i = 0; i < s.length; i++) {
        binary += bin[s.charAt(i) - '0'];
    }

    // Remove the LSB
    binary = binary.substr(0, binary.length - 1);

    var count = 1, prev = -1, i, j = 0;

    for (i = binary.length - 1; i >= 0; i--, j++)

        // If there is 1 in the binary representation
        if (binary.charAt(i) == '1') {

            // Find the number of zeroes in between
            // two 1's in the binary representation
            count = Math.max(count, j - prev);
            prev = j;
        }

    return count;
}

var octal = "13";
document.write( maxFreq(octal));

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
2
```