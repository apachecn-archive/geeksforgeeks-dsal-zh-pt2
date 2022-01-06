# 计算分割二进制字符串的方法，使每个子字符串恰好包含两个 0

> 原文:[https://www . geesforgeks . org/count-way-to-partition-a-binary-string-so-每个子串-包含-恰好两个 0/](https://www.geeksforgeeks.org/count-ways-to-partition-a-binary-string-such-that-each-substring-contains-exactly-two-0s/)

给定[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **字符串**，任务是找到分割字符串的方法数，使得每个分割的子字符串恰好包含两个 **0** s。

**示例:**

> **输入:** str = "00100"
> **输出:** 2
> **解释:**
> 对字符串进行分区的可能方式，使得每个分区恰好包含两个 **0** 分别是:{“00”、“100”}、{“001”、“00”} }。
> 因此，要求的输出为 2。
> 
> **输入:**str = " 000 "
> T3】输出: 0

**方法:**思路是计算给定字符串每两个连续的 **0** s 之间的 **1** s 的计数。按照以下步骤解决问题:

*   初始化一个数组，比如说 **IdxOf0s[]** ，来存储给定字符串中 **0** s 的索引。
*   [迭代给定字符串的字符](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)并将 0 的索引存储到 **IdxOf0s[]** 中。
*   初始化一个变量，比如说**cntway**，来存储对字符串进行分区的方式的计数，这样每个分区正好包含两个 **0** s。
*   如果给定字符串中 **0** 的计数为奇数，则更新**计数= 0** 。
*   否则，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**idxof 0s【】**并使用**cntway * =(idxof 0s[I]–idxof 0s[I–1])**计算对数组进行分区的方式数，其中每个分区正好有两个 **0**
*   最后，打印**cntway**的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find count of ways to partition
// the string such that each partition
// contains exactly two 0s.
int totalWays(int n, string str)
{

    // Stores indices of 0s in
    // the given string.
    vector<int> IdxOf0s;

    // Store the count of ways to partition
    // the string such that each partition
    // contains exactly two 0s.
    int cntWays = 1;

    // Iterate over each characters
    // of the given string
    for (int i = 0; i < n; i++) {

        // If current character is '0'
        if (str[i] == '0') {

            // Insert index
            IdxOf0s.push_back(i);
        }
    }

    // Stores total count of 0s in str
    int M = IdxOf0s.size();

    if (M == 0 or M % 2) {

        return 0;
    }

    // Traverse the array, IdxOf0s[]
    for (int i = 2; i < M; i += 2) {

        // Update cntWays
        cntWays = cntWays * (IdxOf0s[i]
                             - IdxOf0s[i - 1]);
    }

    return cntWays;
}

// Driver Code
int main()
{
    string str = "00100";

    int n = str.length();

    cout << totalWays(n, str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to find count of ways to partition
// the string such that each partition
// contains exactly two 0s.
static int totalWays(int n, String str)
{

    // Stores indices of 0s in
    // the given string.
    ArrayList<Integer> IdxOf0s = 
                    new ArrayList<Integer>();

    // Store the count of ways to partition
    // the string such that each partition
    // contains exactly two 0s.
    int cntWays = 1;

    // Iterate over each characters
    // of the given string
    for (int i = 0; i < n; i++)
    {

        // If current character is '0'
        if (str.charAt(i) == '0')
        {

            // Insert index
            IdxOf0s.add(i);
        }
    }

    // Stores total count of 0s in str
    int M = IdxOf0s.size();
    if ((M == 0) || ((M % 2) != 0))
    {
        return 0;
    }

    // Traverse the array, IdxOf0s[]
    for (int i = 2; i < M; i += 2)
    {

        // Update cntWays
        cntWays = cntWays * (IdxOf0s.get(i)
                             - IdxOf0s.get(i - 1));
    } 
    return cntWays;
}

// Driver code
public static void main(String[] args)
{
    String str = "00100";
    int n = str.length();
    System.out.print(totalWays(n, str));
}
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find count of ways to partition
# thesuch that each partition
# contains exactly two 0s.
def totalWays(n, str):

    # Stores indices of 0s in
    # the given string.
    IdxOf0s = []

    # Store the count of ways to partition
    # the such that each partition
    # contains exactly two 0s.
    cntWays = 1

    # Iterate over each characters
    # of the given string
    for i in range(n):

        # If current character is '0'
        if (str[i] == '0'):

            # Insert index
            IdxOf0s.append(i)

    # Stores total count of 0s in str
    M = len(IdxOf0s)

    if (M == 0 or M % 2):
        return 0

    # Traverse the array, IdxOf0s[]
    for i in range(2, M, 2):

        # Update cntWays
        cntWays = cntWays * (IdxOf0s[i] -
                             IdxOf0s[i - 1])

    return cntWays

# Driver Code
if __name__ == '__main__':

   str = "00100"
   n = len(str)

   print(totalWays(n, str))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections; 
using System.Collections.Generic; 

class GFG
{

  // Function to find count of ways to partition
  // the string such that each partition
  // contains exactly two 0s.
  static int totalWays(int n, string str)
  {

    // Stores indices of 0s in
    // the given string.
    ArrayList IdxOf0s
      = new ArrayList();

    // Store the count of ways to partition
    // the string such that each partition
    // contains exactly two 0s.
    int cntWays = 1;

    // Iterate over each characters
    // of the given string
    for (int i = 0; i < n; i++)
    {

      // If current character is '0'
      if (str[i] == '0')
      {

        // Insert index
        IdxOf0s.Add(i);
      }
    }

    // Stores total count of 0s in str
    int M = IdxOf0s.Count;
    if ((M == 0) || ((M % 2) != 0)) {
      return 0;
    }

    // Traverse the array, IdxOf0s[]
    for (int i = 2; i < M; i += 2)
    {

      // Update cntWays
      cntWays = cntWays * (Convert.ToInt32(IdxOf0s[i]) -
                           Convert.ToInt32(IdxOf0s[i - 1]));
    }
    return cntWays;
  }

  // Driver code
  static public void Main()
  {
    string str = "00100";
    int n = str.Length;
    Console.Write(totalWays(n, str));
  }
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find count of ways to partition
// the string such that each partition
// contains exactly two 0s.
function totalWays(n, str)
{

    // Stores indices of 0s in
    // the given string.
    var IdxOf0s = [];

    // Store the count of ways to partition
    // the string such that each partition
    // contains exactly two 0s.
    var cntWays = 1;

    // Iterate over each characters
    // of the given string
    for (var i = 0; i < n; i++) {

        // If current character is '0'
        if (str[i] == '0') {

            // Insert index
            IdxOf0s.push(i);
        }
    }

    // Stores total count of 0s in str
    var M = IdxOf0s.length;

    if (M == 0 || M % 2) {

        return 0;
    }

    // Traverse the array, IdxOf0s[]
    for (var i = 2; i < M; i += 2) {

        // Update cntWays
        cntWays = cntWays * (IdxOf0s[i]
                            - IdxOf0s[i - 1]);
    }

    return cntWays;
}

// Driver Code
var str = "00100";
var n = str.length;
document.write( totalWays(n, str));

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)