# 通过最多进行 K 次交换来找到最大可能数量

> 原文:[https://www . geeksforgeeks . org/find-最多可做 k 次交换的最大数量/](https://www.geeksforgeeks.org/find-maximum-number-possible-by-doing-at-most-k-swaps/)

给定一个正整数，通过对其数字进行至多 K 次交换操作，找到可能的最大整数。
**例:**

```
Input: M = 254, K = 1
Output: 524
Swap 5 with 2 so number becomes 524

Input: M = 254, K = 2
Output: 542
Swap 5 with 2 so number becomes 524
Swap 4 with 2 so number becomes 542

Input: M = 68543, K = 1 
Output: 86543
Swap 8 with 6 so number becomes 86543

Input: M = 7599, K = 2
Output: 9975
Swap 9 with 5 so number becomes 7995
Swap 9 with 7 so number becomes 9975

Input: M = 76543, K = 1 
Output: 76543
Explanation: No swap is required.

Input: M = 129814999, K = 4
Output: 999984211
Swap 9 with 1 so number becomes 929814991
Swap 9 with 2 so number becomes 999814291
Swap 9 with 8 so number becomes 999914281
Swap 1 with 8 so number becomes 999984211
```

**<u>天真解:</u>**
**进场:**思路是把每个数字都考虑进去，换成跟在后面的数字，一次一个，看是否引出最大数。该过程重复 K 次。如果当前数字与少于下一个数字的数字交换，代码可以进一步优化。
**算法:**

1.  创建一个存储最大字符串或数字的全局变量。
2.  定义一个递归函数，将字符串作为数字和 k 的值
3.  运行嵌套循环，外部循环从 0 到字符串长度-1，内部循环从 i+1 到字符串结尾。
4.  交换 ith 和 jth 字符，检查字符串现在是否是最大值，并更新最大字符串。
5.  用参数递归调用函数:string 和 k-1。
6.  现在再次交换回第 I 个和第 jth 个字符。

## C++

```
// C++ program to find maximum
// integer possible by doing
// at-most K swap operations
// on its digits.
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum
// integer possible by
// doing at-most K swap
// operations on its digits
void findMaximumNum(
    string str, int k, string& max)
{
    // Return if no swaps left
    if (k == 0)
        return;

    int n = str.length();

    // Consider every digit
    for (int i = 0; i < n - 1; i++) {

        // Compare it with all digits after it
        for (int j = i + 1; j < n; j++) {
            // if digit at position i
            // is less than digit
            // at position j, swap it
            // and check for maximum
            // number so far and recurse
            // for remaining swaps
            if (str[i] < str[j]) {
                // swap str[i] with str[j]
                swap(str[i], str[j]);

                // If current num is more
                // than maximum so far
                if (str.compare(max) > 0)
                    max = str;

                // recurse of the other k - 1 swaps
                findMaximumNum(str, k - 1, max);

                // Backtrack
                swap(str[i], str[j]);
            }
        }
    }
}

// Driver code
int main()
{
    string str = "129814999";

    int k = 4;

    string max = str;
    findMaximumNum(str, k, max);

    cout << max << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum
// integer possible by doing
// at-most K swap operations
// on its digits.
import java.util.*;
class GFG{

static String max;
// Function to find maximum
// integer possible by
// doing at-most K swap
// operations on its digits
static void findMaximumNum(char[] str,
                           int k)
{
  // Return if no swaps left
  if (k == 0)
    return;

  int n = str.length;

  // Consider every digit
  for (int i = 0; i < n - 1; i++)
  {
    // Compare it with all digits
    // after it
    for (int j = i + 1; j < n; j++)
    {
      // if digit at position i
      // is less than digit
      // at position j, swap it
      // and check for maximum
      // number so far and recurse
      // for remaining swaps
      if (str[i] < str[j])
      {
        // swap str[i] with
        // str[j]
        char t = str[i];
        str[i] = str[j];
        str[j] = t;

        // If current num is more
        // than maximum so far
        if (String.valueOf(str).compareTo(max) > 0)
          max = String.valueOf(str);

        // recurse of the other
        // k - 1 swaps
        findMaximumNum(str, k - 1);

        // Backtrack
        char c = str[i];
        str[i] = str[j];
        str[j] = c;
      }
    }
  }
}

// Driver code
public static void main(String[] args)
{
  String str = "129814999";
  int k = 4;
  max = str;
  findMaximumNum(str.toCharArray(), k);
  System.out.print(max + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find maximum
# integer possible by doing at-most
# K swap operations on its digits.

# utility function to swap two
# characters of a string
def swap(string, i, j):

    return (string[:i] + string[j] +
            string[i + 1:j] +
            string[i] + string[j + 1:])

# function to find maximum integer
# possible by doing at-most K swap
# operations on its digits
def findMaximumNum(string, k, maxm):

    # return if no swaps left
    if k == 0:
        return

    n = len(string)

    # consider every digit
    for i in range(n - 1):

        # and compare it with all digits after it
        for j in range(i + 1, n):

            # if digit at position i is less than
            # digit at position j, swap it and
            # check for maximum number so far and
            # recurse for remaining swaps
            if string[i] < string[j]:

                # swap string[i] with string[j]
                string = swap(string, i, j)

                # If current num is more than
                # maximum so far
                if string > maxm[0]:
                    maxm[0] = string

                # recurse of the other k - 1 swaps
                findMaximumNum(string, k - 1, maxm)

                # backtrack
                string = swap(string, i, j)

# Driver Code
if __name__ == "__main__":
    string = "129814999"
    k = 4
    maxm = [string]
    findMaximumNum(string, k, maxm)
    print(maxm[0])

# This code is contributed
# by vibhu4agarwal
```

## C#

```
// C# program to find maximum
// integer possible by doing
// at-most K swap operations
// on its digits.
using System;
class GFG{

static String max;
// Function to find maximum
// integer possible by
// doing at-most K swap
// operations on its digits
static void findMaximumNum(char[] str,
                           int k)
{
  // Return if no swaps left
  if (k == 0)
    return;

  int n = str.Length;

  // Consider every digit
  for (int i = 0; i < n - 1; i++)
  {
    // Compare it with all digits
    // after it
    for (int j = i + 1; j < n; j++)
    {
      // if digit at position i
      // is less than digit
      // at position j, swap it
      // and check for maximum
      // number so far and recurse
      // for remaining swaps
      if (str[i] < str[j])
      {
        // swap str[i] with
        // str[j]
        char t = str[i];
        str[i] = str[j];
        str[j] = t;

        // If current num is more
        // than maximum so far
        if (String.Join("", str).CompareTo(max) > 0)
          max = String.Join("", str);

        // recurse of the other
        // k - 1 swaps
        findMaximumNum(str, k - 1);

        // Backtrack
        char c = str[i];
        str[i] = str[j];
        str[j] = c;
      }
    }
  }
}

// Driver code
public static void Main(String[] args)
{
  String str = "129814999";
  int k = 4;
  max = str;
  findMaximumNum(str.ToCharArray(), k);
  Console.Write(max + "\n");
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Javascript program to find maximum
// integer possible by doing
// at-most K swap operations
// on its digits.

let max;

// Function to find maximum
// integer possible by
// doing at-most K swap
// operations on its digits
function findMaximumNum(str,k)
{

    // Return if no swaps left
  if (k == 0)
    return;

  let n = str.length;

  // Consider every digit
  for (let i = 0; i < n - 1; i++)
  {

    // Compare it with all digits
    // after it
    for (let j = i + 1; j < n; j++)
    {
      // if digit at position i
      // is less than digit
      // at position j, swap it
      // and check for maximum
      // number so far and recurse
      // for remaining swaps
      if (str[i] < str[j])
      {

        // swap str[i] with
        // str[j]
        let t = str[i];
        str[i] = str[j];
        str[j] = t;

        // If current num is more
        // than maximum so far
        if ((str).join("")>(max) )
          max = (str).join("");

        // recurse of the other
        // k - 1 swaps
        findMaximumNum(str, k - 1);

        // Backtrack
        let c = str[i];
        str[i] = str[j];
        str[j] = c;
      }
    }
  }
}

// Driver code
let str = "129814999";
let k = 4;
max = str;
findMaximumNum(str.split(""), k);
document.write(max + "<br>");

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
999984211
```

**复杂度分析:**

*   **时间复杂度:** O((n^2)^k).
    对于每个递归调用，生成 n^2 递归调用，直到 k 的值为 0。所以递归调用总数是 O((n^2)^k).
*   **空间复杂度:** O(n)。
    这是存储输出字符串所需的空间。

**<u>【高效解决方案】</u> :**
**方法:**上述方法在每次递归调用时遍历整个字符串，这是非常低效和不必要的。此外，在递归调用中预先计算当前数字之后的最大数字，可以避免与每个数字进行不必要的交换。可以观察到，为了制作最大字符串，最大数字被移到前面。因此，不要尝试所有的对，只尝试那些其中一个元素是最大数字但还没有交换到前面的对。
*每一个测试用例*都有 27580 微秒的提升。
**算法:**

1.  创建一个存储最大字符串或数字的全局变量。
2.  定义一个递归函数，将字符串作为数字、k 值和当前索引。
3.  在当前索引结束的范围内找到最大元素的索引。
4.  如果最大元素的索引不等于当前索引，则递减 k 的值。
5.  运行从当前索引到数组末尾的循环
6.  如果第 I 个数字等于最大元素
7.  在当前索引处交换 ith 和元素，检查字符串现在是否是最大值，并更新最大字符串。
8.  用参数递归调用函数:string 和 k。
9.  现在再一次在当前指数上换回 ith 和 lemon。

## C++

```
// C++ program to find maximum
// integer possible by doing
// at-most K swap operations on
// its digits.
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum
// integer possible by
// doing at-most K swap operations
// on its digits
void findMaximumNum(
    string str, int k,
    string& max, int ctr)
{
    // return if no swaps left
    if (k == 0)
        return;

    int n = str.length();

    // Consider every digit after
    // the cur position
    char maxm = str[ctr];
    for (int j = ctr + 1; j < n; j++) {
        // Find maximum digit greater
        // than at ctr among rest
        if (maxm < str[j])
            maxm = str[j];
    }

    // If maxm is not equal to str[ctr],
    // decrement k
    if (maxm != str[ctr])
        --k;

    // search this maximum among the rest from behind
    //first swap the last maximum digit if it occurs more then 1 time
   //example str= 1293498 and k=1 then max string is 9293418 instead of 9213498
    for (int j = n-1; j >=ctr; j--) {
        // If digit equals maxm swap
        // the digit with current
        // digit and recurse for the rest
        if (str[j] == maxm) {
            // swap str[ctr] with str[j]
            swap(str[ctr], str[j]);

            // If current num is more than
            // maximum so far
            if (str.compare(max) > 0)
                max = str;

            // recurse other swaps after cur
            findMaximumNum(str, k, max, ctr + 1);

            // Backtrack
            swap(str[ctr], str[j]);
        }
    }
}

// Driver code
int main()
{
    string str = "129814999";
    int k = 4;

    string max = str;
    findMaximumNum(str, k, max, 0);

    cout << max << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum
// integer possible by doing
// at-most K swap operations on
// its digits.

import java.io.*;
class Res {
    static String max = "";
}

class Solution {
    // Function to set highest possible digits at given
    // index.
    public static void findMaximumNum(char ar[], int k,
                                      Res r)
    {
        if (k == 0)
            return;
        int n = ar.length;
        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {
                // if digit at position i is less than digit
                // at position j, we swap them and check for
                // maximum number so far.
                if (ar[j] > ar[i]) {
                    char temp = ar[i];
                    ar[i] = ar[j];
                    ar[j] = temp;

                    String st = new String(ar);

                    // if current number is more than
                    // maximum so far
                    if (r.max.compareTo(st) < 0) {
                        r.max = st;
                    }
                    // calling recursive function to set the
                    // next digit.
                    findMaximumNum(ar, k - 1, r);

                    // backtracking
                    temp = ar[i];
                    ar[i] = ar[j];
                    ar[j] = temp;
                }
            }
        }
    }

    // Function to find the largest number after k swaps.
    public static void main(String[] args)
    {
        String str = "129814999";
        int k = 4;
        Res r = new Res();
        r.max = str;
        findMaximumNum(str.toCharArray(), k, r);
        //Print the answer stored in res class
        System.out.println(r.max);
    }
}
```

**Output:** 

```
999984211
```

**复杂度分析:**

*   **时间复杂度:** O(n^k).
    对于每个递归调用，生成 n 个递归调用，直到 k 的值为 0。所以递归调用总数是 O((n)^k).
*   **空间复杂度:** O(n)。
    存储输出字符串所需的空间。

**运动:**

1.  通过对其数字进行至少 K 次交换操作，找到可能的最小整数。
2.  通过对其数字进行 K 次交换操作，找到可能的最大/最小整数。

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。