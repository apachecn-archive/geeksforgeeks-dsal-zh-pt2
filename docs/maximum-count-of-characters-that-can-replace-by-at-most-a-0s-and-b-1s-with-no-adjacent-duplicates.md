# 可以替换的最大字符数？最多 A0 和 B1，没有相邻的副本

> 原文:[https://www . geeksforgeeks . org/最多可被 a-0s 和 b-1s 替换的字符数上限(无相邻重复项)/](https://www.geeksforgeeks.org/maximum-count-of-characters-that-can-replace-by-at-most-a-0s-and-b-1s-with-no-adjacent-duplicates/)

给定一个只包含两个特殊字符“ ***** ”和“**”的字符串 **S** ？**’，以及表示可用 **0 的**和 **1 的**的计数的两个整数 **A** 和 **B** 。任务是统计**最大**可以放在“**位置的字符数？**'这样相邻的两个字符就不会相同。

**示例:**

> **输入:** s = "*？？？*?？？*，A = 4，B = 3
> **输出:** 6
> **说明:**字符串可以修改为“*010*010*”。因此，可以放在“？”位置的最大字符数是(4 + 2 = 6)
> 
> **输入:** s =？？？*?？*，A = 0，B = 5
> **输出:** 3
> **说明:**字符串可以修改为“*1？1*?1*".因此，可以放在“？”位置的最大字符数是(0 + 3 = 3)

**方法:**通过追踪**“？”的**连续**段可以解决任务 s** 并放置 0 和 1，这样在替换“？”后 s，no **合成字符串中的两个**相邻元素相同。

按照以下步骤解决问题:

*   初始化一个向量‘v’，它将存储**的连续段的长度？s**
*   变量“cur”存储**的当前计数？s，**一旦遇到“*”，将 **cur** 的值存储在 **v** 中
*   现在，开始迭代**的存储段长度？s、**贪婪地将 **0s** 和 **1s** 分配到**的位置？s**
*   记录**处可以放置的最大字符数？s**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the maximum number
// of characters 'A' and 'B' that can be
// placed in position of '?'
int maximumChar(string s, int A, int B)
{
    // Length of the string
    int len = s.size();

    // Store the current count of '?'s
    int curr = 0;

    // Store the lengths of contiguous
    // segments of '?'s
    vector<int> v;

    // Traversing the string
    for (int i = 0; i < len; i++) {
        // If character is '?'
        // increment curr by 1
        if (s[i] == '?') {
            curr++;
        }

        // If character is '*'
        else {
            // If curr is not equal to 0
            if (curr != 0) {
                v.push_back(curr);

                // Re-initialise curr to 0
                curr = 0;
            }
        }
    }

    // After traversing the string
    // if curr is not equal to 0
    if (curr != 0) {
        v.push_back(curr);
    }

    // Variable for maximum count
    int count = 0;

    // Traversing the vector
    for (int i = 0; i < v.size(); i++) {
        // Variable to store half of
        // each elements in vector
        int x = v[i] / 2;

        // Variable to store half of
        // each elements with its remainder
        int y = v[i] / 2 + v[i] % 2;

        // If A is greater than B
        if (A > B) {
            // Swap both
            swap(A, B);
        }

        // Increment count by
        // minimum of A and x
        count += min(A, x);

        // Update A
        A -= min(A, x);

        // Increment count by
        // minimum of B and y
        count += min(B, y);

        // Update B
        B -= min(B, y);
    }

    // Return count
    return count;
}

// Driver Code
int main()
{
    string s = "*???*???*";
    int A = 4, B = 3;

    cout << maximumChar(s, A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.ArrayList;

class GFG {

    // Function to count the maximum number
    // of characters 'A' and 'B' that can be
    // placed in position of '?'
    public static int maximumChar(String s, int A, int B)
    {

        // Length of the string
        int len = s.length();

        // Store the current count of '?'s
        int curr = 0;

        // Store the lengths of contiguous
        // segments of '?'s
        ArrayList<Integer> v = new ArrayList<Integer>();

        // Traversing the string
        for (int i = 0; i < len; i++) {
            // If character is '?'
            // increment curr by 1
            if (s.charAt(i) == '?') {
                curr++;
            }

            // If character is '*'
            else {
                // If curr is not equal to 0
                if (curr != 0) {
                    v.add(curr);

                    // Re-initialise curr to 0
                    curr = 0;
                }
            }
        }

        // After traversing the string
        // if curr is not equal to 0
        if (curr != 0) {
            v.add(curr);
        }

        // Variable for maximum count
        int count = 0;

        // Traversing the vector
        for (int i = 0; i < v.size(); i++)
        {

            // Variable to store half of
            // each elements in vector
            int x = v.get(i) / 2;

            // Variable to store half of
            // each elements with its remainder
            int y = v.get(i) / 2 + v.get(i) % 2;

            // If A is greater than B
            if (A > B)
            {

                // Swap both
                int temp = A;
                A = B;
                B = temp;
            }

            // Increment count by
            // minimum of A and x
            count += Math.min(A, x);

            // Update A
            A -= Math.min(A, x);

            // Increment count by
            // minimum of B and y
            count += Math.min(B, y);

            // Update B
            B -= Math.min(B, y);
        }

        // Return count
        return count;
    }

    // Driver Code
    public static void main(String args[]) {
        String s = "*???*???*";
        int A = 4, B = 3;

        System.out.println(maximumChar(s, A, B));
    }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# python program for the above approach
import math

# Function to count the maximum number
# of characters 'A' and 'B' that can be
# placed in position of '?'
def maximumChar(s, A, B):

        # Length of the string
    le = len(s)

    # Store the current count of '?'s
    curr = 0

    # Store the lengths of contiguous
    # segments of '?'s
    v = []

    # Traversing the string
    for i in range(0, le):
                # If character is '?'
                # increment curr by 1
        if (s[i] == '?'):
            curr += 1

            # If character is '*'
        else:
                        # If curr is not equal to 0
            if (curr != 0):
                v.append(curr)

                # Re-initialise curr to 0
                curr = 0

        # After traversing the string
        # if curr is not equal to 0
    if (curr != 0):
        v.append(curr)

        # Variable for maximum count
    count = 0

    # Traversing the vector
    for i in range(0, len(v)):
                # Variable to store half of
                # each elements in vector
        x = v[i] // 2

        # Variable to store half of
        # each elements with its remainder
        y = v[i] // 2 + v[i] % 2

        # If A is greater than B
        if (A > B):
                        # Swap both
            temp = A
            A = B
            B = temp

            # Increment count by
            # minimum of A and x
        count += min(A, x)

        # Update A
        A -= min(A, x)

        # Increment count by
        # minimum of B and y
        count += min(B, y)

        # Update B
        B -= min(B, y)

        # Return count
    return count

# Driver Code
if __name__ == "__main__":

    s = "*???*???*"
    A = 4
    B = 3

    print(maximumChar(s, A, B))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG {

    // Function to count the maximum number
    // of characters 'A' and 'B' that can be
    // placed in position of '?'
    public static int maximumChar(String s, int A, int B)
    {

        // Length of the string
        int len = s.Length;

        // Store the current count of '?'s
        int curr = 0;

        // Store the lengths of contiguous
        // segments of '?'s
        List<int> v = new List<int>();

        // Traversing the string
        for (int i = 0; i < len; i++)
        {

            // If character is '?'
            // increment curr by 1
            if (s[i] == '?') {
                curr++;
            }

            // If character is '*'
            else {
                // If curr is not equal to 0
                if (curr != 0) {
                    v.Add(curr);

                    // Re-initialise curr to 0
                    curr = 0;
                }
            }
        }

        // After traversing the string
        // if curr is not equal to 0
        if (curr != 0) {
            v.Add(curr);
        }

        // Variable for maximum count
        int count = 0;

        // Traversing the vector
        for (int i = 0; i < v.Count; i++)
        {

            // Variable to store half of
            // each elements in vector
            int x = v[i] / 2;

            // Variable to store half of
            // each elements with its remainder
            int y = v[i] / 2 + v[i] % 2;

            // If A is greater than B
            if (A > B)
            {

                // Swap both
                int temp = A;
                A = B;
                B = temp;
            }

            // Increment count by
            // minimum of A and x
            count += Math.Min(A, x);

            // Update A
            A -= Math.Min(A, x);

            // Increment count by
            // minimum of B and y
            count += Math.Min(B, y);

            // Update B
            B -= Math.Min(B, y);
        }

        // Return count
        return count;
    }

    // Driver Code
    public static void Main(String []args) {
        String s = "*???*???*";
        int A = 4, B = 3;

        Console.WriteLine(maximumChar(s, A, B));
    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

       // JavaScript Program to implement
       // the above approach

       // Function to count the maximum number
       // of characters 'A' and 'B' that can be
       // placed in position of '?'
       function maximumChar(s, A, B)
       {

           // Length of the string
           let len = s.length;

           // Store the current count of '?'s
           let curr = 0;

           // Store the lengths of contiguous
           // segments of '?'s
           let v = [];

           // Traversing the string
           for (let i = 0; i < len; i++)
           {

               // If character is '?'
               // increment curr by 1
               if (s[i] == '?') {
                   curr++;
               }

               // If character is '*'
               else
               {

                   // If curr is not equal to 0
                   if (curr != 0) {
                       v.push(curr);

                       // Re-initialise curr to 0
                       curr = 0;
                   }
               }
           }

           // After traversing the string
           // if curr is not equal to 0
           if (curr != 0) {
               v.push(curr);
           }

           // Variable for maximum count
           let count = 0;

           // Traversing the vector
           for (let i = 0; i < v.length; i++)
           {

               // Variable to store half of
               // each elements in vector
               let x = Math.floor(v[i] / 2);

               // Variable to store half of
               // each elements with its remainder
               let y = Math.floor(v[i] / 2) + v[i] % 2;

               // If A is greater than B
               if (A > B)
               {

                   // Swap both
                   let temp = A;
                   A = B;
                   B = temp;
               }

               // Increment count by
               // minimum of A and x
               count = count + Math.min(A, x);

               // Update A
               A = A - Math.min(A, x);

               // Increment count by
               // minimum of B and y
               count = count + Math.min(B, y);

               // Update B
               B = B - Math.min(B, y);
           }

           // Return count
           return count;
       }

       // Driver Code
       let s = "*???*???*";
       let A = 4, B = 3;

       document.write(maximumChar(s, A, B));

   // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)