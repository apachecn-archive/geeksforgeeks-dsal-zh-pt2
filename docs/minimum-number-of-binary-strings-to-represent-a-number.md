# 表示一个数字的二进制字符串的最小数量

> 原文:[https://www . geesforgeks . org/最小二进制字符串数表示数字/](https://www.geeksforgeeks.org/minimum-number-of-binary-strings-to-represent-a-number/)

给定一个数字 **N** 。任务是找到将给定数字表示为二进制字符串之和所需的最小二进制字符串数。
**例:**

> **输入:** 131
> **输出:**所需二进制字符串的最小数量:3
> 111 10 10
> **输入:** 564
> **输出:**所需二进制字符串的最小数量:6
> 111 111 111 111 110 10

**进场:**

*   在数组中存储给定数字的所有数字。
*   找出数组中的最大数字。这个最大值(maxi)表示表示给定数字所需的二进制字符串的数量。
*   现在，通过大量替换 0 和 1 来找到**最大**数。

以下是上述方法的实现:

## C++

```
// C++ program to find the minimum number of
// binary strings to represent a number
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number of
// binary strings to represent a number
void minBinary(int n)
{
    int digit[10], len = 0;

    while (n > 0) {
        digit[len++] = n % 10;
        n /= 10;
    }

    // Storing digits in correct order
    reverse(digit, digit + len);

    int ans = 0;

    // Find the maximum digit in the array
    for (int i = 0; i < len; i++) {
        ans = max(ans, digit[i]);
    }

    cout << "Minimum Number of binary strings needed: "
         << ans << endl;

    // Traverse for all the binary strings
    for (int i = 1; i <= ans; i++)
    {
        int num = 0;
        for (int j = 0; j < len; j++)
        {
            // If digit at jth position is greater
            // than 0 then substitute 1
            if (digit[j] > 0) {

                num = num * 10 + 1;
                digit[j]--;
            }
            else {
                num *= 10;
            }
        }
        cout << num << " ";
    }

}

// Driver code
int main()
{
    int n = 564;

    minBinary(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum number of
// binary Strings to represent a number
import java.util.*;

class GFG
{

    // Function to find the minimum number of
    // binary Strings to represent a number
    static void minBinary(int n)
    {
        int[] digit = new int[10];
        int len = 0;

        while (n > 0)
        {
            digit[len++] = n % 10;
            n /= 10;
        }

        // Storing digits in correct order
        digit = reverse(digit, 0, len - 1);

        int ans = 0;

        // Find the maximum digit in the array
        for (int i = 0; i < len; i++)
        {
            ans = Math.max(ans, digit[i]);
        }

        System.out.print("Minimum Number of binary" +
                   " Strings needed: " + ans + "\n");

        // Traverse for all the binary Strings
        for (int i = 1; i <= ans; i++)
        {
            int num = 0;
            for (int j = 0; j < len; j++)
            {
                // If digit at jth position is greater
                // than 0 then substitute 1
                if (digit[j] > 0)
                {
                    num = num * 10 + 1;
                    digit[j]--;
                }
                else
                {
                    num *= 10;
                }
            }
            System.out.print(num + " ");
        }
    }

    static int[] reverse(int str[],
                         int start, int end)
    {

        // Temporary variable to store character
        int temp;
        while (start <= end)
        {
            // Swapping the first and last character
            temp = str[start];
            str[start] = str[end];
            str[end] = temp;
            start++;
            end--;
        }
        return str;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 564;

        minBinary(n);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the minimum number of
# binary strings to represent a number

# Function to find the minimum number of
# binary strings to represent a number
def minBinary(n):
    digit = [0 for i in range(3)]
    len = 0

    while (n > 0):
        digit[len] = n % 10
        len += 1
        n //= 10

    # Storing digits in correct order
    digit = digit[::-1]

    ans = 0

    # Find the maximum digit in the array
    for i in range(len):
        ans = max(ans, digit[i])

    print("Minimum Number of binary strings needed:", ans)

    # Traverse for all the binary strings
    for i in range(1, ans + 1, 1):
        num = 0
        for j in range(0, len, 1):

            # If digit at jth position is greater
            # than 0 then substitute 1
            if (digit[j] > 0):
                num = num * 10 + 1
                digit[j] -= 1
            else:
                num *= 10
        print(num, end = " ")

# Driver code
if __name__ == '__main__':
    n = 564

    minBinary(n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find the minimum number of
// binary Strings to represent a number
using System;

class GFG
{

    // Function to find the minimum number of
    // binary Strings to represent a number
    static void minBinary(int n)
    {
        int[] digit = new int[10];
        int len = 0;

        while (n > 0)
        {
            digit[len++] = n % 10;
            n /= 10;
        }

        // Storing digits in correct order
        digit = reverse(digit, 0, len - 1);

        int ans = 0;

        // Find the maximum digit in the array
        for (int i = 0; i < len; i++)
        {
            ans = Math.Max(ans, digit[i]);
        }

        Console.Write("Minimum Number of binary" +
                " Strings needed: " + ans + "\n");

        // Traverse for all the binary Strings
        for (int i = 1; i <= ans; i++)
        {
            int num = 0;
            for (int j = 0; j < len; j++)
            {
                // If digit at jth position is greater
                // than 0 then substitute 1
                if (digit[j] > 0)
                {
                    num = num * 10 + 1;
                    digit[j]--;
                }
                else
                {
                    num *= 10;
                }
            }
            Console.Write(num + " ");
        }
    }

    static int[] reverse(int []str,
                         int start, int end)
    {

        // Temporary variable to store character
        int temp;
        while (start <= end)
        {
            // Swapping the first and
            // last character
            temp = str[start];
            str[start] = str[end];
            str[end] = temp;
            start++;
            end--;
        }
        return str;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 564;

        minBinary(n);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to
// find the minimum number of
// binary Strings to represent
// a number

    // Function to find the minimum number of
    // binary Strings to represent a number
    function minBinary(n)
    {
        var digit = Array(10).fill(0);
        var len = 0;

        while (n > 0) {
            digit[len++] = n % 10;
            n = parseInt(n/10);
        }

        // Storing digits in correct order
        digit = reverse(digit, 0, len - 1);

        var ans = 0;

        // Find the maximum digit in the array
        for (i = 0; i < len; i++) {
            ans = Math.max(ans, digit[i]);
        }

        document.write("Minimum Number of binary"
        + " Strings needed: " + ans + "<br/>");

        // Traverse for all the binary Strings
        for (i = 1; i <= ans; i++)
        {
            var num = 0;
            for (j = 0; j < len; j++)
            {
                // If digit at jth position is greater
                // than 0 then substitute 1
                if (digit[j] > 0) {
                    num = num * 10 + 1;
                    digit[j]--;
                } else {
                    num *= 10;
                }
            }
            document.write(num + " ");
        }
    }

    function reverse(str , start , end) {

        // Temporary variable to store character
        var temp;
        while (start <= end) {
            // Swapping the first and last character
            temp = str[start];
            str[start] = str[end];
            str[end] = temp;
            start++;
            end--;
        }
        return str;
    }

    // Driver code

        var n = 564;

        minBinary(n);

// This code contributed by umadevi9616

</script>
```

**输出:**

```
Minimum No of binary strings needed: 6
111 111 111 111 110 10 
```

**时间复杂度:** O(N)

**辅助空间:** O(1)