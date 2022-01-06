# 最小位翻转，使得每 K 个连续位包含至少一个设置位

> 原文:[https://www . geesforgeks . org/最小位翻转-这样每 k 个连续位至少包含一个设置位/](https://www.geeksforgeeks.org/minimum-bit-flips-such-that-every-k-consecutive-bits-contain-at-least-one-set-bit/)

给定一个二进制字符串 **S** 和一个整数 **K** ，任务是找到所需的最小翻转次数，使得长度为 K 的每个子字符串至少包含一个**‘1’**。
**举例:**

> **输入:** S = "10000001" K = 2
> **输出:** 3
> **解释:**
> 我们只需要对字符串 S 进行 3 次更改(在位置 2、4 和 6)，这样字符串在长度为 2 的每个子字符串中至少包含一个‘1’。
> **输入:**S =“000000”K = 3
> **输出:** 2
> **解释:**
> 我们只需要对字符串 S 进行 3 次修改(在位置 2 和位置 5)，这样字符串在长度为 3 的每个子字符串中至少包含一个‘1’。
> **输入:** S = "111010111" K = 2
> **输出:** 0

**天真方法:**
要解决这个问题，最简单的方法是对长度为 K 的每个子串进行迭代，找到满足给定条件所需的最小翻转次数。
***时间复杂度:** O(N * K)*
**高效进场:**
思路是用[滑动窗口](https://www.geeksforgeeks.org/window-sliding-technique/)进场。

*   设置 **K** 的窗口大小。
*   存储以前出现的索引 1。
*   如果当前位未置位，并且当前 **i <sup>th</sup>** 位与**先前设置位**之间的差值超过 **K** ，则设置当前位并将当前索引存储为先前设置位的索引并继续。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count min flips
int CountMinFlips(string s, int n,
                  int k)
{

    // To store the count of minimum
    // flip required
    int cnt = 0;

    // To store the position of last '1'
    int prev = -1;

    for (int i = 0; i < k; i++) {

        // Track last position of '1'
        // in current window of size k
        if (s[i] == '1') {
            prev = i;
        }
    }

    // If no '1' is present in the current
    // window of size K
    if (prev == -1) {
        cnt++;

        // Set last index of window '1'
        s[k - 1] = '1';

        // Track previous '1'
        prev = k - 1;
    }

    // Traverse the given string
    for (int i = k; i < n; i++) {

        // If the current bit is not set,
        // then the condition for flipping
        // the current bit
        if (s[i] != '1') {
            if (prev <= (i - k)) {

                // Set i'th index to '1'
                s[i] = '1';

                // Track previous one
                prev = i;

                // Increment count
                cnt++;
            }
        }

        // Else update the prev set bit
        // position to current position
        else {
            prev = i;
        }
    }

    // Return the final count
    return (cnt);
}

// Driver Code
int main()
{
    // Given binary string
    string str = "10000001";

    // Size of given string str
    int n = str.size();

    // Window size
    int k = 2;

    // Function Call
    cout << CountMinFlips(str, n, k)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count min flips
static int CountMinFlips(char []s, int n,
                                   int k)
{

    // To store the count of minimum
    // flip required
    int cnt = 0;

    // To store the position of last '1'
    int prev = -1;

    for(int i = 0; i < k; i++)
    {

       // Track last position of '1'
       // in current window of size k
       if (s[i] == '1')
       {
           prev = i;
       }
    }

    // If no '1' is present in the current
    // window of size K
    if (prev == -1)
    {
        cnt++;

        // Set last index of window '1'
        s[k - 1] = '1';

        // Track previous '1'
        prev = k - 1;
    }

    // Traverse the given String
    for(int i = k; i < n; i++)
    {

       // If the current bit is not set,
       // then the condition for flipping
       // the current bit
       if (s[i] != '1')
       {
           if (prev <= (i - k))
           {

               // Set i'th index to '1'
               s[i] = '1';

               // Track previous one
               prev = i;

               // Increment count
               cnt++;
           }
       }

       // Else update the prev set bit
       // position to current position
       else
       {
           prev = i;
       }
    }

    // Return the final count
    return (cnt);
}

// Driver Code
public static void main(String[] args)
{

    // Given binary String
    String str = "10000001";

    // Size of given String str
    int n = str.length();

    // Window size
    int k = 2;

    // Function Call
    System.out.print(CountMinFlips(
                     str.toCharArray(), n, k) + "\n");
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 code to count minimum no.
# of flips required such that
# every substring of length K
# contain at least one '1'.

# Function to count min flips
def CountMinFlips(s, n, k):
    cnt = 0
    prev = -1
    for i in range(0, k):
        # Track last position of '1'
        # in current window of size k
        if(s[i]=='1'):
            prev = i;

    # means no '1' is present
    if(prev == -1):
        cnt += 1
        # track previous '1'
        prev = k-1;

    for i in range(k, n):
        if(s[i] != '1'):
            if( prev <= (i-k) ):

                # track previous one
                prev = i;

                # increment count
                cnt += 1
        else:
            prev = i

    return(cnt);

# Driver code
s = "10000001"
n = len(s)
k = 2
print(CountMinFlips(s, n, k))
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to count min flips
static int CountMinFlips(char []s, int n,
                                   int k)
{

    // To store the count of minimum
    // flip required
    int cnt = 0;

    // To store the position of last '1'
    int prev = -1;

    for(int i = 0; i < k; i++)
    {

        // Track last position of '1'
        // in current window of size k
        if (s[i] == '1')
        {
            prev = i;
        }
    }

    // If no '1' is present in the current
    // window of size K
    if (prev == -1)
    {
        cnt++;

        // Set last index of window '1'
        s[k - 1] = '1';

        // Track previous '1'
        prev = k - 1;
    }

    // Traverse the given String
    for(int i = k; i < n; i++)
    {

        // If the current bit is not set,
        // then the condition for flipping
        // the current bit
        if (s[i] != '1')
        {
            if (prev <= (i - k))
            {

                // Set i'th index to '1'
                s[i] = '1';

                // Track previous one
                prev = i;

                // Increment count
                cnt++;
            }
        }

        // Else update the prev set bit
        // position to current position
        else
        {
            prev = i;
        }
    }

    // Return the readonly count
    return (cnt);
}

// Driver Code
public static void Main(String[] args)
{

    // Given binary String
    String str = "10000001";

    // Size of given String str
    int n = str.Length;

    // Window size
    int k = 2;

    // Function Call
    Console.Write(CountMinFlips(
                  str.ToCharArray(), n, k) + "\n");
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to count min flips
function CountMinFlips(s , n,k)
{

    // To store the count of minimum
    // flip required
    var cnt = 0;

    // To store the position of last '1'
    var prev = -1;

    for(i = 0; i < k; i++)
    {

       // Track last position of '1'
       // in current window of size k
       if (s[i] == '1')
       {
           prev = i;
       }
    }

    // If no '1' is present in the current
    // window of size K
    if (prev == -1)
    {
        cnt++;

        // Set last index of window '1'
        s[k - 1] = '1';

        // Track previous '1'
        prev = k - 1;
    }

    // Traverse the given String
    for(i = k; i < n; i++)
    {

       // If the current bit is not set,
       // then the condition for flipping
       // the current bit
       if (s[i] != '1')
       {
           if (prev <= (i - k))
           {

               // Set i'th index to '1'
               s[i] = '1';

               // Track previous one
               prev = i;

               // Increment count
               cnt++;
           }
       }

       // Else update the prev set bit
       // position to current position
       else
       {
           prev = i;
       }
    }

    // Return the final count
    return (cnt);
}

// Driver Code

    // Given binary String
    var str = "10000001";

    // Size of given String str
    var n = str.length;

    // Window size
    var k = 2;

    // Function Call
    document.write(CountMinFlips(
                     str, n, k) );

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
3
```

**时间复杂度:***O(N+K)*
T5】辅助空间: *O(1)*