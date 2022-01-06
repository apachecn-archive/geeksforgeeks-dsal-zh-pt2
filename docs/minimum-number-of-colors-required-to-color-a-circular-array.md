# 给圆形阵列上色所需的最小颜色数

> 原文:[https://www . geesforgeks . org/最小颜色数-圆形阵列需要的颜色数/](https://www.geeksforgeeks.org/minimum-number-of-colors-required-to-color-a-circular-array/)

给定一个包含 **N** 个整数的圆形数组 **arr[]** ，任务是找到给数组元素着色所需的最小颜色数，使得两个具有不同值的相邻元素不能着色相同。
**例:**

> **输入:** arr[] = {1，2，1，1，2}
> **输出:** 2
> **说明:**
> 至少需要 2 种颜色。
> 我们可以将颜色分布为{r，g，r，r，g}，这样就不会有具有不同值的相邻元素颜色相同。
> **输入:** arr[] = {1，2，3，4}
> **输出:** 2
> **说明:**
> 至少需要 2 种颜色。
> 我们可以将颜色分布为{r，g，r，g}。

**进场:**这个问题可以用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决。

1.  如果所有的值都相同，那么只需要一种颜色。
2.  如果有多个不同的元素，并且元素总数是偶数，则需要 2 种颜色。
3.  如果有多个不同的元素，并且元素总数为奇数，则检查:
    *   如果存在具有相同值的相邻元素，则需要 2 种颜色。
    *   否则需要 3 种颜色。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach

#include <bits/stdc++.h>
using namespace std;

// Function that finds minimum number of
// colors required
void colorRequired(int arr[], int n)
{

    // To check that if all the elements
    // are same or not
    bool all_same = true;

    // To check if only one adjacent exist
    bool one_adjacent_same = false;

    // Traverse the array
    for (int i = 0; i < n - 1; i++) {

        // If adjacent elements found
        // different means all are not
        // same
        if (arr[i] != arr[i + 1]) {
            all_same = false;
        }

        // If two adjacent elements found
        // to be same then make
        // one_adjacent_same true
        if (arr[i] == arr[i + 1]) {
            one_adjacent_same = true;
        }
    }

    // If all elements are same
    // then print 1
    if (all_same == true) {
        cout << 1 << endl;
        return;
    }

    // If total number of elements are
    // even or there exist two adjacent
    // elements that are same
    // then print 2
    if (n % 2 == 0
        || one_adjacent_same == true) {
        cout << 2 << endl;
        return;
    }

    // Else 3 type of colors
    // are required
    cout << 3 << endl;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 1, 1, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    colorRequired(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;

class GFG{

// Function that finds minimum number of
// colors required
static void colorRequired(int arr[], int n)
{

    // To check that if all the elements
    // are same or not
    boolean all_same = true;

    // To check if only one adjacent exist
    boolean one_adjacent_same = false;

    // Traverse the array
    for(int i = 0; i < n - 1; i++)
    {

       // If adjacent elements found
       // different means all are not
       // same
       if (arr[i] != arr[i + 1])
       {
           all_same = false;
       }

       // If two adjacent elements found
       // to be same then make
       // one_adjacent_same true
       if (arr[i] == arr[i + 1])
       {
           one_adjacent_same = true;
       }
    }

    // If all elements are same
    // then print 1
    if (all_same == true)
    {
        System.out.print(1 + "\n");
        return;
    }

    // If total number of elements are
    // even or there exist two adjacent
    // elements that are same
    // then print 2
    if (n % 2 == 0 ||
        one_adjacent_same == true)
    {
        System.out.print(2 + "\n");
        return;
    }

    // Else 3 type of colors
    // are required
    System.out.print(3 + "\n");
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 1, 1, 2 };
    int n = arr.length;

    // Function call
    colorRequired(arr, n);
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function that finds minimum number
# of colors required
def colorRequired(arr, n):

    # To check that if all the elements
    # are same or not
    all_same = True

    # To check if only one adjacent exist
    one_adjacent_same = False

    # Traverse the array
    for i in range(n - 1):

        # If adjacent elements found
        # different means all are not
        # same
        if(arr[i] != arr[i + 1]):
            all_same = False

        # If two adjacent elements
        # found to be same then make
        # one_adjacent_same true
        if(arr[i] == arr[i + 1]):
            one_adjacent_same = True

    # If all elements are same
    # then print 1
    if(all_same == True):
        print(1)
        return

    # If total number of elements are
    # even or there exist two adjacent
    # elements that are same
    # then print 2
    if(n % 2 == 0 or one_adjacent_same == True):
        print(2)
        return

    # Else 3 type of colors
    # are required
    print(3)

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 1, 1, 2 ]
    n = len(arr)

    # Function call
    colorRequired(arr, n)

# This code is contributed by Shivam Singh
```

## C#

```
// C# implementation of above approach
using System;
class GFG{

// Function that finds minimum number of
// colors required
static void colorRequired(int []arr, int n)
{

    // To check that if all the elements
    // are same or not
    bool all_same = true;

    // To check if only one adjacent exist
    bool one_adjacent_same = false;

    // Traverse the array
    for(int i = 0; i < n - 1; i++)
    {

        // If adjacent elements found
        // different means all are not
        // same
        if (arr[i] != arr[i + 1])
        {
            all_same = false;
        }

        // If two adjacent elements found
        // to be same then make
        // one_adjacent_same true
        if (arr[i] == arr[i + 1])
        {
            one_adjacent_same = true;
        }
    }

    // If all elements are same
    // then print 1
    if (all_same == true)
    {
        Console.Write(1 + "\n");
        return;
    }

    // If total number of elements are
    // even or there exist two adjacent
    // elements that are same
    // then print 2
    if (n % 2 == 0 ||
        one_adjacent_same == true)
    {
        Console.Write(2 + "\n");
        return;
    }

    // Else 3 type of colors
    // are required
    Console.Write(3 + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 1, 1, 2 };
    int n = arr.Length;

    // Function call
    colorRequired(arr, n);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function that finds minimum number of
// colors required
function colorRequired(arr, n)
{

    // To check that if all the elements
    // are same or not
    var all_same = true;

    // To check if only one adjacent exist
    var one_adjacent_same = false;

    // Traverse the array
    for (var i = 0; i < n - 1; i++) {

        // If adjacent elements found
        // different means all are not
        // same
        if (arr[i] != arr[i + 1]) {
            all_same = false;
        }

        // If two adjacent elements found
        // to be same then make
        // one_adjacent_same true
        if (arr[i] == arr[i + 1]) {
            one_adjacent_same = true;
        }
    }

    // If all elements are same
    // then print 1
    if (all_same == true) {
        document.write( 1 + "<br>");
        return;
    }

    // If total number of elements are
    // even or there exist two adjacent
    // elements that are same
    // then print 2
    if (n % 2 == 0
        || one_adjacent_same == true)
   {
        document.write( 2 + "<br>");
        return;
    }

    // Else 3 type of colors
    // are required
    document.write( 3 + "<br>");
}

// Driver Code
var arr = [1, 2, 1, 1, 2 ];
var n = arr.length;

// Function call
colorRequired(arr, n);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N)* ，其中 N 为元素个数。