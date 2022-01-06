# 在形成几何级数的排序数组中找到所有三元组

> 原文:[https://www . geesforgeks . org/find-all-triples-in-a-sorted-array-forms-geometric-progression/](https://www.geeksforgeeks.org/find-all-triplets-in-a-sorted-array-that-forms-geometric-progression/)

给定一个不同正整数的排序数组，打印所有以整数公比构成几何级数的三元组。
几何级数是一个数字序列，其中第一个项之后的每个项都是通过将前一个项乘以一个固定的非零数(称为公比)得到的。例如，数列 2，6，18，54，…是一个几何级数，公比是 3。
**例:**

```
Input: 
arr = [1, 2, 6, 10, 18, 54]
Output: 
2 6 18
6 18 54

Input: 
arr = [2, 8, 10, 15, 16, 30, 32, 64]
Output: 
2 8 32
8 16 32
16 32 64

Input: 
arr = [ 1, 2, 6, 18, 36, 54]
Output: 
2 6 18
1 6 36
6 18 54
```

想法是从第二个元素开始，将每个元素固定为中间元素，并搜索三元组中的其他两个元素(一个较小，一个较大)。为了使元素 arr[j]处于几何级数中间，必须存在元素 arr[i]和 arr[k],使得–

```
arr[j] / arr[i] = r and arr[k] / arr[j] = r
where r is an positive integer and 0 <= i < j and j < k <= n - 1
```

以下是上述想法的实现–

## C++

```
// C++ program to find if there exist three elements in
// Geometric Progression or not
#include <iostream>
using namespace std;

// The function prints three elements in GP if exists
// Assumption: arr[0..n-1] is sorted.
void findGeometricTriplets(int arr[], int n)
{
    // One by fix every element as middle element
    for (int j = 1; j < n - 1; j++)
    {
        // Initialize i and k for the current j
        int i = j - 1, k = j + 1;

        // Find all i and k such that (i, j, k)
        // forms a triplet of GP
        while (i >= 0 && k <= n - 1)
        {
            // if arr[j]/arr[i] = r and arr[k]/arr[j] = r
            // and r is an integer (i, j, k) forms Geometric
            // Progression
            while (arr[j] % arr[i] == 0 &&
                    arr[k] % arr[j] == 0 &&
                    arr[j] / arr[i] == arr[k] / arr[j])
            {
                // print the triplet
                cout << arr[i] << " " << arr[j]
                     << " " << arr[k] << endl;

                // Since the array is sorted and elements
                // are distinct.
                k++ , i--;
            }

            // if arr[j] is multiple of arr[i] and arr[k] is
            // multiple of arr[j], then arr[j] / arr[i] !=
            // arr[k] / arr[j]. We compare their values to
            // move to next k or previous i.
            if(arr[j] % arr[i] == 0 &&
                    arr[k] % arr[j] == 0)
            {
                if(arr[j] / arr[i] < arr[k] / arr[j])
                    i--;
                else k++;
            }

            // else if arr[j] is multiple of arr[i], then
            // try next k. Else, try previous i.
            else if (arr[j] % arr[i] == 0)
                k++;
            else i--;
        }
    }
}

// Driver code
int main()
{
    // int arr[] = {1, 2, 6, 10, 18, 54};
    // int arr[] = {2, 8, 10, 15, 16, 30, 32, 64};
    // int arr[] = {1, 2, 6, 18, 36, 54};
    int arr[] = {1, 2, 4, 16};
    // int arr[] = {1, 2, 3, 6, 18, 22};
    int n = sizeof(arr) / sizeof(arr[0]);

    findGeometricTriplets(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if there exist three elements in
// Geometric Progression or not
import java.util.*;

class GFG
{

// The function prints three elements in GP if exists
// Assumption: arr[0..n-1] is sorted.
static void findGeometricTriplets(int arr[], int n)
{
    // One by fix every element as middle element
    for (int j = 1; j < n - 1; j++)
    {
        // Initialize i and k for the current j
        int i = j - 1, k = j + 1;

        // Find all i and k such that (i, j, k)
        // forms a triplet of GP
        while (i >= 0 && k <= n - 1)
        {
            // if arr[j]/arr[i] = r and arr[k]/arr[j] = r
            // and r is an integer (i, j, k) forms Geometric
            // Progression
            while (i >= 0 && arr[j] % arr[i] == 0 &&
                    arr[k] % arr[j] == 0 &&
                    arr[j] / arr[i] == arr[k] / arr[j])
            {
                // print the triplet
                System.out.println(arr[i] +" " + arr[j]
                    + " " + arr[k]);

                // Since the array is sorted and elements
                // are distinct.
                k++ ; i--;
            }

            // if arr[j] is multiple of arr[i] and arr[k] is
            // multiple of arr[j], then arr[j] / arr[i] !=
            // arr[k] / arr[j]. We compare their values to
            // move to next k or previous i.
            if(i >= 0 && arr[j] % arr[i] == 0 &&
                    arr[k] % arr[j] == 0)
            {
                if(i >= 0 && arr[j] / arr[i] < arr[k] / arr[j])
                    i--;
                else k++;
            }

            // else if arr[j] is multiple of arr[i], then
            // try next k. Else, try previous i.
            else if (i >= 0 && arr[j] % arr[i] == 0)
                k++;
            else i--;
        }
    }
}

// Driver code
public static void main(String[] args)
{
    // int arr[] = {1, 2, 6, 10, 18, 54};
    // int arr[] = {2, 8, 10, 15, 16, 30, 32, 64};
    // int arr[] = {1, 2, 6, 18, 36, 54};
    int arr[] = {1, 2, 4, 16};
    // int arr[] = {1, 2, 3, 6, 18, 22};
    int n = arr.length;

    findGeometricTriplets(arr, n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 program to find if
# there exist three elements in
# Geometric Progression or not

# The function prints three elements
# in GP if exists.
# Assumption: arr[0..n-1] is sorted.
def findGeometricTriplets(arr, n):

    # One by fix every element
    # as middle element
    for j in range(1, n - 1):

        # Initialize i and k for
        # the current j
        i = j - 1
        k = j + 1

        # Find all i and k such that
        # (i, j, k) forms a triplet of GP
        while (i >= 0 and k <= n - 1):

            # if arr[j]/arr[i] = r and
            # arr[k]/arr[j] = r and r
            # is an integer (i, j, k) forms
            # Geometric Progression
            while (arr[j] % arr[i] == 0 and
                   arr[k] % arr[j] == 0 and
                   arr[j] // arr[i] == arr[k] // arr[j]):

                # print the triplet
                print( arr[i] , " " , arr[j],
                                " " , arr[k])

                # Since the array is sorted and
                # elements are distinct.
                k += 1
                i -= 1

            # if arr[j] is multiple of arr[i]
            # and arr[k] is multiple of arr[j],
            # then arr[j] / arr[i] != arr[k] / arr[j].
            # We compare their values to
            # move to next k or previous i.
            if(arr[j] % arr[i] == 0 and
                        arr[k] % arr[j] == 0):

                if(arr[j] // arr[i] < arr[k] // arr[j]):
                    i -= 1
                else:
                    k += 1

            # else if arr[j] is multiple of
            # arr[i], then try next k. Else,
            # try previous i.
            elif (arr[j] % arr[i] == 0):
                k += 1
            else:
                i -= 1

# Driver code
if __name__ =="__main__":

    arr = [1, 2, 4, 16]
    n = len(arr)

    findGeometricTriplets(arr, n)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find if there exist three elements
// in Geometric Progression or not
using System;

class GFG
{

// The function prints three elements in GP if exists
// Assumption: arr[0..n-1] is sorted.
static void findGeometricTriplets(int []arr, int n)
{

    // One by fix every element as middle element
    for (int j = 1; j < n - 1; j++)
    {
        // Initialize i and k for the current j
        int i = j - 1, k = j + 1;

        // Find all i and k such that (i, j, k)
        // forms a triplet of GP
        while (i >= 0 && k <= n - 1)
        {
            // if arr[j]/arr[i] = r and arr[k]/arr[j] = r
            // and r is an integer (i, j, k) forms Geometric
            // Progression
            while (i >= 0 && arr[j] % arr[i] == 0 &&
                             arr[k] % arr[j] == 0 &&
                    arr[j] / arr[i] == arr[k] / arr[j])
            {
                // print the triplet
            Console.WriteLine(arr[i] +" " +
                              arr[j] + " " + arr[k]);

                // Since the array is sorted and elements
                // are distinct.
                k++ ; i--;
            }

            // if arr[j] is multiple of arr[i] and arr[k] is
            // multiple of arr[j], then arr[j] / arr[i] !=
            // arr[k] / arr[j]. We compare their values to
            // move to next k or previous i.
            if(i >= 0 && arr[j] % arr[i] == 0 &&
                         arr[k] % arr[j] == 0)
            {
                if(i >= 0 && arr[j] / arr[i] <
                             arr[k] / arr[j])
                    i--;
                else k++;
            }

            // else if arr[j] is multiple of arr[i], then
            // try next k. Else, try previous i.
            else if (i >= 0 && arr[j] % arr[i] == 0)
                k++;
            else i--;
        }
    }
}

// Driver code
static public void Main ()
{

    // int arr[] = {1, 2, 6, 10, 18, 54};
    // int arr[] = {2, 8, 10, 15, 16, 30, 32, 64};
    // int arr[] = {1, 2, 6, 18, 36, 54};
    int []arr = {1, 2, 4, 16};

    // int arr[] = {1, 2, 3, 6, 18, 22};
    int n = arr.Length;

    findGeometricTriplets(arr, n);
}
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>
// Javascript program to find if there exist three elements in
// Geometric Progression or not

    // The function prints three elements in GP if exists
    // Assumption: arr[0..n-1] is sorted.
    function findGeometricTriplets(arr,n)
    {

        // One by fix every element as middle element
        for (let j = 1; j < n - 1; j++)
        {

            // Initialize i and k for the current j
            let i = j - 1, k = j + 1;

            // Find all i and k such that (i, j, k)
            // forms a triplet of GP
            while (i >= 0 && k <= n - 1)
            {

                // if arr[j]/arr[i] = r and arr[k]/arr[j] = r
                // and r is an integer (i, j, k) forms Geometric
                // Progression
                while (i >= 0 && arr[j] % arr[i] == 0 &&
                        arr[k] % arr[j] == 0 &&
                        arr[j] / arr[i] == arr[k] / arr[j])
                {

                    // print the triplet
                    document.write(arr[i] +" " + arr[j]
                        + " " + arr[k]+"<br>");

                    // Since the array is sorted and elements
                    // are distinct.
                    k++ ; i--;
                }

                // if arr[j] is multiple of arr[i] and arr[k] is
                // multiple of arr[j], then arr[j] / arr[i] !=
                // arr[k] / arr[j]. We compare their values to
                // move to next k or previous i.
                if(i >= 0 && arr[j] % arr[i] == 0 &&
                        arr[k] % arr[j] == 0)
                {
                    if(i >= 0 && arr[j] / arr[i] < arr[k] / arr[j])
                        i--;
                    else k++;
                }

                // else if arr[j] is multiple of arr[i], then
                // try next k. Else, try previous i.
                else if (i >= 0 && arr[j] % arr[i] == 0)
                    k++;
                else i--;
            }
        }
    }

    // Driver code
    // int arr[] = {1, 2, 6, 10, 18, 54};
    // int arr[] = {2, 8, 10, 15, 16, 30, 32, 64};
    // int arr[] = {1, 2, 6, 18, 36, 54};

    let arr = [1, 2, 4, 16];

    // int arr[] = {1, 2, 3, 6, 18, 22};
    let n = arr.length;
    findGeometricTriplets(arr, n);

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
1 2 4
1 4 16
```

**上述解的时间复杂度**为 O(n <sup>2</sup> )对于每一个 j，我们都在线性时间内找到 I 和 k。
本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。