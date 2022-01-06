# 最小增量数-使所有数组元素相等的其他操作。

> 原文:[https://www . geesforgeks . org/minimum-number-increment-operations-make-array-elements-equal/](https://www.geeksforgeeks.org/minimum-number-increment-operations-make-array-elements-equal/)

给我们一个由 n 个元素组成的数组。在每次操作中，您可以选择任意一个元素，并将其余 n-1 个元素增加 1。你必须让所有的元素都相等，你想做多少次就做多少次。找到为此所需的最小操作数。
示例:

```
Input : arr[] = {1, 2, 3}
Output : Minimum Operation = 3
Explanation : 
operation | increased elements | after increment
    1     |    1, 2            | 2, 3, 3
    2     |    1, 2            | 3, 4, 3
    3     |    1, 3            | 4, 4, 4

Input : arr[] = {4, 3, 4}
Output : Minimum Operation = 2
Explanation : 
operation | increased elements | after increment
     1    |    1, 2           | 5, 4, 4
     2    |    2, 3           | 5, 5, 5
```

**蛮力:**让所有元素相等的一个简单方法是，在每一步找到最大的元素，然后将所有剩余的 n-1 个元素加 1。我们应该继续做这个操作，直到所有元素都变得相等。时间复杂度:O(n^2)
**更好的方法:**如果我们仔细观察每个操作以及问题陈述，我们会发现增加除最大元素之外的所有 n-1 元素类似于仅减少最大元素。所以，最小的元素不需要再减少了，剩下的元素会减少到最小的元素。这样，使所有元素相等所需的操作总数将是*arraySum–n *(小元素)。*时间复杂度与求最小元素和数组和即 O(n)的时间复杂度相同。

```
// find array sum
sum = arraySum (int arr[], int n);

// find the smallest element from array
small = smallest (int arr, int n);

// calculate min operation required
minOperation = sum - (n * small);

// return result
return minOperation;
```

## C++

```
// CPP for finding minimum operation required
#include<bits/stdc++.h>
using namespace std;

// function for finding array sum
int arraySum (int arr[], int n)
{
    int sum = 0;
    for (int i=0; i<n; sum+=arr[i++]);
    return sum;
}

// function for finding smallest element
int smallest (int arr[], int n)
{
    int small = INT_MAX;
    for (int i=0; i<n; i++)
        if (arr[i] < small)
            small = arr[i];
    return small;
}

// function for finding min operation
int minOp (int arr[], int n)
{
    // find array sum
    int sum = arraySum (arr, n);

    // find the smallest element from array
    int small = smallest (arr, n);

    // calculate min operation required
    int minOperation = sum - (n * small);

    // return result
    return minOperation;
}

//driver function
int main()
{
    int arr[] = {5, 6, 2, 4, 3};
    int n = sizeof(arr)/ sizeof(arr[0]);
    cout << "Minimum Operation = " << minOp (arr, n);
    return 0;
}
```

## C++

```
// [STL] - CPP for finding minimum operation required
#include<bits/stdc++.h>
using namespace std;

// function for finding min operation
int minOp (int arr[], int n)
{
    // find array sum
    int sum = accumulate(arr,arr+n,0);

    // find the smallest element from array
    int small = *min_element(arr,arr+n);

    // calculate min operation required
    int minOperation = sum - (n * small);

    // return result
    return minOperation;
}

//driver function
int main()
{
    int arr[] = {5, 6, 2, 4, 3};
    int n = sizeof(arr)/ sizeof(arr[0]);
    cout << "Minimum Operation = " << minOp (arr, n);
    return 0;
}
// This code is contributed by Shubham Singh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find min operation
import java.io.*;

class minOperation
{
    /* Function to print minimum operation required
       to make all elements of an array equal */
    static void printMinOp(int arr[])
    {
        int arraySum, smallest, arr_size = arr.length;
        arraySum = 0;
        smallest = arr[0];
        for (int i = 0; i < arr_size ; i ++)
        {
            /* If current element is smaller than
               update smallest */
            if (arr[i] < smallest)           
                smallest = arr[i];           

            /*find array sum */
            arraySum += arr[i];
        }

        int minOperation = arraySum - arr_size * smallest;

        /* Print min operation required */ 
        System.out.println("Minimum Operation = " +
                               minOperation);

    }

    /* Driver program to test above functions */
    public static void main (String[] args)
    {
        int arr[] = {5, 6, 2, 4, 3};
        printMinOp(arr);
    }
}
```

## 蟒蛇 3

```
# Python 3 for finding minimum
# operation required

# function for finding min
# operation
def minOp (arr, n) :

    # find array sum
    sm = sum(arr)

    # find the smallest element from
    # array
    small = min(arr)

    # calculate min operation required
    minOperation = sm - (n * small)

    # return result
    return minOperation

# Driver function
arr = [5, 6, 2, 4, 3]
n = len(arr)
print( "Minimum Operation = ", minOp (arr, n))

# This code is contributed by Shubham Singh
```

## C#

```
// C# program to find min operation
using System;

class GFG {

    /* Function to print minimum
    operation required to make all
    elements of an array equal */
    static void printMinOp(int []arr)
    {
        int arraySum, smallest,
        arr_size = arr.Length;
        arraySum = 0;
        smallest = arr[0];

        for (int i = 0; i < arr_size ; i ++)
        {
            /* If current element is
            smaller than update smallest */
            if (arr[i] < smallest)        
                smallest = arr[i];        

            /*find array sum */
            arraySum += arr[i];
        }

        int minOperation = arraySum - 
                        arr_size * smallest;

        /* Print min operation required */
        Console.Write("Minimum Operation = " +
                            minOperation);
    }

    /* Driver program to test above
    functions */
    public static void Main ()
    {
        int []arr = {5, 6, 2, 4, 3};

        printMinOp(arr);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP for finding minimum operation required

// function for finding array sum
function arraySum ($arr, $n)
{
    $sum = 0;
    for ($i = 0; $i < $n; $sum += $arr[$i++]);
    return $sum;
}

// function for finding smallest element
function smallest ($arr, $n)
{
    $small = PHP_INT_MAX;
    for ($i = 0; $i < $n; $i++)
        if ($arr[$i] < $small)
            $small = $arr[$i];
    return $small;
}

// function for finding min operation
function minOp ($arr, $n)
{

    // find array sum
    $sum = arraySum ($arr, $n);

    // find the smallest
    // element from array
    $small = smallest ($arr, $n);

    // calculate min operation
    // required
    $minOperation = $sum - ($n * $small);

    // return result
    return $minOperation;
}

    // Driver Code
    $arr = array (5, 6, 2, 4, 3);
    $n = sizeof($arr);
    echo "Minimum Operation = " , minOp ($arr, $n);

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>
// javascript program to find min operationclass minOeration{
    /*
     * Function to print minimum operation
     required to make all elements of an array
     * equal
     */
    function printMinOp(arr)
    {
        var arraySum, smallest, arr_size = arr.length;
        arraySum = 0;
        smallest = arr[0];
        for (i = 0; i < arr_size; i++)
        {

            /*
             * If current element is smaller than update smallest
             */
            if (arr[i] < smallest)
                smallest = arr[i];

            /* find array sum */
            arraySum += arr[i];
        }

        var minOperation = arraySum - arr_size * smallest;

        /* Print min operation required */
        document.write("Minimum Operation = " + minOperation);

    }

    /* Driver program to test above functions */
        var arr = [ 5, 6, 2, 4, 3 ];
        printMinOp(arr);

// This code is contributed by aashish1995
</script>
```

**Output**

```
Minimum Operation = 10
```

本文由[**Shivam Pradhan(anuj _ charm)**](http://www.facebook.com/ma5ter6it)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。