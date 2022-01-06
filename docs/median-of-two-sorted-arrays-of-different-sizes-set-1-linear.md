# 两个不同大小的排序数组的中值|集合 1(线性)

> 原文:[https://www . geeksforgeeks . org/不同大小排序数组的中位数-集合-1-linear/](https://www.geeksforgeeks.org/median-of-two-sorted-arrays-of-different-sizes-set-1-linear/)

这是两个大小相等的排序数组的中值问题的扩展。这里我们也处理大小不等的数组。

**例:**

```
Input: a[] = {1, 12, 15, 26, 38}
       b[] = {2, 13, 24}
Output: 14
Explanation:
After merging arrays the result is
1, 2, 12, 13, 15, 24, 26, 38
median = (13 + 15)/2 = 14.

Input: a[] = {1, 3, 5, 7}
       b[] = {2, 4, 6, 8}
Output: 5
Explanation : 
After merging arrays the result is
1, 2, 3, 4, 5, 6, 7, 8, 9
median = 5 
```

**方法:**

1.  The method discussed in this paper is similar to [equal-size median method 1](https://www.geeksforgeeks.org/median-of-two-sorted-arrays/) . Use [consolidation sorting](https://www.geeksforgeeks.org/merge-sort/) consolidation program.
2.  When comparing the elements of two arrays, keep a variable to track the count.
3.  Perform the merge of two sort arrays. When inserting a new element, increase the count value.
4.  The most effective way to merge two arrays is to compare the tops of two arrays, pop up smaller values and increase the count.
5.  Continue to compare the top/first element of two arrays until there are no remaining elements in any array.
6.  Now, in order to find the intermediate value, we need to deal with two situations.
    *   If the sum of the lengths of the array sizes is even, the elements are stored when the counts are values ((n1+n2)/2)-1 and (n1+n2)/2\. In the merged array, the elements are added and divided by 2 to return the median value.
    *   If the value (sum of sizes) is odd, the (n1+n2)/2nd element (when the count value is (N1+N2)/2) is returned as the median value.

## c++

```
// A C++ program to find median of two sorted arrays of
// unequal sizes
#include <bits/stdc++.h>
using namespace std;

// A utility function to find median of two integers
/* This function returns median of a[] and b[].
Assumptions in this function: Both a[] and b[]
are sorted arrays  */
float findmedian(int a[], int n1, int b[], int n2)
{
    int i = 0; /* Current index of
             i/p array a[] */
    int j = 0; /* Current index of
                  i/p array b[] */
    int k;
    int m1 = -1, m2 = -1;
    for (k = 0; k <= (n1 + n2) / 2; k++) {

        if (i < n1 && j < n2) {
            if (a[i] < b[j]) {
                m2 = m1;
                m1 = a[i];
                i++;
            }
            else {
                m2 = m1;
                m1 = b[j];
                j++;
            }
        }

        /* Below is to handle the case where
           all elements of a[] are
           smaller than smallest(or first)
           element of b[] or a[] is empty*/
        else if (i == n1) {
            m2 = m1;
            m1 = b[j];
            j++;
        }

        /* Below is to handle case where
           all elements of b[] are
           smaller than smallest(or first)
           element of a[] or b[] is empty*/
        else if (j == n2) {
            m2 = m1;
            m1 = a[i];
            i++;
        }
    }

    /*Below is to handle the case where
     sum of number of elements
     of the arrays is even */
    if ((n1 + n2) % 2 == 0)
        return (m1 + m2) * 1.0 / 2;

    /* Below is to handle the case where
       sum of number of elements
       of the arrays is odd */
    return m1;
}

// Driver program to test above functions
int main()
{
    int a[] = { 1, 12, 15, 26, 38 };
    int b[] = { 2, 13, 24 };

    int n1 = sizeof(a) / sizeof(a[0]);
    int n2 = sizeof(b) / sizeof(b[0]);

    printf("%f", findmedian(a, n1, b, n2));

    return 0;
}
```

## Java

```
// A Java program to find median of two sorted arrays of
// unequal sizes

import java.io.*;

class GFG {

    // A utility function to find median of two integers
    /* This function returns median of a[] and b[].
Assumptions in this function: Both a[] and b[]
are sorted arrays */
    static float findmedian(int a[], int n1, int b[], int n2)
    {
        int i = 0; /* Current index of
            i/p array a[] */
        int j = 0; /* Current index of
                i/p array b[] */
        int k;
        int m1 = -1, m2 = -1;
        for (k = 0; k <= (n1 + n2) / 2; k++) {

            if (i < n1 && j < n2) {
                if (a[i] < b[j]) {
                    m2 = m1;
                    m1 = a[i];
                    i++;
                }
                else {
                    m2 = m1;
                    m1 = b[j];
                    j++;
                }
            }

            /* Below is to handle the case where
        all elements of a[] are
        smaller than smallest(or first)
        element of b[] or a[] is empty*/
            else if (i == n1) {
                m2 = m1;
                m1 = b[j];
                j++;
            }

            /* Below is to handle case where
        all elements of b[] are
        smaller than smallest(or first)
        element of a[] or b[] is empty*/
            else if (j == n2) {
                m2 = m1;
                m1 = a[i];
                i++;
            }
        }

        /*Below is to handle the case where
    sum of number of elements
    of the arrays is even */
        if ((n1 + n2) % 2 == 0) {
            return (m1 + m2) * (float)1.0 / 2;
        }
        /* Below is to handle the case where
    sum of number of elements
    of the arrays is odd */
        return m1;
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {
        int a[] = { 1, 12, 15, 26, 38 };
        int b[] = { 2, 13, 24 };

        int n1 = a.length;
        int n2 = b.length;

        System.out.println(findmedian(a, n1, b, n2));
    }
}

// This code has been contributed by inder_verma.
```

## python 3

```
# Python3 program to find median of
# two sorted arrays of unequal sizes

# A utility function to find median
# of two integers
''' This function returns median of
a[] and b[]. Assumptions in this
function: Both a[] and b[] are sorted
arrays '''

def findmedian(a, n1, b, n2):

    i = 0 # Current index of i / p array a[]
    j = 0 # Current index of i / p array b[]

    m1 = -1
    m2 = -1
    for k in range(((n1 + n2) // 2) + 1) :

        if (i < n1 and j < n2) :
            if (a[i] < b[j]) :
                m2 = m1
                m1 = a[i]
                i += 1

            else :
                m2 = m1
                m1 = b[j]
                j += 1

        # Below is to handle the case where
        # all elements of a[] are
        # smaller than smallest(or first)
        # element of b[] or a[] is empty

        elif(i == n1) :
            m2 = m1
            m1 = b[j]
            j += 1

        # Below is to handle case where
        # all elements of b[] are
        # smaller than smallest(or first)
        # element of a[] or b[] is empty
        elif (j == n2) :
            m2 = m1
            m1 = a[i]
            i += 1

    '''Below is to handle the case
    where sum of number of elements
    of the arrays is even '''
    if ((n1 + n2) % 2 == 0):
        return (m1 + m2) * 1.0 / 2

    ''' Below is to handle the case
    where sum of number of elements
    of the arrays is odd '''
    return m1

# Driver Code
if __name__ == "__main__":

    a = [ 1, 12, 15, 26, 38 ]
    b = [ 2, 13, 24 ]

    n1 = len(a)
    n2 = len(b)

    print(findmedian(a, n1, b, n2))

# This code is contributed
# by ChitraNayal
```

## c#

T3

## PHP

T4

## Javascript

```
<script>

// A Javascript program to find median
// of two sorted arrays of unequal sizes

// A utility function to find median of two integers
// This function returns median of a[] and b[].
// Assumptions in this function: Both a[] and b[]
// are sorted arrays
function findmedian(a, n1, b, n2)
{
    let i = 0; /* Current index of
                  i/p array a[] */
    let j = 0; /* Current index of
                  i/p array b[] */
    let k;
    let m1 = -1, m2 = -1;

    for(k = 0; k <= (n1 + n2) / 2; k++)
    {
        if (i < n1 && j < n2)
        {
            if (a[i] < b[j])
            {
                m2 = m1;
                m1 = a[i];
                i++;
            }
            else
            {
                m2 = m1;
                m1 = b[j];
                j++;
            }
        }

        /* Below is to handle the case where
        all elements of a[] are
        smaller than smallest(or first)
        element of b[] or a[] is empty*/
        else if (i == n1)
        {
            m2 = m1;
            m1 = b[j];
            j++;
        }

        /* Below is to handle case where
        all elements of b[] are
        smaller than smallest(or first)
        element of a[] or b[] is empty*/
        else if (j == n2)
        {
            m2 = m1;
            m1 = a[i];
            i++;
        }
    }

    /*Below is to handle the case where
    sum of number of elements
    of the arrays is even */
    if ((n1 + n2) % 2 == 0)
    {
        return (m1 + m2) * 1.0 / 2;
    }

    /* Below is to handle the case where
    sum of number of elements
    of the arrays is odd */
    return m1;
}

// Driver code
let a = [ 1, 12, 15, 26, 38 ];
let b = [ 2, 13, 24 ];
let n1 = a.length;
let n2 = b.length;

document.write(findmedian(a, n1, b, n2));

// This code is contributed by rag2127

</script>
```

```
14.000000
```