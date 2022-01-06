# 最多换 K 位做最大回文

> 原文:[https://www . geesforgeks . org/make-maximum-回文-changing-k-digits/](https://www.geeksforgeeks.org/make-largest-palindrome-changing-k-digits/)

给定一个包含所有数字的字符串，我们需要通过最多改变 K 个数字来将这个字符串转换为回文。如果有多种解决方案，那么按字典顺序打印最大的一个。
示例:

```
Input   : str = “43435”    
          k = 3
Output  : "93939" 
Explanation:
Lexicographically largest palindrome 
after 3 changes is "93939" 

Input :  str = “43435”    
         k = 1
Output : “53435”
Explanation:
Lexicographically largest palindrome 
after 3 changes is “53435”

Input  : str = “12345”    
         k = 1
Output : "Not Possible"
Explanation:
It is not possible to make str palindrome
after 1 change.
```

**进场:**

1.  用两点法解决这个问题。我们从左和右开始，如果两个数字不相等，那么我们用较大的值替换较小的值，并将 k 减少 1。S
2.  顶部当左右指针相互交叉时，如果 k 的值为负，则它们停止后，就不可能使用 k 的变化进行字符串回文。如果 k 是正的，那么我们可以通过从左到右以同样的方式循环一次，并将两个数字都转换为 9，并将 k 减 2，从而进一步最大化字符串。
3.  如果 k 值保持为 1，字符串长度为奇数，那么我们将中间字符设为 9，以最大化整数值。
    以下是上述方法的实施:

## C++

```
// C++ program to get largest palindrome changing
// atmost K digits
#include <bits/stdc++.h>
using namespace std;

// Returns maximum possible
// palindrome using k changes
string maximumPalinUsingKChanges(string str, int k)
{
    string palin = str;

    // Initialize l and r by leftmost and
    // rightmost ends
    int l = 0;
    int r = str.length() - 1;

    //  first try to make string palindrome
    while (l < r) {

        // Replace left and right character by
        // maximum of both
        if (str[l] != str[r]) {
            palin[l] = palin[r] =
                  max(str[l], str[r]);
            k--;
        }
        l++;
        r--;
    }

    // If k is negative then we can't make
    // string palindrome
    if (k < 0)
        return "Not possible";

    l = 0;
    r = str.length() - 1;

    while (l <= r) {

        // At mid character, if K>0 then change
        // it to 9
        if (l == r) {
            if (k > 0)
                palin[l] = '9';
        }

        // If character at lth (same as rth) is
        // less than 9
        if (palin[l] < '9') {
            /* If none of them is changed in the
               previous loop then subtract 2 from K
               and convert both to 9 */
            if (k >= 2 && palin[l] == str[l]
                && palin[r] == str[r]) {
                k -= 2;
                palin[l] = palin[r] = '9';
            }

            /*  If one of them is changed
                in the previous
                loop then subtract 1 from K
                (1 more is
                subtracted already) and make them 9  */
            else if (k >= 1
                     && (palin[l] != str[l]
                         || palin[r] != str[r])) {
                k--;
                palin[l] = palin[r] = '9';
            }
        }
        l++;
        r--;
    }

    return palin;
}

//  Driver code to test above methods
int main()
{
    string str = "43435";
    int k = 3;
    cout << maximumPalinUsingKChanges(str, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to get largest palindrome changing
// atmost K digits

import java.text.ParseException;

class GFG {

  // Returns maximum possible
  // palindrome using k changes
  static String maximumPalinUsingKChanges(String str,
                                          int k)
  {
    char palin[] = str.toCharArray();
    String ans = "";

    // Initialize l and r by leftmost and
    // rightmost ends
    int l = 0;
    int r = str.length() - 1;

    // First try to make String palindrome
    while (l < r) {

      // Replace left and right character by
      // maximum of both
      if (str.charAt(l) != str.charAt(r)) {
        palin[l] = palin[r] = (char)Math.max(
          str.charAt(l), str.charAt(r));
        k--;
      }
      l++;
      r--;
    }

    // If k is negative then we can't make
    // String palindrome
    if (k < 0) {
      return "Not possible";
    }

    l = 0;
    r = str.length() - 1;

    while (l <= r) {

      // At mid character, if K>0 then change
      // it to 9
      if (l == r) {
        if (k > 0) {
          palin[l] = '9';
        }
      }

      // If character at lth (same as rth) is
      // less than 9
      if (palin[l] < '9') {

        /* If none of them is changed in the
            previous loop then subtract 2 from K
            and convert both to 9 */
        if (k >= 2 && palin[l] == str.charAt(l)
            && palin[r] == str.charAt(r)) {
          k -= 2;
          palin[l] = palin[r] = '9';
        }

        /* If one of them is changed in the
        previous loop then subtract
        1 from K (1 more
        is subtracted already) and make them 9 */
        else if (k >= 1
                 && (palin[l] != str.charAt(l)
                     || palin[r]
                     != str.charAt(r))) {
          k--;
          palin[l] = palin[r] = '9';
        }
      }
      l++;
      r--;
    }
    for (int i = 0; i < palin.length; i++)
      ans += palin[i];
    return ans;
  }

  // Driver code to test above methods
  public static void main(String[] args)
    throws ParseException
  {
    String str = "43435";
    int k = 3;
    System.out.println(
      maximumPalinUsingKChanges(str, k));
  }
}
// This code is contributed by 29ajaykumar
```

## C#

```
// C# program to get largest palindrome changing
// atmost K digits

using System;
public class GFG {

  // Returns maximum possible
  // palindrome using k changes
  static String maximumPalinUsingKChanges(String str,
                                          int k)
  {
    char[] palin = str.ToCharArray();
    String ans = "";

    // Initialize l and r by leftmost and
    // rightmost ends
    int l = 0;
    int r = str.Length - 1;

    // First try to make String palindrome
    while (l < r) {

      // Replace left and right character by
      // maximum of both
      if (str[l] != str[r]) {
        palin[l] = palin[r]
          = (char)Math.Max(str[l], str[r]);
        k--;
      }
      l++;
      r--;
    }

    // If k is negative then we can't make
    // String palindrome
    if (k < 0) {
      return "Not possible";
    }

    l = 0;
    r = str.Length - 1;

    while (l <= r) {

      // At mid character, if K>0 then change
      // it to 9
      if (l == r) {
        if (k > 0) {
          palin[l] = '9';
        }
      }

      // If character at lth (same as rth) is
      // less than 9
      if (palin[l] < '9') {

        /* If none of them is changed in the
        previous loop then subtract 2 from K
        and convert both to 9 */
        if (k >= 2 && palin[l] == str[l]
            && palin[r] == str[r]) {
          k -= 2;
          palin[l] = palin[r] = '9';
        }

        /* If one of them is changed in the
        previous loop then subtract 1 from K (1 more
        is subtracted already) and make them 9 */
        else if (k >= 1
                 && (palin[l] != str[l]
                     || palin[r] != str[r])) {
          k--;
          palin[l] = palin[r] = '9';
        }
      }
      l++;
      r--;
    }
    for (int i = 0; i < palin.Length; i++)
      ans += palin[i];
    return ans;
  }

  // Driver code to test above methods
  public static void Main()
  {
    String str = "43435";
    int k = 3;
    Console.Write(maximumPalinUsingKChanges(str, k));
  }
}
// This code is contributed by Rajput-Ji
```

## 计算机编程语言

```
# Python3 program to get largest palindrome changing
# atmost K digits

# Returns maximum possible
# palindrome using k changes
def maximumPalinUsingKChanges(strr, k):
    palin = strr[::]

    # Initialize l and r by leftmost and
    # rightmost ends
    l = 0
    r = len(strr) - 1

    # first try to make palindrome
    while (l <= r):

        # Replace left and right character by
        # maximum of both
        if (strr[l] != strr[r]):
            palin[l] = palin[r] =
                   max(strr[l], strr[r])

            # print(strr[l],strr[r])
            k -= 1
        l += 1
        r -= 1

    # If k is negative then we can't make
    # palindrome
    if (k < 0):
        return "Not possible"

    l = 0
    r = len(strr) - 1

    while (l <= r):

        # At mid character, if K>0 then change
        # it to 9
        if (l == r):
            if (k > 0):
                palin[l] = '9'

        # If character at lth (same as rth) is
        # less than 9
        if (palin[l] < '9'):

            # If none of them is changed in the
            # previous loop then subtract 2 from K
            # and convert both to 9
            if (k >= 2 and palin[l] == strr[l] and
                           palin[r] == strr[r]):
                k -= 2
                palin[l] = palin[r] = '9'

            # If one of them is changed in the previous
            # loop then subtract 1 from K (1 more is
            # subtracted already) and make them 9
            elif (k >= 1 and (palin[l] != strr[l] or
                              palin[r] != strr[r])):
                k -= 1
                palin[l] = palin[r] = '9'

        l += 1
        r -= 1

    return palin

# Driver code
st = "43435"
strr = [i for i in st]
k = 3
a = maximumPalinUsingKChanges(strr, k)
print("".join(a))

# This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>
// Javascript program to get largest palindrome changing
// atmost K digits

// Returns maximum possible
  // palindrome using k changes   
function maximumPalinUsingKChanges(str,k)
{
    let palin = str.split("");
    let ans = "";

    // Initialize l and r by leftmost and
    // rightmost ends
    let l = 0;
    let r = str.length - 1;

    // First try to make String palindrome
    while (l < r) {

      // Replace left and right character by
      // maximum of both
      if (str[l] != str[r]) {
        palin[l] = palin[r] = String.fromCharCode(Math.max(
          str.charAt(l), str.charAt(r)));
        k--;
      }
      l++;
      r--;
    }

    // If k is negative then we can't make
    // String palindrome
    if (k < 0) {
      return "Not possible";
    }

    l = 0;
    r = str.length - 1;

    while (l <= r) {

      // At mid character, if K>0 then change
      // it to 9
      if (l == r) {
        if (k > 0) {
          palin[l] = '9';
        }
      }

      // If character at lth (same as rth) is
      // less than 9
      if (palin[l] < '9') {

        /* If none of them is changed in the
            previous loop then subtract 2 from K
            and convert both to 9 */
        if (k >= 2 && palin[l] == str[l]
            && palin[r] == str[r]) {
          k -= 2;
          palin[l] = palin[r] = '9';
        }

        /* If one of them is changed in the
        previous loop then subtract
        1 from K (1 more
        is subtracted already) and make them 9 */
        else if (k >= 1
                 && (palin[l] != str[l]
                     || palin[r]
                     != str[r])) {
          k--;
          palin[l] = palin[r] = '9';
        }
      }
      l++;
      r--;
    }
    for (let i = 0; i < palin.length; i++)
      ans += palin[i];
    return ans;
}

// Driver code to test above methods
let str = "43435";
let k = 3;
document.write(maximumPalinUsingKChanges(str, k));

// This code is contributed by unknown2108
</script>
```

**输出:**

```
93939
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。