# 最小化交替子序列的移除，以清空给定的二进制字符串

> 原文:[https://www . geeksforgeeks . org/最小化-移除-交替-子序列-空-给定-二进制-字符串/](https://www.geeksforgeeks.org/minimize-removal-of-alternating-subsequences-to-empty-given-binary-string/)

给定长度为 **N** 的二进制[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是最小化从给定的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** 到[的交替子序列的重复移除次数，使字符串为空](https://www.geeksforgeeks.org/stdstringclear-in-cpp/)。

**示例:**

> **输入:**S =“0100100111”
> **输出:** 3
> **解释:**
> 从 S 中删除子序列“010101”将其修改为“0011”。
> 将“0011”中的“01”去掉，使其成为“01”。
> 最后去掉“01”使其成为空字符串。
> 
> **输入:**S = " 1111 "
> T3】输出: 4

**方法:**通过观察 **0** 和 **1** 的交替子序列将被移除，并且移除所有连续的字符 **1s** 或 **0s** 只能在每个单独的操作中移除，而不能在单个操作中移除，可以解决给定的问题。

因此，所需的最小操作次数是连续 **0s** 和**1s**T5 的最大[计数。](https://www.geeksforgeeks.org/maximum-consecutive-ones-or-zeros-in-a-binary-array/)

下面是上述方法的实现:

## C++

```
#include <iostream>
using namespace std;

void minOpsToEmptyString(string S, int N)
{
    // Initialize variables
    int one = 0, zero = 0;

    int x0 = 0, x1 = 0;

    // Traverse the string
    for (int i = 0; i < N; i++) {

        // If current character is 0
        if (S[i] == '0') {
            x0++;
            x1 = 0;
        }
        else {
            x1++;
            x0 = 0;
        }

        // Update maximum consecutive
        // 0s and 1s
        zero = max(x0, zero);
        one = max(x1, one);
    }

    // Print the minimum operation
    cout << max(one, zero) << endl;
}

// Driver code+
int main()
{

    // input string
    string S = "0100100111";

    // length of string
    int N = S.length();

    // Function Call
    minOpsToEmptyString(S, N);
}

// This code is contributed by aditya7409
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to find the minimum
    // number of operations required
    // to empty the string
    public static void
    minOpsToEmptyString(String S,
                        int N)
    {
        // Initialize variables
        int one = 0, zero = 0;

        int x0 = 0, x1 = 0;

        // Traverse the string
        for (int i = 0; i < N; i++) {

            // If current character is 0
            if (S.charAt(i) == '0') {
                x0++;
                x1 = 0;
            }
            else {
                x1++;
                x0 = 0;
            }

            // Update maximum consecutive
            // 0s and 1s
            zero = Math.max(x0, zero);
            one = Math.max(x1, one);
        }

        // Print the minimum operation
        System.out.println(
            Math.max(one, zero));
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S = "0100100111";
        int N = S.length();

        // Function Call
        minOpsToEmptyString(S, N);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
def minOpsToEmptyString(S, N):

    # Initialize variables
    one = 0
    zero = 0
    x0 = 0
    x1 = 0

    # Traverse the string
    for i in range(N):

        # If current character is 0
        if (S[i] == '0'):
            x0 += 1
            x1 = 0
        else:
            x1 += 1
            x0 = 0

        # Update maximum consecutive
        # 0s and 1s
        zero = max(x0, zero)
        one = max(x1, one)

    # Print the minimum operation
    print(max(one, zero))

# Driver code+
if __name__ == "__main__":

    # input string
    S = "0100100111"

    # length of string
    N = len(S)

    # Function Call
    minOpsToEmptyString(S, N)

    # This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to find the minimum
    // number of operations required
    // to empty the string
    public static void
      minOpsToEmptyString(string S, int N)
    {
        // Initialize variables
        int one = 0, zero = 0;

        int x0 = 0, x1 = 0;

        // Traverse the string
        for (int i = 0; i < N; i++)
        {

            // If current character is 0
            if (S[i] == '0')
            {
                x0++;
                x1 = 0;
            }
            else
            {
                x1++;
                x0 = 0;
            }

            // Update maximum consecutive
            // 0s and 1s
            zero = Math.Max(x0, zero);
            one = Math.Max(x1, one);
        }

        // Print the minimum operation
        Console.WriteLine(Math.Max(one, zero));
    }

    // Driver Code
    static public void Main()
    {
        string S = "0100100111";
        int N = S.Length;

        // Function Call
        minOpsToEmptyString(S, N);
    }
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>

// Javascript program of the above approach

// Function to find the minimum
// number of operations required
// to empty the string
function minOpsToEmptyString(S, N)
{

    // Initialize variables
    let one = 0, zero = 0;

    let x0 = 0, x1 = 0;

    // Traverse the string
    for(let i = 0; i < N; i++)
    {

        // If current character is 0
        if (S[i] == '0')
        {
            x0++;
            x1 = 0;
        }
        else
        {
            x1++;
            x0 = 0;
        }

        // Update maximum consecutive
        // 0s and 1s
        zero = Math.max(x0, zero);
        one = Math.max(x1, one);
    }

    // Print the minimum operation
    document.write(Math.max(one, zero));
}

// Driver Code
let S = "0100100111";
let N = S.length;

// Function Call
minOpsToEmptyString(S, N);

// This code is contributed by chinmoy1997pal

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)