# 通过在 M 次迭代后将 01 或 10 全部转换为 11 来查找二进制字符串

> 原文:[https://www . geesforgeks . org/find-二进制-字符串-通过 m 次迭代后转换所有-01 或-10 到-11/](https://www.geeksforgeeks.org/find-binary-string-by-converting-all-01-or-10-to-11-after-m-iterations/)

给定一个大小为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **字符串[]** 和一个整数 **M** 。这个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)可以通过将所有 **0 的**翻转到 **1** 来修改，其中**正好有一个** **1** 作为邻居。任务是在 **M** 这样的迭代之后，找到[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)的最终状态。
注: **2≤N≤10 <sup>3</sup> ，1≤M≤10 <sup>9</sup>**

**示例:**

> ***输入:** str="01100 "，M=1*
> ***输出:** 11110*
> ***解释:**首次迭代后:11110*
> 
> ***输入:** str = "0110100 "，M=3*
> ***输出:** 1110111*
> ***说明:**第一次迭代后:1110110，第二次迭代后:1110111，第三次迭代后:保持不变。*

**方法:**该解决方案基于这样的观察，即修改可以进行不超过 **N** 次迭代，因为即使在每次迭代中，至少一个 **0** 被翻转，那么它将进行最大 **N** 次，并且如果在一次迭代中没有零被翻转，那么这将意味着[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)保持与上一步相同的状态，并且仿真结束。因此，总迭代次数最少为 **N** 和**m**按照以下步骤解决问题:

*   初始化变量 **N** 并将其值设置为[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **字符串**的长度。
*   将 **M** 的值设置为 **N** 或**M**的最小值
*   [在外部 while 循环](https://www.geeksforgeeks.org/nested-loops-in-c-with-examples/)中迭代，直到 **M** 大于 0。
*   初始化字符串**S1 = "**以存储当前迭代后的修改版本。
*   [从 **i=0** 到**I<n**内循环迭代](https://www.geeksforgeeks.org/nested-loops-in-c-with-examples/)
*   用给定的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **字符串[]的**索引检查**处的字符。**
*   如果**字符串[i]=='1 '，**则将该字符添加到[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **s1 中。**
*   否则，在 **i-1** 和 **i+1 索引中检查其相邻字符。**
*   如果正好有一个 **1** ，那么将 **1** 添加到[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **s1 中。**
*   否则，将 **0** 添加到[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **s1 中。**
*   内环后，检查[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **字符串**和 **s1** 是否相同。
*   如果是，则[断开](https://www.geeksforgeeks.org/break-statement-cc/)外环。
*   否则，将[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **s1** 设置为[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **字符串**的新值，并将 **M** 的值减 1。
*   最后，打印[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **s1。**

下面是上述方法的实现。

## C++

```
// C++ program for the above approach.
#include <bits/stdc++.h>
using namespace std;

// Function to find the modified
// binary string after M iterations
void findString(string str, int M)
{
    int N = str.length();

    // Set the value of M to the minimum
    // of N or M.
    M = min(M, N);

    // Declaration of current string state
    string s1 = "";

    // Loop over M iterations
    while (M != 0) {

        // Set the current state as null
        // before each iteration
        s1 = "";

        for (int i = 0; i < N; i++) {

            if (str[i] == '0') {

                // Check if this zero has exactly
                // one 1 as neighbour
                if ((str[i - 1] == '1'
                     && str[i + 1] != '1')
                    || (str[i - 1] != '1'
                        && str[i + 1] == '1'))

                    // Flip the zero
                    s1 += '1';

                else
                    s1 += '0';
            }
            else
                s1 += '1';
        }

        // If there is no change,
        // then no need for
        // further iterations.
        if (str == s1)
            break;

        // Set the current state
        // as the new previous state
        str = s1;
        M--;
    }

    cout << s1;
}

// Driver Code
int main()
{
    // Given String
    string str = "0110100";

    // Number of Iterations
    int M = 3;

    // Function Call
    findString(str, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach.
import java.io.*;
import static java.lang.Math.min;
import java.lang.*;

class GFG
{

// Function to find the modified
// binary string after M iterations
public static void findString(String str, int M)
{
    int N = str.length();

    // Set the value of M to the minimum
    // of N or M.
    M = Math.min(M, N);

    // Declaration of current string state
    String s1 = "";

    // Loop over M iterations
    while (M != 0) {

        // Set the current state as null
        // before each iteration
        s1 = "";

        for (int i = 0; i < N; i++) {

            if (str.charAt(i) == '0') {

                // Check if this zero has exactly
                // one 1 as neighbour
                if ((str.charAt(i) == '1'
                     && str.charAt(i) != '1')
                    || (str.charAt(i) == '1'
                        && str.charAt(i) == '1'))

                    // Flip the zero
                    s1 += '1';

                else
                    s1 += '0';
            }
            else
                s1 += '1';
        }

        // If there is no change,
        // then no need for
        // further iterations.
        if (str == s1)
            break;

        // Set the current state
        // as the new previous state
        str = s1;
        M--;
    }

    System.out.print(s1);
}

// Driver Code
public static void main (String[] args)
{

    // Given String
    String str = "0110100";

    // Number of Iterations
    int M = 3;

    // Function Call
    findString(str, M);

}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python 3 program for the above approach.

# Function to find the modified
# binary string after M iterations
def findString(str,M):
    N = len(str)

    # Set the value of M to the minimum
    # of N or M.
    M = min(M, N)

    # Declaration of current string state
    s1 = ""

    # Loop over M iterations
    while (M != 0):

        # Set the current state as null
        # before each iteration
        s1 = ""

        for i in range(N-1):
            if (str[i] == '0'):

                # Check if this zero has exactly
                # one 1 as neighbour
                if ((str[i - 1] == '1' and str[i + 1] != '1') or (str[i - 1] != '1' and str[i + 1] == '1')):
                    # Flip the zero
                    s1 += '1'

                else:
                    s1 += '0'
            else:
                s1 += '1'

        # If there is no change,
        # then no need for
        # further iterations.
        if (str == s1):
            break
        s1 += '1'

        # Set the current state
        # as the new previous state
        str = s1
        M -= 1

    print(s1)

# Driver Code
if __name__ == '__main__':

    # Given String
    str = "0110100"

    # Number of Iterations
    M = 3

    # Function Call
    findString(str, M)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach.
using System;
class GFG {

    // Function to find the modified
    // binary string after M iterations
    static void findString(string str, int M)
    {
        int N = str.Length;

        // Set the value of M to the minimum
        // of N or M.
        M = Math.Min(M, N);

        // Declaration of current string state
        string s1 = "";

        // Loop over M iterations
        while (M != 0) {

            // Set the current state as null
            // before each iteration
            s1 = "";

            for (int i = 0; i < N; i++) {

                if (str[i] == '0')
                {                                                       
                    // Check if this zero has exactly
                    // one 1 as neighbour
                    if (((i>0 && str[i - 1] == '1') && (i<N-1 && str[i + 1] != '1')) || ((i>0 && str[i - 1] != '1') && (i<N-1 && str[i + 1] == '1')))
                    {
                        // Flip the zero
                        s1 += '1';
                    }
                    else
                    {

                        if(i==0 || i==N-1)
                        {
                            s1 += '1';   
                        }
                        else
                        {
                            s1 += '0';
                        }

                    }
                }
                else
                {
                    s1 += '1';
                }
            }

            // If there is no change,
            // then no need for
            // further iterations.
            if (str == s1)
                break;

            // Set the current state
            // as the new previous state
            //str = s1;
            M--;
        }

        Console.WriteLine(s1);
    }

  static void Main() {
    // Given String
    string str = "0110100";

    // Number of Iterations
    int M = 3;

    // Function Call
    findString(str, M);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the modified
// binary let after M iterations
function findlet(str, M)
{
    let N = str.length;

    // Set the value of M to the minimum
    // of N or M.
    M = Math.min(M, N);

    // Declaration of current let state
    let s1 = "";

    // Loop over M iterations
    while (M != 0) {

        // Set the current state as null
        // before each iteration
        s1 = "";

        for (let i = 0; i < N; i++) {

            if (str[i] == '0') {

                // Check if this zero has exactly
                // one 1 as neighbour
                if ((str[i - 1] == '1'
                     && str[i + 1] != '1')
                    || (str[i - 1] != '1'
                        && str[i + 1] == '1'))

                    // Flip the zero
                    s1 += '1';

                else
                    s1 += '0';
            }
            else
                s1 += '1';
        }

        // If there is no change,
        // then no need for
        // further iterations.
        if (str == s1)
            break;

        // Set the current state
        // as the new previous state
        str = s1;
        M--;
    }

    document.write(s1);
}

// Driver Code

     // Given let
    let str = "0110100";

    // Number of Iterations
    let M = 3;

    // Function Call
    findlet(str, M);

// This code is contributed by splevel62.
</script>
```

**Output**

```
1110111
```

***时间复杂度:** O(min(M，N)*N)*
***辅助空间:** O(1)*