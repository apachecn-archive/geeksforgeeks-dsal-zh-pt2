# 通过移除最小子序列

使给定的二进制字符串不递减

> 原文:[https://www . geeksforgeeks . org/make-a-给定的二进制字符串-通过移除最小的子序列非递减/](https://www.geeksforgeeks.org/make-a-given-binary-string-non-decreasing-by-removing-the-smallest-subsequence/)

给定一个大小为 **N** 的[二进制串](https://www.geeksforgeeks.org/tag/binary-string/) **串**，任务是找到最小子序列的长度，这样在擦除子序列后，得到的串将是最长的连续非递减串。

**示例:**

> **输入:** str = "10011"
> **输出:** 1
> **解释:**删除第一个出现的‘1’会产生一个不递减的子序列，即“0011”。
> 
> **输入:** str = "11110000"
> **输出:** 4

**方法:**根据以下观察结果可以解决问题:

> 非递减子序列可以是以下 3 种类型:
> 
> *   案例 1 : 00000…..
> *   案例二:11111…..
> *   案例三:0000…111111…

按照给定的步骤解决问题:

*   [迭代字符串的字符。](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)
*   计算字符串中存在的 **0** 和 **1** 的数量
*   生成形式为**“0000…”的非递减子序列，**所需的最小清除量是字符串中 **1** 的数量
*   生成形式为**“1111…”的非递减子序列，**所需的最小清除量是字符串中 **0** 的计数
*   生成形式为**“0000…1111…”的非递减子序列，**所需的最小清除量可通过以下步骤获得:
    *   考虑将 **1** s 从左边移除，将 **0** s 从绳子的右端移除。
    *   每次迭代后更新最小值。
*   最后，打印在上述三种情况下获得的最小清除量作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// length of smallest subsequence
// required to be removed to make
// the given string non-decreasing
int min_length(string str)
{

    // Length of the string
    int n = str.length();

    // Count of zeros and ones
    int total_zeros = 0;
    int total_ones = 0;

    // Traverse the string
    for (int i = 0; i < n; i++) {
        if (str[i] == '0')
            total_zeros++;
        else
            total_ones++;
    }

    // Count minimum removals to
  // obtain strings of the form
  // "00000...." or "11111..."
    int ans = min(total_zeros, total_ones);

    int cur_zeros = 0, cur_ones = 0;

    for (char x : str) {

        // Increment count
        if (x == '0')
            cur_zeros++;
        else
            cur_ones++;

        // Remove 1s and remaining 0s
        ans = min(ans, cur_ones
                  + (total_zeros - cur_zeros));
    }

    cout << ans;
}

// Driver Code
int main()
{
    string str = "10011";
    min_length(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.io.*;

class GFG
{

  // Function to return the
  // length of smallest subsequence
  // required to be removed to make
  // the given string non-decreasing
  public static void min_length(String str)
  {

    // Length of the string
    int n = str.length();

    // Count of zeros and ones
    int total_zeros = 0;
    int total_ones = 0;

    // Traverse the string
    for (int i = 0; i < n; i++) {
      if (str.charAt(i) == '0'){
        total_zeros++;
      }
      else{
        total_ones++;
      }
    }

    // Count minimum removals to
    // obtain strings of the form
    // "00000...." or "11111..."
    int ans = Math.min(total_zeros, total_ones);
    int cur_zeros = 0, cur_ones = 0;
    for (int i = 0; i<str.length(); i++)
    {

      // Increment count
      char x = str.charAt(i);
      if (x == '0'){
        cur_zeros++;
      }
      else{
        cur_ones++;
      }

      // Remove 1s and remaining 0s
      ans = Math.min(ans, cur_ones
                     + (total_zeros - cur_zeros));
    }

    System.out.println(ans);
  }

  // Driver Code
  public static void main (String[] args)
  {
    String str = "10011";
    min_length(str);
  }
}

// This code is contributed by rohitsingh07052
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to return the
# length of smallest subsequence
# required to be removed to make
# the given string non-decreasing
def min_length(str):

    # Length of the string
    n = len(str)

    # Count of zeros and ones
    total_zeros = 0
    total_ones = 0

    # Traverse the string
    for i in range(n):
        if (str[i] == '0'):
            total_zeros += 1
        else:
            total_ones += 1

    # Count minimum removals to
  # obtain strings of the form
  # "00000...." or "11111..."
    ans = min(total_zeros, total_ones)
    cur_zeros = 0
    cur_ones = 0
    for x in str:

        # Increment count
        if (x == '0'):
            cur_zeros += 1
        else:
            cur_ones += 1

        # Remove 1s and remaining 0s
        ans = min(ans, cur_ones + (total_zeros - cur_zeros))
    print(ans)

# Driver Code
if __name__ == '__main__':
    str = "10011"
    min_length(str)

    # This code is contributed by SURENDRA_GENGWAR.
```

## C#

```
// C# program for
// the above approach
using System;

class GFG{

// Function to return the
// length of smallest subsequence
// required to be removed to make
// the given string non-decreasing
public static void min_length(string str)
{

    // Length of the string
    int n = str.Length;

    // Count of zeros and ones
    int total_zeros = 0;
    int total_ones = 0;

    // Traverse the string
    for(int i = 0; i < n; i++)
    {
        if (str[i] == '0')
        {
            total_zeros++;
        }
        else
        {
            total_ones++;
        }
    }

    // Count minimum removals to
    // obtain strings of the form
    // "00000...." or "11111..."
    int ans = Math.Min(total_zeros, total_ones);
    int cur_zeros = 0, cur_ones = 0;
    for(int i = 0; i < str.Length; i++)
    {

        // Increment count
        char x = str[i];
        if (x == '0')
        {
            cur_zeros++;
        }
        else
        {
            cur_ones++;
        }

        // Remove 1s and remaining 0s
        ans = Math.Min(ans, cur_ones +
                      (total_zeros - cur_zeros));
    }
    Console.WriteLine(ans);
}

// Driver code
static public void Main()
{
    string str = "10011";
    min_length(str);
}
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>

// Javascript program for
// the above approach

// Function to return the
// length of smallest subsequence
// required to be removed to make
// the given string non-decreasing
function min_length(str)
{

    // Length of the string
    var n = str.length;

    // Count of zeros and ones
    var total_zeros = 0;
    var total_ones = 0;

    // Traverse the string
    for (var i = 0; i < n; i++) {
        if (str[i] == '0')
            total_zeros++;
        else
            total_ones++;
    }

    // Count minimum removals to
  // obtain strings of the form
  // "00000...." or "11111..."
    var ans = Math.min(total_zeros, total_ones);

    var cur_zeros = 0, cur_ones = 0;

    for( var i =0; i< str.length; i++){

        // Increment count
        if (str[i] == '0')
            cur_zeros++;
        else
            cur_ones++;

        // Remove 1s and remaining 0s
        ans = Math.min(ans, cur_ones
                  + (total_zeros - cur_zeros));
    }

    document.write( ans);
}

// Driver Code
var str = "10011";
min_length(str);

</script>
```

**Output**

```
1
```

***时间复杂度:**O(N)**T5
*T8】辅助空间: O(1)****