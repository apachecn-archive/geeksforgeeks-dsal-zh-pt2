# 将一个数组分成相同和的两半

> 原文:[https://www . geesforgeks . org/diving-array-两半-sum/](https://www.geeksforgeeks.org/dividing-array-two-halves-sum/)

给定一个偶数大小的整数数组。我们需要找到是否有可能将数组元素分成两组，从而满足以下条件。

1.  两个子集的大小相同。
2.  机器人集合中元素的总和是相同的。
3.  每个元素都是两个集合之一的一部分。

**示例:**

```
Input: arr[] = {1, 3, 2, 1, 2, 1}
Output : Yes
Explanation: We can get two subsets
as {1, 3, 1} and {2, 2, 1}

Input: {1, 2, 3, 4, 5, 6}
Output : No
```

这个想法是建立在方法 1 的基础上的。
[打印给定 n 大小数组中 r 元素的所有可能组合](https://www.geeksforgeeks.org/print-all-possible-combinations-of-r-elements-in-a-given-array-of-size-n/)
我们生成 n/2 大小的所有子集。对于每个子集，我们检查它的和是否是 2 的和。

## C++

```
// Program to check if we can divide an array into two
// halves such that sum of the two is same.
#include <bits/stdc++.h>
using namespace std;

bool combinationUtil(int arr[], int half[], int start, int end,
                     int index, int n, int sum);

// Returns true if it is possible to divide array into two halves.
// of same sum. This function mainly uses combinationUtil()
bool isPossible(int arr[], int n)
{
    // If size of array is not even.
    if (n % 2 != 0)
        return false;

    // If sum of array is not even.
    int sum = accumulate(arr, arr + n, 0);
    if (sum % 2 != 0)
        return false;

    // A temporary array to store all combination one by one
    int half[n / 2];

    // Print all combination using temporary array 'half[]'
    return combinationUtil(arr, half, 0, n - 1, 0, n, sum);
}

/* arr[] ---> Input Array
   half[] ---> Temporary array to store current combination
               of size n/2
   start & end ---> Starting and Ending indexes in arr[]
   index ---> Current index in half[] */
bool combinationUtil(int arr[], int half[], int start, int end,
                     int index, int n, int sum)
{
    // Current combination is ready to be printed, print it
    if (index == n / 2) {
        int curr_sum = accumulate(half, half + n / 2, 0);
        return (curr_sum + curr_sum == sum);
    }

    // replace index with all possible elements. The condition
    // "end-i+1 >= n/2-index" makes sure that including one element
    // at index will make a combination with remaining elements
    // at remaining positions
    for (int i = start; i <= end && end - i + 1 >= n/2 - index; i++) {
        half[index] = arr[i];
        if (combinationUtil(arr, half, i + 1, end, index + 1, n, sum))
            return true;
    }

    return false;
}

// Driver program to test above functions
int main()
{
    int arr[] = { 1, 2, 4, 4, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    if (isPossible(arr, n))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if we can
// divide an array into two halves
// such that sum of the two is same.
public class DivideArray{

    static int accumulate(int arr[], int first,
                                     int last)
    {
        int init = 0;
        for (int i = first; i< last; i++) {
            init = init + arr[i];
        }

        return init;
    }

    // Returns true if it is possible to divide
    // array into two halves of same sum.
    // This function mainly uses combinationUtil()
    static Boolean isPossible(int arr[], int n)
    {
        // If size of array is not even.
        if (n % 2 != 0)
            return false;

        // If sum of array is not even.
        int sum = accumulate(arr, 0, n);
        if (sum % 2 != 0)
            return false;

        // A temporary array to store all
        // combination one by one int k=n/2;
        int half[] = new int[n/2];

        // Print all combination using temporary
        // array 'half[]'
        return combinationUtil(arr, half, 0, n - 1,
                                0, n, sum);
    }

    /* arr[] ---> Input Array
    half[] ---> Temporary array to store current
                combination of size n/2
    start & end ---> Starting and Ending indexes in arr[]
    index ---> Current index in half[] */
    static Boolean combinationUtil(int arr[], int half[],
                                   int start, int end,
                                   int index, int n,
                                   int sum)
    {
        // Current combination is ready to
        // be printed, print it
        if (index == n / 2) {
            int curr_sum = accumulate(half, 0 , n/2);
            return (curr_sum + curr_sum == sum);
        }

        // replace index with all possible elements.
        // The condition "end-i+1 >= n/2-index" makes
        // sure that including one element at index
        // will make a combination with remaining
        // elements at remaining positions
        for (int i = start; i <= end && end - i + 1 >=
                                  n/2 - index; i++) {
            half[index] = arr[i];
            if (combinationUtil(arr, half, i + 1, end,
                                 index + 1, n, sum))
                return true;
        }

        return false;
    }

    // Driver code
    public static void main(String[] s)
    {
        int arr[] = {1, 2, 4, 4, 5, 6 };

        if (isPossible(arr, arr.length))
        System.out.println("Yes");
        else
        System.out.println("NO");
    }
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python3 program to check if
# we can divide an array into two
# halves such that sum of the two is same.

# Returns true if it is possible to divide
# array into two halves of same sum.
# This function mainly uses combinationUtil()
def isPossible(arr, n):

    # If size of array is not even
    if n % 2 != 0:
        return False

    # If sum of array is not even.
    s = sum(arr)
    if s % 2 != 0:
        return False

    # A temporary array to store
    # all combination one by one
    half = [0] * (n // 2)

    # Print all combination using
    # temporary array 'half[]'
    return combinationUtil(arr, half, 0,
                           n - 1, 0, n, s)

'''
arr[] ---> Input Array
half[] ---> Temporary array to store current
            combination of size n/2
start & end ---> Starting and Ending indexes in arr[]
index ---> Current index in half[]
'''
def combinationUtil(arr, half, start, end, index, n, s):

    # Current combination is
    # ready to be printed, print it
    if index == n // 2:
        curr_sum = sum(half)
        if (curr_sum + curr_sum == s):
            return True
        else:
            return False

    # replace index with all possible elements.
    # The condition "end-i+1 >= n/2-index"
    # makes sure that including one element
    # at index will make a combination with
    # remaining elements at remaining positions
    i = start
    while i <= end and (end - i + 1) >= (n // 2 - index):
        half[index] = arr[i]
        if combinationUtil(arr, half, i + 1, end,
                           index + 1, n, s):
            return True
        i += 1

    return False

# Driver Code
if __name__ == "__main__":
    arr = [1, 2, 4, 4, 5, 6]
    n = len(arr)

    if isPossible(arr, n):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to check if we can
// divide an array into two halves
// such that sum of the two is same.
using System;

public class DivideArray{

    static int accumulate(int []arr, int first,
                                    int last)
    {
        int init = 0;
        for (int i = first; i< last; i++) {
            init = init + arr[i];
        }

        return init;
    }

    // Returns true if it is possible to divide
    // array into two halves of same sum.
    // This function mainly uses combinationUtil()
    static Boolean isPossible(int []arr, int n)
    {
        // If size of array is not even.
        if (n % 2 != 0)
            return false;

        // If sum of array is not even.
        int sum = accumulate(arr, 0, n);
        if (sum % 2 != 0)
            return false;

        // A temporary array to store all
        // combination one by one int k=n/2;
        int []half = new int[n/2];

        // Print all combination using temporary
        // array 'half[]'
        return combinationUtil(arr, half, 0, n - 1,
                                0, n, sum);
    }

    /* arr[] ---> Input Array
    half[] ---> Temporary array to store current
                combination of size n/2
    start & end ---> Starting and Ending indexes in arr[]
    index ---> Current index in half[] */
    static Boolean combinationUtil(int []arr, int []half,
                                int start, int end,
                                int index, int n,
                                int sum)
    {
        // Current combination is ready to
        // be printed, print it
        if (index == n / 2) {
            int curr_sum = accumulate(half, 0 , n/2);
            return (curr_sum + curr_sum == sum);
        }

        // replace index with all possible elements.
        // The condition "end-i+1 >= n/2-index" makes
        // sure that including one element at index
        // will make a combination with remaining
        // elements at remaining positions
        for (int i = start; i <= end && end - i + 1 >=
                                n/2 - index; i++) {
            half[index] = arr[i];
            if (combinationUtil(arr, half, i + 1, end,
                                index + 1, n, sum))
                return true;
        }

        return false;
    }

    // Driver code
    public static void Main()
    {
        int []arr = {1, 2, 4, 4, 5, 6 };

        if (isPossible(arr, arr.Length))
        Console.WriteLine("Yes");
        else
        Console.WriteLine("NO");
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to check if we can
// divide an array into two halves
// such that sum of the two is same.
function accumulate(arr, first, last)
{
    let init = 0;
    for(let i = first; i< last; i++)
    {
        init = init + arr[i];
    }
    return init;
}

// Returns true if it is possible to divide
// array into two halves of same sum.
// This function mainly uses combinationUtil()
function isPossible(arr, n)
{

    // If size of array is not even.
    if (n % 2 != 0)
        return false;

    // If sum of array is not even.
    let sum = accumulate(arr, 0, n);
    if (sum % 2 != 0)
        return false;

    // A temporary array to store all
    // combination one by one let k=n/2;
    let half = [];

    // Print all combination using temporary
    // array 'half[]'
    return combinationUtil(arr, half, 0, n - 1,
                           0, n, sum);
}

/* arr[] ---> Input Array
half[] ---> Temporary array to store current
            combination of size n/2
start & end ---> Starting and Ending indexes in arr[]
index ---> Current index in half[] */
function combinationUtil(arr, half, start, end,
                         index, n, sum)
{

    // Current combination is ready to
    // be printed, print it
    if (index == n / 2)
    {
        let curr_sum = accumulate(half, 0 , n / 2);
        return (curr_sum + curr_sum == sum);
    }

    // Replace index with all possible elements.
    // The condition "end-i+1 >= n/2-index" makes
    // sure that including one element at index
    // will make a combination with remaining
    // elements at remaining positions
    for(let i = start;
            i <= end && end - i + 1 >= n / 2 - index;
            i++)
    {
        half[index] = arr[i];
        if (combinationUtil(arr, half, i + 1, end,
                            index + 1, n, sum))
            return true;
    }
    return false;
}

// Driver Code
let arr = [ 1, 2, 4, 4, 5, 6 ];

if (isPossible(arr, arr.length))
    document.write("Yes");
else
    document.write("NO");

// This code is contributed by susmitakundugoaldanga

</script>
```

**输出:**

```
Yes
```