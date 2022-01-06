# 使用计数排序在值为 1 到 N 的数组中查找重复项

> 原文:[https://www . geesforgeks . org/find-数组中的重复值-1 到-n-使用计数-排序/](https://www.geeksforgeeks.org/find-duplicates-in-an-array-with-values-1-to-n-using-counting-sort/)

给定一个由 **N** 元素组成的常量[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，该数组包含从 **1** 到**N–1**的元素，这些数字中的任何一个出现任意次。
**举例:**

> **输入:** N = 5，arr[] = {1，3，4，2，2}
> **输出:** 2
> **说明:**
> 2 是多次出现的数字。
> **输入:** N = 5，arr[] = {3，1，3，4，2}
> **输出:** 3
> **说明:**
> 3 是多次出现的数字。

**天真法:**天真法是先[排序](https://www.geeksforgeeks.org/sorting-algorithms/)给定数组，然后寻找数组的相邻位置，找到重复的编号。
**时间复杂度:** *O(N*log N)*
**辅助空间:** *O(1)*
**高效途径:**优化上述方法的思路是利用[计数排序的概念](https://www.geeksforgeeks.org/counting-sort/)。由于数组中元素的范围是已知的，因此我们可以使用这种排序技术来临时计算时间复杂度。
思路是初始化另一个大小相同的数组(比如**count[]**)**N**并将所有元素初始化为 **0** 。然后统计数组中每个元素的出现次数，并更新**计数[]** 中的计数。打印所有计数大于 **1** 的元素。
以下是上述方法的实施:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the duplicate
// number using counting sort method
int findDuplicate(int arr[], int n)
{
    int countArr[n + 1], i;

    // Initialize all the elements
    // of the countArr to 0
    for (i = 0; i <= n; i++)
        countArr[i] = 0;

    // Count the occurences of each
    // element of the array
    for (i = 0; i <= n; i++)
        countArr[arr[i]]++;

    bool a = false;

    // Find the element with more
    // than one count
    for (i = 1; i <= n; i++) {

        if (countArr[i] > 1) {
            a = true;
            cout << i << ' ';
        }
    }

    // If unique elements are ther
    // print "-1"
    if (!a)
        cout << "-1";
}

// Driver Code
int main()
{
    // Given N
    int n = 4;

    // Given array arr[]
    int arr[] = { 1, 3, 4, 2, 2 };

    // Function Call
    findDuplicate(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to find the duplicate number
    // using counting sort method
    public static int
    findDuplicate(int arr[], int n)
    {
        int countArr[] = new int[n + 1], i;

        // Initialize all the elements of the
        // countArr to 0
        for (i = 0; i <= n; i++)
            countArr[i] = 0;

        // Count the occurences of each
        // element of the array
        for (i = 0; i <= n; i++)
            countArr[arr[i]]++;

        bool a = false;

        // Find the element with more
        // than one count
        for (i = 1; i <= n; i++) {

            if (countArr[i] > 1) {
                a = true;
                cout << i << ' ';
            }
        }
        if (!a)
            System.out.println("-1");
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 4;
        int arr[] = { 1, 3, 4, 2, 2 };

        // Function Call
        findDuplicate(arr, n);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the duplicate
# number using counting sort method
def findDuplicate(arr, n):

    # Initialize all the elements
    # of the countArr to 0
    countArr = [0] * (n + 1)

    # Count the occurences of each
    # element of the array
    for i in range(n + 1):
        countArr[arr[i]] += 1

    a = False

    # Find the element with more
    # than one count
    for i in range(1, n + 1):
        if(countArr[i] > 1):
            a = True
            print(i, end = " ")

    # If unique elements are there
    # print "-1"
    if(not a):
        print(-1)

# Driver code
if __name__ == '__main__':

    # Given N
    n = 4

    # Given array arr[]
    arr = [ 1, 3, 4, 2, 2 ]

    # Function Call
    findDuplicate(arr, n)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the duplicate number
// using counting sort method
static void findDuplicate(int []arr, int n)
{
    int []countArr = new int[n + 1];
    int i;

    // Initialize all the elements of the
    // countArr to 0
    for(i = 0; i <= n; i++)
       countArr[i] = 0;

    // Count the occurences of each
    // element of the array
    for(i = 0; i <= n; i++)
       countArr[arr[i]]++;

    bool a = false;

    // Find the element with more
    // than one count
    for(i = 1; i <= n; i++)
    {
       if (countArr[i] > 1)
       {
           a = true;
           Console.Write(i + " ");
        }
    }
    if (!a)
        Console.WriteLine("-1");
}

// Driver Code
public static void Main(String[] args)
{
    int n = 4;
    int []arr = { 1, 3, 4, 2, 2 };

    // Function Call
    findDuplicate(arr, n);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to find the duplicate number
    // using counting sort method
    function
    findDuplicate(arr, n)
    {
        let countArr = Array.from({length: n+1}, (_, i) => 0), i;

        // Initialize all the elements of the
        // countArr to 0
        for (i = 0; i <= n; i++)
            countArr[i] = 0;

        // Count the occurences of each
        // element of the array
        for (i = 0; i <= n; i++)
            countArr[arr[i]]++;

        let a = false;

        // Find the element with more
        // than one count
        for (i = 1; i <= n; i++) {

            if (countArr[i] > 1) {
                a = true;
                document.write(i + " ");
            }
        }
        if (!a)
            document.write("-1");
    }

// Driver Code

        let n = 4;
        let arr = [ 1, 3, 4, 2, 2 ];

        // Function Call
        findDuplicate(arr, n);

</script>
```

**Output:** 

```
2
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(N)*
**相关文章:**

1.  [在 O(n)个时间和 O(1)个额外空间中查找重复|设置 1](https://www.geeksforgeeks.org/find-duplicates-in-on-time-and-constant-extra-space/)
2.  [用 O(n)和使用 O(1)额外空间在数组中复制| Set-2](https://www.geeksforgeeks.org/duplicates-array-using-o1-extra-space-set-2/)