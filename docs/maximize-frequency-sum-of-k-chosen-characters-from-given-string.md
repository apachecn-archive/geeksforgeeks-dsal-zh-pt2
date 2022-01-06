# 最大化从给定字符串中选择的 K 个字符的频率和

> 原文:[https://www . geesforgeks . org/maximum-frequency-sum-k-selected-characters-from-给定字符串/](https://www.geeksforgeeks.org/maximize-frequency-sum-of-k-chosen-characters-from-given-string/)

给定一个正整数 **K** 和一个由 **N** 个字符组成的[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S** ，任务是最大化给定字符串中恰好 K 个所选字符的[频率之和。](https://www.geeksforgeeks.org/print-the-frequency-of-each-character-in-alphabetical-order/)

**示例:**

> **输入:**K–3，S = "GEEKSFORGEEKS"
> **输出:** 12
> **解释:**
> 从给定的字符串 S 中选择字符 E，3 个 E 的频率之和为 3*4 = 12，为最大值。
> 
> **输入:** K = 10，S = " GEEKSFORGEEKS "
> T3】输出: 28

**方法:**通过选择那些频率较高的 **K 字符**，使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决给定的问题。按照以下步骤解决问题:

*   初始化一个变量，说 **sum** 到 **0** ，它存储字符串 **S** 中恰好 K 个所选字符的[频率的合成和。](https://www.geeksforgeeks.org/print-the-frequency-of-each-character-in-alphabetical-order/)
*   [找到字符串 **S** 中每个字符](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/)的频率，并将其存储在一个辅助数组中，比如 **freq[]** 。
*   [按降序排列数组**freq[]**](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。
*   [遍历阵列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **freq[]** 并执行以下操作:
    *   如果当前频率小于 **K** ，那么将 **freq[i]*freq[i]** 添加到变量 **sum** 中，因为它最大化了结果和，并且当选择 **freq[i]** 字符时，从 **K** 减少 **freq[i]** 的值。
    *   否则，将 **K*freq[i]** 的值添加到变量**和**中，并且[脱离循环](https://www.geeksforgeeks.org/break-statement-cc/)，因为已经选择了 **K** 字符。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of
// frequencies of the exactly K chosen
// characters from the string S
int maximumSum(string S, int N, int K)
{
    // Stores the resultant maximum sum
    int sum = 0;

    // Stores the frequency of array
    // elements
    int freq[256] = { 0 };

    // Find the frequency of character
    for (int i = 0; i < N; i++) {
        freq[int(S[i])]++;
    }

    // Sort the frequency array in the
    // descending order
    sort(freq, freq + 256, greater<int>());

    // Iterate to choose K elements greedily
    for (int i = 0; i < 256; i++) {

        // If the freq[i] cards are
        // chosen
        if (K > freq[i]) {
            sum += freq[i] * freq[i];
            K -= freq[i];
        }

        // K cards have been picked
        else {
            sum += freq[i] * K;
            break;
        }
    }

    // Return the resultant sum
    return sum;
}

// Driver Code
int main()
{
    string S = "GEEKSFORGEEKS";
    int K = 10;
    int N = S.length();
    cout << maximumSum(S, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to find the maximum sum of
// frequencies of the exactly K chosen
// characters from the String S
static int maximumSum(String S, int N, int K)
{

    // Stores the resultant maximum sum
    int sum = 0;

    // Stores the frequency of array
    // elements
    Integer []freq = new Integer[256];
    Arrays.fill(freq, 0);

    // Find the frequency of character
    for(int i = 0; i < N; i++)
    {
        freq[(int)S.charAt(i)] += 1;
    }

    // Sort the frequency array in the
    // descending order
     Arrays.sort(freq, Collections.reverseOrder());

    // Iterate to choose K elements greedily
    for(int i = 0; i < 256; i++)
    {

        // If the freq[i] cards are
        // chosen
        if (K > freq[i])
        {
            sum += freq[i] * freq[i];
            K -= freq[i];
        }

        // K cards have been picked
        else
        {
            sum += freq[i] * K;
            break;
        }
    }

    // Return the resultant sum
    return sum;
}

// Driver Code
public static void main(String args[])
{
    String S = "GEEKSFORGEEKS";
    int K = 10;
    int N = S.length();

    System.out.print(maximumSum(S, N, K));
}
}

// This code is contributed by ipg2016107
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum sum of
# frequencies of the exactly K chosen
# characters from the string S
def maximumSum(S, N, K):

    # Stores the resultant maximum sum
    sum = 0

    # Stores the frequency of array
    # elements
    freq = [0] * 256

    # Find the frequency of character
    for i in range(N):
        freq[ord(S[i])] += 1

    # Sort the frequency array in the
    # descending order
    freq = sorted(freq)[::-1]

    # Iterate to choose K elements greedily
    for i in range(256):

        # If the freq[i] cards are
        # chosen
        if (K > freq[i]):
            sum += freq[i] * freq[i]
            K -= freq[i]

        # K cards have been picked
        else:
            sum += freq[i] * K
            break

    # Return the resultant sum
    return sum

# Driver Code
if __name__ == '__main__':

    S = "GEEKSFORGEEKS"
    K = 10
    N = len(S)

    print(maximumSum(S, N, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the maximum sum of
// frequencies of the exactly K chosen
// characters from the string S
static int maximumSum(string S, int N, int K)
{

    // Stores the resultant maximum sum
    int sum = 0;

    // Stores the frequency of array
    // elements
    int []freq = new int[256];
    Array.Clear(freq, 0, 256);

    // Find the frequency of character
    for(int i = 0; i < N; i++)
    {
        freq[(int)S[i]]++;
    }

    // Sort the frequency array in the
    // descending order
    Array.Sort(freq);
    Array.Reverse(freq);

    // Iterate to choose K elements greedily
    for(int i = 0; i < 256; i++)
    {

        // If the freq[i] cards are
        // chosen
        if (K > freq[i])
        {
            sum += freq[i] * freq[i];
            K -= freq[i];
        }

        // K cards have been picked
        else
        {
            sum += freq[i] * K;
            break;
        }
    }

    // Return the resultant sum
    return sum;
}

// Driver Code
public static void Main()
{
    string S = "GEEKSFORGEEKS";
    int K = 10;
    int N = S.Length;

    Console.Write(maximumSum(S, N, K));
}
}

// This code is contributed by ipg2016107
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the maximum sum of
// frequencies of the exactly K chosen
// characters from the string S
function maximumSum(S, N, K)
{

    // Stores the resultant maximum sum
    let sum = 0;

    // Stores the frequency of array
    // elements
    let freq = Array.from({length: 256}, (_, i) => 0);

    // Find the frequency of character
    for(let i = 0; i < N; i++)
    {
        freq[S[i].charCodeAt()]++;
    }

    // Sort the frequency array in the
    // descending order
    freq.sort((a, b) => b - a);

    // Iterate to choose K elements greedily
    for(let i = 0; i < 256; i++)
    {

        // If the freq[i] cards are
        // chosen
        if (K > freq[i])
        {
            sum += freq[i] * freq[i];
            K -= freq[i];
        }

        // K cards have been picked
        else
        {
            sum += freq[i] * K;
            break;
        }
    }

    // Return the resultant sum
    return sum;
}       

// Driver Code

    let S = "GEEKSFORGEEKS";
    let K = 10;
    let N = S.length;

    document.write(maximumSum(S.split(''), N, K))

</script>
```

**Output:** 

```
28
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(26)