# 通过对给定的字符串执行 K 运算，字典上最小的字符串

> 原文:[https://www . geeksforgeeks . org/通过对给定字符串执行-k-operations-on-给定字符串执行尽可能最小的字符串/](https://www.geeksforgeeks.org/lexicographically-smallest-string-possible-by-performing-k-operations-on-a-given-string/)

给定一个大小为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 和一个正整数 **K** ，任务是对字符串 **S** 执行 atmat**K**操作，使其在字典上成为最小的。在一次操作中，[将](https://www.geeksforgeeks.org/swap-two-numbers-without-using-temporary-variable/) **S[i]** 和 **S[j]** 互换，然后将 **S[i]** 改为任意字符，给定 **1 ≤ i < j ≤ N** 。

**示例:**

> **输入:** S =【极客】，K = 5
> **输出:** aaaa
> **说明:**
> 第一次操作:取 i = 1，j = 4，交换 S[1]和 S[4]，然后将 S[1]改为‘a’。修改字符串=“aeeg”。
> 第二次操作:取 i = 2，j=4，交换 S[2]和 S[4]，然后将 S[2]改为‘a’。已修改字符串=“aaee”。
> 第三次操作:取 i = 3，j = 4，交换 S[3]和 S[4]，然后将 S[3]改为‘a’。修改字符串=“aaae”。
> 第 4 次操作:取 i = 3，j = 4，交换 S[3]和 S[4]，然后将 S[3]改为‘a’。修改字符串=“AAAA”。
> 
> **输入:** S = "geeksforgeeks "，K = 6
> **输出:**aaaaaaaegeeks
> **解释:**6 次运算后，字典上最小的字符串将是“aaaaaegeeks”。

**方法:**对于 **K≥N** ，字典上最小可能的字符串将是**‘a’**重复 **N** 次，因为在 **N** 操作中， **S** 的所有字符都可以更改为**‘a’**。对于所有其他情况，想法是使用变量 **i** 迭代字符串 **S** ，找到一个合适的 **j** ，对于该字符串**S【j】>S【I】**，然后将**S【j】**转换为**S【I】**并将**S【I】**转换为**‘a’**。当 **K > 0** 时，继续此过程。

按照以下步骤解决问题:

*   如果 **K ≥ N** ，将字符串 **S** 的每个字符转换为**a '**并打印该字符串， **S** 。
*   否则:
    *   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代
        *   如果 **K=0** ，[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
        *   [使用变量 **j** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【I+1，N-1】**中迭代
            *   如果 **S[j] > S[i]** ，设置**S[j]= S[I]**[出圈](https://www.geeksforgeeks.org/break-statement-cc/)。
        *   如果没有找到这样的元素，即 **j=N** 设置**S【j-1】= S【I】**。
        *   设置 **S[i]='a'** 并将 **K** 减 1。
    *   打印字符串， **S** 。

下面是上述方法的实现:

## C++

```
// C++ program to implement the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the lexicographically
// smallest possible string by performing
// K operations on string S
void smallestlexicographicstring(string s, int k)
{

    // Store the size of string, s
    int n = s.size();

    // Check if k>=n, if true, convert
    // every character to 'a'
    if (k >= n) {
        for (int i = 0; i < n; i++) {
            s[i] = 'a';
        }
        cout << s;
        return;
    }

    // Iterate in range[0, n - 1] using i
    for (int i = 0; i < n; i++) {

        // When k reaches 0, break the loop
        if (k == 0) {
            break;
        }

        // If current character is 'a',
        // continue
        if (s[i] == 'a')
            continue;

        // Otherwise, iterate in the
        // range [i + 1, n - 1] using j
        for (int j = i + 1; j < n; j++) {

            // Check if s[j] > s[i]
            if (s[j] > s[i]) {

                // If true, set s[j] = s[i]
                // and break out of the loop
                s[j] = s[i];
                break;
            }

            // Check if j reaches the last index
            else if (j == n - 1)
                s[j] = s[i];
        }

        // Update S[i]
        s[i] = 'a';

        // Decrement k by 1
        k--;
    }

    // Print string
    cout << s;
}

// Driver Code
int main()
{

    // Given String, s
    string s = "geeksforgeeks";

    // Given k
    int k = 6;

    // Function Call
    smallestlexicographicstring(s, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the above approach
public class GFG
{

    // Function to find the lexicographically
    // smallest possible string by performing
    // K operations on string S
    static void smallestlexicographicstring(char[] s, int k)
    {

        // Store the size of string, s
        int n = s.length;

        // Check if k>=n, if true, convert
        // every character to 'a'
        if (k >= n)
        {
            for (int i = 0; i < n; i++)
            {
                s[i] = 'a';
            }
            System.out.print(s);
            return;
        }

        // Iterate in range[0, n - 1] using i
        for (int i = 0; i < n; i++)
        {

            // When k reaches 0, break the loop
            if (k == 0)
            {
                break;
            }

            // If current character is 'a',
            // continue
            if (s[i] == 'a')
                continue;

            // Otherwise, iterate in the
            // range [i + 1, n - 1] using j
            for (int j = i + 1; j < n; j++)
            {

                // Check if s[j] > s[i]
                if (s[j] > s[i])
                {

                    // If true, set s[j] = s[i]
                    // and break out of the loop
                    s[j] = s[i];
                    break;
                }

                // Check if j reaches the last index
                else if (j == n - 1)
                    s[j] = s[i];
            }

            // Update S[i]
            s[i] = 'a';

            // Decrement k by 1
            k--;
        }

        // Print string
        System.out.print(s);
    }

  // Driver code
    public static void main(String[] args)
    {

        // Given String, s
        char[] s = ("geeksforgeeks").toCharArray();

        // Given k
        int k = 6;

        // Function Call
        smallestlexicographicstring(s, k);
    }
}

// This code is contributed by divyesh072019.
```

## 蟒蛇 3

```
# Python3 program to implement the above approach

# Function to find the lexicographically
# smallest possible string by performing
# K operations on string S
def smallestlexicographicstring(s, k):

    # Store the size of string, s
    n = len(s)

    # Check if k>=n, if true, convert
    # every character to 'a'
    if (k >= n):
        for i in range(n):

            s[i] = 'a';

        print(s, end = '')
        return;

    # Iterate in range[0, n - 1] using i
    for i in range(n):

        # When k reaches 0, break the loop
        if (k == 0):
            break;

        # If current character is 'a',
        # continue
        if (s[i] == 'a'):
            continue;

        # Otherwise, iterate in the
        # range [i + 1, n - 1] using j
        for j in range(i + 1, n):

            # Check if s[j] > s[i]
            if (s[j] > s[i]):

                # If true, set s[j] = s[i]
                # and break out of the loop
                s[j] = s[i];
                break;

            # Check if j reaches the last index
            elif (j == n - 1):
                s[j] = s[i];

        # Update S[i]
        s[i] = 'a';

        # Decrement k by 1
        k -= 1

    # Print string
    print(''.join(s), end = '');

# Driver Code
if __name__=='__main__':

    # Given String, s
    s = list("geeksforgeeks");

    # Given k
    k = 6;

    # Function Call
    smallestlexicographicstring(s, k);

    # This code is contributed by rutvik_56.
```

## C#

```
// C# program to implement the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to find the lexicographically
    // smallest possible string by performing
    // K operations on string S
    static void smallestlexicographicstring(char[] s, int k)
    {

        // Store the size of string, s
        int n = s.Length;

        // Check if k>=n, if true, convert
        // every character to 'a'
        if (k >= n)
        {
            for (int i = 0; i < n; i++)
            {
                s[i] = 'a';
            }
            Console.Write(s);
            return;
        }

        // Iterate in range[0, n - 1] using i
        for (int i = 0; i < n; i++)
        {

            // When k reaches 0, break the loop
            if (k == 0)
            {
                break;
            }

            // If current character is 'a',
            // continue
            if (s[i] == 'a')
                continue;

            // Otherwise, iterate in the
            // range [i + 1, n - 1] using j
            for (int j = i + 1; j < n; j++)
            {

                // Check if s[j] > s[i]
                if (s[j] > s[i])
                {

                    // If true, set s[j] = s[i]
                    // and break out of the loop
                    s[j] = s[i];
                    break;
                }

                // Check if j reaches the last index
                else if (j == n - 1)
                    s[j] = s[i];
            }

            // Update S[i]
            s[i] = 'a';

            // Decrement k by 1
            k--;
        }

        // Print string
        Console.Write(s);
    }

  // Driver code
  static void Main()
  {

    // Given String, s
    char[] s = ("geeksforgeeks").ToCharArray();

    // Given k
    int k = 6;

    // Function Call
    smallestlexicographicstring(s, k);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

    // Javascript program to implement
    // the above approach

    // Function to find the lexicographically
    // smallest possible string by performing
    // K operations on string S
    function smallestlexicographicstring(s, k)
    {

        // Store the size of string, s
        let n = s.length;

        // Check if k>=n, if true, convert
        // every character to 'a'
        if (k >= n)
        {
            for (let i = 0; i < n; i++)
            {
                s[i] = 'a';
            }
            document.write(s);
            return;
        }

        // Iterate in range[0, n - 1] using i
        for (let i = 0; i < n; i++)
        {

            // When k reaches 0, break the loop
            if (k == 0)
            {
                break;
            }

            // If current character is 'a',
            // continue
            if (s[i] == 'a')
                continue;

            // Otherwise, iterate in the
            // range [i + 1, n - 1] using j
            for (let j = i + 1; j < n; j++)
            {

                // Check if s[j] > s[i]
                if (s[j].charCodeAt() >
                s[i].charCodeAt())
                {

                    // If true, set s[j] = s[i]
                    // and break out of the loop
                    s[j] = s[i];
                    break;
                }

                // Check if j reaches the last index
                else if (j == n - 1)
                    s[j] = s[i];
            }

            // Update S[i]
            s[i] = 'a';

            // Decrement k by 1
            k--;
        }

        // Print string
        document.write(s.join(""));
    }

    // Given String, s
    let s = ("geeksforgeeks").split('');

    // Given k
    let k = 6;

    // Function Call
    smallestlexicographicstring(s, k);

</script>
```

**Output:** 

```
aaaaaaeegeeks
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(1)