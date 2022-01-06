# 最小化需要移除的 0 的数量，以最大化 1 的最长子串的长度

> 原文:[https://www . geesforgeks . org/minimum-count-of-0s-required-removed-to-maximum-length-of-1s 最长子串/](https://www.geeksforgeeks.org/minimize-count-of-0s-required-to-be-removed-to-maximize-length-of-longest-substring-of-1s/)

给定一个长度为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是从给定的字符串 **S** 中找出需要移除的最小数量的 **0** s，得到 **1s** 的最长子串。

**示例:**

> **输入:** S = "010011"
> **输出:** 2
> **解释:**
> 移除 str[2]和 str[3]将字符串 S 修改为“0111”。因此，所需的最小移除次数是 2。
> 
> **输入:**S = " 011111 "
> T3】输出: 0

**方法:**思路是找到字符串中 **1** 最左边和最右边的索引，然后统计它们之间存在的 **0** 的个数。最后，打印获得的计数值。按照以下步骤解决问题:

*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 找到字符串中第一个和最后一个出现的 **1** ，并将其索引存储在变量中，分别说**左**和**右**。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/) **【左，右】**，如果 **str[i]** 的值等于 **0** ，则将**计数**增加 1。
*   完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum number
// of 0s required to be removed to
// maximize the longest substring of 1s
void minNumZeros(string str)
{
    // Stores leftmost and rightmost
    // indices consisting of 1
    int left = INT_MAX, right = INT_MIN;

    // Stores the count of 0s
    // between left and right
    int count = 0;

    // Traverse the string str
    for (int i = 0; i < str.length(); i++) {

        // If the current character is 1
        if (str[i] == '1') {

            // Update leftmost and rightmost
            // index consisting of 1
            left = min(i, left);
            right = max(right, i);
        }
    }

    // If string consists only of 0s
    if (left == INT_MAX) {
        cout << "0";
        return;
    }

    // Count the number of 0s
    // between left and right
    for (int i = left; i < right; i++) {

        if (str[i] == '0') {
            count++;
        }
    }

    // Print the result
    cout << count;
}

// Driver Code
int main()
{
    string str = "010011";
    minNumZeros(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to count the minimum number
// of 0s required to be removed to
// maximize the longest substring of 1s
static void minNumZeros(String str)
{

    // Stores leftmost and rightmost
    // indices consisting of 1
    int left = Integer.MAX_VALUE;
    int right = Integer.MIN_VALUE;

    // Stores the count of 0s
    // between left and right
    int count = 0;

    // Traverse the string str
    for(int i = 0; i < str.length(); i++)
    {

        // If the current character is 1
        if (str.charAt(i) == '1')
        {

            // Update leftmost and rightmost
            // index consisting of 1
            left = Math.min(i, left);
            right = Math.max(right, i);
        }
    }

    // If string consists only of 0s
    if (left == Integer.MAX_VALUE)
    {
        System.out.print("0");
        return;
    }

    // Count the number of 0s
    // between left and right
    for(int i = left; i < right; i++)
    {
        if (str.charAt(i) == '0')
        {
            count++;
        }
    }

    // Print the result
    System.out.print(count);
}

// Driver Code
public static void main(String[] args)
{
    String str = "010011";

    minNumZeros(str);
}
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python program for the above approach
import sys

# Function to count the minimum number
# of 0s required to be removed to
# maximize the longest substring of 1s
def minNumZeros(st) :

    # Stores leftmost and rightmost
    # indices consisting of 1
    left = sys.maxsize
    right = -sys.maxsize - 1

    # Stores the count of 0s
    # between left and right
    count = 0

    # Traverse the string str
    for i in range(len(st)) :
    #for (int i = 0; i < str.length(); i++) {

        # If the current character is 1
        if st[i] == '1' :

            # Update leftmost and rightmost
            # index consisting of 1
            left = min(i, left)
            right = max(right, i)

    # If string consists only of 0s
    if left == sys.maxsize :
        print("0")
        return

    # Count the number of 0s
    # between left and right
    for i in range(left,right):

    #for (int i = left; i < right; i++) {

        if st[i] == '0' :
            count += 1

    # Print the result
    print(count)

# Driver Code
if __name__ == "__main__" :    
    st = "010011";
    minNumZeros(st)

 # This code is contributed by jana_sayantan.  
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count the minimum number
// of 0s required to be removed to
// maximize the longest substring of 1s
static void minNumZeros(string str)
{

    // Stores leftmost and rightmost
    // indices consisting of 1
    int left = int.MaxValue;
    int right = int.MinValue;

    // Stores the count of 0s
    // between left and right
    int count = 0;

    // Traverse the string str
    for(int i = 0; i < str.Length; i++)
    {

        // If the current character is 1
        if (str[i] == '1')
        {

            // Update leftmost and rightmost
            // index consisting of 1
            left = Math.Min(i, left);
            right = Math.Max(right, i);
        }
    }

    // If string consists only of 0s
    if (left == int.MaxValue)
    {
        Console.WriteLine("0");
        return;
    }

    // Count the number of 0s
    // between left and right
    for(int i = left; i < right; i++)
    {
        if (str[i] == '0')
        {
            count++;
        }
    }

    // Print the result
    Console.WriteLine(count);
}

// Driver Code
static public void Main()
{
    string str = "010011";

    minNumZeros(str);
}
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>
    // javascript program for the above approach
    // Function to count the minimum number
    // of 0s required to be removed to
    // maximize the longest substring of 1s
    function minNumZeros(str)
    {

        // Stores leftmost and rightmost
        // indices consisting of 1
        let left = Number.MAX_VALUE, right = Number.MIN_VALUE;

        // Stores the count of 0s
        // between left and right
        let count = 0;

        // Traverse the string str
        for (let i = 0; i < str.length; i++) {

            // If the current character is 1
            if (str[i] == '1') {

                // Update leftmost and rightmost
                // index consisting of 1
                left = Math.min(i, left);
                right = Math.max(right, i);
            }
        }

        // If string consists only of 0s
        if (left == Number.MAX_VALUE) {
            document.write("0");
            return;
        }

        // Count the number of 0s
        // between left and right
        for (let i = left; i < right; i++) {

            if (str[i] == '0') {
                count++;
            }
        }

        // Print the result
        document.write(count);
    }

    // Driver Code

    let str = "010011";
    minNumZeros(str);

// This code is contributed by vaibhavrabadiya117.
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)