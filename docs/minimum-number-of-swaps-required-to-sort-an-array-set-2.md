# 对数组进行排序所需的最小交换次数|集合 2

> 原文:[https://www . geeksforgeeks . org/最小交换次数-需要对数组集进行排序-2/](https://www.geeksforgeeks.org/minimum-number-of-swaps-required-to-sort-an-array-set-2/)

给定一个由 N 个不同元素组成的数组，找到对数组进行排序所需的最小交换次数。

**注**:问题不是要求按照最少的交换次数对数组进行排序。问题是找到数组可以排序的最小交换。

**示例**:

```
Input: arr[] = {4, 3, 2, 1}
Output: 2
Explanation: Swap index 0 with 3 and 1 with
2 to get the sorted array {1, 2, 3, 4}.

Input: arr[] = { 3, 5, 2, 4, 6, 8}
Output: 3
Explanation: 
Swap 4 and 5 so array = 3, 4, 2, 5, 6, 8
Swap 2 and 3 so array = 2, 4, 3, 5, 6, 8
Swap 4 and 3 so array = 2, 3, 4, 5, 6, 8
So the array is sorted.
```

这个问题已经在[上一篇使用图](https://www.geeksforgeeks.org/minimum-number-swaps-required-sort-array/)讨论过了。本文讨论了另一种解决这个问题的方法，它与循环方法略有不同。

**方法:**
想法是在 C++ 中创建一个[对向量，第一个元素作为数组值，第二个元素作为数组索引。下一步是根据对的第一个元素对对的向量进行排序。之后遍历向量，检查用值映射的索引是否正确，如果不正确，则继续交换，直到元素被正确放置，并继续计算交换的次数。](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)

**算法:**

1.  创建一个成对的向量，遍历数组，对于数组的每个元素，在向量中插入一个元素索引对
2.  从开始到结束遍历向量(循环计数器为 I)。
3.  对于对中第二个元素(索引)不等于的每个元素，用向量的第二个元素(索引)交换向量的第 I 个元素
4.  如果第二个元素(索引)等于 I，则跳过循环的迭代。
5.  如果交换后第二个元素(索引)不等于 I，则递减 I。
6.  递增计数器。

**实施:**

## C++

```
// C++ program to find the minimum number
// of swaps required to sort an array
// of distinct element

#include<bits/stdc++.h>
using namespace std;

// Function to find minimum swaps to
// sort an array
int findMinSwap(int arr[] , int n)
{
    // Declare a vector of pair    
    vector<pair<int,int>> vec(n);

    for(int i=0;i<n;i++)
    {
        vec[i].first=arr[i];
        vec[i].second=i;
    }

    // Sort the vector w.r.t the first
    // element of pair
    sort(vec.begin(),vec.end());

    int ans=0,c=0,j;

    for(int i=0;i<n;i++)
    {  
        // If the element is already placed
        // correct, then continue
        if(vec[i].second==i)
            continue;
        else
        {
            // swap with its respective index
            swap(vec[i].first,vec[vec[i].second].first);
            swap(vec[i].second,vec[vec[i].second].second);
        }

        // swap until the correct
        // index matches
        if(i!=vec[i].second)
            --i;

        // each swap makes one element
        // move to its correct index,
        // so increment answer
        ans++;
    }

    return ans;
}

// Driver code
int main()
{
    int arr[] = {1, 5, 4, 3, 2};

    int n = sizeof(arr)/sizeof(arr[0]);

    cout<<findMinSwap(arr,n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum number 
// of swaps required to sort an array
// of distinct element
import java.util.*;
class GFG
{

static class Point implements Comparable<Point>
{

    public int x, y;   
    public Point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }

    public int compareTo(Point other)
    {
        return this.x - other.x;
    }
}   

// Function to find minimum swaps to 
// sort an array
static int findMinSwap(int[] arr, int n)
{

    // Declare a vector of pair  
    List<Point> vec = new ArrayList<Point>();

    for(int i = 0; i < n; i++)
    {
        vec.add(new Point(arr[i], i));
    }

    // Sort the vector w.r.t the first
    // element of pair
    Collections.sort(vec);  
    int ans = 0;
    for(int i = 0; i < n; i++)
    { 

        // If the element is already placed
        // correct, then continue
        if (vec.get(i).y == i) 
            continue;
        else
        {

            // Swap with its respective index 
            Point temp = vec.get(vec.get(i).y);
            vec.set(vec.get(i).y,vec.get(i));
            vec.set(i, temp);
        } 

        // Swap until the correct 
        // index matches
        if (i != vec.get(i).y)
            --i;

        // Each swap makes one element
        // move to its correct index, 
        // so increment answer
        ans++;
    }
    return ans;
}

// Driver Code
public static void main(String []args)
{
    int[] arr = { 1, 5, 4, 3, 2 };
    int n = arr.length;     
    System.out.println(findMinSwap(arr,n));
}
}

// This code is contributed by Pratham76
```

## 蟒蛇 3

```
# Python3 program to find the minimum number
# of swaps required to sort an array
# of distinct element

# Function to find minimum swaps to
# sort an array
def findMinSwap(arr, n):

    # Declare a vector of pair
    vec = []

    for i in range(n):
        vec.append([arr[i], i])

    # Sort the vector w.r.t the first
    # element of pair
    vec = sorted(vec)

    ans, c, j = -1, 0, 0

    for i in range(n):

        # If the element is already placed
        # correct, then continue
        if(vec[i][1] == i):
            continue
        else:
            # swap with its respective index
            vec[i][0], vec[vec[i][1]][1] = \
                vec[vec[i][1]][1], vec[i][0]
            vec[i][1], vec[vec[i][1]][1] = \
                vec[vec[i][1]][1], vec[i][1]

        # swap until the correct
        # index matches
        if(i != vec[i][1]):
            i -= 1

        # each swap makes one element
        # move to its correct index,
        # so increment answer
        ans += 1

    return ans

# Driver code
arr = [1, 5, 4, 3, 2]
n = len(arr)
print(findMinSwap(arr,n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find the minimum number 
// of swaps required to sort an array
// of distinct element
using System;
using System.Collections.Generic;

class GFG{

// Function to find minimum swaps to 
// sort an array
static int findMinSwap(int[] arr, int n)
{

    // Declare a vector of pair  
    List<Tuple<int,
               int>> vec = new List<Tuple<int,
                                          int>>();

    for(int i = 0; i < n; i++)
    {
        vec.Add(new Tuple<int, int>(arr[i], i));
    }

    // Sort the vector w.r.t the first
    // element of pair
    vec.Sort();

    int ans = 0;

    for(int i = 0; i < n; i++)
    { 

        // If the element is already placed
        // correct, then continue
        if (vec[i].Item2 == i) 
            continue;
        else
        {

            // Swap with its respective index 
            Tuple<int, int> temp = vec[vec[i].Item2];
            vec[vec[i].Item2] = vec[i];
            vec[i] = temp;
        } 

        // Swap until the correct 
        // index matches
        if (i != vec[i].Item2)
            --i;

        // Each swap makes one element
        // move to its correct index, 
        // so increment answer
        ans++;
    }
    return ans;
}

// Driver Code
static void Main()
{
    int[] arr = { 1, 5, 4, 3, 2 };
    int n = arr.Length;

    Console.Write(findMinSwap(arr,n));
}
}

// This code is contributed by divyeshrabadiya07
```

**Output:** 

```
2
```

**复杂度分析:**

*   **时间复杂度:** O(n Log n)。
    对数组进行排序所需的时间为 n log n
*   **辅助空间:** O(n)。
    创建一个额外的数组或向量。所以，空间复杂度是 O(n)