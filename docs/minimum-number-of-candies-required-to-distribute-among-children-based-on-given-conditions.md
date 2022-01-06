# 根据给定条件，在儿童中分发糖果所需的最小数量

> 原文:[https://www . geeksforgeeks . org/根据给定条件在儿童中分配所需的最小糖果数量/](https://www.geeksforgeeks.org/minimum-number-of-candies-required-to-distribute-among-children-based-on-given-conditions/)

给定一个由代表 **N** 儿童等级的 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】】**，任务是找到分配给 **N** 儿童所需的最小糖果数量，使得每个儿童至少获得一颗糖果，并且具有较高等级的儿童比其邻居获得更多糖果。

**示例:**

> **输入:** arr[] = {1，0，2}
> **输出:** 5
> **解释:**
> 将糖果的分发视为满足给定条件的{2，1，2}。所以糖果的总和是 2 + 1 + 2 = 5，这是最少需要的糖果。
> 
> **输入:** arr[] = {1，2，2 }
> T3】输出: 4

**方法:**给定的问题可以用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。按照以下步骤解决问题:

*   初始化一个数组，说 **ans[]** 存储分配给每个孩子的糖果量，用 **1** 初始化到每个数组元素 **ans[]** 。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，如果 **arr[i + 1]** 的值大于 **arr[i]** ，且 **ans[i + 1]** 的值至少为 **ans[i]** ，则将 **ans[i + 1]** 的值更新为 **ans[i] + 1** 。
*   [从后面遍历给定的数组](https://www.geeksforgeeks.org/how-to-traverse-a-c-set-in-reverse-direction/)并执行以下步骤:
    *   如果 **arr[i]** 的值大于 **arr[i + 1]** ，且 **ans[i]** 的值至少为 **ans[i + 1]** ，则将 **ans[i + 1]** 的值更新为 **ans[i] + 1** 。
    *   如果 **arr[i]** 的值等于 **arr[i + 1]** ， **ans[i]** 的值小于 **ans[i + 1]** ，则将 **ans[i + 1]** 的值更新为 **ans[i] + 1** 。
*   完成以上步骤后，[打印数组](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/) **和**的和作为糖果的合成和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum number
// of candies that is to be distributed
int countCandies(int arr[], int n)
{
    // Stores total count of candies
    int sum = 0;

    // Stores the amount of candies
    // allocated to a student
    int ans[n];

    // If the value of N is 1
    if (n == 1) {
        return 1;
    }

    // Initialize with 1 all array
    // element
    for (int i = 0; i < n; i++)
        ans[i] = 1;

    // Traverse the array arr[]
    for (int i = 0; i < n - 1; i++) {

        // If arr[i+1] is greater than
        // arr[i] and ans[i+1] is
        // at most ans[i]
        if (arr[i + 1] > arr[i]
            && ans[i + 1] <= ans[i]) {

            // Assign ans[i]+1 to
            // ans[i+1]
            ans[i + 1] = ans[i] + 1;
        }
    }

    // Iterate until i is atleast 0
    for (int i = n - 2; i >= 0; i--) {

        // If arr[i] is greater than
        // arr[i+1] and ans[i] is
        // at most ans[i+1]
        if (arr[i] > arr[i + 1]
            && ans[i] <= ans[i + 1]) {

            // Assign ans[i+1]+1 to
            // ans[i]
            ans[i] = ans[i + 1] + 1;
        }

        // If arr[i] is equals arr[i+1]
        // and ans[i] is less than
        // ans[i+1]
        else if (arr[i] == arr[i + 1]
                 && ans[i] < ans[i + 1]) {

            // Assign ans[i+1]+1 to
            // ans[i]
            ans[i] = ans[i + 1] + 1;
        }

        // Increment the sum by ans[i]
        sum += ans[i];
    }

    sum += ans[n - 1];

    // Return the resultant sum
    return sum;
}

// Driver Code
int main()
{
    int arr[] = { 1, 0, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << countCandies(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to count the minimum number
// of candies that is to be distributed
static int countCandies(int arr[], int n)
{

    // Stores total count of candies
    int sum = 0;

    // Stores the amount of candies
    // allocated to a student
    int[] ans = new int[n];

    // If the value of N is 1
    if (n == 1)
    {
        return 1;
    }

    // Initialize with 1 all array
    // element
    for(int i = 0; i < n; i++)
        ans[i] = 1;

    // Traverse the array arr[]
    for(int i = 0; i < n - 1; i++)
    {

        // If arr[i+1] is greater than
        // arr[i] and ans[i+1] is
        // at most ans[i]
        if (arr[i + 1] > arr[i] &&
            ans[i + 1] <= ans[i])
        {

            // Assign ans[i]+1 to
            // ans[i+1]
            ans[i + 1] = ans[i] + 1;
        }
    }

    // Iterate until i is atleast 0
    for(int i = n - 2; i >= 0; i--)
    {

        // If arr[i] is greater than
        // arr[i+1] and ans[i] is
        // at most ans[i+1]
        if (arr[i] > arr[i + 1] &&
            ans[i] <= ans[i + 1])
        {

            // Assign ans[i+1]+1 to
            // ans[i]
            ans[i] = ans[i + 1] + 1;
        }

        // If arr[i] is equals arr[i+1]
        // and ans[i] is less than
        // ans[i+1]
        else if (arr[i] == arr[i + 1] &&
                 ans[i] < ans[i + 1])
        {

            // Assign ans[i+1]+1 to
            // ans[i]
            ans[i] = ans[i + 1] + 1;
        }

        // Increment the sum by ans[i]
        sum += ans[i];
    }

    sum += ans[n - 1];

    // Return the resultant sum
    return sum;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 0, 2 };
    int N = arr.length;

    System.out.println(countCandies(arr, N));
}
}

// This code is contributed by patel2127
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the minimum number
# of candies that is to be distributed
def countCandies(arr, n):

    # Stores total count of candies
    sum = 0

    # Stores the amount of candies
    # allocated to a student
    ans = [1] * n

    # If the value of N is 1
    if (n == 1):
        return 1

    # Initialize with 1 all array
    # element
    # for (i = 0 i < n i++)
    #     ans[i] = 1

    # Traverse the array arr[]
    for i in range(n - 1):

        # If arr[i+1] is greater than
        # arr[i] and ans[i+1] is
        # at most ans[i]
        if (arr[i + 1] > arr[i] and
            ans[i + 1] <= ans[i]):

            # Assign ans[i]+1 to
            # ans[i+1]
            ans[i + 1] = ans[i] + 1

    # Iterate until i is atleast 0
    for i in range(n - 2, -1, -1):

        # If arr[i] is greater than
        # arr[i+1] and ans[i] is
        # at most ans[i+1]
        if (arr[i] > arr[i + 1] and
            ans[i] <= ans[i + 1]):

            # Assign ans[i+1]+1 to
            # ans[i]
            ans[i] = ans[i + 1] + 1

        # If arr[i] is equals arr[i+1]
        # and ans[i] is less than
        # ans[i+1]
        elif (arr[i] == arr[i + 1] and
              ans[i] < ans[i + 1]):

            # Assign ans[i+1]+1 to
            # ans[i]
            ans[i] = ans[i + 1] + 1

        # Increment the sum by ans[i]
        sum += ans[i]

    sum += ans[n - 1]

    # Return the resultant sum
    return sum

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 0, 2 ]
    N = len(arr)

    print (countCandies(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
using System;

public class GFG{

    // Function to count the minimum number
// of candies that is to be distributed
static int countCandies(int[] arr, int n)
{

    // Stores total count of candies
    int sum = 0;

    // Stores the amount of candies
    // allocated to a student
    int[] ans = new int[n];

    // If the value of N is 1
    if (n == 1)
    {
        return 1;
    }

    // Initialize with 1 all array
    // element
    for(int i = 0; i < n; i++)
        ans[i] = 1;

    // Traverse the array arr[]
    for(int i = 0; i < n - 1; i++)
    {

        // If arr[i+1] is greater than
        // arr[i] and ans[i+1] is
        // at most ans[i]
        if (arr[i + 1] > arr[i] &&
            ans[i + 1] <= ans[i])
        {

            // Assign ans[i]+1 to
            // ans[i+1]
            ans[i + 1] = ans[i] + 1;
        }
    }

    // Iterate until i is atleast 0
    for(int i = n - 2; i >= 0; i--)
    {

        // If arr[i] is greater than
        // arr[i+1] and ans[i] is
        // at most ans[i+1]
        if (arr[i] > arr[i + 1] &&
            ans[i] <= ans[i + 1])
        {

            // Assign ans[i+1]+1 to
            // ans[i]
            ans[i] = ans[i + 1] + 1;
        }

        // If arr[i] is equals arr[i+1]
        // and ans[i] is less than
        // ans[i+1]
        else if (arr[i] == arr[i + 1] &&
                 ans[i] < ans[i + 1])
        {

            // Assign ans[i+1]+1 to
            // ans[i]
            ans[i] = ans[i + 1] + 1;
        }

        // Increment the sum by ans[i]
        sum += ans[i];
    }

    sum += ans[n - 1];

    // Return the resultant sum
    return sum;
}

// Driver Code

    static public void Main (){

        int[] arr = { 1, 0, 2 };
    int N = arr.Length;

    Console.WriteLine(countCandies(arr, N));

    }
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the minimum number
// of candies that is to be distributed
function countCandies(arr, n)
{

    // Stores total count of candies
    let sum = 0;

    // Stores the amount of candies
    // allocated to a student
    let ans = new Array(n);

    // If the value of N is 1
    if (n == 1)
    {
        return 1;
    }

    // Initialize with 1 all array
    // element
    for(let i = 0; i < n; i++)
        ans[i] = 1;

    // Traverse the array arr[]
    for(let i = 0; i < n - 1; i++)
    {

        // If arr[i+1] is greater than
        // arr[i] and ans[i+1] is
        // at most ans[i]
        if (arr[i + 1] > arr[i] &&
            ans[i + 1] <= ans[i])
        {

            // Assign ans[i]+1 to
            // ans[i+1]
            ans[i + 1] = ans[i] + 1;
        }
    }

    // Iterate until i is atleast 0
    for(let i = n - 2; i >= 0; i--)
    {

        // If arr[i] is greater than
        // arr[i+1] and ans[i] is
        // at most ans[i+1]
        if (arr[i] > arr[i + 1] &&
            ans[i] <= ans[i + 1])
        {

            // Assign ans[i+1]+1 to
            // ans[i]
            ans[i] = ans[i + 1] + 1;
        }

        // If arr[i] is equals arr[i+1]
        // and ans[i] is less than
        // ans[i+1]
        else if (arr[i] == arr[i + 1] &&
                 ans[i] < ans[i + 1])
        {

            // Assign ans[i+1]+1 to
            // ans[i]
            ans[i] = ans[i + 1] + 1;
        }

        // Increment the sum by ans[i]
        sum += ans[i];
    }
    sum += ans[n - 1];

    // Return the resultant sum
    return sum;
}

// Driver Code
let arr = [ 1, 0, 2 ];
let N = arr.length;

document.write(countCandies(arr, N))

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)