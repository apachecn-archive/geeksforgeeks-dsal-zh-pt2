# 最小移动结束操作，使所有字符串相等

> 原文:[https://www . geesforgeks . org/minimum-move-end-operations-make-strings-equal/](https://www.geeksforgeeks.org/minimum-move-end-operations-make-strings-equal/)

给定 n 个相互排列的字符串。我们需要通过一个操作使所有字符串相同，该操作获取任何字符串的前一个字符并将其移动到最后。
**例:**

```
Input : n = 2
        arr[] = {"molzv", "lzvmo"}
Output : 2
Explanation: In first string, we remove
first element("m") from first string and 
append it end. Then we move second character
of first string and move it to end. So after
2 operations, both strings become same.

Input : n = 3
        arr[] = {"kc", "kc", "kc"}
Output : 0
Explanation: already all strings are equal.
```

移动结束操作基本上是左旋转。我们使用[中讨论的方法检查字符串是否是彼此的旋转](https://www.geeksforgeeks.org/a-program-to-check-if-strings-are-rotations-of-each-other/)来计算使两个字符串相同所需的移动到前面的操作的次数。我们一个接一个地将每个字符串视为目标字符串。我们计算使所有其他字符串与当前目标相同所需的旋转次数，最后返回最少的次数。
以下是上述办法的实施情况。

## C++

```
// CPP program to make all strings same using
// move to end operations.
#include <bits/stdc++.h>
using namespace std;

// Returns minimum number of moves to end
// operations to make all strings same.
int minimunMoves(string arr[], int n)
{
    int ans = INT_MAX;
    for (int i = 0; i < n; i++)
    {
        int curr_count = 0; 

        // Consider s[i] as target string and
        // count rotations required to make
        // all other strings same as str[i].
        for (int j = 0; j < n; j++) {

            string tmp = arr[j] + arr[j];

            // find function returns the index where we
            // found arr[i] which is actually count of
            // move-to-front operations.
            int index = tmp.find(arr[i]);

            // If any two strings are not rotations of
            // each other, we can't make them same. 
            if (index == string::npos)
                return -1;

            curr_count += index;
        }

        ans = min(curr_count, ans);
    }

    return ans;
}

// driver code for above function.
int main()
{
    string arr[] = {"xzzwo", "zwoxz", "zzwox", "xzzwo"}; 
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << minimunMoves(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to make all
// strings same using move
// to end operations.
import java.util.*;
class GFG
{

// Returns minimum number of
// moves to end operations
// to make all strings same.
static int minimunMoves(String arr[], int n)
{
    int ans = Integer.MAX_VALUE;
    for (int i = 0; i < n; i++)
    {
        int curr_count = 0;

        // Consider s[i] as target
        // string and count rotations
        // required to make all other
        // strings same as str[i].
        String tmp = "";
        for (int j = 0; j < n; j++)
        {
            tmp = arr[j] + arr[j];

            // find function returns the
            // index where we found arr[i]
            // which is actually count of
            // move-to-front operations.
            int index = tmp.indexOf(arr[i]);

            // If any two strings are not
            // rotations of each other,
            // we can't make them same.
            if (index != -1)
                curr_count += index;
            else
                curr_count = -1; 
        }

        ans = Math.min(curr_count, ans);
    }

    return ans;
}

// Driver code
public static void main(String args[])
{
    String arr[] = {"xzzwo", "zwoxz",
                    "zzwox", "xzzwo"};
    int n = arr.length;
    System.out.println(minimunMoves(arr, n));
}
}

// This code is contributed
// by Kirti_Mangal
```

## 蟒蛇 3

```
# Python 3 program to make all strings
# same using move to end operations.
import sys

# Returns minimum number of moves to end
# operations to make all strings same.
def minimunMoves(arr, n):

    ans = sys.maxsize
    for i in range(n):

        curr_count = 0

        # Consider s[i] as target string and
        # count rotations required to make
        # all other strings same as str[i].
        for j in range(n):

            tmp = arr[j] + arr[j]

            # find function returns the index where
            # we found arr[i] which is actually
            # count of move-to-front operations.
            index = tmp.find(arr[i])

            # If any two strings are not rotations of
            # each other, we can't make them same.
            if (index == len(arr[i])):
                return -1

            curr_count += index

        ans = min(curr_count, ans)

    return ans

# Driver Code
if __name__ == "__main__":

    arr = ["xzzwo", "zwoxz", "zzwox", "xzzwo"]
    n = len(arr)
    print( minimunMoves(arr, n))

# This code is contributed by ita_c
```

## C#

```
using System;

// C# program to make all
// strings same using move
// to end operations.
public class GFG
{

// Returns minimum number of
// moves to end operations
// to make all strings same.
public  static int minimunMoves(string[] arr, int n)
{
    int ans = int.MaxValue;
    for (int i = 0; i < n; i++)
    {
        int curr_count = 0;

        // Consider s[i] as target
        // string and count rotations
        // required to make all other
        // strings same as str[i].
        string tmp = "";
        for (int j = 0; j < n; j++)
        {
            tmp = arr[j] + arr[j];

            // find function returns the
            // index where we found arr[i]
            // which is actually count of
            // move-to-front operations.
            int index = tmp.IndexOf(arr[i], StringComparison.Ordinal);

            // If any two strings are not
            // rotations of each other,
            // we can't make them same.
            if (index == arr[i].Length)
            {
                return -1;
            }

            curr_count += index;
        }

        ans = Math.Min(curr_count, ans);
    }

    return ans;
}

// Driver code
public static void Main(string[] args)
{
    string[] arr = new string[] {"xzzwo", "zwoxz", "zzwox", "xzzwo"};
    int n = arr.Length;
    Console.WriteLine(minimunMoves(arr, n));
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript program to make all
// strings same using move
// to end operations.

    // Returns minimum number of
    // moves to end operations
    // to make all strings same.
    function minimunMoves(arr,n)
    {
        let ans = Number.MAX_VALUE;
    for (let i = 0; i < n; i++)
    {
        let curr_count = 0;

        // Consider s[i] as target
        // string and count rotations
        // required to make all other
        // strings same as str[i].
        let tmp = "";
        for (let j = 0; j < n; j++)
        {
            tmp = arr[j] + arr[j];

            // find function returns the
            // index where we found arr[i]
            // which is actually count of
            // move-to-front operations.
            let index = tmp.indexOf(arr[i]);

            // If any two strings are not
            // rotations of each other,
            // we can't make them same.
            if (index == arr[i].length)
                return -1;

            curr_count += index;
        }

        ans = Math.min(curr_count, ans);
    }

    return ans;
    }

    // Driver code
    let arr=["xzzwo", "zwoxz",
                    "zzwox", "xzzwo"];
    let n = arr.length;
    document.write(minimunMoves(arr, n));

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
5
```

本文由 [**帕万·阿西普**](https://www.facebook.com/pawan.asipu.5) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。