# 从给定的包含字符的三进制字符串中计数至少一次的子字符串

> 原文:[https://www . geeksforgeeks . org/substrings-count-from-给定-包含字符的三进制字符串-至少一次/](https://www.geeksforgeeks.org/count-of-substrings-from-given-ternary-strings-containing-characters-at-least-once/)

给定大小为 **N** 的[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **字符串**，该字符串仅由 **0** 、 **1** 和 **2** 组成，任务是至少查找一次由字符 **0** 、 **1** 和 **2** 组成的[子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)的数量。

**示例:**

> **输入:** str = "0122"
> **输出:** 2
> **解释:**
> 存在 2 个子串，使得子串至少有一次字符 0、1、2 为“012”和“0122”。因此，子字符串的计数是 2。
> 
> **输入:**S = " 00021 "
> T3】输出: 3

**方法:**给定的问题可以使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)解决，思路是制作**大小 3** 的[频率阵列](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)，包含 **0** 、 **1** 、 **2** 的出现。[遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)并相应地更新 **freq** 数组，如果数组中的所有 3 个索引都大于零，则计算它们的最小值并将其增加到变量 **count** 中。按照以下步骤解决问题:

*   [初始化一个大小为**3**T5 的数组 **freq[]** ，存储数组中所有元素的频率。](https://www.geeksforgeeks.org/arrays-in-java/)
*   初始化变量**计数**为 **0** 存储答案 **i** 为 **0** 保持左指针。
*   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/loops-in-java/)**【0，N)** ，并执行以下任务:
    *   将数组**中当前字符**str【**I**的频率增加 **1。******
    *   **[循环遍历](https://www.geeksforgeeks.org/java-while-loop-with-examples/)直到**freq【0】、freq【1】**、**freq【2】**大于 **0、**将第**I-第**位置的字符频率降低 **1** 并将 **i** 的值增加 **1。****
    *   **将 **i** 的值添加到变量**计数中。****
*   **执行上述步骤后，打印**计数**的值作为答案。**

**下面是上述方法的实现。**

## **C++**

```
// C++ program for above approach
#include <iostream>
#include <string>
using namespace std;

// Function to count the number of
// substrings consists of 0, 1, and 2
int countSubstrings(string& str)
{

    // Initialize frequency array
    // of size 3
    int freq[3] = { 0 };

    // Stores the resultant count
    int count = 0;
    int i = 0;

    // Traversing string str
    for (int j = 0; j < str.length(); j++) {

        // Update frequency array
        freq[str[j] - '0']++;

        // If all the characters are
        // present counting number of
        // substrings possible
        while (freq[0] > 0 && freq[1] > 0 && freq[2] > 0) {
            freq[str[i++] - '0']--;
        }

        // Update number of substrings
        count += i;
    }

    // Return the number of substrings
    return count;
}

// Driver Code
int main()
{
    string str = "00021";
    int count = countSubstrings(str);
    cout << count;
    return 0;
}

// This code is contributed by Kdheeraj.
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to count the number of
    // substrings consists of 0, 1, and 2
    public static int countSubstrings(String str)
    {
        // Initialize frequency array
        // of size 3
        int[] freq = new int[3];

        // Stores the resultant count
        int count = 0;
        int i = 0;

        // Traversing string str
        for (int j = 0;
             j < str.length(); j++) {

            // Update frequency array
            freq[str.charAt(j) - '0']++;

            // If all the characters are
            // present counting number of
            // substrings possible
            while (freq[0] > 0 && freq[1] > 0
                   && freq[2] > 0) {
                freq[str.charAt(i++) - '0']--;
            }

            // Update number of substrings
            count += i;
        }

        // Return the number of substrings
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str = "00021";
        System.out.println(
            countSubstrings(str));
    }
}
```

## **蟒蛇 3**

```
# Python program for above approach
# Function to count the number of
# substrings consists of 0, 1, and 2
def countSubstrings(str):

    # Initialize frequency array
    # of size 3
    freq = [ 0 ]*3

    # Stores the resultant count
    count = 0
    i = 0

    # Traversing string str
    for j in range ( 0 ,len(str)):

        # Update frequency array
        freq[ord(str[j]) - ord('0')] += 1

        # If all the characters are
        # present counting number of
        # substrings possible
        while (freq[0] > 0 and freq[1] > 0 and freq[2] > 0):
            i += 1
            freq[ord(str[i]) - ord('0')] -= 1

        # Update number of substrings
        count += i

    # Return the number of substrings
    return count

# Driver Code
str = "00021"
count = countSubstrings(str)
print(count)

# This code is contributed by shivanisinghss2110
```

## **C#**

```
// C# program for the above approach
using System;

class GFG {

    // Function to count the number of
    // substrings consists of 0, 1, and 2
    public static int countSubstrings(string str)
    {

        // Initialize frequency array
        // of size 3
        int[] freq = new int[3];

        // Stores the resultant count
        int count = 0;
        int i = 0;

        // Traversing string str
        for (int j = 0;
             j < str.Length; j++) {

            // Update frequency array
            freq[str[j] - '0']++;

            // If all the characters are
            // present counting number of
            // substrings possible
            while (freq[0] > 0 && freq[1] > 0
                   && freq[2] > 0) {
                freq[str[i++] - '0']--;
            }

            // Update number of substrings
            count += i;
        }

        // Return the number of substrings
        return count;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        string str = "00021";
        Console.Write(countSubstrings(str));
    }
}

// This code is contributed by shivanisinghss2110
```

## **java 描述语言**

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to count the number of
        // substrings consists of 0, 1, and 2
        function countSubstrings(str) {

            // Initialize frequency array
            // of size 3
            let freq = new Array(3).fill(0)

            // Stores the resultant count
            let count = 0;
            let i = 0;

            // Traversing string str
            for (let j = 0; j < str.length; j++) {

                // Update frequency array
                freq[str.charCodeAt(j) - '0'.charCodeAt(0)]++;

                // If all the characters are
                // present counting number of
                // substrings possible
                while (freq[0] > 0 && freq[1] > 0 && freq[2] > 0) {
                    freq[str.charCodeAt(i++) - '0'.charCodeAt(0)]--;
                }

                // Update number of substrings
                count += i;
            }

            // Return the number of substrings
            return count;
        }

        // Driver Code

        let str = "00021";
        let count = countSubstrings(str);
        document.write(count);

// This code is contributed by Potta Lokesh
    </script>
```

****Output:** 

```
3
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**