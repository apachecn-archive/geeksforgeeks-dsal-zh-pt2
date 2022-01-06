# 通过重复删除具有不同开始和结束的子字符串，最小化移动以清空字符串

> 原文:[https://www . geesforgeks . org/minimum-moves-to-empty-a-string-by-reply-deleting-substrings-with-differential-start-and-end/](https://www.geeksforgeeks.org/minimum-moves-to-empty-a-string-by-repeatedly-deleting-substrings-with-different-start-and-end/)

给定一个字符串 **str** ，任务是通过**删除**任何以**开头**和**结尾**字符不同**的子字符串，找到使 **str** 为空所需的**最小**移动次数。如果不能清空字符串，返回“ **-1** ”。**

**示例:**

> **输入:** str = "abba"
> **输出:** 2
> **解释:**按照以下步骤得到空字符串:“ABBA”->(删除 ab)->“ba”->(删除 ba) - >”
> 
> **输入:** aba
> **输出:** -1
> **说明:**给定字符串不可能清空。
> 
> **输入:**ABC
> T3】输出: 1

**进场:**任务可以在观察的基础上解决。

*   如果第一个和最后一个字符不相等，那么只需要**一个**操作
*   否则，检查是否有任何 **2** 指标，**与**第一个** & **最后一个**字符不匹配。如果存在，所需的**最小**操作次数为**两次**，否则**不可能**将管柱缩至空管柱。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of moves
// required to make the string empty.
void numberOfMoves(string& str, int n)
{
    // If the first and the last
    // character are different
    if (str[0] != str[n - 1]) {
        cout << "1";
        return;
    }

    // Check if there is a index i such that
    // s[i] != s[0] and s[i+1] != s[n-1]
    for (int i = 0; i < n - 1; i++) {
        if (str[i] != str[0]
            && str[i + 1] != str[n - 1]) {
            cout << "2";
            return;
        }
    }

    // If no such index exists then
    // the answer is -1
    cout << -1;
    return;
}

// Driver Code
int main()
{
    string str = "abba";
    int n = 4;
    numberOfMoves(str, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.io.*;

class GFG
{

  // Function to find the number of moves
  // required to make the string empty.
  static void numberOfMoves(String str, int n)
  {

    // If the first and the last
    // character are different
    if (str.charAt(0) != str.charAt(n-1)) {
      System.out.println("1");
      return;
    }

    // Check if there is a index i such that
    // s[i] != s[0] and s[i+1] != s[n-1]
    for (int i = 0; i < n - 1; i++) {
      if (str.charAt(i) != str.charAt(0)
          && str.charAt(i+1) != str.charAt(n-1)) {
        System.out.println("2");
        return;
      }
    }

    // If no such index exists then
    // the answer is -1
    System.out.println(-1);
    return;
  }

  // Driver Code
  public static void main (String[] args) {
    String str = "abba";
    int n = 4;
    numberOfMoves(str, n);

  }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Pyhton program for the above approach

# Function to find the number of moves
# required to make the string empty.
def numberOfMoves(str, n):

    # If the first and the last
    # character are different
    if (str[0] != str[n - 1]):
        print("1")
        return

    # Check if there is a index i such that
    # s[i] != s[0] and s[i+1] != s[n-1]
    for i in range(0, len(str)):
        if (str[i] != str[0] and
            str[i + 1] != str[n - 1]):

            print("2")
            return

    # If no such index exists then
    # the answer is -1
    print(-1)
    return

# Driver Code
if __name__ == '__main__':

    str = "abba"
    n = 4;
    numberOfMoves(str, n);

    # This code is contributed by Samim Hossain Mondal.
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

// Function to find the number of moves
// required to make the string empty.
static void numberOfMoves(string str, int n)
{

    // If the first and the last
    // character are different
    if (str[0] != str[n - 1]) {
        Console.WriteLine("1");
        return;
    }

    // Check if there is a index i such that
    // s[i] != s[0] and s[i+1] != s[n-1]
    for (int i = 0; i < n - 1; i++) {
        if (str[i] != str[0]
            && str[i + 1] != str[n - 1]) {
            Console.WriteLine("2");
            return;
        }
    }

    // If no such index exists then
    // the answer is -1
    Console.WriteLine(-1);
    return;
}

// Driver Code
public static void Main(String []args) {

    string str = "abba";
    int n = 4;
    numberOfMoves(str, n);
}
}

// This code is contributed by target_2.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the number of moves
// required to make the string empty.
function numberOfMoves(str, n) {
  // If the first and the last
  // character are different
  if (str[0] != str[n - 1]) {
    document.write("1");
    return;
  }

  // Check if there is a index i such that
  // s[i] != s[0] and s[i+1] != s[n-1]
  for (let i = 0; i < n - 1; i++) {
    if (str[i] != str[0]
      && str[i + 1] != str[n - 1]) {
      document.write("2");
      return;
    }
  }

  // If no such index exists then
  // the answer is -1
  document.write(-1);
  return;
}

// Driver Code

let str = "abba";
let n = 4;
numberOfMoves(str, n);

// This code is contributed by gfgking.
</script>
```

**Output**

```
2
```

***时间复杂度*****:**O(N)
***辅助空间*** **:** O(1)。