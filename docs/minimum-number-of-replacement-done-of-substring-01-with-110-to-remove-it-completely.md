# 用“110”替换子串“01”以将其完全删除的最小次数

> 原文:[https://www . geesforgeks . org/substring-01-with-110-to-remove-it-complete-最小替换完成次数/](https://www.geeksforgeeks.org/minimum-number-of-replacement-done-of-substring-01-with-110-to-remove-it-completely/)

给定一个[二进制串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是找到子串**【01】**到串**【110】**的最小重复替换次数，使得在给定的串 **S** 中不存在任何子串**【01】**。

**示例:**

> **输入:** S = "01"
> **输出:** 1
> **解释:**
> 下面是执行的操作:
> **操作 1:** 在字符串“01”中选择子字符串(0，1)并用“110”替换，将给定的字符串修改为“110”。
> 经过上述操作后，字符串 S(= "110 ")不包含任何作为“01”的子字符串。因此，所需的操作总数为 1。
> 
> **输入:** S = "001"
> **输出:** 3
> **解释:**
> 下面是执行的操作:
> **操作 1:** 在字符串“001”中选择子字符串(1，2)并用“110”替换，将给定的字符串修改为“0110”。
> **操作 2:** 在字符串“0110”中选择子字符串(0，1)，并将其替换为“110”，将给定的字符串修改为“11010”。
> **操作 3:** 在字符串“11010”中选择子字符串(2，3)，并将其替换为“110”，将给定的字符串修改为“111100”。
> 经过以上操作，字符串 S(= "111100 ")不包含任何作为“01”的子字符串。因此，所需的操作总数为 3。

**方法:**给定的问题可以使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决。操作是每当发现一个子串**“01”**时，就用**“110”**代替，现在这个**“0”**的右侧出现**“1”**的数字，组成子串**“01”**，参与将字符串改为**“110”**。因此，思路是[从末端](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)开始遍历字符串，每当**‘0’**出现时，执行给定的操作，直到右侧出现 **1s** 的数量。按照以下步骤解决问题:

*   初始化两个变量，比如 **ans** 和 **cntOne** 都作为 **0** 来存储执行的最小操作数和遍历期间从末尾开始的连续 **1s** 的计数。
*   [从末端](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)穿过给定的弦 **S** ，并执行以下步骤:
    *   如果当前字符是 **0** ，那么将 **ans** 增加到目前为止获得的连续 **1s** 的数量以及连续 **1s** 的计数值的两倍。
    *   否则，将 **cntOne** 的值增加 **1** 。
*   完成上述步骤后，打印**和**的值作为最小操作次数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>

using namespace std;

// Function to find the minimum number
// of replacement of "01" with "110"
// s.t. S doesn't contain substring "10"
void minimumOperations(string S, int N)
{
    // Stores the number of operations
    // performed
    int ans = 0;

    // Stores the resultant count
    // of substrings
    int cntOne = 0;

    // Traverse the string S from end
    for (int i = N - 1; i >= 0; i--) {

        // If the current character
        // is 0
        if (S[i] == '0') {
            ans += cntOne;
            cntOne *= 2;
        }

        // If the current character
        // is 1
        else
            cntOne++;
    }

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    string S = "001";
    int N = S.length();
    minimumOperations(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {
    // Function to find the minimum number
    // of replacement of "01" with "110"
    // s.t. S doesn't contain substring "10"
    public static void minimumOperations(String S, int N)
    {
        // Stores the number of operations
        // performed
        int ans = 0;

        // Stores the resultant count
        // of substrings
        int cntOne = 0;

        // Traverse the string S from end
        for (int i = N - 1; i >= 0; i--) {

            // If the current character
            // is 0
            if (S.charAt(i) == '0') {
                ans += cntOne;
                cntOne *= 2;
            }

            // If the current character
            // is 1
            else
                cntOne++;
        }

        // Print the result
        System.out.println(ans);
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S = "001";
        int N = S.length();
        minimumOperations(S, N);
    }
}

  // This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum number
# of replacement of "01" with "110"
# s.t. S doesn't contain substring "10"
def minimumOperations(S, N):

    # Stores the number of operations
    # performed
    ans = 0

    # Stores the resultant count
    # of substrings
    cntOne = 0

    # Traverse the string S from end
    i = N - 1

    while(i >= 0):

        # If the current character
        # is 0
        if (S[i] == '0'):
            ans += cntOne
            cntOne *= 2

        # If the current character
        # is 1
        else:
            cntOne += 1

        i -= 1

    # Print the result
    print(ans)

# Driver Code
if __name__ == '__main__':

    S = "001"
    N = len(S)

    minimumOperations(S, N)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum number
// of replacement of "01" with "110"
// s.t. S doesn't contain substring "10"
public static void minimumOperations(string S, int N)
{

    // Stores the number of operations
    // performed
    int ans = 0;

    // Stores the resultant count
    // of substrings
    int cntOne = 0;

    // Traverse the string S from end
    for(int i = N - 1; i >= 0; i--)
    {

        // If the current character
        // is 0
        if (S[i] == '0')
        {
            ans += cntOne;
            cntOne *= 2;
        }

        // If the current character
        // is 1
        else
            cntOne++;
    }

    // Print the result
    Console.WriteLine(ans);
}

// Driver code
static void Main()
{
    string S = "001";
    int N = S.Length;

    minimumOperations(S, N);
}
}

// This code is contributed by abhinavjain194
```

## java 描述语言

```
<script>
       // JavaScript program for the above approach

       // Function to find the minimum number
       // of replacement of "01" with "110"
       // s.t. S doesn't contain substring "10"
       function minimumOperations(S, N)
       {

           // Stores the number of operations
           // performed
           let ans = 0;

           // Stores the resultant count
           // of substrings
           let cntOne = 0;

           // Traverse the string S from end
           for (let i = N - 1; i >= 0; i--) {

               // If the current character
               // is 0
               if (S[i] == '0') {
                   ans += cntOne;
                   cntOne *= 2;
               }

               // If the current character
               // is 1
               else
                   cntOne++;
           }

           // Print the result
           document.write(ans);
       }

       // Driver Code

       let S = "001";
       let N = S.length;
       minimumOperations(S, N);

 // This code is contributed by Potta Lokesh
   </script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)