# 尽量减少所需的翻转，使得字符串不包含任何一对连续的 0

> 原文:[https://www . geesforgeks . org/minimum-flips-required-so-string-not-any-pair-of-continuous-0/](https://www.geeksforgeeks.org/minimize-flips-required-such-that-string-does-not-any-pair-of-consecutive-0s/)

给定一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是找到修改字符串所需的最小翻转次数，使其不包含任何一对连续的 **0** s。

**示例:**

> **输入:**S =“10001”
> T3】输出: 1
> **解释:**
> 翻转 S[2]将 S 修改为“10101”。
> 因此，要求的输出为 1。
> 
> **输入:**S =“100001”
> T3】输出: 2
> **解释:**
> 翻转 S[1]将 S 修改为“110001”。
> 翻转 S[3]将 S 修改为“110101”。

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。按照以下步骤解决问题:

*   [迭代字符串的字符](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)。对于每一个**I<sup>th</sup>T5【字符，检查**S【I】**和**S【I+1】**是否等于**‘0’**。如果发现为真，则递增计数并将 **S[i + 1]** 更新为**‘1’**。**
*   最后，打印获得的计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum flips required
// such that a string does not contain
// any pair of consecutive 0s
bool cntMinOperation(string S, int N)
{

    // Stores minimum count of flips
    int cntOp = 0;

    // Iterate over the characters
    // of the string
    for (int i = 0; i < N - 1; i++) {

        // If two consecutive characters
        // are equal to '0'
        if (S[i] == '0' && S[i + 1] == '0') {

            // Update S[i + 1]
            S[i + 1] = '1';

            // Update cntOp
            cntOp += 1;
        }
    }

    return cntOp;
}

// Driver Code
int main()
{
    string S = "10001";
    int N = S.length();
    cout << cntMinOperation(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to find minimum flips required
// such that a String does not contain
// any pair of consecutive 0s
static int cntMinOperation(char []S, int N)
{

    // Stores minimum count of flips
    int cntOp = 0;

    // Iterate over the characters
    // of the String
    for (int i = 0; i < N - 1; i++)
    {

        // If two consecutive characters
        // are equal to '0'
        if (S[i] == '0' && S[i + 1] == '0')
        {

            // Update S[i + 1]
            S[i + 1] = '1';

            // Update cntOp
            cntOp += 1;
        }
    }
    return cntOp;
}

// Driver Code
public static void main(String[] args)
{
    String S = "10001";
    int N = S.length();
    System.out.print(cntMinOperation(S.toCharArray(), N));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find minimum flips required
# such that a string does not contain
# any pair of consecutive 0s
def cntMinOperation(S, N):

    # Stores minimum count of flips
    cntOp = 0

    # Iterate over the characters
    # of the string
    for i in range(N - 1):

        # If two consecutive characters
        # are equal to '0'
        if (S[i] == '0' and S[i + 1] == '0'):

            # Update S[i + 1]
            S[i + 1] = '1'

            # Update cntOp
            cntOp += 1
    return cntOp

# Driver Code
if __name__ == '__main__':
    S = "10001"
    N = len(S)
    print(cntMinOperation([i for i in S], N))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to find minimum flips required
  // such that a String does not contain
  // any pair of consecutive 0s
  static int cntMinOperation(char []S, int N)
  {

    // Stores minimum count of flips
    int cntOp = 0;

    // Iterate over the characters
    // of the String
    for (int i = 0; i < N - 1; i++)
    {

      // If two consecutive characters
      // are equal to '0'
      if (S[i] == '0' && S[i + 1] == '0')
      {

        // Update S[i + 1]
        S[i + 1] = '1';

        // Update cntOp
        cntOp += 1;
      }
    }
    return cntOp;
  }

  // Driver Code
  public static void Main(string[] args)
  {
    string S = "10001";
    int N = S.Length;
    Console.WriteLine(cntMinOperation(S.ToCharArray(), N));
  }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    // Function to find minimum flips required
    // such that a String does not contain
    // any pair of consecutive 0s
    function cntMinOperation(S, N)
    {

      // Stores minimum count of flips
      let cntOp = 0;

      // Iterate over the characters
      // of the String
      for (let i = 0; i < N - 1; i++)
      {

        // If two consecutive characters
        // are equal to '0'
        if (S[i] == '0' && S[i + 1] == '0')
        {

          // Update S[i + 1]
          S[i + 1] = '1';

          // Update cntOp
          cntOp += 1;
        }
      }
      return cntOp;
    }

    let S = "10001";
    let N = S.length;
    document.write(cntMinOperation(S.split(''), N));

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)