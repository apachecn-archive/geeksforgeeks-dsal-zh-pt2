# 由至少一个元音和一个辅音组成的 N 个大小字符串的计数

> 原文:[https://www . geesforgeks . org/count-of-n-size-strings-由至少一个元音和一个辅音组成/](https://www.geeksforgeeks.org/count-of-n-size-strings-consisting-of-at-least-one-vowel-and-one-consonant/)

给定一个整数 **N** ，它代表一个字符串的长度，任务是计算长度为 N 的可能字符串的数量，N 只由一个元音和一个辅音组成。
**注:**自输出可大打印模 1000000007
**例:**

> **输入:** N = 2
> **输出:** 210
> **说明:**
> 英文字母共有 5 个元音，21 个辅音。
> 所以对于元音‘a’我们可以有 42 串形式为‘ab’、‘ba’、‘AC’、‘ca’、‘ad’、‘da’等等的音。
> 对于其他 4 个元音，同样的过程重复，我们总共得到 210 个这样的字符串。
> **输入:** N = 3
> **输出:** 8190

**方法:**
要解决上面提到的问题，我们需要忽略只包含元音(至少允许一个辅音)和只包含辅音(至少允许一个元音)的字符串。因此，所需的答案是:

> 所有可能的 N 长度字符串–(仅由元音组成的 N 长度字符串+仅由辅音组成的 N 长度字符串)= 26<sup>N</sup>–(5<sup>N</sup>+21<sup>N</sup>)

下面是上述方法的实现:

## C++

```
// C++ program to count all
// possible strings of length N
// consisting of atleast one
// vowel and one consonant
#include <bits/stdc++.h>
using namespace std;

const unsigned long long mod = 1e9 + 7;

// Function to return base^exponent
unsigned long long expo(
    unsigned long long base,
    unsigned long long exponent)
{

    unsigned long long ans = 1;

    while (exponent != 0) {
        if ((exponent & 1) == 1) {
            ans = ans * base;
            ans = ans % mod;
        }

        base = base * base;
        base %= mod;
        exponent >>= 1;
    }

    return ans % mod;
}

// Function to count all possible strings
unsigned long long findCount(
    unsigned long long N)
{
    // All possible strings of length N
    unsigned long long ans
        = (expo(26, N)

           // vowels only
           - expo(5, N)

           // consonants only
           - expo(21, N))

          % mod;

    ans += mod;
    ans %= mod;

    // Return the
    // final result
    return ans;
}

// Driver Program
int main()
{
    unsigned long long N = 3;
    cout << findCount(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count all
// possible Strings of length N
// consisting of atleast one
// vowel and one consonant
class GFG{

static int mod = (int) (1e9 + 7);

// Function to return base^exponent
static int expo(int base, int exponent)
{
    int ans = 1;

    while (exponent != 0)
    {
        if ((exponent & 1) == 1)
        {
            ans = ans * base;
            ans = ans % mod;
        }
        base = base * base;
        base %= mod;
        exponent >>= 1;
    }
    return ans % mod;
}

// Function to count all possible Strings
static int findCount(int N)
{

    // All possible Strings of length N
    int ans = (expo(26, N) -

               // Vowels only
               expo(5, N) -

               // Consonants only
               expo(21, N))% mod;
    ans += mod;
    ans %= mod;

    // Return the
    // final result
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int N = 3;
    System.out.print(findCount(N));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to count all
# possible strings of length N
# consisting of atleast one
# vowel and one consonant
mod = 1e9 + 7

# Function to return base^exponent
def expo(base, exponent):
    ans = 1
    while (exponent != 0):
        if ((exponent & 1) == 1):
            ans = ans * base
            ans = ans % mod

        base = base * base
        base %= mod
        exponent >>= 1

    return ans % mod

# Function to count all
# possible strings
def findCount(N):

    # All possible strings
    # of length N
    ans = ((expo(26, N) -

            # vowels only
            expo(5, N) -

            # consonants only
            expo(21, N)) %
            mod)

    ans += mod
    ans %= mod

    # Return the
    # final result
    return ans

# Driver Program
if __name__ == "__main__":
    N = 3
    print (int(findCount(N)))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to count all possible Strings
// of length N consisting of atleast one
// vowel and one consonant
using System;

class GFG{

static int mod = (int)(1e9 + 7);

// Function to return base^exponent
static int expo(int Base, int exponent)
{
    int ans = 1;

    while (exponent != 0)
    {
        if ((exponent & 1) == 1)
        {
            ans = ans * Base;
            ans = ans % mod;
        }
        Base = Base * Base;
        Base %= mod;
        exponent >>= 1;
    }
    return ans % mod;
}

// Function to count all possible Strings
static int findCount(int N)
{

    // All possible Strings of length N
    int ans = (expo(26, N) -

               // Vowels only
               expo(5, N) -

               // Consonants only
               expo(21, N)) % mod;
    ans += mod;
    ans %= mod;

    // Return the
    // readonly result
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int N = 3;

    Console.Write(findCount(N));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to count all
// possible Strings of length N
// consisting of atleast one
// vowel and one consonant   
var mod = parseInt( 1e9 + 7);

    // Function to return base^exponent
    function expo(base , exponent) {
        var ans = 1;

        while (exponent != 0) {
            if ((exponent & 1) == 1) {
                ans = ans * base;
                ans = ans % mod;
            }
            base = base * base;
            base %= mod;
            exponent >>= 1;
        }
        return ans % mod;
    }

    // Function to count all possible Strings
    function findCount(N) {

        // All possible Strings of length N
        var ans = (expo(26, N) -

        // Vowels only
                expo(5, N) -

                // Consonants only
                expo(21, N)) % mod;
        ans += mod;
        ans %= mod;

        // Return the
        // final result
        return ans;
    }

    // Driver code

        var N = 3;
        document.write(findCount(N));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
8190
```