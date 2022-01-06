# 给定字符串中反向双音素子串的计数

> 原文:[https://www . geesforgeks . org/count-of-reverse-bitonic-substrings-in-a-给定字符串/](https://www.geeksforgeeks.org/count-of-reverse-bitonic-substrings-in-a-given-string/)

给定一个字符串 **S** ，任务是统计给定字符串中 [**反向双音素子字符串**](https://www.geeksforgeeks.org/check-if-a-given-string-is-a-reverse-bitonic-string-or-not/) 的数量。

> **反向双音素子字符串:**字符串中字符的 ASCII 值遵循以下任一模式的字符串:
> 
> *   严格递增
> *   严格递减
> *   *描述*放松然后增加

**示例:**

> **输入:** S = "bade"
> **输出:** 10
> **解释:**
> 所有可能的长度为 1 的子串，{“b”、“a”、“d”、“e”}总是反向双音素。
> 长度为 2 的反向双音素子串是{“ba”、“ad”、“de”}。
> 长度为 3 的反向双音素子串是{“坏的”、“ade”}。
> 只有长度为 4 的反双音素子串才是“bade”。
> 因此，反向双音素子串的计数为 10。
> 
> **输入:**S = " ABC "
> T3】输出: 6

**方法:**
方法是[生成给定字符串的所有可能的子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)，并对每个子字符串执行以下步骤来解决问题:

*   遍历字符串，检查每个字符的下一个字符的 ASCII 值是否小于当前字符的 ASCII 值。
*   如果在任何时候，下一个字符的 ASCII 值大于当前字符的 ASCII 值，则从该索引开始遍历，并从现在开始为每个字符检查下一个字符的 ASCII 值是否大于当前字符的 ASCII 值。
*   如果在到达子字符串末尾之前，下一个字符的 ASCII 值小于当前字符的 ASCII 值，则忽略该子字符串。
*   如果到达子串的末尾，增加**计数**。
*   对所有子字符串完成上述所有步骤后，打印**计数的最终值。**

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the number
// of reverse bitonic substrings
int CountsubString(char str[], int n)
{
    // Stores the count
    int c = 0;

    // All possible lengths of substrings
    for (int len = 1; len <= n; len++) {

        // Starting point of a substring
        for (int i = 0; i <= n - len; i++) {

            // Ending point of a substring
            int j = i + len - 1;

            char temp = str[i], f = 0;

            // Condition for reverse
            // bitonic substrings of
            // length 1
            if (j == i) {

                c++;
                continue;
            }

            int k = i + 1;

            // Check for decreasing sequence
            while (temp > str[k] && k <= j) {

                temp = str[k];

                k++;
            }

            // If end of substring
            // is reached
            if (k > j) {
                c++;
                f = 2;
            }

            // For increasing sequence
            while (temp < str[k] && k <= j
                && f != 2) {

                temp = str[k];

                k++;
            }

            // If end of substring
            // is reached
            if (k > j && f != 2) {
                c++;
                f = 0;
            }
        }
    }

    // Return the number
    // of bitonic substrings
    return c;
}

// Driver Code
int main()
{
    char str[] = "bade";
    cout << CountsubString(str, strlen(str));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to calculate the number
// of reverse bitonic substrings
public static int CountsubString(char[] str,
                                 int n)
{

    // Stores the count
    int c = 0;

    // All possible lengths of substrings
    for(int len = 1; len <= n; len++)
    {

        // Starting point of a substring
        for(int i = 0; i <= n - len; i++)
        {

            // Ending point of a substring
            int j = i + len - 1;

            char temp = str[i], f = 0;

            // Condition for reverse
            // bitonic substrings of
            // length 1
            if (j == i)
            {
                c++;
                continue;
            }

            int k = i + 1;

            // Check for decreasing sequence
            while (temp > str[k] && k <= j)
            {
                temp = str[k];
                k++;
            }

            // If end of substring
            // is reached
            if (k > j)
            {
                c++;
                f = 2;
            }

            // For increasing sequence
            while (k <= j && temp < str[k] &&
                   f != 2)
            {
                temp = str[k];
                k++;
            }

            // If end of substring
            // is reached
            if (k > j && f != 2)
            {
                c++;
                f = 0;
            }
        }
    }

    // Return the number
    // of bitonic substrings
    return c;
}

// Driver code
public static void main(String[] args)
{
    char str[] = { 'b', 'a', 'd', 'e' };

    System.out.println(CountsubString(
                       str, str.length));
}
}

// This cdoe is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to calculate the number
# of reverse bitonic substrings
def CountsubString(strr, n):

    # Stores the count
    c = 0

    # All possible lengths of substrings
    for len in range(n + 1):

        # Starting point of a substring
        for i in range(n - len):

            # Ending point of a substring
            j = i + len - 1

            temp = strr[i]
            f = 0

            # Condition for reverse
            # bitonic substrings of
            # length 1
            if (j == i):
                c += 1
                continue

            k = i + 1

            # Check for decreasing sequence
            while (k <= j and temp > strr[k]):
                temp = strr[k]
                k += 1

            # If end of substring
            # is reache
            if (k > j):
                c += 1
                f = 2

            # For increasing sequence
            while (k <= j and f != 2 and
                temp < strr[k]):
                temp = strr[k]
                k += 1

            # If end of substring
            # is reached
            if (k > j and f != 2):
                c += 1
                f = 0

    # Return the number
    # of bitonic substrings
    return c

# Driver Code
if __name__ == '__main__':

    strr = "bade"
    print(CountsubString(strr, len(strr)))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to calculate the number
// of reverse bitonic substrings
public static int CountsubString(char[] str,
                                 int n)
{

    // Stores the count
    int c = 0;

    // All possible lengths of substrings
    for(int len = 1; len <= n; len++)
    {

        // Starting point of a substring
        for(int i = 0; i <= n - len; i++)
        {

            // Ending point of a substring
            int j = i + len - 1;

            char temp = str[i], f = '0';

            // Condition for reverse
            // bitonic substrings of
            // length 1
            if (j == i)
            {
                c++;
                continue;
            }

            int k = i + 1;

            // Check for decreasing sequence
            while (temp > str[k] && k <= j)
            {
                temp = str[k];
                k++;
            }

            // If end of substring
            // is reached
            if (k > j)
            {
                c++;
                f = '2';
            }

            // For increasing sequence
            while (k <= j && temp < str[k] &&
                   f != '2')
            {
                temp = str[k];
                k++;
            }

            // If end of substring
            // is reached
            if (k > j && f != 2)
            {
                c++;
                f = '0';
            }
        }
    }

    // Return the number
    // of bitonic substrings
    return c;
}

// Driver code
public static void Main(String[] args)
{
    char []str = { 'b', 'a', 'd', 'e' };

    Console.WriteLine(CountsubString(
                      str, str.Length) - 1);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Function to calculate the number
// of reverse bitonic substrings
function CountsubString(str, n)
{
    // Stores the count
    var c = 0;

    // All possible lengths of substrings
    for (var len = 1; len <= n; len++) {

        // Starting point of a substring
        for (var i = 0; i <= n - len; i++) {

            // Ending point of a substring
            var j = i + len - 1;

            var temp = str[i], f = 0;

            // Condition for reverse
            // bitonic substrings of
            // length 1
            if (j == i) {

                c++;
                continue;
            }

            var k = i + 1;

            // Check for decreasing sequence
            while (temp > str[k] && k <= j) {

                temp = str[k];

                k++;
            }

            // If end of substring
            // is reached
            if (k > j) {
                c++;
                f = 2;
            }

            // For increasing sequence
            while (temp < str[k] && k <= j
                && f != 2) {

                temp = str[k];

                k++;
            }

            // If end of substring
            // is reached
            if (k > j && f != 2) {
                c++;
                f = 0;
            }
        }
    }

    // Return the number
    // of bitonic substrings
    return c;
}

// Driver Code
var str = "bade".split('');
document.write( CountsubString(str, str.length));

// This code is contributed by importantly.
</script>
```

**输出:**

```
10
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)