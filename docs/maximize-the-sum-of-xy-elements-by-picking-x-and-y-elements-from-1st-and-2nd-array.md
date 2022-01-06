# 通过从第一个和第二个数组中拾取 X 和 Y 元素来最大化 X+Y 元素的总和

> 原文:[https://www . geeksforgeeks . org/通过从第一个和第二个数组中选取 x 和 y 元素来最大化 xy 元素的总和/](https://www.geeksforgeeks.org/maximize-the-sum-of-xy-elements-by-picking-x-and-y-elements-from-1st-and-2nd-array/)

给定两个大小为 N 的数组以及两个数字 X 和 Y，任务是通过考虑以下几点来最大化总和:

*   从第一个数组中选择 **x** 值，从第二个数组中选择 **y** 值，使 X+Y 值的总和最大。
*   给出 X + Y 等于 n。

**示例:**

> **输入:** arr1[] = {1，4，1}，arr2[] = {2，5，3}，N = 3，X = 2，Y = 1
> **输出:** 8
> 为了最大化两个数组的和，
> 从第一个数组中选取第一个和第二个元素，从第二个数组中选取第三个元素。
> 
> **输入:** A[] = {1，4，1，2}，B[] = {4，3，2，5}，N = 4，X = 2，Y = 2
> **输出:** 14

**方法:**可以使用贪婪的方法来解决上述问题。以下是所需的步骤:

*   通过找出两个数组元素之间的最大差异，首先找出数组中具有最大值的元素。
*   为此，找出第一个数组和第二个数组的值之间的绝对差值，然后将其存储在另一个数组中。
*   按降序对该数组进行排序。
*   排序时，跟踪数组中元素的原始位置。
*   现在比较两个数组的元素，并将较大的值添加到 maxAmount 中。
*   如果两者具有相同的值，如果 X 不为零，则添加第一个数组的元素，否则添加第二个数组的元素。
*   遍历完数组后，返回计算出的最大数量。

下面是上述方法的实现:

## C++

```
// C++ program to print the maximum
// possible sum from two arrays.
#include <bits/stdc++.h>
using namespace std;

// class that store values of two arrays
// and also store their absolute difference
class triplet {
public:
    int first;
    int second;
    int diff;
    triplet(int f, int s, int d)
        : first(f), second(s), diff(d)
    {
    }
};

// Compare function used to sort array in decreasing order
bool compare(triplet& a, triplet& b)
{
    return a.diff > b.diff; // decreasing order
}

/// Function to find the maximum possible
/// sum that can be generated from 2 arrays
int findMaxAmount(int arr1[], int arr2[], int n, int x, int y)
{
    // vector where each index stores 3 things:
    // Value of 1st array
    // Value of 2nd array
    // Their absolute difference
    vector<triplet> v;

    for (int i = 0; i < n; i++) {
        triplet t(arr1[i], arr2[i], abs(arr1[i] - arr2[i]));
        v.push_back(t);
    }

    // sort according to their absolute difference
    sort(v.begin(), v.end(), compare);

    // it will store maximum sum
    int maxAmount = 0;

    int i = 0;

    // Run loop for N times or
    // value of X or Y becomes zero
    while (i < n && x > 0 && y > 0) {

        // if 1st array element has greater
        // value, add it to maxAmount
        if (v[i].first > v[i].second) {
            maxAmount += v[i].first;
            x--;
        }

        // if 2nd array element has greater
        // value, add it to maxAmount
        if (v[i].first < v[i].second) {
            maxAmount += v[i].second;
            y--;
        }

        // if both have same value, add element
        // of first array if X is not zero
        // else add element of second array
        if (v[i].first == v[i].second) {
            if (x > 0) {
                maxAmount += v[i].first;
                x--;
            }
            else if (y > 0) {
                maxAmount += v[i].second;
                y--;
            }
        }

        // increment after picking element
        i++;
    }

    // add the remaining values
    // of first array to maxAmount
    while (i < v.size() && x--) {
        maxAmount += v[i++].first;
    }

    // add the remaining values of
    // second array to maxAmount
    while (i < v.size() && y--) {
        maxAmount += v[i++].second;
    }

    return maxAmount;
}

// Driver Code
int main()
{
    int A[] = { 1, 4, 1, 2 };
    int B[] = { 4, 3, 2, 5 };
    int n = sizeof(A) / sizeof(A[0]);

    int X = 2, Y = 2;

    cout << findMaxAmount(A, B, n, X, Y) << "\n";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the maximum
// possible sum from two arrays.
import java.util.*;

// class that store values of two arrays
// and also store their absolute difference
class Triplet implements Comparable<Triplet>
{
    int first;
    int second;
    int diff;

    Triplet(int f, int s, int d)
    {
        first = f;
        second = s;
        diff = d;
    }

    // CompareTo function used to sort
    // array in decreasing order
    public int compareTo(Triplet o)
    {
        return o.diff - this.diff;
    }
}
class GFG{

// Function to find the maximum possible
// sum that can be generated from 2 arrays
public static int findMaxAmount(int arr1[],
                                int arr2[],
                                int n, int x,
                                int y)
{

    // Vector where each index
    // stores 3 things:
    // Value of 1st array
    // Value of 2nd array
    // Their absolute difference
    Vector<Triplet> v = new Vector<>();

    for(int i = 0; i < n; i++)
    {
       v.add(new Triplet(arr1[i], arr2[i],
                         Math.abs(arr1[i] -
                                  arr2[i])));
    }

    // Sort according to their
    // absolute difference
    Collections.sort(v);

    // It will store maximum sum
    int maxAmount = 0;

    int i = 0;

    // Run loop for N times or
    // value of X or Y becomes zero
    while (i < n && x > 0 && y > 0)
    {

        // If 1st array element has greater
        // value, add it to maxAmount
        if (v.get(i).first > v.get(i).second)
        {
            maxAmount += v.get(i).first;
            x--;
        }

        // If 2nd array element has greater
        // value, add it to maxAmount
        if (v.get(i).first < v.get(i).second)
        {
            maxAmount += v.get(i).second;
            y--;
        }

        // If both have same value, add element
        // of first array if X is not zero
        // else add element of second array
        if (v.get(i).first == v.get(i).second)
        {
            if (x > 0)
            {
                maxAmount += v.get(i).first;
                x--;
            }
            else if (y > 0)
            {
                maxAmount += v.get(i).second;
                y--;
            }
        }

        // Increment after picking element
        i++;
    }

    // Add the remaining values
    // of first array to maxAmount
    while (i < v.size() && x-- > 0)
    {
        maxAmount += v.get(i++).first;
    }

    // Add the remaining values of
    // second array to maxAmount
    while (i < v.size() && y-- > 0)
    {
        maxAmount += v.get(i++).second;
    }

    return maxAmount;
}

// Driver Code
public static void main(String []args)
{
    int A[] = { 1, 4, 1, 2 };
    int B[] = { 4, 3, 2, 5 };
    int n = A.length;

    int X = 2, Y = 2;

    System.out.println(findMaxAmount(A, B, n, X, Y));
}
}

// This code is contributed by jrishabh99
```

## 蟒蛇 3

```
# Python3 program to print the maximum
# possible sum from two arrays.

# Class that store values of two arrays
# and also store their absolute difference
class triplet:

    def __init__(self, f, s, d):
        self.first = f
        self.second = s
        self.diff = d

# Function to find the maximum possible
# sum that can be generated from 2 arrays
def findMaxAmount(arr1, arr2, n, x, y):

    # vector where each index stores 3 things:
    # Value of 1st array
    # Value of 2nd array
    # Their absolute difference
    v = []

    for i in range(0, n):
        t = triplet(arr1[i], arr2[i],
                abs(arr1[i] - arr2[i]))
        v.append(t)

    # sort according to their absolute difference
    v.sort(key = lambda x: x.diff, reverse = True)

    # it will store maximum sum
    maxAmount, i = 0, 0

    # Run loop for N times or
    # value of X or Y becomes zero
    while i < n and x > 0 and y > 0:

        # if 1st array element has greater
        # value, add it to maxAmount
        if v[i].first > v[i].second:
            maxAmount += v[i].first
            x -= 1

        # if 2nd array element has greater
        # value, add it to maxAmount
        if v[i].first < v[i].second:
            maxAmount += v[i].second
            y -= 1

        # if both have same value, add element
        # of first array if X is not zero
        # else add element of second array
        if v[i].first == v[i].second:
            if x > 0:
                maxAmount += v[i].first
                x -= 1

            elif y > 0:
                maxAmount += v[i].second
                y -= 1

        # increment after picking element
        i += 1

    # add the remaining values
    # of first array to maxAmount
    while i < len(v) and x > 0:
        maxAmount += v[i].first
        i, x = i + 1, x - 1

    # add the remaining values of
    # second array to maxAmount
    while i < len(v) and y > 0:
        maxAmount += v[i].second
        i, y = i + 1, y - 1

    return maxAmount

# Driver Code
if __name__ == "__main__":

    A = [1, 4, 1, 2]
    B = [4, 3, 2, 5]
    n = len(A)

    X, Y = 2, 2

    print(findMaxAmount(A, B, n, X, Y))

# This code is contributed by Rituraj Jain
```

**Output:** 

```
14
```

**时间复杂度:**O(N log N)
T3】辅助空间: O(N)