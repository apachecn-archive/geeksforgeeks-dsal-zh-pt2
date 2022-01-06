# 最大化分区，使得没有两个子串有任何共同的字符

> 原文:[https://www . geeksforgeeks . org/maximize-partitions-so-no-two-substrings-有任何共同的字符/](https://www.geeksforgeeks.org/maximize-partitions-such-that-no-two-substrings-have-any-common-character/)

给定大小为 **N** 的字符串 **str** ，任务是打印在最大可能分割之后形成的子字符串的数量，使得没有两个子字符串具有相同的字符。
**例:**

> **输入:**str = " ababcbacadefegdehijhklij "
> **输出:** 3
> **解释:**
> 在索引 8 和索引 15 处的划分产生三个子串“ababcbaca”、“defegde”和“hijhkij”，使得它们都没有共同的字符。所以，最大分区数是 3。
> **输入:** str = "aaa"
> **输出:** 1
> **解释:**
> 由于字符串由单个字符组成，因此无法进行分区。

**进场:**

1.  从字符串末尾找到每个唯一字符的最后一个索引，并将其存储在[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。
2.  遍历数组，从索引 0 到最后一个索引，并创建一个单独的变量来存储分区的结束索引。
3.  遍历字符串中的每个变量，检查由存储在映射中的**字符串[i]** 的索引表示的分区的结束是否大于前一个结束。如果是，请更新它。
4.  检查当前变量是否超过分区的结尾。意味着找到了第一个分区。将分区的结尾更新为 **max(k，mp[str[i]])** 。
5.  遍历整个字符串，使用类似的过程找到下一个分区，以此类推。

以下是上述方法的实现:

## C++

```
// C++ program to find the
// maximum number of
// partitions possible such
// that no two substrings
// have common character

#include 
using namespace std;

// Function to calculate and return
// the maximum number of partitions
int maximum_partition(string str)
{
    // r: Stores the maximum number
    // of partitions
    // k: Stores the ending index
    // of the partition
    int i = 0, j = 0, k = 0;
    int c = 0, r = 0;

    // Stores the last index
    // of every unique character
    // of the string
    unordered_map m;

    // Traverse the string and
    // store the last index
    // of every character
    for (i = str.length() - 1;
        i >= 0;
        i--) {

        if (m[str[i]] == 0) {
            m[str[i]] = i;
        }
    }

    i = 0;

    // Store the last index of the
    // first character from map
    k = m[str[i]];

    for (i = 0; i < str.length(); i++) {

        if (i <= k) {
            c = c + 1;

            // Update K to find
            // the end of partition
            k = max(k, m[str[i]]);
        }

        // Otherwise, the end of
        // partition is found
        else {

            // Increment r
            r = r + 1;
            c = 1;

            // Update k for the
            // next partition
            k = max(k, m[str[i]]);
        }
    }

    // Add the last partition
    if (c != 0) {
        r = r + 1;
    }
    return r;
}

// Driver Program
int main()
{
    string str
        = "ababcbacadefegdehijhklij";
    cout << maximum_partition(str);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// maximum number of
// partitions possible such
// that no two subStrings
// have common character
import java.util.*;
class GFG{

// Function to calculate and return
// the maximum number of partitions
static int maximum_partition(String str)
{
  // r: Stores the maximum number
  // of partitions
  // k: Stores the ending index
  // of the partition
  int i = 0, j = 0, k = 0;
  int c = 0, r = 0;

  // Stores the last index
  // of every unique character
  // of the String
  HashMap<Character,
          Integer> m = new HashMap<>();

  // Traverse the String and
  // store the last index
  // of every character
  for (i = str.length() - 1;
       i >= 0; i--)
  {
    if (!m.containsKey(str.charAt(i)))
    {
      m.put(str.charAt(i), i);
    }
  }

  i = 0;

  // Store the last index of the
  // first character from map
  k = m.get(str.charAt(i));

  for (i = 0; i < str.length(); i++)
  {
    if (i <= k)
    {
      c = c + 1;

      // Update K to find
      // the end of partition
      k = Math.max(k, m.get(str.charAt(i)));
    }

    // Otherwise, the end of
    // partition is found
    else
    {
      // Increment r
      r = r + 1;
      c = 1;

      // Update k for the
      // next partition
      k = Math.max(k, m.get(str.charAt(i)));
    }
  }

  // Add the last
  // partition
  if (c != 0)
  {
    r = r + 1;
  }
  return r;
}

// Driver code
public static void main(String[] args)
{
  String str = "ababcbacadefegdehijhklij";
  System.out.print(maximum_partition(str));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to find the
# maximum number of
# partitions possible such
# that no two substrings
# have common character

# Function to calculate and return
# the maximum number of partitions
def maximum_partition(strr):

    # r: Stores the maximum number
    # of partitions
    # k: Stores the ending index
    # of the partition
    i = 0
    j = 0
    k = 0
    c = 0
    r = 0

    # Stores the last index
    # of every unique character
    # of the string
    m = {}

    # Traverse the and
    # store the last index
    # of every character
    for i in range(len(strr) - 1, -1, -1):

        if (strr[i] not in m):
            m[strr[i]] = i

    i = 0

    # Store the last index of the
    # first character from map
    k = m[strr[i]]

    for i in range(len(strr)):

        if (i <= k):
            c = c + 1

            # Update K to find
            # the end of partition
            k = max(k, m[strr[i]])

        # Otherwise, the end of
        # partition is found
        else:

            # Increment r
            r = r + 1
            c = 1

            # Update k for the
            # next partition
            k = max(k, m[strr[i]])

    # Add the last partition
    if (c != 0):
        r = r + 1

    return r

# Driver Code
if __name__ == '__main__':
    strr = "ababcbacadefegdehijhklij"
    print(maximum_partition(strr))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to find the
// maximum number of
// partitions possible such
// that no two subStrings
// have common character
using System;
using System.Collections.Generic;
class GFG{

// Function to calculate and return
// the maximum number of partitions
static int maximum_partition(String str)
{
  // r: Stores the maximum number
  // of partitions
  // k: Stores the ending index
  // of the partition
  int i = 0, j = 0, k = 0;
  int c = 0, r = 0;

  // Stores the last index
  // of every unique character
  // of the String
  Dictionary<char,
             int> m = new Dictionary<char,  
                                     int>();

  // Traverse the String and
  // store the last index
  // of every character
  for (i = str.Length - 1;
       i >= 0; i--)
  {
    if (!m.ContainsKey(str[i]))
    {
      m.Add(str[i], i);
    }
  }

  i = 0;

  // Store the last index of the
  // first character from map
  k = m[str[i]];

  for (i = 0; i < str.Length; i++)
  {
    if (i <= k)
    {
      c = c + 1;

      // Update K to find
      // the end of partition
      k = Math.Max(k, m[str[i]]);
    }

    // Otherwise, the end of
    // partition is found
    else
    {
      // Increment r
      r = r + 1;
      c = 1;

      // Update k for the
      // next partition
      k = Math.Max(k, m[str[i]]);
    }
  }

  // Add the last
  // partition
  if (c != 0)
  {
    r = r + 1;
  }

  return r;
}

// Driver code
public static void Main(String[] args)
{
  String str = "ababcbacadefegdehijhklij";
  Console.Write(maximum_partition(str));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program to find the
// maximum number of
// partitions possible such
// that no two substrings
// have common character

// Function to calculate and return
// the maximum number of partitions
function maximum_partition( str)
{
    // r: Stores the maximum number
    // of partitions
    // k: Stores the ending index
    // of the partition
    var i = 0, j = 0, k = 0;
    var c = 0, r = 0;

    // Stores the last index
    // of every unique character
    // of the string
    var m = new Map();

    // Traverse the string and
    // store the last index
    // of every character
    for (i = str.length - 1;
        i >= 0;
        i--) {

        if (!m.has(str[i])) {
            m.set(str[i],i);
        }
    }

    i = 0;

    // Store the last index of the
    // first character from map
    k = m.get(str[i]);

    for (i = 0; i < str.length; i++) {

        if (i <= k) {
            c = c + 1;

            // Update K to find
            // the end of partition
            k = Math.max(k, m.get(str[i]));
        }

        // Otherwise, the end of
        // partition is found
        else {

            // Increment r
            r = r + 1;
            c = 1;

            // Update k for the
            // next partition
            k = Math.max(k, m.get(str[i]));
        }
    }

    // Add the last partition
    if (c != 0) {
        r = r + 1;
    }
    return r;
}

// Driver Program
var str
    = "ababcbacadefegdehijhklij";
document.write( maximum_partition(str));

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)