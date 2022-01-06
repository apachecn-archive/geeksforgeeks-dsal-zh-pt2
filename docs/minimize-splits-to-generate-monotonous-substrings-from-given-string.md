# 最小化分裂，从给定的字符串生成单调的子字符串

> 原文:[https://www . geesforgeks . org/minimum-splits-to-generate-单调-substrings-from-给定字符串/](https://www.geeksforgeeks.org/minimize-splits-to-generate-monotonous-substrings-from-given-string/)

给定一个字符串 **str** ，任务是找到给定的字符串 **S** 可以拆分成的最小数量的子字符串，这样每个子字符串都是单调递增或递减的。

**示例:**

> **输入:**str = " abcdba "
> **输出:** 2
> **解释:**
> 字符串可以拆分为最少 2 个单调的子字符串{【ABCD】(**递增**)、【CBA】(**递减** )}
> **输入:**str = " aecdhba "
> **输出:** 3
> **解释**

**方法:**按照以下步骤解决问题:

*   初始化一个变量**正在进行= 'N'** 以跟踪当前序列的顺序。
*   迭代字符串，对于每个字符，请执行以下步骤:
*   如果**正在进行== 'N'** :
    *   如果**当前字符<前一个字符**，则用 **D** (非递增)更新**正在进行的**。
    *   否则，如果**curr _ character>prev _ character**，则用 **I** (非递减)更新**进行中的**。
    *   否则，用 **N** 更新**正在进行的**(非增非减)。
*   否则，如果**正在进行== 'I'** :
    *   如果**curr _ character>prev _ character**那么用 **I** 更新**正在进行的**。
    *   否则，如果**curr _ character<prev _ character**则用 **N** 更新**正在进行的**并增加答案。
    *   否则，用 **I** 更新**正在进行的**。
*   否则，请执行以下步骤:
    *   如果**curr _ character<prev _ character**然后用 **D** 更新**正在进行的**。
    *   否则，如果**curr _ character>prev _ character**则用 **N** 更新**正在进行的**并增加答案。
    *   否则，用 **D** 更新**正在进行的**。
*   最后打印**答案+1** 为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to return final result
int minReqSubstring(string s, int n)
{

    // Initialize variable to keep
    // track of ongoing sequence
    char ongoing = 'N';

    int count = 0, l = s.size();

    for(int i = 1; i < l; i++)
    {

        // If current sequence is neither
        // increasing nor decreasing
        if (ongoing == 'N')
        {

            // If prev char is greater
            if (s[i] < s[i - 1])
            {
                ongoing = 'D';
            }

            // If prev char is same
            else if (s[i] == s[i - 1])
            {
                ongoing = 'N';
            }

            // Otherwise
            else
            {
                ongoing = 'I';
            }
        }

        // If current sequence
        // is Non-Decreasing
        else if (ongoing == 'I')
        {

            // If prev char is smaller
            if (s[i] > s[i - 1])
            {
                ongoing = 'I';
            }

            // If prev char is same
            else if (s[i] == s[i - 1])
            {

                // Update ongoing
                ongoing = 'I';
            }

            // Otherwise
            else
            {

                // Update ongoing
                ongoing = 'N';

                // Increase count
                count += 1;
            }
        }

        // If current sequence
        // is Non-Increasing
        else
        {

            // If prev char is greater,
            // then update ongoing with D
            if (s[i] < s[i - 1])
            {
                ongoing = 'D';
            }

            // If prev char is equal, then
            // update current with D
            else if (s[i] == s[i - 1])
            {
                ongoing = 'D';
            }

            // Otherwise, update ongoing
            // with N and increment count
            else
            {
                ongoing = 'N';
                count += 1;
            }
        }
    }

    // Return count+1
    return count + 1;
}

// Driver Code
int main()
{
    string S = "aeccdhba";
    int n = S.size();

    cout << (minReqSubstring(S, n));
    return 0;
}

// This code is contributed by Amit Katiyar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;

class GFG {

    // Function to return final result
    static int minReqSubstring(String s, int n)
    {

        // Initialize variable to keep
        // track of ongoing sequence
        char ongoing = 'N';

        int count = 0, l = s.length();

        for (int i = 1; i < l; i++) {

            // If current sequence is neither
            // increasing nor decreasing
            if (ongoing == 'N') {

                // If prev char is greater
                if (s.charAt(i) < s.charAt(i - 1)) {
                    ongoing = 'D';
                }

                // If prev char is same
                else if (s.charAt(i) == s.charAt(i - 1)) {
                    ongoing = 'N';
                }

                // Otherwise
                else {
                    ongoing = 'I';
                }
            }

            // If current sequence
            // is Non-Decreasing
            else if (ongoing == 'I') {

                // If prev char is smaller
                if (s.charAt(i) > s.charAt(i - 1)) {
                    ongoing = 'I';
                }

                // If prev char is same
                else if (s.charAt(i) == s.charAt(i - 1)) {

                    // Update ongoing
                    ongoing = 'I';
                }

                // Otherwise
                else {

                    // Update ongoing
                    ongoing = 'N';

                    // Increase count
                    count += 1;
                }
            }

            // If current sequence
            // is Non-Increasing
            else {

                // If prev char is greater,
                // then update ongoing with D
                if (s.charAt(i) < s.charAt(i - 1)) {
                    ongoing = 'D';
                }

                // If prev char is equal, then
                // update current with D
                else if (s.charAt(i) == s.charAt(i - 1)) {
                    ongoing = 'D';
                }

                // Otherwise, update ongoing
                // with N and increment count
                else {
                    ongoing = 'N';
                    count += 1;
                }
            }
        }

        // Return count+1
        return count + 1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S = "aeccdhba";
        int n = S.length();
        System.out.print(
            minReqSubstring(S, n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to return final result
def minReqSubstring(s, n):

    # Initialize variable to keep
    # track of ongoing sequence
    ongoing = 'N'
    count, l = 0, len(s)

    for i in range(1, l):

        # If current sequence is neither
        # increasing nor decreasing
        if ongoing == 'N':

            # If prev char is greater
            if s[i] < s[i - 1]:
                ongoing = 'D'

            # If prev char is same
            elif s[i] == s[i - 1]:
                ongoing = 'N'

            # Otherwise
            else:
                ongoing = 'I'

        # If current sequence
        # is Non-Decreasing
        elif ongoing == 'I':

            # If prev char is smaller
            if s[i] > s[i - 1]:
                ongoing = 'I'

            # If prev char is same
            elif s[i] == s[i - 1]:

                # Update ongoing
                ongoing = 'I'

            # Otherwise
            else:

                # Update ongoing
                ongoing = 'N'

                # Increase count
                count += 1

        # If current sequence
        # is Non-Increasing
        else:

            # If prev char is greater,
            # then update ongoing with D
            if s[i] < s[i - 1]:
                ongoing = 'D'

            # If prev char is equal, then
            # update current with D
            elif s[i] == s[i - 1]:
                ongoing = 'D'

            # Otherwise, update ongoing
            # with N and increment count
            else:
                ongoing = 'N'
                count += 1

    # Return count + 1
    return count + 1

# Driver code
S = "aeccdhba"
n = len(S)

print(minReqSubstring(S, n))

# This code is contributed by Stuti Pathak
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG{

  // Function to return readonly result
  static int minReqSubstring(String s, int n)
  {

    // Initialize variable to keep
    // track of ongoing sequence
    char ongoing = 'N';

    int count = 0, l = s.Length;

    for (int i = 1; i < l; i++)
    {

      // If current sequence is neither
      // increasing nor decreasing
      if (ongoing == 'N')
      {

        // If prev char is greater
        if (s[i] < s[i - 1])
        {
          ongoing = 'D';
        }

        // If prev char is same
        else if (s[i] == s[i - 1])
        {
          ongoing = 'N';
        }

        // Otherwise
        else
        {
          ongoing = 'I';
        }
      }

      // If current sequence
      // is Non-Decreasing
      else if (ongoing == 'I')
      {

        // If prev char is smaller
        if (s[i] > s[i - 1])
        {
          ongoing = 'I';
        }

        // If prev char is same
        else if (s[i] == s[i - 1])
        {

          // Update ongoing
          ongoing = 'I';
        }

        // Otherwise
        else
        {

          // Update ongoing
          ongoing = 'N';

          // Increase count
          count += 1;
        }
      }

      // If current sequence
      // is Non-Increasing
      else
      {

        // If prev char is greater,
        // then update ongoing with D
        if (s[i] < s[i - 1])
        {
          ongoing = 'D';
        }

        // If prev char is equal, then
        // update current with D
        else if (s[i] == s[i - 1])
        {
          ongoing = 'D';
        }

        // Otherwise, update ongoing
        // with N and increment count
        else
        {
          ongoing = 'N';
          count += 1;
        }
      }
    }

    // Return count+1
    return count + 1;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    String S = "aeccdhba";
    int n = S.Length;
    Console.Write(minReqSubstring(S, n));
  }
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>
// javascript program for the
// above approach

    // Function to return final result
    function minReqSubstring(s, n)
    {

        // Initialize variable to keep
        // track of ongoing sequence
        let ongoing = 'N';

        let count = 0, l = s.length;

        for (let i = 1; i < l; i++) {

            // If current sequence is neither
            // increasing nor decreasing
            if (ongoing == 'N') {

                // If prev char is greater
                if (s[i] < s[i - 1]) {
                    ongoing = 'D';
                }

                // If prev char is same
                else if (s[i] == s[i - 1]) {
                    ongoing = 'N';
                }

                // Otherwise
                else {
                    ongoing = 'I';
                }
            }

            // If current sequence
            // is Non-Decreasing
            else if (ongoing == 'I') {

                // If prev char is smaller
                if (s[i] > s[i - 1]) {
                    ongoing = 'I';
                }

                // If prev char is same
                else if (s[i] == s[i - 1]) {

                    // Update ongoing
                    ongoing = 'I';
                }

                // Otherwise
                else {

                    // Update ongoing
                    ongoing = 'N';

                    // Increase count
                    count += 1;
                }
            }

            // If current sequence
            // is Non-Increasing
            else {

                // If prev char is greater,
                // then update ongoing with D
                if (s[i] < s[i - 1]) {
                    ongoing = 'D';
                }

                // If prev char is equal, then
                // update current with D
                else if (s[i] == s[i - 1]) {
                    ongoing = 'D';
                }

                // Otherwise, update ongoing
                // with N and increment count
                else {
                    ongoing = 'N';
                    count += 1;
                }
            }
        }

        // Return count+1
        return count + 1;
    }

// Driver Code

    let S = "aeccdhba";
        let n = S.length;
        document.write(
            minReqSubstring(S, n));

// This code is contributed by target_2.
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*