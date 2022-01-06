# 最大化子序列偶数和奇数索引元素之和之间的差值

> 原文:[https://www . geeksforgeeks . org/最大化子序列的偶数和奇数索引元素之和的差值/](https://www.geeksforgeeks.org/maximize-difference-between-sum-of-even-and-odd-indexed-elements-of-a-subsequence/)

给定一个由正整数 **N** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是从给定的数组中找出子序列的偶数和奇数索引元素之和之间的最大可能差。

**示例:**

> **输入:** arr[] = { 3，2，1，4，5，2，1，7，8，9 }
> **输出:** 15
> **解释:**
> 考虑数组中的子序列{ 3，1，5，1，9 }
> 偶数索引数组元素之和= 3 + 5 + 9 = 17
> 奇数索引数组元素之和= 1+1 = 2
> 因此，偶数索引数组元素之和之间的差
> 
> **输入:** arr[] = {1，2，3，4，5，6}
> **输出:** 6

**朴素方法:**解决这个问题最简单的方法是[生成给定数组的所有可能的子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)，对于每个子序列，计算子序列的偶数和奇数索引元素之和的差。最后，打印得到的最大差值。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**有效方法:**为了优化上述方法，想法是将[局部最大值](https://www.geeksforgeeks.org/find-indices-of-all-local-maxima-and-local-minima-in-an-array/)存储在子序列的偶数索引处，并将[局部最小值](https://www.geeksforgeeks.org/find-indices-of-all-local-maxima-and-local-minima-in-an-array/)存储在子序列的奇数索引处。最后，打印子序列的偶数和奇数索引之和的差值。
按照以下步骤解决问题:

*   初始化一个变量，比如 **maxDiff** ，以存储一个子序列的偶数和奇数索引元素之和之间的最大差值。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并检查**arr【I】>arr【I+1】**和**arr【I】<arr【I–1】**是否存在。如果发现为真，则更新 **maxDiff += arr[i]** 。
*   否则，检查 **arr[i] > arr[i + 1]** 和**arr[I]<arr[I–1]**是否存在。如果发现是真的，那么更新 **maxDiff -= arr[i]** 。
*   最后打印 **maxDiff** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum possible difference
// between sum of even and odd indices
int maxPossibleDiff(vector<int>& arr, int N)
{

    // Convert arr[] into 1-based indexing
    arr.push_back(-1);

    // Reverse the array
    reverse(arr.begin(), arr.end());

    // Convert arr[] into 1 based index
    arr.push_back(-1);

    // Reverse the array
    reverse(arr.begin(), arr.end());

    // Stores maximum difference between
    // sum of even and odd indexed elements
    int maxDiff = 0;

    // Traverse the array
    for (int i = 1; i <= N; i++) {

        // If arr[i] is local maxima
        if (arr[i] > arr[i - 1]
            && arr[i] > arr[i + 1]) {

            // Update maxDiff
            maxDiff += arr[i];
        }

        // If arr[i] is local minima
        if (arr[i] < arr[i - 1]
            && arr[i] < arr[i + 1]) {

            // Update maxDiff
            maxDiff -= arr[i];
        }
    }
    cout << maxDiff;
}

// Driver Code
int main()
{

    vector<int> arr = { 3, 2, 1, 4, 5,
                        2, 1, 7, 8, 9 };

    // Size of array
    int N = arr.size();

    // Function Call
    maxPossibleDiff(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find the maximum possible
// difference between sum of even and
// odd indices
static void maxPossibleDiff(Vector<Integer> arr, int N)
{

    // Convert arr[] into 1-based indexing
    arr.add(-1);

    // Reverse the array
    Collections.reverse(arr);

    // Convert arr[] into 1 based index
    arr.add(-1);

    // Reverse the array
    Collections.reverse(arr);

    // Stores maximum difference between
    // sum of even and odd indexed elements
    int maxDiff = 0;

    // Traverse the array
    for(int i = 1; i <= N; i++)
    {

        // If arr.get(i) is local maxima
        if (arr.get(i) > arr.get(i - 1) &&
            arr.get(i) > arr.get(i + 1))
        {

            // Update maxDiff
            maxDiff += arr.get(i);
        }

        // If arr.get(i) is local minima
        if (arr.get(i) < arr.get(i - 1) &&
            arr.get(i) < arr.get(i + 1))
        {

            // Update maxDiff
            maxDiff -= arr.get(i);
        }
    }
    System.out.print(maxDiff);
}

// Driver Code
public static void main(String[] args)
{
    int[] array = { 3, 2, 1, 4, 5,
                    2, 1, 7, 8, 9 };
    Vector<Integer> v = new Vector<>();
    for(int i :array)
    {
        v.add(i);
    }

    // Size of array
    int N = v.size();

    // Function Call
    maxPossibleDiff(v, N);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
#Python3 program to implement
#the above approach

#Function to find the maximum possible difference
#between sum of even and odd indices
def maxPossibleDiff(arr,  N):

    #Convert arr[] o 1-based indexing
    arr.append(-1)

    #Reverse the array
    arr = arr[::-1]

    #Convert arr[] o 1 based index
    arr.append(-1)

    #Reverse the array
    arr = arr[::-1]

    #Stores maximum difference between
    #sum of even and odd indexed elements
    maxDiff = 0

    #Traverse the array
    for i in range(1,N+1):

        #If arr[i] is local maxima
        if (arr[i] > arr[i - 1] and arr[i] > arr[i + 1]):

            #Update maxDiff
            maxDiff += arr[i]

        #If arr[i] is local minima
        if (arr[i] < arr[i - 1] and arr[i] < arr[i + 1]):

            #Update maxDiff
            maxDiff -= arr[i]
    print (maxDiff)

#Driver Code
if __name__ == '__main__':

    arr = [3, 2, 1, 4, 5, 2, 1, 7, 8, 9]

    #Size of array
    N = len(arr)

    #Function Call
    maxPossibleDiff(arr, N)
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

public class GFG{

// Function to find the maximum possible
// difference between sum of even and
// odd indices
static void maxPossibleDiff(List<int> arr, int N)
{

    // Convert []arr into 1-based indexing
    arr.Add(-1);

    // Reverse the array
    arr.Reverse();

    // Convert []arr into 1 based index
    arr.Add(-1);

    // Reverse the array
    arr.Reverse();

    // Stores maximum difference between
    // sum of even and odd indexed elements
    int maxDiff = 0;

    // Traverse the array
    for(int i = 1; i <= N; i++)
    {

        // If arr[i] is local maxima
        if (arr[i] > arr[i - 1] &&
            arr[i] > arr[i + 1])
        {

            // Update maxDiff
            maxDiff += arr[i];
        }

        // If arr[i] is local minima
        if (arr[i] < arr[i - 1] &&
            arr[i] < arr[i + 1])
        {

            // Update maxDiff
            maxDiff -= arr[i];
        }
    }
    Console.Write(maxDiff);
}

// Driver Code
public static void Main(String[] args)
{
    int[] array = { 3, 2, 1, 4, 5,
                    2, 1, 7, 8, 9 };
    List<int> v = new List<int>();
    foreach(int i in array)
    {
        v.Add(i);
    }

    // Size of array
    int N = v.Count;

    // Function Call
    maxPossibleDiff(v, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the maximum possible difference
// between sum of even and odd indices
function maxPossibleDiff(arr, N)
{

    // Convert arr[] into 1-based indexing
    arr.push(-1);

    // Reverse the array
    arr.reverse();

    // Convert arr[] into 1 based index
    arr.push(-1);

    // Reverse the array
    arr.reverse();

    // Stores maximum difference between
    // sum of even and odd indexed elements
    var maxDiff = 0;

    // Traverse the array
    for (var i = 1; i <= N; i++) {

        // If arr[i] is local maxima
        if (arr[i] > arr[i - 1]
            && arr[i] > arr[i + 1]) {

            // Update maxDiff
            maxDiff += arr[i];
        }

        // If arr[i] is local minima
        if (arr[i] < arr[i - 1]
            && arr[i] < arr[i + 1]) {

            // Update maxDiff
            maxDiff -= arr[i];
        }
    }
    document.write( maxDiff);
}

// Driver Code

var arr = [3, 2, 1, 4, 5,
                    2, 1, 7, 8, 9];

// Size of array
var N = arr.length;

// Function Call
maxPossibleDiff(arr, N);

</script>   
```

**Output:** 

```
15
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)