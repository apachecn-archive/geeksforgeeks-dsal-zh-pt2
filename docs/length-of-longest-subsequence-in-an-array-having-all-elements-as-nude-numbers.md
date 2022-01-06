# 数组中最长子序列的长度，数组中所有元素都是裸编号

> 原文:[https://www . geeksforgeeks . org/数组中最长子序列的长度将所有元素都作为裸编号/](https://www.geeksforgeeks.org/length-of-longest-subsequence-in-an-array-having-all-elements-as-nude-numbers/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是打印数组最长子序列的长度，使其所有元素都是[个裸数字。](https://www.geeksforgeeks.org/check-whether-a-given-number-n-is-a-nude-number-or-not/)

**示例:**

> **输入:** arr[] = {34，34，2，2，3，333，221，32 }
> **输出:** 4
> **解释:**
> 最长的裸色号子序列是{2，2，3，333}，因此答案是 4。
> **输入:** arr[] = {456，44，104，133，39，325 }
> **输出:** 1
> **解释:**
> 最长裸色号子序列为{44}，因此答案为 1。

**方法:**要解决问题，请按照下面给出的步骤操作:

*   遍历给定的数组，对于数组中的每个元素[检查它是否是一个裸号](https://www.geeksforgeeks.org/check-whether-a-given-number-n-is-a-nude-number-or-not/)。
*   如果元素是一个**裸编号**，它将被包含在最终的最长子序列中。因此将子序列中的元素计数增加 **1** 。
*   完成上述步骤后，打印计数值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the number
// is a Nude number
bool isNudeNum(int n)
{
    // Variable initialization
    int copy, length, flag = 0;
    copy = n;
    string temp;

    // Integer 'copy' is converted
    // to a string
    temp = to_string(copy);

    // Total digits in the number
    length = temp.length();

    // Loop through all digits and check
    // if every digit divides n or not
    for (int i = 0; i < length; i++) {

        int num = temp[i] - '0';

        if (num == 0 or n % num != 0) {

            // flag is used to keep check
            flag = 1;
        }
    }

    // Return true or false as per
    // the condition
    if (flag == 1)
        return false;

    else
        return true;
}

// Function to find the longest subsequence
// which contain all Nude numbers
int longestNudeSubseq(int arr[], int n)
{
    int answer = 0;

    // Find the length of longest
    // Nude number subsequence
    for (int i = 0; i < n; i++) {
        if (isNudeNum(arr[i]))
            answer++;
    }
    return answer;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 34, 34, 2, 2, 3,
                  333, 221, 32 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << longestNudeSubseq(arr, n)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check if the number
// is a Nude number
static boolean isNudeNum(int n)
{

    // Variable initialization
    int copy, length, flag = 0;
    copy = n;
    String temp;

    // Integer 'copy' is converted
    // to a String
    temp = String.valueOf(copy);

    // Total digits in the number
    length = temp.length();

    // Loop through all digits and check
    // if every digit divides n or not
    for(int i = 0; i < length; i++)
    {
        int num = temp.charAt(i) - '0';

        if (num == 0 || n % num != 0)
        {

            // flag is used to keep check
            flag = 1;
        }
    }

    // Return true or false as per
    // the condition
    if (flag == 1)
        return false;
    else
        return true;
}

// Function to find the longest subsequence
// which contain all Nude numbers
static int longestNudeSubseq(int arr[], int n)
{
    int answer = 0;

    // Find the length of longest
    // Nude number subsequence
    for(int i = 0; i < n; i++)
    {
        if (isNudeNum(arr[i]))
            answer++;
    }
    return answer;
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 34, 34, 2, 2, 3,
                  333, 221, 32 };

    int n = arr.length;

    // Function call
    System.out.print(longestNudeSubseq(arr, n) + "\n");
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the number
# is a Nude number
def isNudeNum(n):

    # Variable initialization
    flag = 0
    copy = n

    # Integer 'copy' is converted
    # to a string
    temp = str(copy)

    # Total digits in the number
    length = len(temp)

    # Loop through all digits and check
    # if every digit divides n or not
    for i in range(length):
        num = ord(temp[i]) - ord('0')

        if ((num == 0) or (n % num != 0)):

            # flag is used to keep check
            flag = 1

    # Return true or false as per
    # the condition
    if (flag == 1):
        return False
    else:
        return True

# Function to find the longest subsequence
# which contain all Nude numbers
def longestNudeSubseq(arr, n):

    answer = 0

    # Find the length of longest
    # Nude number subsequence
    for i in range(n):
        if (isNudeNum(arr[i])):
            answer += 1

    return answer

# Driver Code

# Given array arr[]
arr = [ 34, 34, 2, 2, 3,
        333, 221, 32 ]

n = len(arr)

# Function call
print(longestNudeSubseq(arr, n))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if the number
// is a Nude number
static bool isNudeNum(int n)
{

    // Variable initialization
    int copy, length, flag = 0;
    copy = n;
    String temp;

    // int 'copy' is converted
    // to a String
    temp = String.Join("", copy);

    // Total digits in the number
    length = temp.Length;

    // Loop through all digits and check
    // if every digit divides n or not
    for(int i = 0; i < length; i++)
    {
        int num = temp[i] - '0';

        if (num == 0 || n % num != 0)
        {

            // flag is used to keep check
            flag = 1;
        }
    }

    // Return true or false as per
    // the condition
    if (flag == 1)
        return false;
    else
        return true;
}

// Function to find the longest subsequence
// which contain all Nude numbers
static int longestNudeSubseq(int []arr, int n)
{
    int answer = 0;

    // Find the length of longest
    // Nude number subsequence
    for(int i = 0; i < n; i++)
    {
        if (isNudeNum(arr[i]))
            answer++;
    }
    return answer;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 34, 34, 2, 2, 3,
                  333, 221, 32 };

    int n = arr.Length;

    // Function call
    Console.Write(longestNudeSubseq(arr, n) + "\n");
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to check if the number
    // is a Nude number
    function isNudeNum(n)
    {
        // Variable initialization
        let copy, length, flag = 0;
        copy = n;
        let temp;

        // Integer 'copy' is converted
        // to a string
        temp = copy.toString();

        // Total digits in the number
        length = temp.length;

        // Loop through all digits and check
        // if every digit divides n or not
        for (let i = 0; i < length; i++) {

            let num = temp[i].charCodeAt() - '0'.charCodeAt(); 

            if (num == 0 || n % num != 0) {

                // flag is used to keep check
                flag = 1;
            }
        }

        // Return true or false as per
        // the condition
        if (flag == 1)
            return false;

        else
            return true;
    }

    // Function to find the longest subsequence
    // which contain all Nude numbers
    function longestNudeSubseq(arr, n)
    {
        let answer = 0;

        // Find the length of longest
        // Nude number subsequence
        for (let i = 0; i < n; i++) {
            if (isNudeNum(arr[i]))
                answer++;
        }
        return answer;
    }

    // Given array arr[]
    let arr = [ 34, 34, 2, 2, 3,
                  333, 221, 32 ];

    let n = arr.length;

    // Function Call
    document.write(longestNudeSubseq(arr, n));

    // This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
4
```

**时间复杂度:*****O(N * log<sub>10</sub>N)*** ****辅助空间:** *O(1)***