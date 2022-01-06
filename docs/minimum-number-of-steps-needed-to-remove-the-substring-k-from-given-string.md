# 从给定字符串中移除子字符串 K 所需的最小步骤数

> 原文:[https://www . geesforgeks . org/从给定字符串中移除子字符串 k 所需的最小步骤数/](https://www.geeksforgeeks.org/minimum-number-of-steps-needed-to-remove-the-substring-k-from-given-string/)

给定一个二进制字符串 **S** 和一个子字符串 **K** ，任务是找到翻转二进制字符串中的字符所需的最小步骤数，使其不包含给定的子字符串 **K** 。**注:**一步到位，我们可以从 0 变为 1，反之亦然。
**示例:**

> **输入:**S =“0111011”，K =“011”
> **输出:** 2
> **解释:**
> 在上面的字符串中我们有 2 次的子字符串 011，因此更改第 3 位和第 7 位。
> 
> **输入:**S =“010010”，K =“0100”
> **输出:** 1
> **解释:**
> 在上面的字符串中我们有 1 次的子字符串 0100，将字符串的第 4 位改为 1。

**天真方法:**天真方法是使用[模式搜索](https://www.geeksforgeeks.org/naive-algorithm-for-pattern-searching/)。遍历 **N 的字符串！次** (N =二进制字符串的长度)。在每次迭代中，检查子串 **K** ，如果匹配，则增加计数。最后，打印计数，这将是使字符串不包含给定子字符串 **K** 所需的步骤数。

**时间复杂度:** *O(M*N)* 其中 **M** 为子串长度， **N** 为二进制串长度。
**辅助空间:** *O(1)*

**高效方法:**对上述方法进行优化，思路是**将子串替换为空串**，从原始串长度中减去合成串长度。之后，将结果字符串除以给定子字符串 **K** 的长度，以获得翻转给定字符串 **S** 的字符所需的最小步骤数，从而使其不包含给定子字符串 **K** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
#include <boost/algorithm/string/replace.hpp>
using namespace std;

// Function that counts the total
// number of character to be flipped
// such the string b doesn't contains
// string sub as a substring
int flipCharacters(string b,
                   string sub)
{

    // Replacing the substring with ""
    // and find the difference between
    // the length of the resultant
    // string and the original
    // string length
    int res = b.size();
    boost::replace_all(b, sub, "");
    res = res - b.size();

    // Divide the result
    // with substring length
    int temp = res / sub.size();

    // Return the final count
    return temp;
}

// Driver Code
int main()
{

    // Given string S and substring K
    string S = "010010";
    string K = "0100";

    // Function call
    int result = flipCharacters(S, K);

    // Print the minimum flip
    cout << (result);
}

// This code is contributed by Amit Katiyar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

public class Test {

    // Function that counts the total
    // number of character to be flipped
    // such the string b doesn't contains
    // string sub as a substring
    static int flipCharacters(String b,
                              String sub)
    {

        // Replacing the substring with ""
        // and find the difference between
        // the length of the resultant
        // string and the original
        // string length

        int res = b.length()
                  - b.replaceAll(sub, "")
                        .length();

        // Divide the result
        // with substring length

        int temp = res / sub.length();

        // Return the final count
        return temp;
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given string S and substring K
        String S = "010010";
        String K = "0100";

        // Function Call
        int result = flipCharacters(S, K);

        // Print the minimum flip
        System.out.println(result);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
def flipCharacters(b, sub):

    # Replace the substring with
    # "" (emptryString)
    b1 = b.replace(sub, "")

    n = int((len(b)-len(b1))/len(sub))

    return n

# Driver Code
if __name__ == '__main__':

# Given string S and substring K
    S ="010010"
    X ="0100"

# Function Call
    result = flipCharacters(S, X)

# Print the minimum flip
    print(result)
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function that counts the total
  // number of character to be flipped
  // such the string b doesn't contains
  // string sub as a substring
  static int flipCharacters(string b,
                            string sub)
  {

    // Replacing the substring with ""
    // and find the difference between
    // the length of the resultant
    // string and the original
    // string length

    int res = b.Length -
              b.Replace(sub, "").Length;

    // Divide the result
    // with substring length
    int temp = res / sub.Length;

    // Return the final count
    return temp;
  }

  // Driver Code
  public static void Main(string[] args)
  {

    // Given string S and substring K
    string S = "010010";
    string K = "0100";

    // Function Call
    int result = flipCharacters(S, K);

    // Print the minimum flip
    Console.Write(result);
  }
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function that counts the total
// number of character to be flipped
// such the string b doesn't contains
// string sub as a substring
function flipCharacters(b, sub)
{

    // Replacing the substring with ""
    // and find the difference between
    // the length of the resultant
    // string and the original
    // string length
    var res = b.length - b.replace(sub, "").length;

    // Divide the result
    // with substring length
    var temp = parseInt(res / sub.length);

    // Return the final count
    return temp;
}

// Driver Code

// Given string S and substring K
var S = "010010";
var K = "0100";

// Function call
var result = flipCharacters(S, K);

// Print the minimum flip
document.write(result);

</script>
```

**Output:** 

```
1
```

**时间复杂度:** *O(N)* ，其中 N 是字符串的长度。
T5【辅助空间: *O(1)*