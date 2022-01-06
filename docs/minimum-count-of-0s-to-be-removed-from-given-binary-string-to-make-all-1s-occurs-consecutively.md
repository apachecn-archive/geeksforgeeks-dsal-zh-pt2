# 从给定的二进制字符串中移除 0 的最小计数，以使所有 1 连续出现

> 原文:[https://www . geesforgeks . org/从给定二进制字符串中移除 0 的最小计数使全 1 连续出现/](https://www.geeksforgeeks.org/minimum-count-of-0s-to-be-removed-from-given-binary-string-to-make-all-1s-occurs-consecutively/)

给定一个大小为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是找到必须从字符串 **S** 中移除的 **0s** 的最小数量，以便所有的 **1s** 连续出现。

**示例:**

> **输入:** S = "010001011"
> **输出:** 4
> **解释:**
> 从字符串 S 中删除字符{ S[2]、S[3]、S[4]、S[6] }将字符串 S 修改为“01111”。
> 因此，要求输出为 4。
> 
> **输入:** S = "011110000"
> **输出:** 0
> **说明:**
> S 中的所有 1 都已经分组在一起，因此，需要的输出为 0。

**方法:**通过观察去掉字符串中的前导和结尾 **0s** 并不能最小化必须去掉的 **0s** 的个数，可以解决给定的问题。因此，思路是找到字符串 **S** 中 **1** 的第一个和最后一个出现，并找到它们之间 **0s** 的计数。按照以下步骤解决问题:

*   [从左到右遍历字符串中的字符， **S**](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) ，找到给定字符串中第一个出现的 **1** s 的索引，比如 **X** 。
*   从右向左遍历字符串，找到给定字符串中最后一次出现的 **1** s 的索引，说 **Y** 。
*   完成上述步骤后，打印索引 **X** 和 **Y** 之间的 **0s** 的计数作为结果。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum count of
// 0s removed from the string S such
// that all 1s occurs consecutively
void makeContiguous(string S, int N)
{
    // Stores the first and the last
    // occurrence of 1
    int fst_occur, lst_occur;

    // Iterate over the characters
    // the string, S
    for (int x = 0; x < N; x++) {

        // If current character
        // is '1'
        if (S[x] == '1') {

            // Update fst_occur
            fst_occur = x;
            break;
        }
    }

    // Iterate over the characters
    // the string, S
    for (int x = N - 1; x >= 0; x--) {

        // If current character
        // is '1'
        if (S[x] == '1') {

            // Update lst_occur
            lst_occur = x;
            break;
        }
    }

    // Stores the count of 0s between
    // fst_occur and lst_occur
    int count = 0;

    // Iterate over the characters of S
    // between fst_occur and lst_occur
    for (int x = fst_occur;
        x <= lst_occur; x++) {

        // If current character is '0'
        if (S[x] == '0') {

            // Update count
            count++;
        }
    }

    // Print the resultant minimum count
    cout << count;
}

// Driver Code
int main()
{
    string S = "010001011";
    int N = S.size();
    makeContiguous(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG{

// Function to find minimum count of
// 0s removed from the String S such
// that all 1s occurs consecutively
static void makeContiguous(String S, int N)
{
    // Stores the first and the last
    // occurrence of 1
    int fst_occur=0, lst_occur=0;

    // Iterate over the characters
    // the String, S
    for (int x = 0; x < N; x++) {

        // If current character
        // is '1'
        if (S.charAt(x) == '1') {

            // Update fst_occur
            fst_occur = x;
            break;
        }
    }

    // Iterate over the characters
    // the String, S
    for (int x = N - 1; x >= 0; x--) {

        // If current character
        // is '1'
        if (S.charAt(x) == '1') {

            // Update lst_occur
            lst_occur = x;
            break;
        }
    }

    // Stores the count of 0s between
    // fst_occur and lst_occur
    int count = 0;

    // Iterate over the characters of S
    // between fst_occur and lst_occur
    for (int x = fst_occur; x <= lst_occur; x++) {

        // If current character is '0'
        if (S.charAt(x) == '0') {

            // Update count
            count++;
        }
    }

    // Print the resultant minimum count
    System.out.print(count);
}

// Driver Code
public static void main(String[] args)
{
    String S = "010001011";
    int N = S.length();
    makeContiguous(S, N);

}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find minimum count of
# 0s removed from the string S such
# that all 1s occurs consecutively
def makeContiguous(S, N):

    # Stores the first and the last
    # occurrence of 1
    fst_occur = 0
    lst_occur = 0

    # Iterate over the characters
    # the string, S
    for x in range(N):

        # If current character
        # is '1'
        if (S[x] == '1'):

            # Update fst_occur
            fst_occur = x
            break

    # Iterate over the characters
    # the string, S
    x = N - 1
    while(x >= 0):

        # If current character
        # is '1'
        if (S[x] == '1'):

            # Update lst_occur
            lst_occur = x
            break
        x -= 1

    # Stores the count of 0s between
    # fst_occur and lst_occur
    count = 0

    # Iterate over the characters of S
    # between fst_occur and lst_occur
    for x in range(fst_occur,lst_occur+1,1):
        # If current character is '0'
        if (S[x] == '0'):
            # Update count
            count += 1

    # Print the resultant minimum count
    print(count)

# Driver Code
if __name__ == '__main__':
    S = "010001011"
    N = len(S)
    makeContiguous(S, N)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find minimum count of
// 0s removed from the string S such
// that all 1s occurs consecutively
static void makeContiguous(string S, int N)
{

    // Stores the first and the last
    // occurrence of 1
    int fst_occur = 0, lst_occur = 0;

    // Iterate over the characters
    // the string, S
    for(int x = 0; x < N; x++)
    {

        // If current character
        // is '1'
        if (S[x] == '1')
        {

            // Update fst_occur
            fst_occur = x;
            break;
        }
    }

    // Iterate over the characters
    // the string, S
    for(int x = N - 1; x >= 0; x--)
    {

        // If current character
        // is '1'
        if (S[x] == '1')
        {

            // Update lst_occur
            lst_occur = x;
            break;
        }
    }

    // Stores the count of 0s between
    // fst_occur and lst_occur
    int count = 0;

    // Iterate over the characters of S
    // between fst_occur and lst_occur
    for(int x = fst_occur; x <= lst_occur; x++)
    {

        // If current character is '0'
        if (S[x] == '0')
        {

            // Update count
            count++;
        }
    }

    // Print the resultant minimum count
    Console.Write(count);
}

// Driver Code
public static void Main()
{
    string S = "010001011";
    int N = S.Length;

    makeContiguous(S, N);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
// javascript program for the above approach   
// Function to find minimum count of
    // 0s removed from the String S such
    // that all 1s occurs consecutively
    function makeContiguous( S , N)
    {

        // Stores the first and the last
        // occurrence of 1
        var fst_occur = 0, lst_occur = 0;

        // Iterate over the characters
        // the String, S
        for (var x = 0; x < N; x++) {

            // If current character
            // is '1'
            if (S.charAt(x) == '1') {

                // Update fst_occur
                fst_occur = x;
                break;
            }
        }

        // Iterate over the characters
        // the String, S
        for (var x = N - 1; x >= 0; x--) {

            // If current character
            // is '1'
            if (S.charAt(x) == '1') {

                // Update lst_occur
                lst_occur = x;
                break;
            }
        }

        // Stores the count of 0s between
        // fst_occur and lst_occur
        var count = 0;

        // Iterate over the characters of S
        // between fst_occur and lst_occur
        for (x = fst_occur; x <= lst_occur; x++) {

            // If current character is '0'
            if (S.charAt(x) == '0') {

                // Update count
                count++;
            }
        }

        // Print the resultant minimum count
        document.write(count);
    }

    // Driver Code

        var S = "010001011";
        var N = S.length;
        makeContiguous(S, N);

// This code is contributed by umadevi9616
</script>
```

**Output**

```
4
```