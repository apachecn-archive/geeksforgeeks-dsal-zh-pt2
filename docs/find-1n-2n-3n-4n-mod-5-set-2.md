# Find (1^n + 2^n + 3^n + 4^n) mod 5 |第 2 集

> 原文:[https://www.geeksforgeeks.org/find-1n-2n-3n-4n-mod-5-set-2/](https://www.geeksforgeeks.org/find-1n-2n-3n-4n-mod-5-set-2/)

给定一个非常大的数字 **N** 。任务是找到**(1<sup>n</sup>+2<sup>n</sup>+3<sup>n</sup>+4<sup>n</sup>)mod 5**。
**示例:**

> **输入:** N = 4
> **输出:**4
> (1+16+81+256)% 5 = 354% 5 = 4
> **输入:**N = 782346293782632873467731
> **输出:** 0

**进场:**(1<sup>n</sup>+2<sup>n</sup>+3<sup>n</sup>+4<sup>n</sup>mod 5 =(1<sup>n mod？(5)</sup> + 2 <sup>n mod？(5)</sup> + 3 <sup>n mod？(5)</sup> + 4 <sup>n mod？(5)</sup> ) mod 5。
这个公式是正确的，因为 5 是素数，它与 1，2，3，4 是互素的。
知道[吗？(n)](https://www.geeksforgeeks.org/eulers-totient-function/) 和[模大数](https://www.geeksforgeeks.org/how-to-compute-mod-of-a-big-number/)
**？(5) = 4** ，故名**(1<sup>n</sup>+2<sup>n</sup>+3<sup>n</sup>+4<sup>n</sup>)mod 5 =(1<sup>n mod 4</sup>+2<sup>n mod 4</sup>+3<sup>n mod 4</sup>+4<sup>n mod 4</sup>)mod 5**
如下

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return A mod B
int A_mod_B(string N, int a)
{
    // length of the string
    int len = N.size();

    // to store required answer
    int ans = 0;
    for (int i = 0; i < len; i++)
        ans = (ans * 10 + (int)N[i] - '0') % a;

    return ans % a;
}

// Function to return (1^n + 2^n + 3^n + 4^n) % 5
int findMod(string N)
{
    // ?(5) = 4
    int mod = A_mod_B(N, 4);

    int ans = (1 + pow(2, mod) + pow(3, mod)
               + pow(4, mod));

    return (ans % 5);
}

// Driver code
int main()
{
    string N = "4";
    cout << findMod(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return A mod B
static int A_mod_B(String N, int a)
{
    // length of the string
    int len = N.length();

    // to store required answer
    int ans = 0;
    for (int i = 0; i < len; i++)
        ans = (ans * 10 + (int)N.charAt(i) - '0') % a;

    return ans % a;
}

// Function to return (1^n + 2^n + 3^n + 4^n) % 5
static int findMod(String N)
{
    // ?(5) = 4
    int mod = A_mod_B(N, 4);

    int ans = (1 + (int)Math.pow(2, mod) +
                (int)Math.pow(3, mod) +
                (int)Math.pow(4, mod));

    return (ans % 5);
}

// Driver code
public static void main(String args[])
{
    String N = "4";
    System.out.println(findMod(N));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return A mod B
def A_mod_B(N, a):

    # length of the string
    Len = len(N)

    # to store required answer
    ans = 0
    for i in range(Len):
        ans = (ans * 10 + int(N[i])) % a

    return ans % a

# Function to return (1^n + 2^n + 3^n + 4^n) % 5
def findMod(N):

    # ?(5) = 4
    mod = A_mod_B(N, 4)

    ans = (1 + pow(2, mod) +
               pow(3, mod) + pow(4, mod))

    return ans % 5

# Driver code
N = "4"
print(findMod(N))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return A mod B
static int A_mod_B(string N, int a)
{
    // length of the string
    int len = N.Length;

    // to store required answer
    int ans = 0;
    for (int i = 0; i < len; i++)
        ans = (ans * 10 + (int)N[i] - '0') % a;

    return ans % a;
}

// Function to return (1^n + 2^n + 3^n + 4^n) % 5
static int findMod(string N)
{
    // ?(5) = 4
    int mod = A_mod_B(N, 4);

    int ans = (1 + (int)Math.Pow(2, mod) +
                (int)Math.Pow(3, mod) +
                (int)Math.Pow(4, mod));

    return (ans % 5);
}

// Driver code
public static void Main()
{
    string N = "4";
    Console.WriteLine(findMod(N));
}
}

// This code is contributed by Code_Mech.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return A mod B
function A_mod_B($N, $a)
{
    // length of the string
    $len = strlen($N);

    // to store required answer
    $ans = 0;
    for ($i = 0; $i < $len; $i++)
        $ans = ($ans * 10 +
               (int)$N[$i] - '0') % $a;

    return $ans % $a;
}

// Function to return
// (1^n + 2^n + 3^n + 4^n) % 5
function findMod($N)
{
    // ?(5) = 4
    $mod = A_mod_B($N, 4);

    $ans = (1 + pow(2, $mod) +
                pow(3, $mod) + pow(4, $mod));

    return ($ans % 5);
}

// Driver code
$N = "4";
echo findMod($N);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return A mod B
function A_mod_B(N, a)
{
    // length of the string
    var len = N.length;

    // to store required answer
    var ans = 0;
    for (var i = 0; i < len; i++)
        ans = (ans * 10 + parseInt(N.charAt(i) - '0')) % a;

    return ans % a;
}

// Function to return (1^n + 2^n + 3^n + 4^n) % 5
function findMod(N)
{
    // ?(5) = 4
    var mod = A_mod_B(N, 4);

    var ans = (1 + parseInt(Math.pow(2, mod) +
                Math.pow(3, mod) +
                Math.pow(4, mod)));

    return (ans % 5);
}

// Driver Code
var N = "4";

// Function call
document.write(findMod(N));

// This code is contributed by Kirti

</script>
```

**Output:** 

```
4
```