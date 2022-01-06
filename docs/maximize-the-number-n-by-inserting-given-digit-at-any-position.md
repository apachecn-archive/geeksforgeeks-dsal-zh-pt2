# 通过在任意位置插入给定的数字来最大化数字 n

> 原文:[https://www . geesforgeks . org/通过在任意位置插入给定的数字来最大化数字 n/](https://www.geeksforgeeks.org/maximize-the-number-n-by-inserting-given-digit-at-any-position/)

给定一个正整数 **N** 和一个数字 **K** ，任务是通过在其中插入给定的数字**K****N**找到给定数字 **N** 的最大值。

**示例:**

> **输入:** N = 6673，K = 6
> **输出:** 66763
> **说明:**
> N 中任意位置插入 K 形成的数字全部为{66673，66763，66736}。所有形成的数字中最大的是 66763。
> 
> **输入:** N = 1234，K = 5
> T3】输出: 51234

**方法:**在**下一位数字**比 **K** 小**的位置插入 **K** 即可解决给定问题。按照以下步骤解决问题:**

*   初始化两个[字符串](https://www.geeksforgeeks.org/string-data-structure/)表示 **S** ，通过将给定的数字**N**T6】打造成一个字符串和一个字符串**结果**为 **""** ，在其中插入 **K** 后存储最大可能的数字。
*   初始化两个变量，说 **L** 为[字符串的长度](https://www.geeksforgeeks.org/5-different-methods-find-length-string-c/) **S** 和 **i** 为 **0** 。
*   [遍历字符串**S**T3**K**小于**S【I】**并将字符**S【I】**追加到字符串**结果**中。](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)
*   现在将 **K** 附加到**结果**上，然后将字符串的所有剩余字符附加到**结果**上。
*   完成以上步骤后，打印字符串**结果**和最大可能数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum value
// of N after inserting the digit K
void maximizeNumber(int N, int K)
{
    // Convert it into N to string
    string s = to_string(N);
    int L = s.length();

    // Stores the maximum value of N
    // after inserting K
    string result;
    int i = 0;

    // Iterate till all digits that
    // are not less than K
    while ((i < L) && (K <= (s[i] - '0'))) {

        // Add the current digit to
        // the string result
        result.push_back(s[i]);
        ++i;
    }

    // Add digit 'K' to result
    result.push_back(char(K + '0'));

    // Iterate through all remaining
    // characters
    while (i < L) {

        // Add current digit to result
        result.push_back(s[i]);
        ++i;
    }

    // Print the maximum number formed
    cout << result;
}

// Driver Code
int main()
{
    int N = 6673, K = 6;
    maximizeNumber(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

    // Function to find the maximum value
    // of N after inserting the digit K
public static void maximizeNumber(int N, int K)
{
    // Convert it into N to string
    String s = Integer.toString(N);
    int L = s.length();

    // Stores the maximum value of N
    // after inserting K
    String result =  "";
    int i = 0;

    // Iterate till all digits that
    // are not less than K
    while ((i < L) && (K <= ((int)s.charAt(i) - (int)'0'))) {

        // Add the current digit to
        // the string result
        result += (s.charAt(i));
        ++i;
    }

    // Add digit 'K' to result
    result += ((char)(K + (int)'0'));

    // Iterate through all remaining
    // characters
    while (i < L) {

        // Add current digit to result
        result += (s.charAt(i));
        ++i;
    }

    // Print the maximum number formed
    System.out.println(result);
}

    // Driver Code
    public static void main (String args[]) {
        int N = 6673, K = 6;
        maximizeNumber(N, K);
    }

}

// This code is contributed by _saurabh_Jaiswal.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the maximum value
# of N after inserting the digit K
def maximizeNumber(N, K):

    # Convert it into N to string
    s = str(N)
    L = len(s)

    # Stores the maximum value of N
    # after inserting K
    result = ""
    i = 0

    # Iterate till all digits that
    # are not less than K
    while ((i < L) and (K <= (ord(s[i]) - ord('0')))):

        # Add the current digit to
        # the string result
        result += (s[i])
        i += 1

    # Add digit 'K' to result
    result += (chr(K + ord('0')))

    # Iterate through all remaining
    # characters
    while (i < L):

        # Add current digit to result
        result += (s[i])
        i += 1

    # Print the maximum number formed
    print(result)

# Driver Code
if __name__ == "__main__":

    N = 6673
    K = 6
    maximizeNumber(N, K)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for above approach
using System;

class GFG{

    // Function to find the maximum value
    // of N after inserting the digit K
public static void maximizeNumber(int N, int K)
{
    // Convert it into N to string
    String s = N.ToString();
    int L = s.Length;

    // Stores the maximum value of N
    // after inserting K
    string result =  "";
    int i = 0;

    // Iterate till all digits that
    // are not less than K
    while ((i < L) && (K <= ((int)s[i]- (int)'0'))) {

        // Add the current digit to
        // the string result
        result += (s[i]);
        ++i;
    }

    // Add digit 'K' to result
    result += ((char)(K + (int)'0'));

    // Iterate through all remaining
    // characters
    while (i < L) {

        // Add current digit to result
        result += (s[i]);
        ++i;
    }

    // Print the maximum number formed
     Console.Write(result);
}
// Driver Code
static void Main()
{

    int N = 6673, K = 6;
    maximizeNumber(N, K);
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the maximum value
// of N after inserting the digit K
function maximizeNumber(N, K)
{

    // Convert it into N to string
    let s = String(N);
    let L = s.length;

    // Stores the maximum value of N
    // after inserting K
    let result = [];
    let i = 0;

    // Iterate till all digits that
    // are not less than K
    while ((i < L) && (K <= (s[i].charCodeAt(0) - '0'.charCodeAt(0)))) {

        // Add the current digit to
        // the string result
        result.push(s[i]);
        ++i;
    }

    // Add digit 'K' to result
    result.push(String.fromCharCode(K + '0'.charCodeAt(0)));

    // Iterate through all remaining
    // characters
    while (i < L) {

        // Add current digit to result
        result.push(s[i]);
        ++i;
    }

    // Print the maximum number formed
    document.write(result.join(""));
}

// Driver Code
let N = 6673, K = 6;
maximizeNumber(N, K);

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
66763
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)