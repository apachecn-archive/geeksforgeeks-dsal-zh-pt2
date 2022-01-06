# 二进制数的最大分割数

> 原文:[https://www . geesforgeks . org/二进制数的最大拆分数/](https://www.geeksforgeeks.org/maximum-number-of-splits-of-a-binary-number/)

给定一个二进制字符串 **S** ，任务是找到你能把它分成的最大部分数，这样每个部分都可以被 **2** 整除。如果字符串不能满足给定条件进行拆分，则打印 **-1** 。
**举例:**

> **输入:**S = " 100 "
> T3】输出: 2
> 拆分如下:
> “10”ans“0”。
> **输入:** S = "110"
> **输出:** 1

**进场:**这个问题可以贪婪地解决，从左端开始，在一个指数 **j** 处切入，使得 **j** 是子串 up**j**可被 **2** 整除的最小指数。现在，用剩余的字符串继续这一步。众所周知，任何以 **0** 结尾的二进制数都可以被 **2** 整除。因此，在每一个零后面加上一个截，答案将等于字符串中零的数量。唯一不可能得到答案的情况是当给定的字符串是奇数时，即无论如何在字符串上进行切割，最后一个分割部分总是奇数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the required count
int cntSplits(string s)
{
    // If the splitting is not possible
    if (s[s.size() - 1] == '1')
        return -1;

    // To store the final ans
    int ans = 0;

    // Counting the number of zeros
    for (int i = 0; i < s.size(); i++)
        ans += (s[i] == '0');

    // Return the final answer
    return ans;
}

// Driver code
int main()
{
    string s = "10010";

    cout << cntSplits(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the required count
static int cntSplits(String s)
{
    // If the splitting is not possible
    if (s.charAt(s.length() - 1) == '1')
        return -1;

    // To store the final ans
    int ans = 0;

    // Counting the number of zeros
    for (int i = 0; i < s.length(); i++)
        ans += (s.charAt(i) == '0') ? 1 : 0;

    // Return the final answer
    return ans;
}

// Driver code
public static void main(String []args)
{
    String s = "10010";

    System.out.println(cntSplits(s));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the required count
def cntSplits(s) :

    # If the splitting is not possible
    if (s[len(s) - 1] == '1') :
        return -1;

    # To store the count of zeroes
    ans = 0;

    # Counting the number of zeroes
    for i in range(len(s)) :
        ans += (s[i] == '0');

    # Return the final answer
    return ans ;

# Driver code
if __name__ == "__main__" :

    s = "10010";

    print(cntSplits(s));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the required count
static int cntSplits(String s)
{
    // If the splitting is not possible
    if (s[s.Length - 1] == '1')
        return -1;

    // To store the final ans
    int ans = 0;

    // Counting the number of zeros
    for (int i = 0; i < s.Length; i++)
        ans += (s[i] == '0') ? 1 : 0;

    // Return the final answer
    return ans;
}

// Driver code
public static void Main(String []args)
{
    String s = "10010";

    Console.WriteLine(cntSplits(s));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the required count
function cntSplits(s)
{
    // If the splitting is not possible
    if (s[s.length - 1] == '1')
        return -1;

    // To store the final ans
    var ans = 0;

    // Counting the number of zeros
    for (var i = 0; i < s.length; i++)
        ans += (s[i] == '0');

    // Return the final answer
    return ans;
}

// Driver code
var s = "10010";
document.write( cntSplits(s));

</script>
```

**Output:** 

```
3
```

时间复杂度:O(|s|)

辅助空间:0(1)