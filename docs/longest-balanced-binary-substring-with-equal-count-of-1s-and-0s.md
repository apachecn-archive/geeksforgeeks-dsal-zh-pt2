# 1 和 0 计数相等的最长平衡二进制子串

> 原文:[https://www . geeksforgeeks . org/最长平衡二进制子串等于 1 和 0 的计数/](https://www.geeksforgeeks.org/longest-balanced-binary-substring-with-equal-count-of-1s-and-0s/)

给定一个大小为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **字符串[]** 。任务是找到最长的平衡[子串](https://www.geeksforgeeks.org/substring-in-java/)。如果子串包含相等数量的 **0** 和 **1** ，则该子串是平衡的。

**示例:**

> **输入:** str = "110101010"
> **输出:** 10101010
> **说明:**形成的子串包含相等的 1 和 0 的计数，即 1 和 0 的计数相同等于 4。
> 
> **输入:** str = "0000"
> **输出:** -1

**天真方法:**一个简单的解决方案是使用两个嵌套循环来[生成每个子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)。以及第三循环，对当前[子串](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)中的 **0s** 和 **1s** 的数量进行计数。然后打印其中最长的子串。
***时间复杂度:** O(N^3)*
***辅助空间:** O(1)*

**高效解:**借助预计算，存储 **0s** 的计数与 **1s** 的计数从开始到当前指标的差值。然后，该差值可用于确定相等的最长子串 **0s** 和 **1s** ，作为差值数组中任何重复值之间的最大距离。使用[基于地图的哈希](https://www.geeksforgeeks.org/hashing-data-structure/)进行预计算。按照以下步骤解决问题:

*   [初始化地图< int，int >](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) **m[]。**
*   将**m【0】**的值设置为 **-1。**
*   初始化变量 **count_0，count_1，res，开始**和**结束**。
*   [使用变量 **i** 遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **字符串【】**，并执行以下任务:
    *   将 **1s** 和 **0s** 的计数分别记录为 **count_1** 和 **count_0** 。
    *   查看 **count_1** 和 **count_0** 之间的当前差值是否已经存在于地图**m【】**中。如果是，则执行以下任务:
        *   来自先前外观和当前索引的子串具有相同数量的 **0s** 和 **1s** 。
        *   如果当前找到的子串长度大于 **res** ，则将找到的子串设置为目前为止的答案。
    *   如果是第一次出现，将当前差值和当前索引存储在地图中，即**m【count _ 1–count _ 0】**等于 **i** 。
*   如果 **count_0** 和 **count_1** 都是 **0、**，则打印 **-1。**
*   否则，打印从**开始到**结束的子串。

下面是上述方法的实现。

## C++

```
// C++ for finding length
// of longest balanced substring
#include <bits/stdc++.h>
using namespace std;

// Returns length of the longest substring
// with equal number of zeros and ones.
string stringLen(string str)
{

    // Create a map to store differences
    // between counts of 1s and 0s.
    map<int, int> m;

    // Initially difference is 0.
    m[0] = -1;

    int count_0 = 0, count_1 = 0;
    int start, end, res = 0;
    for (int i = 0; i < str.size(); i++) {

        // Keeping track of counts of
        // 0s and 1s.
        if (str[i] == '0')
            count_0++;
        else
            count_1++;

        // If difference between current counts
        // already exists, then substring between
        // previous and current index has same
        // no. of 0s and 1s. Update result if this
        // substring is more than current result.
        if (m.find(count_1 - count_0) != m.end()) {

            if ((i - m[count_1 - count_0]) > res) {

                start = m.find(
                             count_1 - count_0)
                            ->second;
                end = i;
                res = end - start;
            }
        }

        // If current difference
        // is seen first time.
        else
            m[count_1 - count_0] = i;
    }

    if (count_0 == 0 || count_1 == 0)
        return "-1";

    // Return the substring
    // between found indices
    return str.substr(start + 1, end + 1);
}

// Driver Code
int main()
{
    string str = "110101010";
    cout << stringLen(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.io.*;
class GFG
{

  // Returns length of the longest substring
  // with equal number of zeros and ones.
  static String stringLen(String str)
  {

    // Create a map to store differences
    // between counts of 1s and 0s.
    int [] m = new int[100000];

    // Initially difference is 0.
    m[0] = -1;

    int count_0 = 0; int count_1 = 0;
    int start = 0; int end = 0; int res = 0;
    for (int i = 0; i < str.length(); i++) {

      // Keeping track of counts of
      // 0s and 1s.
      if (str.charAt(i) == '0')
        count_0++;
      else
        count_1++;

      // If difference between current counts
      // already exists, then substring between
      // previous and current index has same
      // no. of 0s and 1s. Update result if this
      // substring is more than current result.
      if (m[count_1 - count_0]!= 0) {

        if ((i - m[count_1 - count_0]) > res) {

          start = m[count_1 - count_0];

          end = i;
          res = end - start;
        }
      }

      // If current difference
      // is seen first time.
      else
        m[count_1 - count_0] = i;
    }

    if (count_0 == 0 || count_1 == 0)
      return "-1";

    // Return the substring
    // between found indices
    return str.substring(start , end + 2);
  }

  // Driver Code
  public static void main (String[] args)
  {
    String str = "110101010";

    System.out.println(stringLen(str));
  }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python for finding length
# of longest balanced substring

# Returns length of the longest substring
# with equal number of zeros and ones.
def stringLen (str) :

    # Create a map to store differences
    # between counts of 1s and 0s.
    m = {}

    # Initially difference is 0.
    m[0] = -1

    count_0 = 0
    count_1 = 0
    res = 0
    for i in range(len(str)):

        # Keeping track of counts of
        # 0s and 1s.
        if (str[i] == '0'):
            count_0 += 1
        else:
            count_1 += 1

        # If difference between current counts
        # already exists, then substring between
        # previous and current index has same
        # no. of 0s and 1s. Update result if this
        # substring is more than current result.
        if ((count_1 - count_0) in m):

            if ((i - m[count_1 - count_0]) > res):

                start = m[(count_1 - count_0)]
                end = i
                res = end - start

        # If current difference
        # is seen first time.
        else:
            m[count_1 - count_0] = i

    if (count_0 == 0 or count_1 == 0):
        return "-1"

    # Return the substring
    # between found indices
    return str[start + 1 : start + 1 + end + 1]

# Driver Code
str = "110101010"
print(stringLen(str))

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# code for the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

  // Returns length of the longest substring
  // with equal number of zeros and ones.
  static string stringLen(string str)
  {

    // Create a map to store differences
    // between counts of 1s and 0s.
    int []m = new int[100000];

    // Initially difference is 0.
    m[0] = -1;

    int count_0 = 0; int count_1 = 0;
    int start = 0; int end = 0; int res = 0;
    for (int i = 0; i < str.Length; i++) {

      // Keeping track of counts of
      // 0s and 1s.
      if (str[i] == '0')
        count_0++;
      else
        count_1++;

      // If difference between current counts
      // already exists, then substring between
      // previous and current index has same
      // no. of 0s and 1s. Update result if this
      // substring is more than current result.
      if (m[count_1 - count_0]!= 0) {

        if ((i - m[count_1 - count_0]) > res) {

          start = m[count_1 - count_0];

          end = i;
          res = end - start;
        }
      }

      // If current difference
      // is seen first time.
      else
        m[count_1 - count_0] = i;
    }

    if (count_0 == 0 || count_1 == 0)
      return "-1";

    // Return the substring
    // between found indices
    return str.Substring(start, end - start + 2);
  }

  // Driver Code
  public static void Main ()
  {
    string str = "110101010";

    Console.Write(stringLen(str));
  }
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
    // JavaScript for finding length
    // of longest balanced substring

    // Returns length of the longest substring
    // with equal number of zeros and ones.
    const stringLen = (str) => {

        // Create a map to store differences
        // between counts of 1s and 0s.
        let m = {};

        // Initially difference is 0.
        m[0] = -1;

        let count_0 = 0, count_1 = 0;
        let start, end, res = 0;
        for (let i = 0; i < str.length; i++) {

            // Keeping track of counts of
            // 0s and 1s.
            if (str[i] == '0')
                count_0++;
            else
                count_1++;

            // If difference between current counts
            // already exists, then substring between
            // previous and current index has same
            // no. of 0s and 1s. Update result if this
            // substring is more than current result.
            if ((count_1 - count_0) in m) {

                if ((i - m[count_1 - count_0]) > res) {

                    start = m[(count_1 - count_0)];
                    end = i;
                    res = end - start;
                }
            }

            // If current difference
            // is seen first time.
            else
                m[count_1 - count_0] = i;
        }

        if (count_0 == 0 || count_1 == 0)
            return "-1";

        // Return the substring
        // between found indices
        return str.substring(start + 1, start + 1 + end + 1);
    }

    // Driver Code
    let str = "110101010";
    document.write(stringLen(str));

    // This code is contributed by rakeshsahni
</script>
```

**Output**

```
10101010
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)