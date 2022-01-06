# 最小翻转，使所有 1 在右边，0 在左边

> 原文:[https://www . geesforgeks . org/minimum-flips-to-make-all-1s in-right-and-0s in-left/](https://www.geeksforgeeks.org/minimum-flips-to-make-all-1s-in-right-and-0s-in-left/)

给定[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **字符串**，任务是找到需要翻转的最小字符数，使所有 **1** s 位于右侧， **0** s 位于左侧。

**示例:**

> **输入:** str = "100101"
> **输出:** 2
> **解释:**
> 翻转 str[0]，str[4]修改 str = "000111 "。因此，所需的输出为 2。
> 
> **输入:**S =“00101001”
> **输出:** 2
> **解释:**
> 翻转 str[2]，str[4]修改 str =“00000001”。因此，所需的输出为 2。

**进场:**思路是统计该弦各指标右侧 **0** s 的个数，统计该弦各指标左侧 **1** s 的个数。按照以下步骤解决问题:

*   初始化一个变量，比如 **cntzero** ，以存储给定字符串中 **0** 的总计数。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)并计算给定字符串中 **0** 的总数。
*   如果给定字符串中的 **cntzero** 为 **0** ，或者等于字符串的长度，则结果为 **0** 。
*   遍历字符串，对于每个索引，找到索引左侧的 **1** s 的计数和索引右侧的 **0** s 的计数之和。
*   从得到的所有和中找出最小值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum count
// of flips required to make all 1s on
// the right and all 0s on the left of
// the given string
int minimumCntOfFlipsRequired(string str)
{
    // Stores length of str
    int n = str.length();

    // Store count of 0s in the string
    int zeros = 0;

    // Traverse the string
    for (int i = 0; i < n; i++) {

        // If current character is 0
        if (str[i] == '0') {

            // Update zeros
            zeros++;
        }
    }

    // If count of 0s in the string
    // is 0 or n
    if (zeros == 0 || zeros == n) {
        return 0;
    }

    // Store minimum count of flips
    // required to make all 0s on
    // the left and all 1s on the right
    int minFlips = INT_MAX;

    // Stores count of 1s on the left
    // of each index
    int currOnes = 0;

    // Stores count of flips required to make
    // string monotonically increasing
    int flips;

    // Traverse the string
    for (int i = 0; i < n; i++) {

        // If current character
        // is 1
        if (str[i] == '1') {

            // Update currOnes
            currOnes++;
        }

        // Update flips
        flips = currOnes + (zeros - (i + 1 - currOnes));

        // Update the minimum
        // count of flips
        minFlips = min(minFlips, flips);
    }

    return minFlips;
}

// Driver Code
int main()
{
    string str = "100101";
    cout << minimumCntOfFlipsRequired(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.io.*;

class GFG {

    // Function to find the minimum count of flips
    // required to make all 1s on the right and
    // all 0s on the left of the given string
    public static int minimumCntOfFlipsRequired(
        String str)
    {
        // Stores length of str
        int n = str.length();

        // Store count of 0s in the string
        int zeros = 0;

        // Traverse the string
        for (int i = 0; i < n; i++) {

            // If current character is 0
            if (str.charAt(i) == '0') {

                // Update zeros
                zeros++;
            }
        }

        // If count of 0s in the string
        // is 0 or n
        if (zeros == 0 || zeros == n) {
            return 0;
        }

        // Store minimum count of flips
        // required to make all 0s on
        // the left and 1s on the right
        int minFlips = Integer.MAX_VALUE;

        // Stores count of 1s on the left
        // side of each index
        int currOnes = 0;

        // Stores count of flips required to make
        // all 0s on the left and 1s on the right
        int flips;

        // Traverse the string
        for (int i = 0; i < n; i++) {

            // If current character is 1
            if (str.charAt(i) == '1') {

                // Update currOnes
                currOnes++;
            }

            // Update flips
            flips = currOnes + (zeros - (i + 1 - currOnes));

            // Update the minimum
            // count of flips
            minFlips = Math.min(minFlips, flips);
        }

        return minFlips;
    }

    // Driver code
    public static void main(String[] args)
    {
        String s1 = "100101";
        System.out.println(minimumCntOfFlipsRequired(s1));
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the minimum count
# of flips required to make all 1s on
# the right and all 0s on the left of
# the given string
def minimumCntOfFlipsRequired(str):

    # Stores length of str
    n = len(str);

    # Store count of 0s in the string
    zeros = 0;

    # Traverse the string
    for i in range(n):

        # If current character
        # is 0
        if (str[i] == '0'):

            # Update zeros
            zeros += 1;

    # If count of 0s in the string
    # is 0 or n
    if (zeros == 0 or zeros == n):
        return 0;

    # Store minimum count of flips
    # required to make all 0s on the
    # left and all 1s on the right
    minFlips = 10000001;

    # Stores count of 1s on the left
    # of each index
    currOnes = 0;

    # Stores count of flips required to make
    # all 0s on the left and all 1s on the right
    flips = 0;

    # Traverse the string
    for i in range(n):

        # If current character is 1
        if (str[i] == '1'):

            # Update currOnes
            currOnes += 1;

        # Update flips
        flips = currOnes + (zeros - (i + 1 - currOnes));

        # Update the minimum
        # count of flips
        minFlips = min(minFlips, flips);

    return minFlips;

# Driver Code
if __name__ == '__main__':
    str = "100101";
    print(minimumCntOfFlipsRequired(str));
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to find the minimum count of flips
// required to make all 1s on the right and
// all 0s on the left of the given string
public static int minimumCntOfFlipsRequired(string str)
{

    // Stores length of str
    int n = str.Length;

    // Store count of 0s in the string
    int zeros = 0;

    // Traverse the string
    for(int i = 0; i < n; i++)
    {

        // If current character is 0
        if (str[i] == '0')
        {

            // Update zeros
            zeros++;
        }
    }

    // If count of 0s in the string
    // is 0 or n
    if (zeros == 0 || zeros == n)
    {
        return 0;
    }

    // Store minimum count of flips
    // required to make all 0s on
    // the left and 1s on the right
    int minFlips = Int32.MaxValue;

    // Stores count of 1s on the left
    // side of each index
    int currOnes = 0;

    // Stores count of flips required
    // to make all 0s on the left and
    // 1s on the right
    int flips;

    // Traverse the string
    for(int i = 0; i < n; i++)
    {

        // If current character is 1
        if (str[i] == '1')
        {

            // Update currOnes
            currOnes++;
        }

        // Update flips
        flips = currOnes +
             (zeros - (i + 1 - currOnes));

        // Update the minimum
        // count of flips
        minFlips = Math.Min(minFlips, flips);
    }
    return minFlips;
}

// Driver code
public static void Main()
{
    string s1 = "100101";

    Console.WriteLine(minimumCntOfFlipsRequired(s1));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

    // Function to find the minimum count of flips
    // required to make all 1s on the right and
    // all 0s on the left of the given string
   function minimumCntOfFlipsRequired(str)
    {
        // Stores length of str
        let n = str.length;

        // Store count of 0s in the string
        let zeros = 0;

        // Traverse the string
        for (let i = 0; i < n; i++) {

            // If current character is 0
            if (str[i] == '0') {

                // Update zeros
                zeros++;
            }
        }

        // If count of 0s in the string
        // is 0 or n
        if (zeros == 0 || zeros == n) {
            return 0;
        }

        // Store minimum count of flips
        // required to make all 0s on
        // the left and 1s on the right
        let minFlips = Number.MAX_VALUE;

        // Stores count of 1s on the left
        // side of each index
        let currOnes = 0;

        // Stores count of flips required to make
        // all 0s on the left and 1s on the right
        let flips;

        // Traverse the string
        for (let i = 0; i < n; i++) {

            // If current character is 1
            if (str[i] == '1') {

                // Update currOnes
                currOnes++;
            }

            // Update flips
            flips = currOnes + (zeros - (i + 1 - currOnes));

            // Update the minimum
            // count of flips
            minFlips = Math.min(minFlips, flips);
        }

        return minFlips;
    }

    // Driver Code

    let s1 = "100101";
    document.write(minimumCntOfFlipsRequired(s1));

</script>
```

**Output**

```
2
```

***时间复杂度:** O(N)，其中 N 为弦的长度*
***辅助空间:** O(1)*