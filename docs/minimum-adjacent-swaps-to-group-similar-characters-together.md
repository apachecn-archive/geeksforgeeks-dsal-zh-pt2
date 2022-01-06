# 将相似字符组合在一起的最小相邻互换量

> 原文:[https://www . geesforgeks . org/最小-相邻-互换-到-组-相似-字符-在一起/](https://www.geeksforgeeks.org/minimum-adjacent-swaps-to-group-similar-characters-together/)

给定一个长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，仅由小写英文字符组成，任务是找到将相同字符组合在一起所需的最小相邻互换数量。

**示例:**

> **输入:**S =【cbabc】
> T3】输出: 4
> **解释:**
> 将字符 S[0]交换为 S[1]。因此，S =“bcabc”。
> 将字符 S[1]交换为 S[2]。因此，S =“bacbc”。
> 将字符 S[2]交换为 S[3]。因此，S =“babcc”。
> 将字符 S[1]交换为 S[2]。因此，S =“bbacc”。
> 因此，所需的总掉期是 4。
> 
> **输入:** S = "abcd"
> **输出:** 0
> **说明:**
> 所有人物性格鲜明。因此，不需要交换。

**方法:**想法是存储每个字符的索引。然后，对于每个字符，找到相邻的绝对差异，并将其添加到答案中。按照以下步骤解决问题:

1.  初始化一个 [2D 向量](https://www.geeksforgeeks.org/2d-vector-in-cpp-with-user-defined-size/) **arr[]** ，其中向量 **arr[i]** 将存储字符 **(i + 'a')** 的索引和一个变量**答案**初始化为 **0** 。
2.  [在范围**【0，N-1】**内迭代给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)。
3.  将索引 **i** 添加到**arr【S[I]–‘a’】**中。
4.  遍历字符串后，遍历从 **i = 'a'** 到 **'z'** 的 [2D 向量](https://www.geeksforgeeks.org/2d-vector-in-cpp-with-user-defined-size/)**arr【】**。
5.  对于每个字符 **i** ，找到该向量中出现的字符 **i** 的索引的绝对相邻差，并将它们添加到**答案**中。
6.  遍历 [2D 向量](https://www.geeksforgeeks.org/2d-vector-in-cpp-with-user-defined-size/)后，打印**答案**作为最小互换次数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum adjacent
// swaps required to make all the
// same character adjacent
int minSwaps(string S, int n)
{
    // Initialize answer
    int swaps = 0;

    // Create a 2D array of size 26
    vector<vector<int> > arr(26);

    // Traverse the string
    for (int i = 0; i < n; i++) {

        // Get character
        int pos = S[i] - 'a';

        // Append the current index in
        // the corresponding vector
        arr[pos].push_back(i);
    }

    // Traverse each character from a to z
    for (char ch = 'a'; ch <= 'z'; ++ch) {
        int pos = ch - 'a';

        // Add difference of adjacent index
        for (int i = 1;
             i < arr[pos].size(); ++i) {

            swaps += abs(arr[pos][i]
                         - arr[pos][i - 1] - 1);
        }
    }

    // Return answer
    return swaps;
}

// Driver Code
int main()
{
    // Given string
    string S = "abbccabbcc";

    // Size of string
    int N = S.length();

    // Function Call
    cout << minSwaps(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find minimum adjacent
// swaps required to make all the
// same character adjacent
static int minSwaps(String S, int n)
{

    // Initialize answer
    int swaps = 0;

    // Create a 2D array of size 26
    @SuppressWarnings("unchecked")
    Vector<Integer> []arr = new Vector[26];
    for(int i = 0; i < arr.length; i++)
        arr[i] = new Vector<Integer>();

    // Traverse the String
    for(int i = 0; i < n; i++)
    {

        // Get character
        int pos = S.charAt(i) - 'a';

        // Append the current index in
        // the corresponding vector
        arr[pos].add(i);
    }

    // Traverse each character from a to z
    for(char ch = 'a'; ch <= 'z'; ++ch)
    {
        int pos = ch - 'a';

        // Add difference of adjacent index
        for(int i = 1; i < arr[pos].size(); ++i)
        {
            swaps += Math.abs(arr[pos].get(i) -
                              arr[pos].get(i - 1) - 1);
        }
    }

    // Return answer
    return swaps;
}

// Driver Code
public static void main(String[] args)
{

    // Given String
    String S = "abbccabbcc";

    // Size of String
    int N = S.length();

    // Function Call
    System.out.print(minSwaps(S, N));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find minimum adjacent
# swaps required to make all the
# same character adjacent
def minSwaps(S, n):

    # Initialize answer
    swaps = 0

    # Create a 2D array of size 26
    arr = [[] for i in range(26)]

    # Traverse the string
    for i in range(n):

        # Get character
        pos = ord(S[i]) - ord('a')

        # Append the current index in
        # the corresponding vector
        arr[pos].append(i)

    # Traverse each character from a to z
    for ch in range(ord('a'), ord('z') + 1):
        pos = ch - ord('a')

        # Add difference of adjacent index
        for i in range(1, len(arr[pos])):
            swaps += abs(arr[pos][i] -
                         arr[pos][i - 1] - 1)

    # Return answer
    return swaps

# Driver Code
if __name__ == '__main__':

    # Given string
    S = "abbccabbcc"

    # Size of string
    N = len(S)

    # Function Call
    print(minSwaps(S, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to find minimum
// adjacent swaps required
// to make all the same
// character adjacent
static int minSwaps(String S,
                    int n)
{   
  // Initialize answer
  int swaps = 0;

  // Create a 2D array
  // of size 26
  List<int> []arr =
       new List<int>[26];

  for(int i = 0;
          i < arr.Length; i++)
    arr[i] = new List<int>();

  // Traverse the String
  for(int i = 0; i < n; i++)
  {
    // Get character
    int pos = S[i] - 'a';

    // Append the current index in
    // the corresponding vector
    arr[pos].Add(i);
  }

  // Traverse each character
  // from a to z
  for(char ch = 'a';
           ch <= 'z'; ++ch)
  {
    int pos = ch - 'a';

    // Add difference of
    // adjacent index
    for(int i = 1;
            i < arr[pos].Count; ++i)
    {
      swaps += Math.Abs(arr[pos][i] -
                        arr[pos][i - 1] - 1);
    }
  }

  // Return answer
  return swaps;
}

// Driver Code
public static void Main(String[] args)
{   
  // Given String
  String S = "abbccabbcc";

  // Size of String
  int N = S.Length;

  // Function Call
  Console.Write(minSwaps(S, N));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find minimum adjacent
// swaps required to make all the
// same character adjacent
function minSwaps(S,n)
{
    // Initialize answer
    let swaps = 0;

    // Create a 2D array of size 26   
    let arr = new Array(26);
    for(let i = 0; i < arr.length; i++)
        arr[i] = [];

    // Traverse the String
    for(let i = 0; i < n; i++)
    {

        // Get character
        let pos = S[i].charCodeAt(0) - 'a'.charCodeAt(0);

        // Append the current index in
        // the corresponding vector
        arr[pos].push(i);
    }

    // Traverse each character from a to z
    for(let ch = 'a'.charCodeAt(0); ch <= 'z'.charCodeAt(0); ++ch)
    {
        let pos = ch - 'a'.charCodeAt(0);

        // Add difference of adjacent index
        for(let i = 1; i < arr[pos].length; ++i)
        {
            swaps += Math.abs(arr[pos][i] -
                              arr[pos][i-1] - 1);
        }
    }

    // Return answer
    return swaps;
}

// Driver Code

// Given String
let S = "abbccabbcc";

// Size of String
let N = S.length;

// Function Call
document.write(minSwaps(S, N));

// This code is contributed by patel2127
</script>
```

**Output**

```
10
```

***时间复杂度:** O(26*N)*
***辅助空间:** O(N)*