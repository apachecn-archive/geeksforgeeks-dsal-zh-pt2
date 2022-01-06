# 旋转给定数字的数字可能达到的最大值

> 原文:[https://www . geesforgeks . org/给定数字的最大可能旋转位数/](https://www.geeksforgeeks.org/maximum-value-possible-by-rotating-digits-of-a-given-number/)

给定一个正整数 **N** ，任务是在整数 **N** 的所有数字旋转中找到最大值。

**示例:**

> **输入:**N = 657
> T3】输出:765
> T6】说明:657 的所有旋转都是{657，576，765}。所有这些旋转中的最大值是 765。
> 
> **输入:** N = 7092
> **输出:** 9270
> **说明:**
> 7092 的所有旋转都是{7092，2709，9270，0927}。所有这些旋转的最大值是 9270。

**逼近:**思路是[找到数字](https://www.geeksforgeeks.org/generate-all-rotations-of-a-number/) **N** 的所有旋转，打印所有生成数字中的最大值。按照以下步骤解决问题:

*   [统计数字](https://www.geeksforgeeks.org/program-count-digits-integer-3-different-methods/) **N** 中出现的位数，即 **log <sub>10</sub> N** 的[上限](https://www.geeksforgeeks.org/upper_bound-in-cpp/)。
*   初始化一个变量，用 **N** 的值表示**和**，以存储生成的最大值。
*   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)****【1，记录<sub>10</sub>(N)–1】**并执行以下步骤:

    *   用下一次旋转更新 **N** 的值。
    *   现在，如果生成的下一个旋转超过 **ans** ，那么用 **N** 的旋转值更新 **ans**** 
*   **完成上述步骤后，打印**和**的值作为所需答案。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum value
// possible by rotations of digits of N
void findLargestRotation(int num)
{
    // Store the required result
    int ans = num;

    // Store the number of digits
    int len = floor(log10(num) + 1);

    int x = pow(10, len - 1);

    // Iterate over the range[1, len-1]
    for (int i = 1; i < len; i++) {

        // Store the unit's digit
        int lastDigit = num % 10;

        // Store the remaining number
        num = num / 10;

        // Find the next rotation
        num += (lastDigit * x);

        // If the current rotation is
        // greater than the overall
        // answer, then update answer
        if (num > ans) {
            ans = num;
        }
    }

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    int N = 657;
    findLargestRotation(N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to find the maximum value
// possible by rotations of digits of N
static void findLargestRotation(int num)
{

    // Store the required result
    int ans = num;

    // Store the number of digits
    int len = (int)Math.floor(((int)Math.log10(num)) + 1);
    int x = (int)Math.pow(10, len - 1);

    // Iterate over the range[1, len-1]
    for (int i = 1; i < len; i++) {

        // Store the unit's digit
        int lastDigit = num % 10;

        // Store the remaining number
        num = num / 10;

        // Find the next rotation
        num += (lastDigit * x);

        // If the current rotation is
        // greater than the overall
        // answer, then update answer
        if (num > ans) {
            ans = num;
        }
    }

    // Print the result
    System.out.print(ans);
}

// Driver Code
public static void main(String[] args)
{
    int N = 657;
    findLargestRotation(N);
}
}

// This code is contributed by sanjoy_62.
```

## **蟒蛇 3**

```
# Python program for the above approach

# Function to find the maximum value
# possible by rotations of digits of N
def findLargestRotation(num):

    # Store the required result
    ans = num

    # Store the number of digits
    length = len(str(num))
    x = 10**(length - 1)

    # Iterate over the range[1, len-1]
    for i in range(1, length):

        # Store the unit's digit
        lastDigit = num % 10

        # Store the remaining number
        num = num // 10

        # Find the next rotation
        num += (lastDigit * x)

        # If the current rotation is
        # greater than the overall
        # answer, then update answer
        if (num > ans):
            ans = num

    # Print the result
    print(ans)

# Driver Code
N = 657
findLargestRotation(N)

# This code is contributed by rohitsingh07052.
```

## **C#**

```
// C# program for the above approach
using System;
class GFG{

// Function to find the maximum value
// possible by rotations of digits of N
static void findLargestRotation(int num)
{

    // Store the required result
    int ans = num;

    // Store the number of digits
    double lg = (double)(Math.Log10(num) + 1);
    int len = (int)(Math.Floor(lg));
    int x = (int)Math.Pow(10, len - 1);

    // Iterate over the range[1, len-1]
    for (int i = 1; i < len; i++) {

        // Store the unit's digit
        int lastDigit = num % 10;

        // Store the remaining number
        num = num / 10;

        // Find the next rotation
        num += (lastDigit * x);

        // If the current rotation is
        // greater than the overall
        // answer, then update answer
        if (num > ans) {
            ans = num;
        }
    }

    // Print the result
    Console.Write(ans);
}

// Driver Code
public static void Main(string[] args)
{
    int N = 657;
    findLargestRotation(N);
}
}

// This code is contributed by souravghosh0416,
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Function to find the maximum value
// possible by rotations of digits of N
function findLargestRotation(num)
{
    // Store the required result
    let ans = num;

    // Store the number of digits
    let len = Math.floor(Math.log10(num) + 1);

    let x = Math.pow(10, len - 1);

    // Iterate over the range[1, len-1]
    for (let i = 1; i < len; i++) {

        // Store the unit's digit
        let lastDigit = num % 10;

        // Store the remaining number
        num = parseInt(num / 10);

        // Find the next rotation
        num += (lastDigit * x);

        // If the current rotation is
        // greater than the overall
        // answer, then update answer
        if (num > ans) {
            ans = num;
        }
    }

    // Print the result
    document.write(ans);
}

// Driver Code
let N = 657;
findLargestRotation(N);

// This code is contributed by souravmahato348.
</script>
```

****Output:** 

```
765
```** 

*****时间复杂度:**O(log<sub>10</sub>N)*
***辅助空间:** O(1)***