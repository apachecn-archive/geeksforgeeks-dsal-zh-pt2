# 通过移除相等的第一阵列元素对来最小化剩余的阵列大小

> 原文:[https://www . geesforgeks . org/通过删除相等的第一对数组元素来最小化剩余数组大小/](https://www.geeksforgeeks.org/minimize-remaining-array-sizes-by-removing-equal-pairs-of-first-array-elements/)

给定两个二进制[数组](https://www.geeksforgeeks.org/array-data-structure/)**【L1】**和**L2【】**，每个数组大小为 **N** ，任务是在执行以下操作后最小化剩余数组元素的数量:

*   如果两个数组的第一个元素相同，则将其从两个数组中移除。
*   否则，从 **L1[]** 中移除第一个元素，并将其追加到数组的末尾 **L1[]** 。

**示例:**

> **输入:** L1 = {1，0，1，0}，L2 = {0，1，0，1}
> **输出:** 0
> **解释:**
> L1【0】= 1，L2【0】= 0。因此，L1[]修改为{0，1，0，1}。
> 由于 L1[0]和 L2[0]相等，因此两者都从各自的数组中移除。
> 现在，L1[]修改为{1，0，1}，L2 修改为{1，0，1}。
> 对于接下来的三个步骤，第一个数组元素相等。因此，剩余元素的计数为 0。
> 
> **输入:** L1 = {1，1，0，0}，L2 = {0，0，0，1 }
> T3】输出: 2

**方式:**思路是将 **1** s、 **0** s 的计数存储在数组**L1【】**中。然后，在[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**L2【】**的同时，如果遇到 **1** ，则递减 **1** s 的计数。否则，递减 **0** s 的计数。在任何时刻，如果两个计数中的任何一个变得小于 **0** ，则这表明在该特定索引之后，不能再移除任何元素。按照以下步骤解决问题:

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**【L1】**并统计 **0** s 和 **1** s 的个数并存储在变量中，分别说**零**和**一**。
*   现在，[遍历阵列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**【L2】**并执行以下步骤:
    *   如果**L2【】**当前元素为 **1** ，则以 **1** 递减**一**。否则，将**减零**为 **1** 。
    *   如果在任何时刻**1**或**0**变为负值，将指数存储在变量 **ans** 和[中，脱离循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   完成上述步骤后，打印**(N–ans)**的值作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the remaining
// elements in the arrays
void countRemainingElements(
    int L1[], int L2[], int n)
{
    // Stores the count of 1s in L1[]
    int one = 0;

    // Store the count of 0s in L2[]
    int zero = 0;

    // Traverse the array L1[]
    for (int i = 0; i < n; i++) {

        // If condition is true
        if (L1[i] == 1)

            // Increment one by 1
            one++;
        else

            // Increment zero by 1
            zero++;
    }

    // Stores the index after which no
    // further removals are possible
    int ans = n;

    // Traverse the array L2[]
    for (int i = 0; i < n; i++) {

        // If condition is true
        if (L2[i] == 1) {

            // Decrement one by 1
            one--;

            // If one < 0, then break
            // out of the loop
            if (one < 0) {
                ans = i;
                break;
            }
        }
        else {

            // Decrement zero by 1
            zero--;

            // If zero < 0, then
            // break out of loop
            if (zero < 0) {
                ans = i;
                break;
            }
        }
    }

    // Print the answer
    cout << n - ans;
}

// Driver Code
int main()
{
    int L1[] = { 1, 1, 0, 0 };
    int L2[] = { 0, 0, 0, 1 };
    int N = sizeof(L1) / sizeof(L1[0]);

    // Function Call
    countRemainingElements(L1, L2, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to count the remaining
// elements in the arrays
static void countRemainingElements(int[] L1,
                                   int[] L2,
                                   int n)
{

    // Stores the count of 1s in L1[]
    int one = 0;

    // Store the count of 0s in L2[]
    int zero = 0;

    // Traverse the array L1[]
    for(int i = 0; i < n; i++)
    {

        // If condition is true
        if (L1[i] == 1)

            // Increment one by 1
            one++;
        else

            // Increment zero by 1
            zero++;
    }

    // Stores the index after which no
    // further removals are possible
    int ans = n;

    // Traverse the array L2[]
    for(int i = 0; i < n; i++)
    {

        // If condition is true
        if (L2[i] == 1)
        {

            // Decrement one by 1
            one--;

            // If one < 0, then break
            // out of the loop
            if (one < 0)
            {
                ans = i;
                break;
            }
        }
        else
        {

            // Decrement zero by 1
            zero--;

            // If zero < 0, then
            // break out of loop
            if (zero < 0)
            {
                ans = i;
                break;
            }
        }
    }

    // Print the answer
    System.out.println(n - ans);
}

// Driver Code
public static void main(String[] args)
{
    int[] L1 = { 1, 1, 0, 0 };
    int[] L2 = { 0, 0, 0, 1 };
    int N = L1.length;

    // Function Call
    countRemainingElements(L1, L2, N);
}
}

// This code is contributed by Dharanendra L V
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count the remaining
// elements in the arrays
static void countRemainingElements(int[] L1,
                                   int[] L2,
                                   int n)
{

    // Stores the count of 1s in L1[]
    int one = 0;

    // Store the count of 0s in L2[]
    int zero = 0;

    // Traverse the array L1[]
    for(int i = 0; i < n; i++)
    {

        // If condition is true
        if (L1[i] == 1)

            // Increment one by 1
            one++;
        else

            // Increment zero by 1
            zero++;
    }

    // Stores the index after which no
    // further removals are possible
    int ans = n;

    // Traverse the array L2[]
    for(int i = 0; i < n; i++)
    {

        // If condition is true
        if (L2[i] == 1)
        {

            // Decrement one by 1
            one--;

            // If one < 0, then break
            // out of the loop
            if (one < 0)
            {
                ans = i;
                break;
            }
        }
        else
        {

            // Decrement zero by 1
            zero--;

            // If zero < 0, then
            // break out of loop
            if (zero < 0)
            {
                ans = i;
                break;
            }
        }
    }

    // Print the answer
    Console.WriteLine(n - ans);
}

// Driver Code
static public void Main()
{
    int[] L1 = { 1, 1, 0, 0 };
    int[] L2 = { 0, 0, 0, 1 };
    int N = L1.Length;

    // Function Call
    countRemainingElements(L1, L2, N);
}
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to count the remaining
# elements in the arrays
def countRemainingElements(L1, L2, n):

    # Stores the count of 1s in L1
    one = 0;

    # Store the count of 0s in L2
    zero = 0;

    # Traverse the array L1
    for i in range(n):

        # If condition is True
        if (L1[i] == 1):

            # Increment one by 1
            one += 1;
        else:

            # Increment zero by 1
            zero += 1;

    # Stores the index after which no
    # further removals are possible
    ans = n;

    # Traverse the array L2
    for i in range(n):

        # If condition is True
        if (L2[i] == 1):

            # Decrement one by 1
            one -= 1;

            # If one < 0, then break
            # out of the loop
            if (one < 0):
                ans = i;
                break;           
        else:

            # Decrement zero by 1
            zero -= 1;

            # If zero < 0, then
            # break out of loop
            if (zero < 0):
                ans = i;
                break;

    # Print the answer
    print(n - ans);

# Driver Code
if __name__ == '__main__':
    L1 = [ 1, 1, 0, 0 ];
    L2 = [ 0, 0, 0, 1 ];
    N = len(L1);

    # Function Call
    countRemainingElements(L1, L2, N);

# This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript program for
// the above approach

// Function to count the remaining
// elements in the arrays
function countRemainingElements( L1, L2, n)
{

    // Stores the count of 1s in L1[]
    let one = 0;

    // Store the count of 0s in L2[]
    let zero = 0;

    // Traverse the array L1[]
    for(let i = 0; i < n; i++)
    {

        // If condition is true
        if (L1[i] == 1)

            // Increment one by 1
            one++;
        else

            // Increment zero by 1
            zero++;
    }

    // Stores the index after which no
    // further removals are possible
    let ans = n;

    // Traverse the array L2[]
    for(let i = 0; i < n; i++)
    {

        // If condition is true
        if (L2[i] == 1)
        {

            // Decrement one by 1
            one--;

            // If one < 0, then break
            // out of the loop
            if (one < 0)
            {
                ans = i;
                break;
            }
        }
        else
        {

            // Decrement zero by 1
            zero--;

            // If zero < 0, then
            // break out of loop
            if (zero < 0)
            {
                ans = i;
                break;
            }
        }
    }

    // Print the answer
    document.write(n - ans);
}

// Driver Code

    let L1 = [ 1, 1, 0, 0 ];
    let L2 = [ 0, 0, 0, 1 ];
    let N = L1.length;

    // Function Call
    countRemainingElements(L1, L2, N);

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)