# 最多使用两个数字之间的一次交换来最大化两个数字的总和

> 原文:[https://www . geeksforgeeks . org/最大化两个数之和-最多使用它们之间的一个交换/](https://www.geeksforgeeks.org/maximise-the-sum-of-two-numbers-using-at-most-one-swap-between-them/)

给定两个自然数 **N1** 和 **N2** ，任务是在它们之间交换一个位数后找到最大可能和。
**例:**

> **输入:** N1 = 984788，N2 = 706
> **输出:** 988194
> **解释:**
> 将 N1 的 4 换成 N2 的 7，得到 N1 = 987788，N2 = 406
> Sum = 988194
> 
> **输入:** N1 = 9987，N2 = 123
> **输出:** 10740
> **解释:**
> 将 N1 的 8 换成 N2 的 1，得到 N1 = 9917，N2 = 823
> 总和= 10740

**进场:**

1.  比较 **N1** 和 **N2** ，将两个中较大的[数字分别存储在数组 **arr1** 中，较小的数字分别存储在 **arr2** 中。](https://www.geeksforgeeks.org/program-count-digits-integer-3-different-methods/)
2.  **如果两个数长度不同**，则在 **arr2** 中找到最大元素的指标，在 **arr1** 中找到最显著的指标，[互换](https://www.geeksforgeeks.org/swap-two-variables-in-one-line-in-c-c-python-php-and-java/)使之和最大。
3.  **如果两个数长度相同**，
    *   同时迭代数组 **arr1** 和 **arr2** 。
    *   对于两个数组中索引 **i** 处的每个数字，找出当前数字与索引“I”左侧最大数字之间的差异。
    *   比较差异，找出最重要的数字和最重要的索引，其值需要交换。
4.  从 **arr1** 和 **arr2** 恢复新的数字，计算最大和。

下面的代码是上述方法的实现:

## C++

```
// C++ program to maximise the sum of two
// Numbers using at most one swap between them

#include <bits/stdc++.h>
using namespace std;

#define MAX 100

// Function to maximize the sum
// by swapping only one digit
void findMaxSum(int n1, int n2)
{

    int arr1[MAX] = { 0 }, arr2[MAX] = { 0 };
    int l1 = 0, l2 = 0;

    int max1 = max(n1, n2);
    int min1 = min(n1, n2);

    // Store digits of max(n1, n2)
    for (int i = max1; i > 0; i /= 10)
        arr1[l1++] = (i % 10);

    // Store digits of min(n1, n2)
    for (int i = min1; i > 0; i /= 10)
        arr2[l2++] = (i % 10);

    int f = 0;

    // If length of the two numbers
    // are unequal
    if (l1 != l2) {
        // Find the most significant number
        // and the most significant index
        // for swapping
        int index = (max_element(arr2, arr2 + l2) - arr2);
        for (int i = l1 - 1; i > (l2 - 1); i--) {
            if (arr1[i] < arr2[index]) {
                swap(arr1[i], arr2[index]);
                f = 1;
                break;
            }
        }
    }

    // If both numbers are
    // of equal length
    if (f != 1) {

        int index1 = 0, index2 = 0;
        int diff1 = 0, diff2 = 0;
        for (int i = l2 - 1; i >= 0; i--) {

            // Fetch the index of current maximum
            // digit present in both the arrays
            index1 = (max_element(arr1, arr1 + i) - arr1);
            index2 = (max_element(arr2, arr2 + i) - arr2);

            // Compute the difference
            diff1 = (arr2[index2] - arr1[i]);
            diff2 = (arr1[index1] - arr2[i]);

            // Find the most significant index
            // and the most significant digit
            // to be swapped
            if (diff1 > 0 || diff2 > 0) {

                if (diff1 > diff2) {
                    swap(arr1[i], arr2[index2]);
                    break;
                }

                else if (diff2 > diff1) {
                    swap(arr2[i], arr1[index1]);
                    break;
                }

                else if (diff1 == diff2) {

                    if (index1 <= index2) {
                        swap(arr2[i], arr1[index1]);
                        break;
                    }

                    else if (index2 <= index1) {
                        swap(arr1[i], arr2[index2]);
                        break;
                    }
                }
            }
        }
    }

    // Restore the new numbers
    int f_n1 = 0, f_n2 = 0;
    for (int i = l1 - 1; i >= 0; i--) {
        f_n1 = (f_n1 * 10) + arr1[i];
        f_n2 = (f_n2 * 10) + arr2[i];
    }

    // Display the maximized sum
    cout << (f_n1 + f_n2) << "\n";
}

// Driver function
int main()
{
    int N1 = 9987;
    int N2 = 123;

    findMaxSum(N1, N2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to maximise the sum of two
// Numbers using at most one swap between them
import java.util.*;

class GFG{

static int MAX = 100;

static int max_element(int arr[], int pos)
{
    int tmp = arr[0];
    int ind = 0;

    for(int i = 1; i < pos; i++)
    {
        if (tmp < arr[i])
        {
            tmp = arr[i];
            ind = i;
        }
    }
    return ind;
}

// Function to maximize the sum
// by swapping only one digit
static void findMaxSum(int n1, int n2)
{
    int []arr1 = new int[MAX];
    int []arr2 = new int[MAX];
    int l1 = 0, l2 = 0;

    int max1 = Math.max(n1, n2);
    int min1 = Math.min(n1, n2);

    // Store digits of max(n1, n2)
    for(int i = max1; i > 0; i /= 10)
        arr1[l1++] = (i % 10);

    // Store digits of min(n1, n2)
    for(int i = min1; i > 0; i /= 10)
        arr2[l2++] = (i % 10);

    int f = 0;

    // If length of the two numbers
    // are unequal
    if (l1 != l2)
    {

        // Find the most significant number
        // and the most significant index
        // for swapping
        int index = (max_element(arr2, l2));
        for(int i = l1 - 1; i > (l2 - 1); i--)
        {
            if (arr1[i] < arr2[index])
            {
                int tmp = arr1[i];
                arr1[i] = arr2[index];
                arr2[index] = tmp;
                f = 1;
                break;
            }
        }
    }

    // If both numbers are
    // of equal length
    if (f != 1)
    {
        int index1 = 0, index2 = 0;
        int diff1 = 0, diff2 = 0;

        for(int i = l2 - 1; i >= 0; i--)
        {

            // Fetch the index of current maximum
            // digit present in both the arrays
            index1 = (max_element(arr1, i));
            index2 = (max_element(arr2, i));

            // Compute the difference
            diff1 = (arr2[index2] - arr1[i]);
            diff2 = (arr1[index1] - arr2[i]);

            // Find the most significant index
            // and the most significant digit
            // to be swapped
            if (diff1 > 0 || diff2 > 0)
            {
                if (diff1 > diff2)
                {
                    int tmp = arr1[i];
                    arr1[i] = arr2[index2];
                    arr2[index2] = tmp;
                    break;
                }

                else if (diff2 > diff1)
                {
                    int tmp = arr1[index1];
                    arr1[index1] = arr2[i];
                    arr2[i] = tmp;
                    break;
                }

                else if (diff1 == diff2)
                {
                    if (index1 <= index2)
                    {
                        int tmp = arr1[index1];
                        arr1[index1] = arr2[i];
                        arr2[i] = tmp;
                        break;
                    }

                    else if (index2 <= index1)
                    {
                        int tmp = arr1[i];
                        arr1[i] = arr2[index2];
                        arr2[index2] = tmp;
                        break;
                    }
                }
            }
        }
    }

    // Restore the new numbers
    int f_n1 = 0, f_n2 = 0;
    for(int i = l1 - 1; i >= 0; i--)
    {
        f_n1 = (f_n1 * 10) + arr1[i];
        f_n2 = (f_n2 * 10) + arr2[i];
    }

    // Display the maximized sum
    System.out.println(f_n1 + f_n2);
}

// Driver code
public static void main(String[] args)
{
    int N1 = 9987;
    int N2 = 123;

    findMaxSum(N1, N2);
}
}

// This code is contributed by grand_master
```

## 蟒蛇 3

```
# Python program to maximise the sum of two
# Numbers using at most one swap between them
MAX = 100

# Function to maximize the sum
# by swapping only one digit
def findMaxSum(n1, n2):

    arr1 = [0]*(MAX)
    arr2 = [0]*(MAX)
    l1 = 0
    l2 = 0

    max1 = max(n1, n2);
    min1 = min(n1, n2);

    # Store digits of max(n1, n2)
    i = max1
    while i > 0:
        arr1[l1] = (i % 10)
        l1 += 1
        i //= 10

    # Store digits of min(n1, n2)
    i = min1
    while i > 0:
        arr2[l2] = (i % 10)
        l2 += 1
        i //= 10

    f = 0

    # If length of the two numbers
    # are unequal
    if (l1 != l2):

        # Find the most significant number
        # and the most significant index
        # for swapping
        index = arr2.index(max(arr2))
        for i in range ( l1 - 1, (l2 - 1), -1):
            if (arr1[i] < arr2[index]):
                (arr1[i], arr2[index]) = (arr2[index],arr1[i])
                f = 1
                break

    # If both numbers are
    # of equal length
    if (f != 1):

        index1 = 0
        index2 = 0
        diff1 = 0
        diff2 = 0
        for i in range( l2 - 1, -1,-1):

            # Fetch the index of current maximum
            # digit present in both the arrays
            index1 = arr1.index(max(arr1[:i]))
            index2 = arr2.index(max(arr2[:i]))

            # Compute the difference
            diff1 = (arr2[index2] - arr1[i]);
            diff2 = (arr1[index1] - arr2[i]);

            # Find the most significant index
            # and the most significant digit
            # to be swapped
            if (diff1 > 0 or diff2 > 0):
                if (diff1 > diff2):
                    arr1[i], arr2[index2] = arr2[index2],arr1[i]
                    break

                elif (diff2 > diff1):
                    arr2[i], arr1[index1] = arr1[index1],arr2[i]
                    break

                elif (diff1 == diff2):
                    if (index1 <= index2):
                        arr2[i], arr1[index1] = arr1[index1],arr2[i]
                        break

                    elif (index2 <= index1):
                        arr1[i], arr2[index2] = arr2[index2],arr1[i]
                        break;

    # Restore the new numbers
    f_n1 = 0
    f_n2 = 0
    for i in range (l1 - 1, -1,-1):
        f_n1 = (f_n1 * 10) + arr1[i]
        f_n2 = (f_n2 * 10) + arr2[i]

    # Display the maximized sum
    print(f_n1 + f_n2)

# Driver function
N1 = 9987
N2 = 123

findMaxSum(N1, N2)

# This code is contributed by ANKITKUMAR34
```

## C#

```
// C# program to maximise the sum of two
// Numbers using at most one swap between them
using System;

class GFG{

static int MAX = 100;

static int max_element(int []arr, int pos)
{
    int tmp = arr[0];
    int ind = 0;

    for(int i = 1; i < pos; i++)
    {
        if (tmp < arr[i])
        {
            tmp = arr[i];
            ind = i;
        }
    }
    return ind;
}

// Function to maximize the sum
// by swapping only one digit
static void findMaxSum(int n1, int n2)
{

    int []arr1 = new int[MAX];
    int []arr2 = new int[MAX];
    int l1 = 0, l2 = 0;

    int max1 = Math.Max(n1, n2);
    int min1 = Math.Min(n1, n2);

    // Store digits of max(n1, n2)
    for(int i = max1; i > 0; i /= 10)
        arr1[l1++] = (i % 10);

    // Store digits of min(n1, n2)
    for(int i = min1; i > 0; i /= 10)
        arr2[l2++] = (i % 10);

    int f = 0;

    // If length of the two numbers
    // are unequal
    if (l1 != l2)
    {

        // Find the most significant number
        // and the most significant index
        // for swapping
        int index = (max_element(arr2,l2));
        for(int i = l1 - 1; i > (l2 - 1); i--)
        {
            if (arr1[i] < arr2[index])
            {
                int tmp = arr1[i];
                arr1[i] = arr2[index];
                arr2[index] = tmp;
                f = 1;
                break;
            }
        }
    }

    // If both numbers are
    // of equal length
    if (f != 1)
    {
        int index1 = 0, index2 = 0;
        int diff1 = 0, diff2 = 0;

        for(int i = l2 - 1; i >= 0; i--)
        {

            // Fetch the index of current maximum
            // digit present in both the arrays
            index1 = (max_element(arr1, i));
            index2 = (max_element(arr2, i));

            // Compute the difference
            diff1 = (arr2[index2] - arr1[i]);
            diff2 = (arr1[index1] - arr2[i]);

            // Find the most significant index
            // and the most significant digit
            // to be swapped
            if (diff1 > 0 || diff2 > 0)
            {
                if (diff1 > diff2)
                {
                    int tmp = arr1[i];
                    arr1[i] = arr2[index2];
                    arr2[index2] = tmp;
                    break;
                }

                else if (diff2 > diff1)
                {
                    int tmp = arr1[index1];
                    arr1[index1] = arr2[i];
                    arr2[i] = tmp;
                    break;
                }

                else if (diff1 == diff2)
                {
                    if (index1 <= index2)
                    {
                        int tmp = arr1[index1];
                        arr1[index1] = arr2[i];
                        arr2[i] = tmp;
                        break;
                    }

                    else if (index2 <= index1)
                    {
                        int tmp = arr1[i];
                        arr1[i] = arr2[index2];
                        arr2[index2] = tmp;
                        break;
                    }
                }
            }
        }
    }

    // Restore the new numbers
    int f_n1 = 0, f_n2 = 0;
    for(int i = l1 - 1; i >= 0; i--)
    {
        f_n1 = (f_n1 * 10) + arr1[i];
        f_n2 = (f_n2 * 10) + arr2[i];
    }

    // Display the maximized sum
    Console.Write(f_n1 + f_n2);
}

// Driver code
public static void Main(string[] args)
{
    int N1 = 9987;
    int N2 = 123;

    findMaxSum(N1, N2);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// JavaScript program to maximise the sum of two
// Numbers using at most one swap between them

let MAX = 100;

function max_element(arr, pos)
{
    let tmp = arr[0];
    let ind = 0;

    for(let i = 1; i < pos; i++)
    {
        if (tmp < arr[i])
        {
            tmp = arr[i];
            ind = i;
        }
    }
    return ind;
}

// Function to maximize the sum
// by swapping only one digit
function findMaxSum(n1, n2)
{
    let arr1 = Array.from({length: MAX}, (_, i) => 0);
    let arr2 = Array.from({length: MAX}, (_, i) => 0);
    let l1 = 0, l2 = 0;

    let max1 = Math.max(n1, n2);
    let min1 = Math.min(n1, n2);

    // Store digits of max(n1, n2)
    for(let i = max1; i > 0; i = Math.floor(i / 10))
        arr1[l1++] = (i % 10);

    // Store digits of min(n1, n2)
    for(let i = min1; i > 0; i = Math.floor(i / 10))
        arr2[l2++] = (i % 10);

    let f = 0;

    // If length of the two numbers
    // are unequal
    if (l1 != l2)
    {

        // Find the most significant number
        // and the most significant index
        // for swapping
        let index = (max_element(arr2, l2));
        for(let i = l1 - 1; i > (l2 - 1); i--)
        {
            if (arr1[i] < arr2[index])
            {
                let tmp = arr1[i];
                arr1[i] = arr2[index];
                arr2[index] = tmp;
                f = 1;
                break;
            }
        }
    }

    // If both numbers are
    // of equal length
    if (f != 1)
    {
        let index1 = 0, index2 = 0;
        let diff1 = 0, diff2 = 0;

        for(let i = l2 - 1; i >= 0; i--)
        {

            // Fetch the index of current maximum
            // digit present in both the arrays
            index1 = (max_element(arr1, i));
            index2 = (max_element(arr2, i));

            // Compute the difference
            diff1 = (arr2[index2] - arr1[i]);
            diff2 = (arr1[index1] - arr2[i]);

            // Find the most significant index
            // and the most significant digit
            // to be swapped
            if (diff1 > 0 || diff2 > 0)
            {
                if (diff1 > diff2)
                {
                    let tmp = arr1[i];
                    arr1[i] = arr2[index2];
                    arr2[index2] = tmp;
                    break;
                }

                else if (diff2 > diff1)
                {
                    let tmp = arr1[index1];
                    arr1[index1] = arr2[i];
                    arr2[i] = tmp;
                    break;
                }

                else if (diff1 == diff2)
                {
                    if (index1 <= index2)
                    {
                        let tmp = arr1[index1];
                        arr1[index1] = arr2[i];
                        arr2[i] = tmp;
                        break;
                    }

                    else if (index2 <= index1)
                    {
                        let tmp = arr1[i];
                        arr1[i] = arr2[index2];
                        arr2[index2] = tmp;
                        break;
                    }
                }
            }
        }
    }

    // Restore the new numbers
    let f_n1 = 0, f_n2 = 0;
    for(let i = l1 - 1; i >= 0; i--)
    {
        f_n1 = (f_n1 * 10) + arr1[i];
        f_n2 = (f_n2 * 10) + arr2[i];
    }

    // Display the maximized sum
    document.write(f_n1 + f_n2);
}

// Driver Code

    let N1 = 9987;
    let N2 = 123;

    findMaxSum(N1, N2); 

</script>
```

**Output:** 

```
10740
```

时间复杂度:0(n)

辅助空间:0(最大)