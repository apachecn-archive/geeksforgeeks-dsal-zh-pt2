# 从任一端到给定字符串中最大和最小字符的最小跳转次数

> 原文:[https://www . geesforgeks . org/最小-从任一端跳到另一端-给定字符串中的最大和最小字符/](https://www.geeksforgeeks.org/minimum-jumps-from-either-end-to-reach-largest-and-smallest-character-in-given-string/)

给定一个字符串 **str** ，任务是找到达到字典上最大和最小**字符所需的**最小**移动次数。在一次移动中，可以从给定字符串的最左侧或最右侧进行跳转。**

**示例:**

> **输入:** str = AEDCB，N = 5
> **输出** : 2
> **说明:**从最左侧走两步到达 A 和 E
> 
> **输入:** str = BACDEFHG，N = 8
> **输出** : 4
> **说明:**从最左侧走两步到达 A，从最右侧走两步到达 H(2+2=4)
> 
> **输入** : str = CDBA，N = 4
> **输出** : 3
> **说明:**从最右侧走三步到达 A 然后 D

**方法:**这个问题是基于实现的。按照以下步骤解决给定的问题。

*   找到字符串中**最大**和**最小**元素的索引
*   计算这些指标的最小值和最大值，找出可以采取的**最小步数**和**最大步数**
*   到达两个元素的可能方式只有**三种**
    *   从**开始**遍历并覆盖两个元素，即 min_steps+1
    *   从最后一个**开始遍历**并覆盖两个元素，即 **n-max_steps**
    *   从**开始和结束**遍历，即**最小步数+1+n-最大步数**
*   最终的答案是所有可能的三种遍历方式中的最小**。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Minimum number of moves required  to
// reach and largest and smallest ASCII values
int min_moves(string s, int n)
{
    int maxpos = 0, minpos = 0;

    // Finding index of maximum
    // and minimum element in string
    for (int i = 0; i < n; i++) {

        if (s[i] > s[maxpos])
            maxpos = i;

        if (s[i] < s[minpos])
            minpos = i;
    }

    // Calculating minimum ans maximum steps
    // that can be taken

    int min_steps = min(maxpos, minpos);
    int max_steps = max(maxpos, minpos);

    // Only three possible ways
    // to reach both elements
    int ans1, ans2, ans3;

    ans1 = n - min_steps;

    ans2 = max_steps + 1;

    ans3 = min_steps + 1 + n - max_steps;

    int result;

    // Minimum steps in all three ways
    result = min(ans1, min(ans2, ans3));

    // Return the final result
    return result;
}

// Driver code
int main()
{

    string str = "BACDEFHG";
    int N = str.length();

    cout << min_moves(str, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java code for the above approach
import java.io.*;
class GFG
{

// Minimum number of moves required  to
// reach and largest and smallest ASCII values
static int min_moves(String s, int n)
{
    int maxpos = 0, minpos = 0;

    // Finding index of maximum
    // and minimum element in string
    for (int i = 0; i < n; i++) {

        if (s.charAt(i) > s.charAt(maxpos))
            maxpos = i;

        if (s.charAt(i)  < s.charAt(minpos))
            minpos = i;
    }

    // Calculating minimum ans maximum steps
    // that can be taken

    int min_steps = Math.min(maxpos, minpos);
    int max_steps = Math.max(maxpos, minpos);

    // Only three possible ways
    // to reach both elements
    int ans1, ans2, ans3;

    ans1 = n - min_steps;

    ans2 = max_steps + 1;

    ans3 = min_steps + 1 + n - max_steps;

    int result;

    // Minimum steps in all three ways
    result = Math.min(ans1, Math.min(ans2, ans3));

    // Return the final result
    return result;
}

// Driver code
    public static void main (String[] args) {
       String str = "BACDEFHG";
    int N = str.length();

        System.out.println(min_moves(str, N));
    }
}

// This code is contributed by Potta Lokesh
```

## **蟒蛇 3**

```
# Python code for the above approach

# Minimum number of moves required to
# reach and largest and smallest ASCII values
def min_moves(s, n):
    maxpos = 0;
    minpos = 0;

    # Finding index of maximum
    # and minimum element in string
    for i in range(n):

        if (s[i] > s[maxpos]):
            maxpos = i;

        if (s[i] < s[minpos]):
            minpos = i;

    # Calculating minimum ans maximum steps
    # that can be taken
    min_steps = min(maxpos, minpos);
    max_steps = max(maxpos, minpos);

    # Only three possible ways
    # to reach both elements
    ans1, ans2, ans3 = 0,0,0;
    ans1 = n - min_steps;
    ans2 = max_steps + 1;
    ans3 = min_steps + 1 + n - max_steps;

    result=0;

    # Minimum steps in all three ways
    result = min(ans1, min(ans2, ans3));

    # Return the final result
    return result;

# Driver code
if __name__ == '__main__':
    str = "BACDEFHG";
    N = len(str);

    print(min_moves(str, N));

# This code is contributed by shikhasingrajput
```

## **C#**

```
// C# program for above approach
using System;

class GFG{

// Minimum number of moves required  to
// reach and largest and smallest ASCII values
static int min_moves(string s, int n)
{
    int maxpos = 0, minpos = 0;

    // Finding index of maximum
    // and minimum element in string
    for(int i = 0; i < n; i++)
    {
        if (s[i] > s[maxpos])
            maxpos = i;

        if (s[i] < s[minpos])
            minpos = i;
    }

    // Calculating minimum ans maximum steps
    // that can be taken
    int min_steps = Math.Min(maxpos, minpos);
    int max_steps = Math.Max(maxpos, minpos);

    // Only three possible ways
    // to reach both elements
    int ans1, ans2, ans3;

    ans1 = n - min_steps;
    ans2 = max_steps + 1;
    ans3 = min_steps + 1 + n - max_steps;

    int result;

    // Minimum steps in all three ways
    result = Math.Min(ans1, Math.Min(ans2, ans3));

    // Return the final result
    return result;
}

// Driver code
public static void Main(string[] args)
{
    String str = "BACDEFHG";
    int N = str.Length;

    Console.WriteLine(min_moves(str, N));
}
}

// This code is contributed by ukasp
```

## **java 描述语言**

```
<script>

// JavaScript program for above approach

// Minimum number of moves required to
// reach and largest and smallest ASCII values
const min_moves = (s, n) => {

    let maxpos = 0, minpos = 0;

    // Finding index of maximum
    // and minimum element in string
    for(let i = 0; i < n; i++)
    {
        if (s[i] > s[maxpos])
            maxpos = i;

        if (s[i] < s[minpos])
            minpos = i;
    }

    // Calculating minimum ans maximum steps
    // that can be taken
    let min_steps = Math.min(maxpos, minpos);
    let max_steps = Math.max(maxpos, minpos);

    // Only three possible ways
    // to reach both elements
    let ans1, ans2, ans3;

    ans1 = n - min_steps;
    ans2 = max_steps + 1;
    ans3 = min_steps + 1 + n - max_steps;

    let result;

    // Minimum steps in all three ways
    result = Math.min(ans1, Math.min(ans2, ans3));

    // Return the final result
    return result;
}

// Driver code
let str = "BACDEFHG";
let N = str.length;

document.write(min_moves(str, N));

// This code is contributed by rakeshsahni

</script>
```

****Output**

```
4
```** 

****时间复杂度:**O(N)
T3】辅助空间: O(1)**