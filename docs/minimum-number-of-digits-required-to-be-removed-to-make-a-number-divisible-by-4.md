# 要使一个数能被 4 整除，需要去掉的最小位数

> 原文:[https://www . geeksforgeeks . org/最小位数-需要删除才能使数字被 4 整除/](https://www.geeksforgeeks.org/minimum-number-of-digits-required-to-be-removed-to-make-a-number-divisible-by-4/)

给定一个数字 **N** ，任务是计算要从 **N** 中移除的最小位数，使其可被 **4** 整除。

**示例:**

> **输入:** N = 12367
> **输出:** 1
> **说明:** *从数字 1236 中去掉 7，使数字可被 4 整除。因此，要删除的最小位数是 1。*
> 
> **输入:**N = 243775
> T3】输出: 4

**方法:**这个想法是基于[4](https://www.geeksforgeeks.org/check-large-number-divisible-4-not/)可除性的基本规则:如果一个数的最后两位数组成的数可以被 4 整除，那么原始数就可以被 **4** 整除。现在，想法是从最后一个开始检查由两位数组成的数字是否能被 4 整除。按照以下步骤解决问题:

*   [将数字 **N** 转换为字符串](https://www.geeksforgeeks.org/converting-string-to-number-and-vice-versa-in-c/)并存储在 **S** 中。
*   用字符串**的[长度初始化变量**和**，以存储所需的最小删除次数。](https://www.geeksforgeeks.org/5-different-methods-find-length-string-c/)**
*   **[使用变量 **i** 从头到尾遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 。

    *   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【I–1，0】**。
        *   如果 **S[j]** 和 **S[i]** 形成的数可被 4 整除，则执行以下步骤:
            *   将索引 **i** 和 **j** 之间的位数存储在变量中，比如说 **K1** ，等于**(I–j–1)**，将索引 **i** 之前的位数存储在变量中，比如说 **K2** ，等于**(N–I–1)**。 **K1** 和 **K2** 的和表示要删除的位数，使得 **S[j]** 和 **S[i]** 成为新数字的最后两位。
            *   如果 **(K1 + K2)** 的值小于 **ans** 的值，则更新 **ans** 为 **(K1 + K2)** 。** 
*   **遍历字符串后，如果**和**的值仍然不变，检查是否有 **S[i]** 可被 4 整除。如果发现是真的，更新 **ans** 为**(S–1 的长度)**。**
*   **完成上述步骤后，打印**和**的值作为结果。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum number
// of digits required to be removed to
// make a given number divisible by 4
void minimumDeletions(string s)
{
    // Store the size of the string
    int n = s.length();

    // Stores the required result
    int ans = n;

    // Check for every pair of digits
    // if the number formed by them
    // is divisible by 4 or not
    for (int i = n - 1; i >= 0; i--) {

        // Store s[i] in a variable
        int t = s[i] - '0';

        // If it is divisible by 2
        if (t % 2 == 0) {
            for (int j = i - 1;
                 j >= 0; j--) {

                // Store the number formed
                // by s[j] and s[i]
                int num = (s[j] - '0')
                              * 10
                          + t;

                // Check if it is
                // divisible by 4
                if (num % 4 == 0) {

                    // Store the number of digits
                    // required to be deleted
                    int k1 = i - j - 1;
                    int k2 = n - i - 1;

                    // Update ans
                    ans = min(ans,
                              k1 + k2);
                }
            }
        }
    }

    // If value of ans is unchanged, then
    // check if any s[i] is divisible by 4
    if (ans == n) {

        for (int i = 0; i < n; i++) {

            int num = s[i] - '0';

            // If true, update ans to n - 1
            if (num % 4 == 0) {
                ans = n - 1;
            }
        }
    }

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    string str = "12367";
    minimumDeletions(str);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;
class GFG {

  // Function to count the minimum number
  // of digits required to be removed to
  // make a given number divisible by 4
  static void minimumDeletions(String s)
  {

    // Store the size of the string
    int n = s.length();

    // Stores the required result
    int ans = n;

    // Check for every pair of digits
    // if the number formed by them
    // is divisible by 4 or not
    for (int i = n - 1; i >= 0; i--) {

      // Store s[i] in a variable
      int t = s.charAt(i) - '0';

      // If it is divisible by 2
      if (t % 2 == 0) {
        for (int j = i - 1; j >= 0; j--) {

          // Store the number formed
          // by s[j] and s[i]
          int num = (s.charAt(j) - '0') * 10 + t;

          // Check if it is
          // divisible by 4
          if (num % 4 == 0) {

            // Store the number of digits
            // required to be deleted
            int k1 = i - j - 1;
            int k2 = n - i - 1;

            // Update ans
            ans = Math.min(ans, k1 + k2);
          }
        }
      }
    }

    // If value of ans is unchanged, then
    // check if any s[i] is divisible by 4
    if (ans == n) {

      for (int i = 0; i < n; i++) {

        int num = s.charAt(i) - '0';

        // If true, update ans to n - 1
        if (num % 4 == 0) {
          ans = n - 1;
        }
      }
    }

    // Print the result
    System.out.println(ans);
  }

  // Driver Code
  static public void main(String[] args)
  {
    String str = "12367";
    minimumDeletions(str);
  }
}

// This code is contributed by ukasp.
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to count the minimum number
# of digits required to be removed to
# make a given number divisible by 4
def minimumDeletions(s):

    # Store the size of the string
    n = len(s)

    # Stores the required result
    ans = n

    # Check for every pair of digits
    # if the number formed by them
    # is divisible by 4 or not
    for i in range(n - 1, -1, -1):

        # Store s[i] in a variable
        t = ord(s[i]) - ord('0')

        # If it is divisible by 2
        if (t % 2 == 0):
            for j in range(i - 1, -1, -1):

                # Store the number formed
                # by s[j] and s[i]
                num = (ord(s[j]) - ord('0'))* 10 + t

                # Check if it is
                # divisible by 4
                if (num % 4 == 0):

                    # Store the number of digits
                    # required to be deleted
                    k1 = i - j - 1
                    k2 = n - i - 1

                    # Update ans
                    ans = min(ans, k1 + k2)

    # If value of ans is unchanged, then
    # check if any s[i] is divisible by 4
    if (ans == n):
        for i in range(n):
            num = ord(s[i]) - ord('0')

            # If true, update ans to n - 1
            if (num % 4 == 0):
                ans = n - 1

    # Prthe result
    print (ans)

# Driver Code
if __name__ == '__main__':
    str = "12367"
    minimumDeletions(str)

    # This code is contributed by mohit kumar 29.
```

## **C#**

```
// C# program for the above approach
using System;
class GFG
{

// Function to count the minimum number
// of digits required to be removed to
// make a given number divisible by 4
static void minimumDeletions(string s)
{

    // Store the size of the string
    int n = s.Length;

    // Stores the required result
    int ans = n;

    // Check for every pair of digits
    // if the number formed by them
    // is divisible by 4 or not
    for (int i = n - 1; i >= 0; i--) {

        // Store s[i] in a variable
        int t = s[i] - '0';

        // If it is divisible by 2
        if (t % 2 == 0) {
            for (int j = i - 1;
                 j >= 0; j--) {

                // Store the number formed
                // by s[j] and s[i]
                int num = (s[j] - '0')
                              * 10
                          + t;

                // Check if it is
                // divisible by 4
                if (num % 4 == 0) {

                    // Store the number of digits
                    // required to be deleted
                    int k1 = i - j - 1;
                    int k2 = n - i - 1;

                    // Update ans
                    ans = Math.Min(ans,
                              k1 + k2);
                }
            }
        }
    }

    // If value of ans is unchanged, then
    // check if any s[i] is divisible by 4
    if (ans == n) {

        for (int i = 0; i < n; i++) {

            int num = s[i] - '0';

            // If true, update ans to n - 1
            if (num % 4 == 0) {
                ans = n - 1;
            }
        }
    }

    // Print the result
    Console.WriteLine(ans);
}

// Driver Code
static public void Main()
{
    string str = "12367";
    minimumDeletions(str);
}
}

// This code is contributed by sanjoy_62.
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Function to count the minimum number
// of digits required to be removed to
// make a given number divisible by 4
function minimumDeletions(s)
{

    // Store the size of the string
    let n = s.length;

    // Stores the required result
    let ans = n;

    // Check for every pair of digits
    // if the number formed by them
    // is divisible by 4 or not
    for(let i = n - 1; i >= 0; i--)
    {

        // Store s[i] in a variable
        let t = s[i] - '0';

        // If it is divisible by 2
        if (t % 2 == 0)
        {
            for(let j = i - 1;
                     j >= 0; j--)
            {

                // Store the number formed
                // by s[j] and s[i]
                let num = (s[j] - '0') * 10 + t;

                // Check if it is
                // divisible by 4
                if (num % 4 === 0)
                {

                    // Store the number of digits
                    // required to be deleted
                    let k1 = i - j - 1;
                    let k2 = n - i - 1;

                    // Update ans
                    ans = Math.min(ans,
                            k1 + k2);
                }
            }
        }
    }

    // If value of ans is unchanged, then
    // check if any s[i] is divisible by 4
    if (ans === n)
    {
        for(let i = 0; i < n; i++)
        {
            let num = s[i] - '0';

            // If true, update ans to n - 1
            if (num % 4 === 0)
            {
                ans = n - 1;
            }
        }
    }

    // Print the result
    document.write(ans);
}

// Driver Code
let str = "12367";

minimumDeletions(str);

// This code is contributed by Manoj.

</script>
```

****Output:** 

```
1
```** 

*****时间复杂度:**O((log<sub>10</sub>N)<sup>2</sup>)*
***辅助空间:** O (1)***