# 找出从数组中删除元素可以得到的最大点数

> 原文:[https://www . geesforgeks . org/find-通过从数组中删除元素可以获得的最大点数/](https://www.geeksforgeeks.org/find-maximum-points-which-can-be-obtained-by-deleting-elements-from-array/)

给定一个数组 **A** ，该数组具有 **N** 元素和两个整数 L 和 R，其中，![1\leq a_{x} \leq 10^{5}  ](img/564860d9f2b7eb62ba2e028c3fc87618.png "Rendered by QuickLaTeX.com")和![1\leq L \leq R \leq N  ](img/6de48463009149c05eb1e7f30309016b.png "Rendered by QuickLaTeX.com")。你可以选择数组的任意元素(比如说 **a <sub> x </sub>** )并删除它，还可以删除所有等于 **a <sub> x </sub> +1** ，**a<sub>x</sub>+2**……**a<sub>x</sub>+R**和 **a <sub> x </sub> -1** ，**这一步将花费**一<sub>x</sub>T37】点。任务是在从数组中删除所有元素后最大化总成本。
**举例:****** 

```
Input : 2 1 2 3 2 2 1
        L = 1, R = 1
Output : 8
We select 2 to delete, then (2-1)=1 and (2+1)=3 will need to be deleted, 
for given L and R range respectively.
Repeat this until 2 is completely removed. So, total cost = 2*4 = 8.

Input : 2 4 2 9 5
        L = 1, R = 2
Output : 18
We select 2 to delete, then 5 and then 9.
So total cost = 2*2 + 5 + 9 = 18.
```

**逼近:**我们会找到所有元素的计数。现在假设选择了一个元素 X，那么[X-L，X+R]范围内的所有元素都将被删除。现在，我们从 L 和 R 中选择最小范围，并找到当选择元素 X 时最多要删除哪些元素。我们的结果将是以前删除的元素的最大值，并且当元素 X 被删除时。我们将使用动态编程来存储之前删除的元素的结果，并进一步使用它。

## C++

```
// C++ program to find maximum cost after
// deleting all the elements form the array
#include <bits/stdc++.h>
using namespace std;

// function to return maximum cost obtained
int maxCost(int a[], int n, int l, int r)
{

    int mx = 0, k;
    // find maximum element of the array.
    for (int i = 0; i < n; ++i)
        mx = max(mx, a[i]);

    // initialize count of all elements to zero.
    int count[mx + 1];
    memset(count, 0, sizeof(count));

    // calculate frequency of all elements of array.
    for (int i = 0; i < n; i++)
        count[a[i]]++;

    // stores cost of deleted elements.
    int res[mx + 1];
    res[0] = 0;

    // selecting minimum range from L and R.
    l = min(l, r);

    for (int num = 1; num <= mx; num++) {

        // finds upto which elements are to be
        // deleted when element num is selected.
        k = max(num - l - 1, 0);

        // get maximum when selecting element num or not.
        res[num] = max(res[num - 1], num * count[num] + res[k]);
    }

    return res[mx];
}

// Driver program
int main()
{
    int a[] = { 2, 1, 2, 3, 2, 2, 1 }, l = 1, r = 1;

    // size of array
    int n = sizeof(a) / sizeof(a[0]);

    // function call to find maximum cost
    cout << maxCost(a, n, l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to find maximum cost after
//deleting all the elements form the array

public class GFG {

    //function to return maximum cost obtained
    static int maxCost(int a[], int n, int l, int r)
    {

     int mx = 0, k;
     // find maximum element of the array.
     for (int i = 0; i < n; ++i)
         mx = Math.max(mx, a[i]);

     // initialize count of all elements to zero.
     int[] count = new int[mx + 1];
     for(int i = 0; i < count.length; i++)
         count[i] = 0;

     // calculate frequency of all elements of array.
     for (int i = 0; i < n; i++)
         count[a[i]]++;

     // stores cost of deleted elements.
     int[] res = new int[mx + 1];
     res[0] = 0;

     // selecting minimum range from L and R.
     l = Math.min(l, r);

     for (int num = 1; num <= mx; num++) {

         // finds upto which elements are to be
         // deleted when element num is selected.
         k = Math.max(num - l - 1, 0);

         // get maximum when selecting element num or not.
         res[num] = Math.max(res[num - 1], num * count[num] + res[k]);
     }

     return res[mx];
    }

    //Driver program
    public static void main(String[] args) {

        int a[] = { 2, 1, 2, 3, 2, 2, 1 }, l = 1, r = 1;

         // size of array
         int n = a.length;

         // function call to find maximum cost
         System.out.println(maxCost(a, n, l, r));
    }
}
```

## 蟒蛇 3

```
# Python 3 Program to find maximum cost after
# deleting all the elements form the array

# function to return maximum cost obtained
def maxCost(a, n, l, r) :

    mx = 0

    # find maximum element of the array.
    for i in range(n) :
        mx = max(mx, a[i])

    # create and initialize count of all elements to zero.
    count = [0] * (mx + 1)

    # calculate frequency of all elements of array.
    for i in range(n) :
        count[a[i]] += 1

    # stores cost of deleted elements.
    res = [0] * (mx + 1)
    res[0] = 0

    # selecting minimum range from L and R.
    l = min(l, r)

    for num in range(1, mx + 1) :

        # finds upto which elements are to be
        # deleted when element num is selected.
        k = max(num - l - 1, 0)

        # get maximum when selecting element num or not.
        res[num] = max(res[num - 1], num * count[num] + res[k])

    return res[mx]

# Driver code
if __name__ == "__main__" :

    a = [2, 1, 2, 3, 2, 2, 1 ]
    l, r = 1, 1

    # size of array
    n =  len(a)

    # function call to find maximum cost
    print(maxCost(a, n, l, r))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to find maximum cost
// after deleting all the elements
// form the array
using System;

class GFG
{

// function to return maximum
// cost obtained
static int maxCost(int []a, int n,
                   int l, int r)
{
    int mx = 0, k;

    // find maximum element
    // of the array.
    for (int i = 0; i < n; ++i)
        mx = Math.Max(mx, a[i]);

    // initialize count of all
    // elements to zero.
    int[] count = new int[mx + 1];
    for(int i = 0; i < count.Length; i++)
        count[i] = 0;

    // calculate frequency of all
    // elements of array.
    for (int i = 0; i < n; i++)
        count[a[i]]++;

    // stores cost of deleted elements.
    int[] res = new int[mx + 1];
    res[0] = 0;

    // selecting minimum range
    // from L and R.
    l = Math.Min(l, r);

    for (int num = 1; num <= mx; num++)
    {

        // finds upto which elements
        // are to be deleted when
        // element num is selected.
        k = Math.Max(num - l - 1, 0);

        // get maximum when selecting
        // element num or not.
        res[num] = Math.Max(res[num - 1], num *
                          count[num] + res[k]);
    }

return res[mx];
}

// Driver Code
public static void Main()
{
    int []a = { 2, 1, 2, 3, 2, 2, 1 };
    int l = 1, r = 1;

    // size of array
    int n = a.Length;

    // function call to find maximum cost
    Console.WriteLine(maxCost(a, n, l, r));
}
}

// This code is contributed
// by inder_verma
```

## java 描述语言

```
<script>

// Javascript program to find maximum cost after
// deleting all the elements form the array

// function to return maximum cost obtained
function maxCost(a, n, l, r)
{

    var mx = 0, k;
    // find maximum element of the array.
    for (var i = 0; i < n; ++i)
        mx = Math.max(mx, a[i]);

    // initialize count of all elements to zero.
    var count = new Array(mx + 1);
    count.fill(0);

    // calculate frequency of all elements of array.
    for (var i = 0; i < n; i++)
        count[a[i]]++;

    // stores cost of deleted elements.
    var res = new Array(mx + 1);
    res[0] = 0;

    // selecting minimum range from L and R.
    l = Math.min(l, r);

    for (var num = 1; num <= mx; num++) {

        // finds upto which elements are to be
        // deleted when element num is selected.
        k = Math.max(num - l - 1, 0);

        // get maximum when selecting element num or not.
        res[num] = Math.max(res[num - 1],
        num * count[num] + res[k]);
    }

    return res[mx];
}

var a = [ 2, 1, 2, 3, 2, 2, 1 ];
var l = 1, r = 1;
// size of array
var n = a.length;

// function call to find maximum cost
document.write(maxCost(a, n, l, r));

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
8
```

**时间复杂度:** O(max(A))