# 按顺序从两个数组中选取元素的最大和

> 原文:[https://www . geeksforgeeks . org/按顺序从两个数组中选取元素的最大总和/](https://www.geeksforgeeks.org/maximum-sum-by-picking-elements-from-two-arrays-in-order/)

给定两个大小为 **N** 的数组和两个表示元素最大数量的整数 **X** 和 **Y** ，可以分别从数组 **A** 和数组 **B** 中进行选择。
每次 **i <sup>th</sup>** 转弯时，可以选择**A【I】**或**B【I】**。任务是做出导致最大可能总和的选择。
**注:**保证 **(X + Y) ≥ N** 。
**举例:**

> **输入:** A[] = {1，2，3，4，5}，B[] = {5，4，3，2，1}，X = 3， Y = 2
> **输出:** 21
> i = 0 - > 5 采摘
> i = 1 - > 4 采摘
> i = 2 - > 3 采摘
> i = 3 - > 4 采摘
> i = 4 - > 5 采摘
> 5 + 4 + 3 + 4 + 5 = 21
> **输入:** A[] = {1，4，3，2，7，5

**方法:**使用贪婪方法选择将导致最大和的元素。以下步骤将有助于解决这个问题:

*   根据绝对差对元素对进行排序，即**| A[I]–B[I]|**按降序排列。
*   比较 **A[i]** 和 **B[i]** 值，较大的一个将该值加到**和**中。
*   如果元素是从**A【I】**中选择的，则将 **X** 减 1，否则将 **Y** 减 1。
*   最后打印**和**。

以下是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate the
// maximum sum obtained by making an
// Optimal selection of elements from two given arrays

import java.io.*;
import java.util.*;
import java.lang.*;

// User defined Pair class
class Pair {
    int x;
    int y;

    // Constructor
    public Pair(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
}

// Class to define user defined comparator
class Compare {

    // Function to reverse the elements of an array
    static void reverseArray(Pair[] arr, int start, int end)
    {

        int tempx, tempy;
        while (start < end) {
            tempx = arr[start].x;
            tempy = arr[start].y;
            arr[start].x = arr[end].x;
            arr[start].y = arr[end].y;
            arr[end].x = tempx;
            arr[end].y = tempy;
            start++;
            end--;
        }
    }

    // Function to sort the pair according to the
    // absolute differences
    static Pair[] compare(Pair[] arr, int N)
    {

        // Comparator to sort the pair according to
        // the absolute differences
        Arrays.sort(arr, new Comparator<Pair>() {
            @Override
            public int compare(Pair p1, Pair p2)
            {
                return (Math.abs(p1.x - p1.y) - Math.abs(p2.x - p2.y));
            }
        });

        // To get in descending order
        reverseArray(arr, 0, N - 1);
        return arr;
    }
}

// Driver class
class GFG {

    // Function to calculate the
    // maximum possible sum obtained by making an
    // optimal selection elements from two given arrays

    static int getMaximumSum(int[] A, int[] B, int N,
                                        int X, int Y)
    {
        int num1, num2, sum = 0;

        // Making a single pair array having
        // arr[i] element as (Ai, Bi)
        Pair[] arr = new Pair[N];
        for (int i = 0; i < N; i++) {
            arr[i] = new Pair(A[i], B[i]);
        }

        // Sorting according to the absolute differences
        // in the decreasing order
        Compare obj = new Compare();
        obj.compare(arr, N);

        // Applying Greedy approach to make an optimal
        // selection
        for (int i = 0; i < N; i++) {
            num1 = arr[i].x;
            num2 = arr[i].y;

            // If A[i] > B[i]
            if (num1 > num2) {

                // If element from A can be picked
                if (X > 0) {
                    sum += num1;
                    X--;
                }

                // Insufficient X
                // Make a pick from B
                else if (Y > 0) {
                    sum += num2;
                    Y--;
                }
            }

            // If B[i] > A[i]
            else if (num2 > num1 && Y > 0) {

                // If element from B can be picked
                if (Y > 0) {
                    sum += num2;
                    Y--;
                }

                // Insufficient Y
                // Make a pick from A
                else {
                    sum += num1;
                    X--;
                }
            }

            // If A[i] = B[i]
            // Doesn't make a difference so any value
            //  can be picked
            else {
                sum += num1;
                if (X > 0) {
                    X--;
                }
                else if (Y > 0)
                    Y--;
            }
        }
        return sum;
    }

    // Driver code
    public static void main(String args[])
    {
        int X = 3, Y = 2;
        int[] A = { 1, 2, 3, 4, 5 };
        int[] B = { 5, 4, 3, 2, 1 };
        int N = A.length;
        System.out.println(getMaximumSum(A, B, N, X, Y));
    }
}
```

## C++

```
#include <bits/stdc++.h>
using namespace std;
long long getMaximumSum(vector<int> a, vector<int>b, int n, int x, int y) {
        vector<vector<int> > v;
        long long tsum=0;
        for(int i=0;i<n;i++)
        {
            v.push_back({abs(a[i]-b[i]),a[i],b[i]});
        }
        sort(v.begin(),v.end(),greater<vector<int> >());
        for(int i=0;i<v.size();i++)
        {
            if(v[i][1]>v[i][2] && x>0)
            {
                tsum+=v[i][1];
                x--;
            }
            else if(v[i][1]<v[i][2] && y>0)
            {
                tsum+=v[i][2];
                y--;
            }
            else
            {
                tsum+=min(v[i][2],v[i][1]);  
            }
        }
        return tsum;
}
int main() {
    int x = 3, y = 2;
    vector<int> a= { 1, 2, 3, 4, 5 };
    vector<int> b= { 5, 4, 3, 2, 1 };
    int n = a.size();
    cout<<getMaximumSum(a, b, n, x, y);
    return 0;
}
```

**Output:** 

```
21
```