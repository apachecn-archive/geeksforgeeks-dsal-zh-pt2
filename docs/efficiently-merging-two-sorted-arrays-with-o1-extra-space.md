# 用 O(1)个额外空间高效合并两个排序数组

> 原文:[https://www . geesforgeks . org/efficient-merging-two-sorted-array-with-O1-extra-space/](https://www.geeksforgeeks.org/efficiently-merging-two-sorted-arrays-with-o1-extra-space/)

给定两个排序后的数组，我们需要在 O((n+m)*log(n+m))的时间内用 O(1)的额外空间将它们合并成一个排序后的数组，此时 n 是第一个数组的大小，m 是第二个数组的大小。

**示例:**

```
Input: ar1[] = {10};
       ar2[] = {2, 3};
Output: ar1[] = {2}
        ar2[] = {3, 10}  

Input: ar1[] = {1, 5, 9, 10, 15, 20};
       ar2[] = {2, 3, 8, 13};
Output: ar1[] = {1, 2, 3, 5, 8, 9}
        ar2[] = {10, 13, 15, 20}
```

**我们在下面的帖子中讨论了一个二次时间解。**

在[这篇](https://www.geeksforgeeks.org/merge-two-sorted-arrays-o1-extra-space/)的帖子中，讨论了一个更好的解决方案。
想法:我们开始比较彼此远离而不是相邻的元素。
对于每次通过，我们计算间隙，并比较间隙右侧的元素。每通过一次，差距缩小到除以 2 的上限。

**示例:**

```
First example: 
a1[] = {3 27 38 43}, 
a2[] = {9 10 82}
Start with 
gap =  ceiling of n/2 = 4 
[This gap is for whole merged array]
3 27 38 43   9 10 82 
3 27 38 43   9 10 82
3 10 38 43   9 27 82

gap = 2:
3 10 38 43   9 27 82
3 10 38 43   9 27 82
3 10 38 43   9 27 82 
3 10 9 43   38 27 82
3 10 9 27   38 43 82

gap = 1:
3 10 9 27   38 43 82
3 10 9 27   38 43 82
3 9 10 27   38 43 82
3 9 10 27   38 43 82
3 9 10 27   38 43 82
3 9 10 27   38 43 82
Output : 3 9 10 27 38 43 82

Second Example: 
a1[] = {10 27 38 43 82}, 
a2[] = {3 9}
Start with gap = ceiling of n/2 (4):
10 27 38 43 82   3 9 
10 27 38 43 82   3 9
10 3 38 43 82   27 9
10 3 9 43 82   27 38

gap = 2:
10 3 9 43 82   27 38
9 3 10 43 82   27 38
9 3 10 43 82   27 38
9 3 10 43 82   27 38
9 3 10 27 82   43 38
9 3 10 27 38   43 82

gap = 1
9 3 10 27 38   43 82
3 9 10 27 38   43 82
3 9 10 27 38   43 82
3 9 10 27 38   43 82
3 9 10 27 38   43 82
3 9 10 27 38   43 82

Output : 3 9 10 27 38   43 82
```

下面是上述想法的实现:

## C++

```
// Merging two sorted arrays with O(1)
// extra space
#include <bits/stdc++.h>
using namespace std;

// Function to find next gap.
int nextGap(int gap)
{
    if (gap <= 1)
        return 0;
    return (gap / 2) + (gap % 2);
}

void merge(int* arr1, int* arr2, int n, int m)
{
    int i, j, gap = n + m;
    for (gap = nextGap(gap);
         gap > 0; gap = nextGap(gap))
    {
        // comparing elements in the first array.
        for (i = 0; i + gap < n; i++)
            if (arr1[i] > arr1[i + gap])
                swap(arr1[i], arr1[i + gap]);

        // comparing elements in both arrays.
        for (j = gap > n ? gap - n : 0;
             i < n && j < m;
             i++, j++)
            if (arr1[i] > arr2[j])
                swap(arr1[i], arr2[j]);

        if (j < m) {
            // comparing elements in the second array.
            for (j = 0; j + gap < m; j++)
                if (arr2[j] > arr2[j + gap])
                    swap(arr2[j], arr2[j + gap]);
        }
    }
}

// Driver code
int main()
{
    int a1[] = { 10, 27, 38, 43, 82 };
    int a2[] = { 3, 9 };
    int n = sizeof(a1) / sizeof(int);
    int m = sizeof(a2) / sizeof(int);

    // Function Call
    merge(a1, a2, n, m);

    printf("First Array: ");
    for (int i = 0; i < n; i++)
        printf("%d ", a1[i]);

    printf("\nSecond Array: ");
    for (int i = 0; i < m; i++)
        printf("%d ", a2[i]);
    printf("\n");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Merging two sorted arrays
// with O(1) extra space

public class MergeTwoSortedArrays {

    // Function to find next gap.
    private static int nextGap(int gap)
    {
        if (gap <= 1)
            return 0;
        return (gap / 2) + (gap % 2);
    }

    private static void merge(int[] arr1,
                              int[] arr2, int n,
                              int m)
    {
        int i, j, gap = n + m;
        for (gap = nextGap(gap); gap > 0;
             gap = nextGap(gap))
        {
            // comparing elements in the first
            // array.
            for (i = 0; i + gap < n; i++)
                if (arr1[i] > arr1[i + gap])
                {
                    int temp = arr1[i];
                    arr1[i] = arr1[i + gap];
                    arr1[i + gap] = temp;
                }

            // comparing elements in both arrays.
            for (j = gap > n ? gap - n : 0;
                 i < n && j < m;
                 i++, j++)
                if (arr1[i] > arr2[j])
                {
                    int temp = arr1[i];
                    arr1[i] = arr2[j];
                    arr2[j] = temp;
                }

            if (j < m)
            {
                // comparing elements in the
                // second array.
                for (j = 0; j + gap < m; j++)
                    if (arr2[j] > arr2[j + gap])
                    {
                        int temp = arr2[j];
                        arr2[j] = arr2[j + gap];
                        arr2[j + gap] = temp;
                    }
            }
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] a1 = { 10, 27, 38, 43, 82 };
        int[] a2 = { 3, 9 };

        // Function Call
        merge(a1, a2, a1.length, a2.length);

        System.out.print("First Array: ");
        for (int i = 0; i < a1.length; i++) {
            System.out.print(a1[i] + " ");
        }

        System.out.println();

        System.out.print("Second Array: ");
        for (int i = 0; i < a2.length; i++) {
            System.out.print(a2[i] + " ");
        }
    }
}

// This code is contributed by Vinisha Shah
```

## 蟒蛇 3

```
# Merging two sorted arrays with O(1)
# extra space

# Function to find next gap.

def nextGap(gap):

    if (gap <= 1):
        return 0
    return (gap // 2) + (gap % 2)

def merge(arr1, arr2, n, m):

    gap = n + m
    gap = nextGap(gap)
    while gap > 0:

        # comparing elements in
        # the first array.
        i = 0
        while i + gap < n:
            if (arr1[i] > arr1[i + gap]):
                arr1[i], arr1[i + gap] = arr1[i + gap], arr1[i]

            i += 1

        # comparing elements in both arrays.
        j = gap - n if gap > n else 0
        while i < n and j < m:
            if (arr1[i] > arr2[j]):
                arr1[i], arr2[j] = arr2[j], arr1[i]

            i += 1
            j += 1

        if (j < m):

            # comparing elements in the
            # second array.
            j = 0
            while j + gap < m:
                if (arr2[j] > arr2[j + gap]):
                    arr2[j], arr2[j + gap] = arr2[j + gap], arr2[j]

                j += 1

        gap = nextGap(gap)

# Driver code
if __name__ == "__main__":

    a1 = [10, 27, 38, 43, 82]
    a2 = [3, 9]
    n = len(a1)
    m = len(a2)

    # Function Call
    merge(a1, a2, n, m)

    print("First Array: ", end="")
    for i in range(n):
        print(a1[i], end=" ")
    print()

    print("Second Array: ", end="")
    for i in range(m):
        print(a2[i], end=" ")
    print()

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program for Merging two sorted arrays
// with O(1) extra space
using System;

class GFG {

    // Function to find next gap.
    static int nextGap(int gap)
    {
        if (gap <= 1)
            return 0;
        return (gap / 2) + (gap % 2);
    }

    private static void merge(int[] arr1, int[] arr2, int n,
                              int m)
    {
        int i, j, gap = n + m;
        for (gap = nextGap(gap); gap > 0;
             gap = nextGap(gap))
        {
            // comparing elements in the first
            // array.
            for (i = 0; i + gap < n; i++)
                if (arr1[i] > arr1[i + gap])
                {
                    int temp = arr1[i];
                    arr1[i] = arr1[i + gap];
                    arr1[i + gap] = temp;
                }

            // comparing elements in both arrays.
            for (j = gap > n ? gap - n : 0; i < n && j < m;
                 i++, j++)
                if (arr1[i] > arr2[j])
                {
                    int temp = arr1[i];
                    arr1[i] = arr2[j];
                    arr2[j] = temp;
                }

            if (j < m) {
                // comparing elements in the
                // second array.
                for (j = 0; j + gap < m; j++)
                    if (arr2[j] > arr2[j + gap])
                    {
                        int temp = arr2[j];
                        arr2[j] = arr2[j + gap];
                        arr2[j + gap] = temp;
                    }
            }
        }
    }

    // Driver code
    public static void Main()
    {
        int[] a1 = { 10, 27, 38, 43, 82 };
        int[] a2 = { 3, 9 };

        // Function Call
        merge(a1, a2, a1.Length, a2.Length);

        Console.Write("First Array: ");
        for (int i = 0; i < a1.Length; i++) {
            Console.Write(a1[i] + " ");
        }

        Console.WriteLine();

        Console.Write("Second Array: ");
        for (int i = 0; i < a2.Length; i++) {
            Console.Write(a2[i] + " ");
        }
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Merging two sorted arrays
// with O(1) extra space

// Function to find next gap.
function nextGap($gap)
{
    if ($gap <= 1)
        return 0;
    return ($gap / 2) +
           ($gap % 2);
}

function merge($arr1, $arr2,
               $n, $m)
{
    $i;
    $j;
    $gap = $n + $m;
    for ($gap = nextGap($gap);
         $gap > 0; $gap = nextGap($gap))
    {
        // comparing elements
        // in the first array.
        for ($i = 0; $i + $gap < $n; $i++)
            if ($arr1[$i] > $arr1[$i + $gap])
            {
                $tmp = $arr1[$i];
                $arr1[$i] = $arr1[$i + $gap];
                $arr1[$i + $gap] = $tmp;
            }

        // comparing elements
        // in both arrays.
        for ($j = $gap > $n ? $gap - $n : 0 ;
             $i < $n && $j < $m; $i++, $j++)
            if ($arr1[$i] > $arr2[$j])
            {
                $tmp = $arr1[$i];
                $arr1[$i] = $arr2[$j];
                $arr2[$j] = $tmp;
            }

        if ($j < $m)
        {
            // comparing elements in
            // the second array.
            for ($j = 0; $j + $gap < $m; $j++)
                if ($arr2[$j] > $arr2[$j + $gap])
                {
                    $tmp = $arr2[$j];
                    $arr2[$j] = $arr2[$j + $gap];
                    $arr2[$j + $gap] = $tmp;
                }
        }
    }

    echo "First Array: ";
    for ($i = 0; $i < $n; $i++)
        echo $arr1[$i]." ";

    echo "\nSecond Array: ";
    for ($i = 0; $i < $m; $i++)
        echo $arr2[$i] . " ";
    echo"\n";

}

// Driver code
$a1 = array(10, 27, 38, 43 ,82);
$a2 = array(3,9);
$n = sizeof($a1);
$m = sizeof($a2);

// Function Call
merge($a1, $a2, $n, $m);

// This code is contributed
// by mits.
?>
```

## java 描述语言

```
<script>
    // Javascript program for Merging two sorted arrays
    // with O(1) extra space

    // Function to find next gap.
    function nextGap(gap)
    {
        if (gap <= 1)
            return 0;
        return parseInt(gap / 2, 10) + (gap % 2);
    }

    function merge(arr1, arr2, n, m)
    {
        let i, j, gap = n + m;
        for (gap = nextGap(gap); gap > 0;
             gap = nextGap(gap))
        {
            // comparing elements in the first
            // array.
            for (i = 0; i + gap < n; i++)
                if (arr1[i] > arr1[i + gap])
                {
                    let temp = arr1[i];
                    arr1[i] = arr1[i + gap];
                    arr1[i + gap] = temp;
                }

            // comparing elements in both arrays.
            for (j = gap > n ? gap - n : 0; i < n && j < m;
                 i++, j++)
                if (arr1[i] > arr2[j])
                {
                    let temp = arr1[i];
                    arr1[i] = arr2[j];
                    arr2[j] = temp;
                }

            if (j < m) {
                // comparing elements in the
                // second array.
                for (j = 0; j + gap < m; j++)
                    if (arr2[j] > arr2[j + gap])
                    {
                        let temp = arr2[j];
                        arr2[j] = arr2[j + gap];
                        arr2[j + gap] = temp;
                    }
            }
        }
    }

    let a1 = [ 10, 27, 38, 43, 82 ];
    let a2 = [ 3, 9 ];

    // Function Call
    merge(a1, a2, a1.length, a2.length);

    document.write("First Array: ");
    for (let i = 0; i < a1.length; i++) {
      document.write(a1[i] + " ");
    }

    document.write("</br>");

    document.write("Second Array: ");
    for (let i = 0; i < a2.length; i++) {
      document.write(a2[i] + " ");
    }

</script>
```

**Output**

```
First Array: 3 9 10 27 38 
Second Array: 43 82
```

#### **O(m+n)时间复杂度中的另一种方法:**

这里我们使用以下技巧:

```
Suppose we have a number A and we want to 
convert it to a number B and there is also a 
constraint that we can recover number A any 
time without using other variable.To achieve 
this we chose a number N which is greater 
than both numbers and add B*N in A.
so A --> A+B*N

To get number B out of (A+B*N) 
we divide (A+B*N) by N.
so (A+B*N)/N = B.

To get number A out of (A+B*N) 
we take modulo with N.
so (A+B*N)%N = A.

-> In short by taking modulo 
we get old number back and taking divide 
we new number.
```

我们首先找到两个数组的最大元素，并将其递增 1，以避免取模运算过程中 0 和最大元素的冲突。想法是从同时开始遍历两个数组。假设 a 中的一个元素是 a[i]，b 中的一个元素是 b[j]，k 是下一个最小值出现的位置。现在，如果 k

下面是上述想法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

void mergeArray(int a[], int b[], int n, int m)
{
    int mx = 0;

    // Find maximum element of both array
    for (int i = 0; i < n; i++) {
        mx = max(mx, a[i]);
    }
    for (int i = 0; i < m; i++) {
        mx = max(mx, b[i]);
    }

    // increment by one to avoid collision of 0 and maximum
    // element of array in modulo operation
    mx++;
    int i = 0, j = 0, k = 0;
    while (i < n && j < m && k < (n + m)) {

        // recover back original element to compare
        int e1 = a[i] % mx;
        int e2 = b[j] % mx;
        if (e1 <= e2) {

            // update element by adding multiplication
            // with new number
            if (k < n)
                a[k] += (e1 * mx);
            else
                b[k - n] += (e1 * mx);
            i++;
            k++;
        }
        else {

            // update element by adding multiplication
            // with new number
            if (k < n)
                a[k] += (e2 * mx);
            else
                b[k - n] += (e2 * mx);
            j++;
            k++;
        }
    }

    // process those elements which are left in array a
    while (i < n) {
        int el = a[i] % mx;
        if (k < n)
            a[k] += (el * mx);
        else
            b[k - n] += (el * mx);
        i++;
        k++;
    }

    // process those elements which are left in array b
    while (j < m) {
        int el = b[j] % mx;
        if (k < n)
            a[k] += (el * mx);
        else
            b[k - n] += (el * mx);
        j++;
        k++;
    }

    // finally update elements by dividing
    // with maximum element
    for (int i = 0; i < n; i++)
        a[i] = a[i] / mx;

    // finally update elements by dividing
    // with maximum element
    for (int i = 0; i < m; i++)
        b[i] = b[i] / mx;

    return;
}

// Driver Code
int main()
{
    int a[] = { 3, 5, 6, 8, 12 };
    int b[] = { 1, 4, 9, 13 };
    int n = sizeof(a) / sizeof(int); // Length of a
    int m = sizeof(b) / sizeof(int); // length of b

    // Function Call
    mergeArray(a, b, n, m);

    cout << "First array : ";
    for (int i = 0; i < n; i++)
        cout << a[i] << " ";
    cout << endl;

    cout << "Second array : ";
    for (int i = 0; i < m; i++)
        cout << b[i] << " ";
    cout << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;

class GFG{

static void mergeArray(int a[], int b[],
                       int n, int m)
{
    int mx = 0;

    // Find maximum element of both array
    for(int i = 0; i < n; i++)
    {
        mx = Math.max(mx, a[i]);
    }

    for(int i = 0; i < m; i++)
    {
        mx = Math.max(mx, b[i]);
    }

    // Increment one two avoid collision of
    // 0 and maximum element of array in
    // modulo operation
    mx++;
    int i = 0, j = 0, k = 0;

    while (i < n && j < m && k < (n + m))
    {

        // Recover back original element
        // to compare
        int e1 = a[i] % mx;
        int e2 = b[j] % mx;

        if (e1 <= e2)
        {

            // Update element by adding
            // multiplication with new number
            if (k < n)
                a[k] += (e1 * mx);
            else
                b[k - n] += (e1 * mx);

            i++;
            k++;
        }
        else
        {

            // Update element by adding
            // multiplication with new number
            if (k < n)
                a[k] += (e2 * mx);
            else
                b[k - n] += (e2 * mx);

            j++;
            k++;
        }
    }

    // Process those elements which are
    // left in array a
    while (i < n)
    {
        int el = a[i] % mx;
        if (k < n)
            a[k] += (el * mx);
        else
            b[k - n] += (el * mx);

        i++;
        k++;
    }

    // Process those elements which are
    // left in array a
    while (j < m)
    {
        int el = b[j] % mx;

        if (k < n)
            b[k] += (el * mx);
        else
            b[k - n] += (el * mx);

        j++;
        k++;
    }

    // Finally update elements by dividing
    // with maximum element
    for(int in = 0; in < n; in++)
        a[in] = a[in] / mx;

    // Finally update elements by dividing
    // with maximum element
    for(int in = 0; in < m; in++)
        b[in] = b[in] / mx;

    return;
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 3, 5, 6, 8, 12 };
    int b[] = { 1, 4, 9, 13 };

    // Length of a
    int n = a.length;

    // length of b
    int m = b.length;

    // Function Call
    mergeArray(a, b, n, m);

    System.out.print("First array : ");
    for(int i = 0; i < n; i++)
        System.out.print(a[i] + " ");

    System.out.println();

      System.out.print("Second array : ");
    for(int i = 0; i < m; i++)
        System.out.print(b[i] + " ");

    System.out.println();
}
}

// This code is contributed by yashbeersingh42
```

## C#

```
using System;

public class GFG{

  static void mergeArray(int[] a, int[] b,
                         int n, int m)
  {
    int mx = 0;

    // Find maximum element of both array
    for(int I = 0; I < n; I++)
    {
      mx = Math.Max(mx, a[I]);
    }

    for(int I = 0; I < m; I++)
    {
      mx = Math.Max(mx, b[I]);
    }

    // Increment one two avoid collision of
    // 0 and maximum element of array in
    // modulo operation
    mx++;
    int i = 0, j = 0, k = 0;

    while (i < n && j < m && k < (n + m))
    {

      // Recover back original element
      // to compare
      int e1 = a[i] % mx;
      int e2 = b[j] % mx;

      if (e1 <= e2)
      {

        // Update element by adding
        // multiplication with new number
        if (k < n)
          a[k] += (e1 * mx);
        else
          b[k - n] += (e1 * mx);

        i++;
        k++;
      }
      else
      {

        // Update element by adding
        // multiplication with new number
        if (k < n)
          a[k] += (e2 * mx);
        else
          b[k - n] += (e2 * mx);

        j++;
        k++;
      }
    }

    // Process those elements which are
    // left in array a
    while (i < n)
    {
      int el = a[i] % mx;
      if (k < n)
        a[k] += (el * mx);
      else
        b[k - n] += (el * mx);

      i++;
      k++;
    }

    // Process those elements which are
    // left in array a
    while (j < m)
    {
      int el = b[j] % mx;

      if (k < n)
        b[k] += (el * mx);
      else
        b[k - n] += (el * mx);

      j++;
      k++;
    }

    // Finally update elements by dividing
    // with maximum element
    for(int In = 0; In < n; In++)
      a[In] = a[In] / mx;

    // Finally update elements by dividing
    // with maximum element
    for(int In = 0; In < m; In++)
      b[In] = b[In] / mx;

    return;
  }

  // Driver code
  static public void Main (){
    int[] a = { 3, 5, 6, 8, 12 };
    int[] b = { 1, 4, 9, 13 };

    // Length of a
    int n = a.Length;

    // length of b
    int m = b.Length;

    // Function Call
    mergeArray(a, b, n, m);

    Console.Write("First array : ");
    for(int i = 0; i < n; i++)
      Console.Write(a[i] + " ");

    Console.WriteLine();

    Console.Write("Second array : ");
    for(int i = 0; i < m; i++)
      Console.Write(b[i] + " ");

    Console.WriteLine();
  }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

function mergeArray(a, b, n, m)
{
    let mx = 0;

    // Find maximum element of both array
    for(let i = 0; i < n; i++)
    {
        mx = Math.max(mx, a[i]);
    }
    for(let i = 0; i < m; i++)
    {
        mx = Math.max(mx, b[i]);
    }

    // Increment by one to avoid collision
    // of 0 and maximum element of array
    // in modulo operation
    mx++;
    let i = 0, j = 0, k = 0;

    while (i < n && j < m && k < (n + m))
    {

        // Recover back original element
        // to compare
        let e1 = a[i] % mx;
        let e2 = b[j] % mx;

        if (e1 <= e2)
        {

            // Update element by adding
            // multiplication with new number
            if (k < n)
                a[k] += (e1 * mx);
            else
                b[k - n] += (e1 * mx);

            i++;
            k++;
        }
        else
        {

            // Update element by adding
            // multiplication with new number
            if (k < n)
                a[k] += (e2 * mx);
            else
                b[k - n] += (e2 * mx);

            j++;
            k++;
        }
    }

    // Process those elements which
    // are left in array a
    while (i < n)
    {
        let el = a[i] % mx;
        if (k < n)
            a[k] += (el * mx);
        else
            b[k - n] += (el * mx);

        i++;
        k++;
    }

    // Process those elements which
    // are left in array b
    while (j < m)
    {
        let el = b[j] % mx;
        if (k < n)
            a[k] += (el * mx);
        else
            b[k - n] += (el * mx);

        j++;
        k++;
    }

    // Finally update elements by dividing
    // with maximum element
    for(let i = 0; i < n; i++)
        a[i] = parseInt(a[i] / mx);

    // Finally update elements by dividing
    // with maximum element
    for(let i = 0; i < m; i++)
        b[i] = parseInt(b[i] / mx);

    return;
}

// Driver Code
var a = [ 3, 5, 6, 8, 12 ];
var b = [ 1, 4, 9, 13 ];

// Length of a
var n = a.length;

// Length of b
var m = b.length;

// Function Call
mergeArray(a, b, n, m);

document.write("First array : ");
for(let i = 0; i < n; i++)
    document.write(a[i] + " ");

document.write('<br>')

document.write("Second array : ");
for(let i = 0; i < m; i++)
    document.write(b[i] + " ");

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
First array : 1 3 4 5 6 
Second array : 8 9 12 13
```

**时间复杂度:** O(m+n)

**我们在下面的帖子里讨论了一个简单高效的解决方案。**

在这篇文章中，讨论了一个更好、更简单的解决方案。

想法是:我们将遍历第一个数组，并将其与第二个数组的第一个元素进行比较。如果第二个数组的第一个元素小于第一个数组，我们将交换然后对第二个数组进行排序。

1.  首先，我们必须遍历数组 1，然后将其与数组 2 的第一个元素进行比较。
    如果小于数组 1，那么我们交换两者。

2.  交换之后，我们将再次对数组 2 进行排序，以便数组 2 的最小元素
    出现在第一个位置，我们可以再次与数组 1 交换
3.  为了对数组 2 进行排序，我们将数组 2 的第一个元素存储在一个变量中，并将所有元素左移，并将数组 2 中的第一个元素存储在最后一个元素中。

## C++

```
#include <bits/stdc++.h>
using namespace std;

void mergeArray(int arr1[], int arr2[],
                int n, int m)
{

    // Now traverse the array1 and if
    // arr2 first element
    // is less than arr1 then swap
    for(int i = 0; i < n; i++)
    {
        if (arr1[i] > arr2[0])
        {

            // Swap
            int temp = arr1[i];
            arr1[i] = arr2[0];
            arr2[0] = temp;

            // After swapping we have to sort the array2
            // again so that it can be again swap with
            // arr1

            // We will store the firstElement of array2
            // and left shift all the element and store
            // the firstElement in arr2[k-1]
            int firstElement = arr2[0];

            int k;

            for(k = 1;
                k < m && arr2[k] < firstElement;
                k++)
            {
                arr2[k - 1] = arr2[k];
            }
            arr2[k - 1] = firstElement;
        }
    }

    // Read the arr1
    for(int i = 0; i < n; i++)
    {
        cout << arr1[i] << " ";
    }
    cout << endl;

    // Read the arr2
    for(int i = 0; i < m; i++)
    {
        cout << arr2[i] << " ";
    }
}

// Driver Code
int main()
{
    int arr1[] = { 1, 3, 5, 7 };
    int arr2[] = { 0, 2, 6, 8, 9 };
    int n = sizeof(arr1)/sizeof(arr1[0]), m =  sizeof(arr2)/sizeof(arr2[0]);

    mergeArray(arr1, arr2, n, m);
}

// This code is contributed by yashbeersingh42
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;

class GFG {

    public static void mergeArray(int[] arr1, int[] arr2)
    {

        // length of first arr1
        int n = arr1.length;

        // length of second arr2
        int m = arr2.length;

        // Now traverse the array1 and if
        // arr2 first element
        // is less than arr1 then swap
        for (int i = 0; i < n; i++) {

            if (arr1[i] > arr2[0]) {

                // swap
                int temp = arr1[i];
                arr1[i] = arr2[0];
                arr2[0] = temp;

                // after swapping we have to sort the array2
                // again so that it can be again swap with
                // arr1

                // we will store the firstElement of array2
                // and left shift all the element and store
                // the firstElement in arr2[k-1]

                int firstElement = arr2[0];

                int k;
                for (k = 1;
                     k < m && arr2[k] < firstElement;
                     k++)
                {
                    arr2[k - 1] = arr2[k];
                }
                arr2[k - 1] = firstElement;
            }
        }

        // read the arr1
        for (int i : arr1) {
            System.out.print(i + " ");
        }

        System.out.println();

        // read the arr2
        for (int i : arr2) {
            System.out.print(i + " ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr1 = { 1, 3, 5, 7 };

        int[] arr2 = { 0, 2, 6, 8, 9 };
        mergeArray(arr1, arr2);
    }
}
```

## C#

```
using System;

class GFG{

public static void mergeArray(int[] arr1,
                              int[] arr2)
{

    // Length of first arr1
    int n = arr1.Length;

    // Length of second arr2
    int m = arr2.Length;

    // Now traverse the array1 and if
    // arr2 first element
    // is less than arr1 then swap
    for(int i = 0; i < n; i++)
    {
        if (arr1[i] > arr2[0])
        {

            // Swap
            int temp = arr1[i];
            arr1[i] = arr2[0];
            arr2[0] = temp;

            // After swapping we have to sort the array2
            // again so that it can be again swap with
            // arr1

            // We will store the firstElement of array2
            // and left shift all the element and store
            // the firstElement in arr2[k-1]
            int firstElement = arr2[0];

            int k;
            for(k = 1;
                k < m && arr2[k] < firstElement;
                k++)
            {
                arr2[k - 1] = arr2[k];
            }
            arr2[k - 1] = firstElement;
        }
    }

    // Read the arr1
    foreach (int i in arr1)
    {
        Console.Write(i + " ");
    }

    Console.WriteLine();

    // Read the arr2
    foreach(int i in arr2)
    {
        Console.Write(i + " ");
    }
}

// Driver Code
static public void Main()
{
    int[] arr1 = { 1, 3, 5, 7 };
    int[] arr2 = { 0, 2, 6, 8, 9 };

    mergeArray(arr1, arr2);
}
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>

function mergeArray(arr1, arr2,
                n, m)
{

    // Now traverse the array1 and if
    // arr2 first element
    // is less than arr1 then swap
    for(let i = 0; i < n; i++)
    {
        if (arr1[i] > arr2[0])
        {

            // Swap
            let temp = arr1[i];
            arr1[i] = arr2[0];
            arr2[0] = temp;

            // After swapping we have to sort the array2
            // again so that it can be again swap with
            // arr1

            // We will store the firstElement of array2
            // and left shift all the element and store
            // the firstElement in arr2[k-1]
            let firstElement = arr2[0];

            let k;

            for(k = 1;
                k < m && arr2[k] < firstElement;
                k++)
            {
                arr2[k - 1] = arr2[k];
            }
            arr2[k - 1] = firstElement;
        }
    }

    // Read the arr1
    for(let i = 0; i < n; i++)
    {
        document.write(arr1[i] + " ");
    }
    document.write("<br>");

    // Read the arr2
    for(let i = 0; i < m; i++)
    {
        document.write(arr2[i] + " ");
    }
}

// Driver Code

    let arr1 = [ 1, 3, 5, 7 ];
    let arr2 = [ 0, 2, 6, 8, 9 ];
    let n = 4, m = 5;

    mergeArray(arr1, arr2, n, m);

//This code is contributed by Mayank Tyagi
</script>
```

**Output**

```
0 1 2 3 
5 6 7 8 9
```

**时间复杂度:**O(n * m)
T3】空间复杂度: O(1)

本文由 [**什洛米·埃尔海亚尼**](https://www.facebook.com/shlomi.elhaiani) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果您发现任何不正确的地方，请写评论，或者分享更多关于上述主题的信息。