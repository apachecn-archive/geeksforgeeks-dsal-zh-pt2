# 用同一组数字找到小于 N 的最大数字

> 原文:[https://www . geesforgeks . org/find-最大数字-小于 n-同位数/](https://www.geeksforgeeks.org/find-largest-number-smaller-than-n-with-same-set-of-digits/)

给定一个字符串形式的数字 **N** 。任务是找到与 N 有相同数字集且小于 N 的最大数字。如果找不到任何这样的数字，则打印“不可能”。

**示例**:

```
Input:  N = "218765"
Output: 218756

Input:  N = "1234"
Output: Not Possible

Input: N = "262345"
Output: 256432
```

以下是对小于 N 的最大数值的一些观察:

1.  如果所有数字都按升序排序，那么输出总是“不可能”。比如 1234。
2.  如果所有的数字都按降序排序，那么我们需要交换最后两位数字。比如 4321。
3.  对于其他情况，我们需要从最右侧处理数字(为什么？因为我们需要找到所有较小数字中最大的一个)。

**算法**:

*   从最右边的数字开始遍历给定的数字，继续遍历，直到找到一个比先前遍历的数字大的数字。例如，如果输入的数字是“262345”，我们就停在 6，因为 6 比前面的数字 5 大。如果我们找不到这样的数字，那么输出就是“不可能”。
*   现在在上面找到的数字“d”的右边搜索比“d”小的最大数字。对于“262345？，6 的右侧包含“2345”。小于 6 的最大数字是 5。
*   交换上面找到的两位数，我们得到上面例子中的“252346”。
*   现在按降序将所有数字从“d”旁边的位置排序到数字的末尾。排序后得到的数字就是输出。对于上面的例子，我们用粗体 25 **2346** 对数字进行排序。我们得到 **256432** ，这是之前输入 **262345** 的较小数字。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find previous number
void findPrevious(string number, int n)
{
    int i, j;

    // I) Start from the right most digit
    // and find the first digit that is
    // smaller than the digit next to it.
    for (i = n - 1; i > 0; i--)
        if (number[i] < number[i - 1])
            break;

    // If no such digit is found
    // then all digits are in ascending order
    // means there cannot be a smallest number
    // with same set of digits
    if (i == 0) {
        cout << "Previous number is not possible";
        return;
    }

    // II) Find the greatest digit on
    // right side of (i-1)'th digit that is
    // smaller than number[i-1]
    int x = number[i - 1], greatest = i;
    for (j = i; j < n; j++)
        if (number[j] < x && number[j] > number[greatest])
            greatest = j;

    // III) Swap the above found smallest digit with number[i-1]
    swap(number[greatest], number[i - 1]);

    // IV) Sort the digits after (i-1) in descending order
    sort(number.begin() + i, number.begin() + n, greater<char>());

    cout << "Greatest smaller number with same set of digits is " << number;

    return;
}

// Driver code
int main()
{
    string digits = "262345";
    int n = digits.length();

    findPrevious(digits, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

    // Function to find previous number
    static void findPrevious(char[] number, int n)
    {
        int i, j;

        // I) Start from the right most digit
        // and find the first digit that is
        // smaller than the digit next to it.
        for (i = n - 1; i > 0; i--)
        {
            if (number[i] < number[i - 1])
            {
                break;
            }
        }

        // If no such digit is found
        // then all digits are in ascending order
        // means there cannot be a smallest number
        // with same set of digits
        if (i == 0)
        {
            System.out.print("Previous number is not possible");
            return;
        }

        // II) Find the greatest digit on
        // right side of (i-1)'th digit that is
        // smaller than number[i-1]
        int x = number[i - 1], greatest = i;
        for (j = i; j < n; j++)
        {
            if (number[j] < x && number[j] > number[greatest])
            {
                greatest = j;
            }
        }

        // III) Swap the above found smallest digit with number[i-1]
        swap(number, greatest, i - 1);

        // IV) Sort the digits after (i-1) in descending order
        Arrays.sort(number, i, n);
        reverse(number, i, n - 1);
        System.out.print("Greatest smaller number with" +
              "same set of digits is " + String.valueOf(number));

        return;
    }

    static String swap(char[] ch, int i, int j)
    {
        char temp = ch[i];
        ch[i] = ch[j];
        ch[j] = temp;
        return String.valueOf(ch);
    }

    static void reverse(char str[], int start, int end)
    {

        // Temporary variable to store character
        char temp;
        while (start <= end)
        {
            // Swapping the first and last character
            temp = str[start];
            str[start] = str[end];
            str[end] = temp;
            start++;
            end--;
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        String digits = "262345";
        int n = digits.length();

        findPrevious(digits.toCharArray(), n);
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to find previous number
def findPrevious(number, n):

    # This is necessary as strings
    # do not support item assignment
    number = list(number)

    i, j = -1, -1

    # I) Start from the right most digit
    # and find the first digit that is
    # smaller than the digit next to it.
    for i in range(n - 1, 0, -1):
        if number[i] < number[i - 1]:
            break

    # If no such digit is found
    # then all digits are in ascending order
    # means there cannot be a smallest number
    # with same set of digits
    if i == 0:
        print("Previous number is not possible")
        return

    x, greatest = number[i - 1], i

    # II) Find the greatest digit on
    # right side of(i-1)'th digit that is
    # smaller than number[i-1]
    for j in range(i, n):
        if (number[j] < x and
            number[j] > number[greatest]):
            greatest = j

    # III) Swap the above found smallest digit
    # with number[i-1]
    (number[greatest],
     number[i - 1]) = (number[i - 1],
                       number[greatest])

    l = number[i:]
    del number[i:]

    # IV) Sort the digits after(i-1)
    # in descending order
    l.sort(reverse = True)

    number += l

    # Again join the list to make it string
    number = '' . join(number)
    print("Greatest smaller number with",
          "same set of digits is", number)

    return

# Driver Code
if __name__ == "__main__":
    digits = "262345"
    n = len(digits)

    findPrevious(digits, n)

# This code is contributed by sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to find previous number
    static void findPrevious(char[] number, int n)
    {
        int i, j;

        // I) Start from the right most digit
        // and find the first digit that is
        // smaller than the digit next to it.
        for (i = n - 1; i > 0; i--)
        {
            if (number[i] < number[i - 1])
            {
                break;
            }
        }

        // If no such digit is found
        // then all digits are in ascending order
        // means there cannot be a smallest number
        // with same set of digits
        if (i == 0)
        {
            Console.Write("Previous number is not possible");
            return;
        }

        // II) Find the greatest digit on
        // right side of (i-1)'th digit that is
        // smaller than number[i-1]
        int x = number[i - 1], greatest = i;
        for (j = i; j < n; j++)
        {
            if (number[j] < x && number[j] > number[greatest])
            {
                greatest = j;
            }
        }

        // III) Swap the above found
        // smallest digit with number[i-1]
        swap(number, greatest, i - 1);

        // IV) Sort the digits after (i-1) in descending order
        Array.Sort(number, i, n-i);
        reverse(number, i, n - 1);
        Console.Write("Greatest smaller number with" +
            "same set of digits is " + String.Join("",number));

        return;
    }

    static String swap(char[] ch, int i, int j)
    {
        char temp = ch[i];
        ch[i] = ch[j];
        ch[j] = temp;
        return String.Join("",ch);
    }

    static void reverse(char []str, int start, int end)
    {

        // Temporary variable to store character
        char temp;
        while (start <= end)
        {
            // Swapping the first and last character
            temp = str[start];
            str[start] = str[end];
            str[end] = temp;
            start++;
            end--;
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        String digits = "262345";
        int n = digits.Length;

        findPrevious(digits.ToCharArray(), n);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to find previous number
function findPrevious(number, n)
{
    let i, j;

    // I) Start from the right most digit
    // and find the first digit that is
    // smaller than the digit next to it.
    for(i = n - 1; i > 0; i--)
    {
        if (number[i] < number[i - 1])
        {
            break;
        }
    }

    // If no such digit is found then all
    // digits are in ascending order means
    // there cannot be a smallest number
    // with same set of digits
    if (i == 0)
    {
        document.write("Previous number " +
                       "is not possible");
        return;
    }

    // II) Find the greatest digit on right
    // side of (i-1)'th digit that is smaller
    // than number[i-1]
    let x = number[i - 1], greatest = i;
    for(j = i; j < n; j++)
    {
        if (number[j] < x && number[j] >
            number[greatest])
        {
            greatest = j;
        }
    }

    // III) Swap the above found smallest
    // digit with number[i-1]
    swap(number, greatest, i - 1);

    // IV) Sort the digits after (i-1)
    // in descending order
    number = number.slice(0, i).concat(
             number.slice(i, n).sort(
                 function(a, b){return b - a;}));

    document.write("Greatest smaller number with " +
                   "same set of digits is " +
                   (number).join(""));

    return;
}

function swap(ch, i, j)
{
    let temp = ch[i];
    ch[i] = ch[j];
    ch[j] = temp;
    return String.valueOf(ch);
}

function reverse(str, start, end)
{

    // Temporary variable to store character
    let temp;

    while (start <= end)
    {

        // Swapping the first and last character
        temp = str[start];
        str[start] = str[end];
        str[end] = temp;
        start++;
        end--;
    }
}

// Driver code
let digits = "262345";
let n = digits.length;

findPrevious(digits.split(""), n);

// This code is contributed by rag2127

</script>
```

**Output:** 

```
Greatest smaller number with same set of digits is 256432
```