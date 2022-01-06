# 具有给定频率的连续字符对总和的二进制字符串

> 原文:[https://www . geeksforgeeks . org/create-a-给定频率的二进制字符串-连续字符对的总和/](https://www.geeksforgeeks.org/create-a-binary-string-with-given-frequencies-of-sums-of-consecutive-pair-of-characters/)

给定三个整数 **P** 、 **Q** 和 **R** ，任务是生成一个二进制字符串，其中 P、Q 和 R 对连续字符的和分别为 0、1 和 2。
**示例:**

> **输入:** P = 1，Q = 2，R = 2
> **输出:** 111001
> **解释:**
> 子串“00”、“10”、“01”和“11”分别有和 0、1、1 和 2。
> 因此，以下一组子字符串{ {“11”}、{“11”}、{“10”}、{“00”}、{“01”} }满足给定的约束。因此，子字符串形成的字符串是 111001。
> **输入:** P = 3，Q = 1，R = 0
> **输出:** 10000

**方法:**为了解决这个问题，我们需要遵循以下步骤:

*   如果**P****R**为*非零*，则至少有一对和为 1 的连续字符。因此，如果所提供的 **Q** 是 0，在这种情况下，则不能形成这样的串。因此，返回 *-1* 。
*   如果 Q 为零，且 P 和 R 中只有一个非零，则 P 非零时追加 **0 P+1** 次*或 R 非零时追加 **1 R+1** 次*。**
*   如果它们都不为零:
    *   分别追加 **0** 和 **1** **P + 1** 和 **Q + 1** 次。
    *   交替追加 **0** 和**1****Q–1**时间。

下面是上述方法的实现:

## C++

```
// C++ program to generate a binary
// string with given frequencies
// of sums of consecutive
// pair of characters

#include <bits/stdc++.h>
using namespace std;

// A Function that generates
// and returns the binary string
string build_binary_str(int p,
                        int q, int r)
{

    // P: Frequency of consecutive
    // characters with sum 0
    // Q: Frequency of consecutive
    // characters with sum 1
    // R: Frequency of consecutive
    // characters with sum 2

    string ans = "";

    // If no consecutive
    // character adds up to 1
    if (q == 0) {

        // Not possible if both P
        // and Q are non - zero
        if (p != 0 && r != 0) {
            return "-1";
        }

        else {

            // If P is not equal to 0
            if (p) {

                // Append 0 P + 1 times
                ans = string(p + 1, '0');
            }
            else {
                // Append 1 R + 1 times
                ans = string(r + 1, '1');
            }
        }
    }
    else {

        // Append "01" to satisfy Q
        for (int i = 1; i <= q + 1; i++) {
            if (i % 2 == 0) {
                ans += '0';
            }
            else {
                ans += '1';
            }
        }

        // Append "0" P times
        ans.insert(1, string(p, '0'));

        // Append "1" R times
        ans.insert(0, string(r, '1'));
    }
    return ans;
}

// Driver Code
int main()
{
    int p = 1, q = 2, r = 2;
    cout << build_binary_str(p, q, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate a binary
// String with given frequencies
// of sums of consecutive
// pair of characters
 class GFG{

// A Function that generates
// and returns the binary String
static String build_binary_str(int p,
                               int q, int r)
{

    // P: Frequency of consecutive
    // characters with sum 0
    // Q: Frequency of consecutive
    // characters with sum 1
    // R: Frequency of consecutive
    // characters with sum 2
    String ans = "";

    // If no consecutive
    // character adds up to 1
    if (q == 0)
    {

        // Not possible if both P
        // and Q are non - zero
        if (p != 0 && r != 0)
        {
            return "-1";
        }

        else
        {

            // If P is not equal to 0
            if (p > 0)
            {

                // Append 0 P + 1 times
                ans = Strings(p + 1, '0');
            }
            else
            {
                // Append 1 R + 1 times
                ans = Strings(r + 1, '1');
            }
        }
    }
    else
    {

        // Append "01" to satisfy Q
        for (int i = 1; i <= q + 1; i++)
        {
            if (i % 2 == 0)
            {
                ans += '0';
            }
            else
            {
                ans += '1';
            }
        }

        // Append "0" P times
        ans = ans.substring(0, 1) + Strings(p, '0') + ans.substring(1);

        // Append "1" R times
        ans = Strings(r, '1') + ans;
    }
    return ans;
}

static String Strings(int p, char c)
{
    String ans = "";
    for (int i = 0; i < p; i++)
        ans += c;
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int p = 1, q = 2, r = 2;
    System.out.print(build_binary_str(p, q, r));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program to generate a binary
# string with given frequencies
# of sums of consecutive
# pair of characters

# A Function that generates
# and returns the binary string
def build_binary_str(p, q, r):

    # P: Frequency of consecutive
    # characters with sum 0
    # Q: Frequency of consecutive
    # characters with sum 1
    # R: Frequency of consecutive
    # characters with sum 2
    ans = ""

    # If no consecutive
    # character adds up to 1
    if (q == 0):

        # Not possible if both P
        # and Q are non - zero
        if (p != 0 and r != 0):
            return "-1"

        else:

            # If P is not equal to 0
            if (p):

                # Append 0 P + 1 times
                temp = ""
                for i in range(p + 1):
                    temp += '0'

                ans = temp

            else:

                # Append 1 R + 1 times
                temp = ""
                for i in range(r + 1):
                    temp += '1'

                ans = temp

    else:

        # Append "01" to satisfy Q
        for i in range(1, q + 2):
            if (i % 2 == 0):
                ans += '0'
            else:
                ans += '1'

        # Append "0" P times
        temp = ""
        for i in range(p):
            temp += '0'

        st = ""
        st += ans[0]
        st += temp

        for i in range(1, len(ans)):
            st += ans[i]

        ans = st

        # Append "1" R times
        temp = ""
        for i in range(r):
            temp += '1'

        ans = temp + ans

    return ans

# Driver Code
if __name__ == '__main__':

    p = 1
    q = 2
    r = 2

    print(build_binary_str(p, q, r))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program to generate a binary
// String with given frequencies
// of sums of consecutive
// pair of characters
using System;
class GFG{

// A Function that generates
// and returns the binary String
static String build_binary_str(int p,
                               int q, int r)
{
  // P: Frequency of consecutive
  // characters with sum 0
  // Q: Frequency of consecutive
  // characters with sum 1
  // R: Frequency of consecutive
  // characters with sum 2
  String ans = "";

  // If no consecutive
  // character adds up to 1
  if (q == 0)
  {
    // Not possible if both P
    // and Q are non - zero
    if (p != 0 && r != 0)
    {
      return "-1";
    }

    else
    {         
      // If P is not equal to 0
      if (p > 0)
      {
        // Append 0 P + 1 times
        ans = Strings(p + 1, '0');
      }
      else
      {
        // Append 1 R + 1 times
        ans = Strings(r + 1, '1');
      }
    }
  }
  else
  {
    // Append "01" to satisfy Q
    for (int i = 1; i <= q + 1; i++)
    {
      if (i % 2 == 0)
      {
        ans += '0';
      }
      else
      {
        ans += '1';
      }
    }

    // Append "0" P times
    ans = ans.Substring(0, 1) +
          Strings(p, '0') +
          ans.Substring(1);

    // Append "1" R times
    ans = Strings(r, '1') + ans;
  }
  return ans;
}

  static String Strings(int p, char c)
  {
    String ans = "";
    for (int i = 0; i < p; i++)
      ans += c;
    return ans;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int p = 1, q = 2, r = 2;
    Console.Write(build_binary_str(p,
                                   q, r));
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to generate a binary
// string with given frequencies
// of sums of consecutive
// pair of characters

// A Function that generates
// and returns the binary string
function build_binary_str(p, q, r)
{

    // P: Frequency of consecutive
    // characters with sum 0
    // Q: Frequency of consecutive
    // characters with sum 1
    // R: Frequency of consecutive
    // characters with sum 2
    let ans = "";

    // If no consecutive
    // character adds up to 1
    if (q == 0) {

        // Not possible if both P
        // and Q are non - zero
        if (p != 0 && r != 0) {
            return "-1";
        }

        else {

            // If P is not equal to 0
            if (p) {

                // Append 0 P + 1 times
                ans = new Array(p + 1, '0');
            }
            else {
                // Append 1 R + 1 times
                ans = String(r + 1, '1');
            }
        }
    }
    else {

        // Append "01" to satisfy Q
        for (let i = 1; i <= q + 1; i++) {
            if (i % 2 == 0) {
                ans += '0';
            }
            else {
                ans += '1';
            }
        }

        // Append "0" P times
        ans = ans.substr(0, 1) + Strings(p, '0') + ans.substr(1);

        // Append "1" R times
        ans = Strings(r, '1') + ans;
    }
    return ans;
}

function Strings(p, c)
{
    let ans = "";
    for (let i = 0; i < p; i++)
        ans += c;
    return ans;
}

// Driver Code
let p = 1, q = 2, r = 2;
document.write(build_binary_str(p, q, r));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
111001
```

**时间复杂度:** *O(P + Q + R)*