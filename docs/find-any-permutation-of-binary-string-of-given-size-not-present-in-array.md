# 查找数组中不存在的给定大小的二进制字符串的任何排列

> 原文:[https://www . geesforgeks . org/find-任意排列给定大小的二进制字符串-不存在于数组中/](https://www.geeksforgeeks.org/find-any-permutation-of-binary-string-of-given-size-not-present-in-array/)

给定一个由 **N** 个不同的二进制字符串组成的数组 **arr[]** ，每个二进制字符串都有 **N** 个字符，任务是找到任何有 **N** 个字符的二进制字符串，这样它就不会出现在给定的数组 **arr[]** 中。

**示例:**

> **输入:**arr[]= {“10”，“01”}
> **输出:** 00
> **说明:**数组 arr[]中没有出现字符串“00”。另一个有效的字符串可以是“11”，它也不会出现在 arr[]数组中。
> 
> **输入:**arr[]{“111”、“011”、“001”}
> **输出:** 101
> **说明:**数组 arr[]中没有出现字符串“101”。另一个有效的字符串是“000”、“010”、“100”和“110”。

**天真方法:**给定的问题可以通过[生成所有具有 **N** 位](https://www.geeksforgeeks.org/generate-all-the-binary-strings-of-n-bits/)的二进制字符串并返回 1 <sup>st</sup> 字符串以使其不出现在给定的数组**arr【】**中来解决。

***时间复杂度:**O(2<sup>N</sup>* N<sup>2</sup>)*
***辅助空间:** O(N)*

**有效方法:**给定的问题可以通过使用类似于康托对角变元的方法来优化。可以观察到，结果字符串必须至少有一个位不同于**arr【】**中的所有字符串。因此，生成的二进制字符串可以通过将 1 <sup>st</sup> 字符串的 1 <sup>st</sup> 元素的[补码](https://www.geeksforgeeks.org/1s-2s-complement-binary-number/)作为 1 <sup>st</sup> 元素，将 2 <sup>nd</sup> 字符串的 2 <sup>nd</sup> 元素的补码作为 2 <sup>nd</sup> 元素，以此类推。以下是要遵循的步骤:

*   创建一个字符串**和**，存储结果字符串。最初，它是空的。
*   以对角线顺序遍历给定的字符串，即 1 <sup>st</sup> 字符串的 1 <sup>st</sup> 元素，2 <sup>nd</sup> 字符串的 2 <sup>nd</sup> 元素，以此类推，并将当前索引处的值的补码追加到字符串 **ans** 中。
*   在遍历完整数组**arr【】**后，存储在**和**中的字符串是所需的有效字符串之一。

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find a binary string of
// N bits that does not occur in the
// given array arr[]
string findString(vector<string>& arr, int N)
{
    // Stores the resultant string
    string ans = "";

    // Loop to iterate over all the given
    // strings in a diagonal order
    for (int i = 0; i < N; i++) {

        // Append the complement of element
        // at current index into ans
        ans += arr[i][i] == '0' ? '1' : '0';
    }

    // Return Answer
    return ans;
}

// Driver code
int main()
{
    vector<string> arr{ "111", "011", "001" };
    int N = arr.size();

    cout << findString(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach

import java.io.*;

class GFG {

      // Function to find a binary string of
    // N bits that does not occur in the
    // givrn array arr[]
    static String findString(String arr[], int N)
    {
        // Stores the resultant string
        String ans = "";

        // Loop to iterate over all the given
        // strings in a diagonal order
        for (int i = 0; i < N; i++) {

            // Append the complement of element
            // at current index into ans
            ans += arr[i].charAt(i) == '0' ? '1' : '0';
        }

        // Return Answer
        return ans;
    }

    // Driver code
    public static void main (String[] args) {
           String arr[] = { "111", "011", "001" };
        int N = arr.length;

        System.out.println(findString(arr, N));
    }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python 3 Program for the above approach

# Function to find a binary string of
# N bits that does not occur in the
# givrn array arr[]
def findString(arr, N):

    # Stores the resultant string
    ans = ""

    # Loop to iterate over all the given
    # strings in a diagonal order
    for i in range(N):

        # Append the complement of element
        # at current index into ans
        ans += '1' if arr[i][i] == '0' else '0'

    # Return Answer
    return ans

# Driver code
if __name__ == '__main__':
    arr = ["111", "011", "001"]
    N = len(arr)

    print(findString(arr, N))

    # This code is contributed by bgangwar59.
```

## C#

```
// C# Program for the above approach
using System;

class GFG {

    // Function to find a binary string of
    // N bits that does not occur in the
    // givrn array arr[]
    static string findString(string[] arr, int N)
    {

        // Stores the resultant string
        string ans = "";

        // Loop to iterate over all the given
        // strings in a diagonal order
        for (int i = 0; i < N; i++) {

            // Append the complement of element
            // at current index into ans
            ans += arr[i][i] == '0' ? '1' : '0';
        }

        // Return Answer
        return ans;
    }

    // Driver code
    public static void Main(String[] args)
    {
        string[] arr = { "111", "011", "001" };
        int N = arr.Length;

        Console.WriteLine(findString(arr, N));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find a binary string of
        // N bits that does not occur in the
        // givrn array arr[]
        function findString(arr, N)
        {

            // Stores the resultant string
            let ans = "";

            // Loop to iterate over all the given
            // strings in a diagonal order
            for (let i = 0; i < N; i++) {

                // Append the complement of element
                // at current index into ans
                ans += arr[i][i] == '0' ? '1' : '0';
            }

            // Return Answer
            return ans;
        }

        // Driver code
        let arr = ["111", "011", "001"];
        let N = arr.length;

        document.write(findString(arr, N));

     // This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
000
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)