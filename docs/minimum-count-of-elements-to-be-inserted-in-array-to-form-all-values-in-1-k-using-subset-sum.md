# 使用子集和

在[1，K]中形成所有值的数组中要插入的元素的最小数量

> 原文:[https://www . geeksforgeeks . org/数组中要插入的最小元素数-形成 1-k 中的所有值-使用子集-总和/](https://www.geeksforgeeks.org/minimum-count-of-elements-to-be-inserted-in-array-to-form-all-values-in-1-k-using-subset-sum/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[排序的](https://www.geeksforgeeks.org/sorting-algorithms/) [数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到要插入到数组中的元素的最小数量，从而通过添加修改后的数组的任意[子集的元素，可以形成范围**【1，K】**中的任意值。](https://www.geeksforgeeks.org/find-whether-an-array-is-subset-of-another-array-set-1/)

**示例:**

> **输入:** arr[] = {1，3}，K = 6
> **输出:** 1
> **解释:**
> 将数字 2 添加到数组中会将数组 arr[]修改为{1，2，3}。现在，范围[1，6]内的每个和值都可以形成:
> 
> 1.  总和= 1:子集为{1}。
> 2.  总和= 2:子集为{2}。
> 3.  总和= 3:子集为{3}。
> 4.  Sum = 4:子集为{1，3}。
> 5.  总和= 5:子集为{2，3}。
> 6.  Sum = 6:子集为{1，2，3}。
> 
> 因此，要添加的元素的最小数量是 1。
> 
> **输入:** arr[] = {1，5，10}，K = 20
> T3】输出: 2

**方法:**给定的问题可以通过使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决，该方法基于以下观察:

1.  将 **X** 视为最大值，使得范围**【1，X】**中的所有数字可以通过对数组的任何子集求和而形成。
2.  然后可以观察到，通过将整数 **Y** 添加到数组中，范围修改为**【1，X+Y】**，因为现在可以形成范围**【X，X+Y】**中的每个数字。
3.  因此，想法是[贪婪地](https://www.geeksforgeeks.org/greedy-algorithms/)添加最能增加范围的元素，并且不会跳过获得的新范围内的任何数字。可以通过每次向数组中添加 **X** 并将 **X** 修改为 **2*X.** 来完成

按照以下步骤解决问题:

*   初始化两个整数变量，比如 **i** 和**计数**为 **0** ，分别存储数组元素的索引和需要的元素个数。
*   初始化一个变量，比如说**需要一个**作为 **1** ，来存储每个数字可以组成的数字。
*   迭代[直到](https://www.geeksforgeeks.org/c-c-do-while-loop-with-examples/) **要求≤ K，**并执行以下操作:
    *   如果 **i** < **N** 和**需要 um>=****arr**，那么将**required um**增加**arr【I】**，将 **i** 增加 **1** 。
    *   否则，将 **requiredNum** 增加 **requiredNum，**和 **count** 增加 **1** 。
*   最后，完成上述步骤后，打印在**计数**中得到的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to find the count of minimum
// elements to be inserted to form every
// number in a range
int minElements(int arr[], int N, int K)
{
    // Stores the count of numbers needed
    int count = 0;

    // Stores the numbers upto which every
    // numbers can be formed
    long long requiredNum = 1;

    // Stores the index of the array arr[]
    int i = 0;

    // Iterate until requiredSum is less than
    // or equal to K
    while (requiredNum <= K) {

        // If i is less than N and requiredSum
        // is greater than or equal to arr[i]
        if (i < N && requiredNum >= arr[i]) {

            // Increment requiredSum
            // by arr[i]
            requiredNum += arr[i];

            // Increment i by 1
            i++;
        }

        // Otherwise
        else {

            // Increment count by 1
            count++;

            // Increment requiredSum
            // by requiredSum
            requiredNum += requiredNum;
        }
    }

    // Return result
    return count;
}

// Driver Code
int main()
{
    // Input
    int arr[] = { 1, 3 };
    int K = 6;
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << minElements(arr, N, K) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {
    // Function to find the count of minimum
    // elements to be inserted to form every
    // number in a range
    public static int minElements(int arr[], int N, int K)
    {
        // Stores the count of numbers needed
        int count = 0;

        // Stores the numbers upto which every
        // numbers can be formed
        long requiredNum = 1;

        // Stores the index of the array arr[]
        int i = 0;

        // Iterate until requiredSum is less than
        // or equal to K
        while (requiredNum <= K) {

            // If i is less than N and requiredSum
            // is greater than or equal to arr[i]
            if (i < N && requiredNum >= arr[i]) {

                // Increment requiredSum
                // by arr[i]
                requiredNum += arr[i];

                // Increment i by 1
                i++;
            }

            // Otherwise
            else {

                // Increment count by 1
                count++;

                // Increment requiredSum
                // by requiredSum
                requiredNum += requiredNum;
            }
        }

        // Return result
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Input
        int arr[] = { 1, 3 };
        int K = 6;
        int N = arr.length;

        // Function Call
        System.out.println(minElements(arr, N, K));
        // This code is contributed by Potta Lokesh
    }
}
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the count of minimum
# elements to be inserted to form every
# number in a range
def minElements(arr, N, K):

    # Stores the count of numbers needed
    count = 0

    # Stores the numbers upto which every
    # numbers can be formed
    requiredNum = 1

    # Stores the index of the array arr[]
    i = 0

    # Iterate until requiredSum is less than
    # or equal to K
    while (requiredNum <= K):

        # If i is less than N and requiredSum
        # is greater than or equal to arr[i]
        if (i < N and requiredNum >= arr[i]):

            # Increment requiredSum
            # by arr[i]
            requiredNum += arr[i]

            # Increment i by 1
            i += 1

        # Otherwise
        else:
            # Increment count by 1
            count += 1

            # Increment requiredSum
            # by requiredSum
            requiredNum += requiredNum

    # Return result
    return count

# Driver Code
if __name__ == '__main__':
    # Input
    arr = [1, 3]
    K = 6
    N = len(arr)

    # Function Call
    print(minElements(arr, N, K))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

class GFG {
    // Function to find the count of minimum
    // elements to be inserted to form every
    // number in a range
    public static int minElements(int[] arr, int N, int K)
    {
        // Stores the count of numbers needed
        int count = 0;

        // Stores the numbers upto which every
        // numbers can be formed
        long requiredNum = 1;

        // Stores the index of the array arr[]
        int i = 0;

        // Iterate until requiredSum is less than
        // or equal to K
        while (requiredNum <= K) {

            // If i is less than N and requiredSum
            // is greater than or equal to arr[i]
            if (i < N && requiredNum >= arr[i]) {

                // Increment requiredSum
                // by arr[i]
                requiredNum += arr[i];

                // Increment i by 1
                i++;
            }

            // Otherwise
            else {

                // Increment count by 1
                count++;

                // Increment requiredSum
                // by requiredSum
                requiredNum += requiredNum;
            }
        }

        // Return result
        return count;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        // Input
        int[] arr = { 1, 3 };
        int K = 6;
        int N = arr.Length;

        // Function Call
        Console.Write(minElements(arr, N, K));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the count of minimum
// elements to be inserted to form every
// number in a range
function minElements(arr, N, K) {
    // Stores the count of numbers needed
    let count = 0;

    // Stores the numbers upto which every
    // numbers can be formed
    let requiredNum = 1;

    // Stores the index of the array arr[]
    let i = 0;

    // Iterate until requiredSum is less than
    // or equal to K
    while (requiredNum <= K) {

        // If i is less than N and requiredSum
        // is greater than or equal to arr[i]
        if (i < N && requiredNum >= arr[i]) {

            // Increment requiredSum
            // by arr[i]
            requiredNum += arr[i];

            // Increment i by 1
            i++;
        }

        // Otherwise
        else {

            // Increment count by 1
            count++;

            // Increment requiredSum
            // by requiredSum
            requiredNum += requiredNum;
        }
    }

    // Return result
    return count;
}

// Driver Code

// Input
let arr = [1, 3];
let K = 6;
let N = arr.length;

// Function Call
document.write(minElements(arr, N, K) + "<br>");

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output**

```
1
```

***时间复杂度:** O(N + log(K))*
***辅助空间:** O(1)*