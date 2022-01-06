# 反转字符串的最小相邻交换次数

> 原文:[https://www . geesforgeks . org/最小相邻交换次数-反转字符串/](https://www.geeksforgeeks.org/minimum-number-of-adjacent-swaps-to-reverse-a-string/)

赐一[弦**T3**s**。任务是最小化反转字符串所需的相邻交换的数量。**](https://www.geeksforgeeks.org/category/data-structures/c-strings/)

****示例:****

> ****输入** : s = "abc"
> **输出** : 3
> **解释**:按照下面的操作解决给定的问题。
> 互换(1，2)—>“BAC”
> 互换(2，3)—>“BCA”
> 互换(1，2)—>“CBA”**
> 
> ****输入** : s = "ba"
> **输出** : 1**

****逼近**:这个问题可以通过将给定的字符串与其反转进行比较，并计算形成反转字符串所需的交换次数来解决。按照以下步骤解决问题:**

*   **将字符串 **s2** 初始化为原始字符串 **s** 的副本。**
*   **反弦 **s2****
*   **初始化**结果= 0** ，以存储反转字符串所需的相邻交换次数。**
*   **对两个字符串使用两个指针 I 和 j 进行迭代，并通过两个指针 **i** 和 **j** 找到 **s2** 中 **s** 的每次出现

    *   每次设置**结果=结果+j–I**。** 
*   **返回结果作为最终答案。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum adjacent swaps
// Required to reverse the string
int min_swaps(string s)
{
    string s2 = s;

    // Reverse a string
    reverse(s2.begin(), s2.end());

    int i = 0, j = 0;
    int result = 0;
    int n = s.length();
    while (i < n) {

        j = i;

        // Iterate till characters
        // of both the strings match
        while (s[j] != s2[i]) {
            j += 1;
        }

        // Iterating until i=j
        // result will be j-i
        while (i < j) {
            char temp = s[j];
            s[j] = s[j - 1];
            s[j - 1] = temp;
            j -= 1;
            result += 1;
        }
        i += 1;
    }
    return result;
}

// Driver code
int main()
{
    string s = "abc";

    cout << min_swaps(s);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for above approach
public class GFG {

    static int min_swaps(String s)
    {
        String s2 = "";

        // Reverse a string
        char[] cArray = s.toCharArray();
        for (int k = cArray.length - 1; k > -1; k--) {
            s2 += cArray[k];
        }

        int i = 0, j = 0;
        int result = 0;
        int n = s.length();
        while (i < n) {

            j = i;

            // Iterate till characters
            // of both the strings match
            while (s.charAt(j) != s2.charAt(i)) {
                j += 1;
            }

            // Iterating until i=j
            // result will be j-i
            while (i < j) {
                char temp = s.charAt(j);
                char[] ch = s.toCharArray();
                ch[j] = ch[j - 1];
                ch[j - 1] = temp;
                s = new String(ch);
                j -= 1;
                result += 1;
            }
            i += 1;
        }
        return result;
    }

    // Driver code
    static public void main(String []args)
    {
        String s = "abc";

        System.out.println(min_swaps(s));
    }
}

// This code is contributed by AnkThon
```

## **蟒蛇 3**

```
# python program for above approach

# Function to find minimum adjacent swaps
# Required to reverse the string
def min_swaps(s):

    s2 = s.copy()

    # Reverse a string
    s2.reverse()

    i = 0
    j = 0
    result = 0
    n = len(s)
    while (i < n):

        j = i

        # Iterate till characters
        # of both the strings match
        while (s[j] != s2[i]):
            j += 1

            # Iterating until i=j
            # result will be j-i
        while (i < j):
            temp = s[j]
            s[j] = s[j - 1]
            s[j - 1] = temp
            j -= 1
            result += 1

        i += 1

    return result

# Driver code
if __name__ == "__main__":

    s = "abc"
    s = list(s)
    print(min_swaps(s))

    # This code is contributed by rakeshsahni
```

## **C#**

```
using System;

public class GFG {
    static int min_swaps(string s)
    {
        string s2 = String.Empty;

        // Reverse a string
        char[] cArray = s.ToCharArray();
        for (int k = cArray.Length - 1; k > -1; k--) {
            s2 += cArray[k];
        }

        int i = 0, j = 0;
        int result = 0;
        int n = s.Length;
        while (i < n) {

            j = i;

            // Iterate till characters
            // of both the strings match
            while (s[j] != s2[i]) {
                j += 1;
            }

            // Iterating until i=j
            // result will be j-i
            while (i < j) {
                char temp = s[j];
                char[] ch = s.ToCharArray();
                ch[j] = ch[j - 1];
                ch[j - 1] = temp;
                s = new string(ch);
                j -= 1;
                result += 1;
            }
            i += 1;
        }
        return result;
    }

    // Driver code
    static public void Main()
    {
        string s = "abc";

        Console.WriteLine(min_swaps(s));
    }
}

// This code is contributed by maddler.
```

## **java 描述语言**

```
<script>

// Javascript program for above approach

// Function to find minimum adjacent swaps
// Required to reverse the string
function min_swaps(s)
{

    var s2 = JSON.parse(JSON.stringify(s));
    s = s.split('');
    s2 = s2.split('');

    // Reverse a string
    s2.reverse();
    var i = 0, j = 0;
    var result = 0;
    var n = s.length;
    while (i < n) {

        j = i;

        // Iterate till characters
        // of both the strings match
        while (s[j] != s2[i]) {
            j += 1;
        }

        // Iterating until i=j
        // result will be j-i
        while (i < j) {
            var temp = s[j];
            s[j] = s[j - 1];
            s[j - 1] = temp;
            j -= 1;
            result += 1;
        }
        i += 1;
    }
    return result;
}

// Driver code
var s = "abc";
document.write(min_swaps(s));

// This code is contributed by rutvik_56.
</script>
```

****Output:** 

```
3
```** 

****时间复杂度** : O(N <sup>2</sup> ，其中 N 是给定字符串的大小。**

****辅助空间** : O(1)。**