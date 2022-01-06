# 找出最接近的左右较小元素之间的最大差异

> 原文:[https://www . geeksforgeeks . org/find-最接近的左右较小元素之间的最大差异/](https://www.geeksforgeeks.org/find-maximum-difference-between-nearest-left-and-right-smaller-elements/)

给定一个整数数组，任务是找出数组中每个元素最左边和最右边较小元素之间的最大绝对差。

**注:**如果任何元素的右侧或左侧没有较小的元素，那么我们取零作为较小的元素。例如，对于最左边的元素，左侧最近的较小元素被认为是 0。同样，对于最右边的元素，右边较小的元素被认为是 0。

**示例:**

```
Input : arr[] = {2, 1, 8}
Output : 1
Left smaller  LS[] {0, 0, 1}
Right smaller RS[] {1, 0, 0}
Maximum Diff of abs(LS[i] - RS[i]) = 1 

Input  : arr[] = {2, 4, 8, 7, 7, 9, 3}
Output : 4
Left smaller   LS[] = {0, 2, 4, 4, 4, 7, 2}
Right smaller  RS[] = {0, 3, 7, 3, 3, 3, 0}
Maximum Diff of abs(LS[i] - RS[i]) = 7 - 3 = 4 

Input : arr[] = {5, 1, 9, 2, 5, 1, 7}
Output : 1
```

一个**简单的解决方案**是为每个元素找到最近的左右较小元素，然后更新左右较小元素之间的最大差异，这需要 O(n^2)时间。

一个**高效的解决方案**需要 O(n)个时间。我们使用一个[堆栈](https://www.geeksforgeeks.org/stack-data-structure-introduction-program/)。这个想法基于[下一篇更大元素文章](https://www.geeksforgeeks.org/next-greater-element/)中讨论的方法。有趣的是，我们使用相同的函数计算左小和右小。

```
Let input array be 'arr[]' and size of array be 'n'

Find all smaller element on left side
     1\. Create a new empty stack S and an array LS[]
     2\. For every element 'arr[i]' in the input arr[],
          where 'i' goes from 0 to n-1.
        a) while S is nonempty and the top element of 
           S is greater than or equal to 'arr[i]':
           pop S

        b) if S is empty:
           'arr[i]' has no preceding smaller value 
            LS[i] = 0 

        c) else:
            the nearest smaller value to 'arr[i]' is top
            of stack
              LS[i] = s.top()

        d) push 'arr[i]' onto S   

Find all smaller element on right side
     3\. First reverse array arr[]. After reversing the array, 
        right smaller become left smaller.
     4\. Create an array RRS[] and repeat steps  1 and 2 to 
        fill RRS (in-place of LS).

5\. Initialize result as -1 and do following for every element
   arr[i]. In the reversed array right smaller for arr[i] is
   stored at RRS[n-i-1]
      return result = max(result, LS[i]-RRS[n-i-1])
```

以下是上述想法的实现

## C++

```
// C++ program to find the difference b/w left and
// right smaller element of every element in array
#include<bits/stdc++.h>
using namespace std;

// Function to fill left smaller element for every
// element of arr[0..n-1]. These values are filled
// in SE[0..n-1]
void leftSmaller(int arr[], int n, int SE[])
{
    // Create an empty stack
    stack<int>S;

    // Traverse all array elements
    // compute nearest smaller elements of every element
    for (int i=0; i<n; i++)
    {
        // Keep removing top element from S while the top
        // element is greater than or equal to arr[i]
        while (!S.empty() && S.top() >= arr[i])
            S.pop();

        // Store the smaller element of current element
        if (!S.empty())
            SE[i] = S.top();

        // If all elements in S were greater than arr[i]
        else
            SE[i] = 0;

        // Push this element
        S.push(arr[i]);
    }
}

// Function returns maximum difference b/w Left &
// right smaller element
int findMaxDiff(int arr[], int n)
{
    int LS[n]; // To store left smaller elements

    // find left smaller element of every element
    leftSmaller(arr, n, LS);

    // find right smaller element of every element
    // first reverse the array and do the same process
    int RRS[n]; // To store right smaller elements in
                // reverse array
    reverse(arr, arr + n);
    leftSmaller(arr, n, RRS);

    // find maximum absolute difference b/w LS & RRS
    // In the reversed array right smaller for arr[i] is
    // stored at RRS[n-i-1]
    int result = -1;
    for (int i=0 ; i< n ; i++)
        result = max(result, abs(LS[i] - RRS[n-1-i]));

    // return maximum difference b/w LS & RRS
    return result;
}

// Driver program
int main()
{
    int arr[] = {2, 4, 8, 7, 7, 9, 3};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << "Maximum diff : "
        << findMaxDiff(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the difference b/w left and
// right smaller element of every element in array
import java.util.*;

class GFG
{

    // Function to fill left smaller element for every
    // element of arr[0..n-1]. These values are filled
    // in SE[0..n-1]
    static void leftSmaller(int arr[], int n, int SE[])
    {
        // Create an empty stack
        Stack<Integer> S = new Stack<>();

        // Traverse all array elements
        // compute nearest smaller elements of every element
        for (int i = 0; i < n; i++)
        {
            // Keep removing top element from S while the top
            // element is greater than or equal to arr[i]
            while (!S.empty() && S.peek() >= arr[i])
            {
                S.pop();
            }

            // Store the smaller element of current element
            if (!S.empty())
            {
                SE[i] = S.peek();
            }
            // If all elements in S were greater than arr[i]
            else
            {
                SE[i] = 0;
            }

            // Push this element
            S.push(arr[i]);
        }
    }

    // Function returns maximum difference b/w Left &
    // right smaller element
    static int findMaxDiff(int arr[], int n)
    {
        int[] LS = new int[n]; // To store left smaller elements

        // find left smaller element of every element
        leftSmaller(arr, n, LS);

        // find right smaller element of every element
        // first reverse the array and do the same process
        int[] RRS = new int[n]; // To store right smaller elements in

        // reverse array
        reverse(arr);
        leftSmaller(arr, n, RRS);

        // find maximum absolute difference b/w LS & RRS
        // In the reversed array right smaller for arr[i] is
        // stored at RRS[n-i-1]
        int result = -1;
        for (int i = 0; i < n; i++)
        {
            result = Math.max(result, Math.abs(LS[i] - RRS[n - 1 - i]));
        }

        // return maximum difference b/w LS & RRS
        return result;
    }

    static void reverse(int a[])
    {
        int i, k, n = a.length;
        int t;
        for (i = 0; i < n / 2; i++)
        {
            t = a[i];
            a[i] = a[n - i - 1];
            a[n - i - 1] = t;
        }
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = {2, 4, 8, 7, 7, 9, 3};
        int n = arr.length;
        System.out.println("Maximum diff : "
                + findMaxDiff(arr, n));
    }
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python program to find the difference b/w left and
# right smaller element of every element in the array

# Function to fill left smaller element for every
# element of arr[0..n-1]. These values are filled
# in SE[0..n-1]
def leftsmaller(arr, n, SE):

    # create an empty stack
    sta = []
    # Traverse all array elements
    # compute nearest smaller elements of every element
    for i in range(n):

        # Keep removing top element from S while the top
        # element is greater than or equal to arr[i]
        while(sta != [] and sta[len(sta)-1] >= arr[i]):
            sta.pop()

        # Store the smaller element of current element
        if(sta != []):
            SE[i]=sta[len(sta)-1]
        # If all elements in S were greater than arr[i]
        else:
            SE[i]=0

        # push this element
        sta.append(arr[i])

# Function returns maximum difference b/w  Left  &
# right smaller element
def findMaxDiff(arr, n):
    ls=[0]*n # to store left smaller elements
    rs=[0]*n # to store right smaller elements

    # find left smaller elements of every element
    leftsmaller(arr, n, ls)

    # find right smaller element of every element
    # by sending reverse of array
    leftsmaller(arr[::-1], n, rs)

    # find maximum absolute difference b/w LS  & RRS
    # In the reversed array right smaller for arr[i] is
    # stored at RRS[n-i-1]
    res = -1
    for i in range(n):
        res = max(res, abs(ls[i] - rs[n-1-i]))
    # return maximum difference b/w LS  & RRS
    return res

# Driver Program
if __name__=='__main__':
    arr = [2, 4, 8, 7, 7, 9, 3]
    print "Maximum Diff :", findMaxDiff(arr, len(arr))

#Contributed By: Harshit Sidhwa
```

## C#

```
// C# program to find the difference b/w left and
// right smaller element of every element in array
using System;
using System.Collections.Generic;

class GFG
{

    // Function to fill left smaller element for every
    // element of arr[0..n-1]. These values are filled
    // in SE[0..n-1]
    static void leftSmaller(int []arr, int n, int []SE)
    {
        // Create an empty stack
        Stack<int> S = new Stack<int>();

        // Traverse all array elements
        // compute nearest smaller elements of every element
        for (int i = 0; i < n; i++)
        {
            // Keep removing top element from S while the top
            // element is greater than or equal to arr[i]
            while (S.Count != 0 && S.Peek() >= arr[i])
            {
                S.Pop();
            }

            // Store the smaller element of current element
            if (S.Count != 0)
            {
                SE[i] = S.Peek();
            }

            // If all elements in S were greater than arr[i]
            else
            {
                SE[i] = 0;
            }

            // Push this element
            S.Push(arr[i]);
        }
    }

    // Function returns maximum difference b/w Left &
    // right smaller element
    static int findMaxDiff(int []arr, int n)
    {
        int[] LS = new int[n]; // To store left smaller elements

        // find left smaller element of every element
        leftSmaller(arr, n, LS);

        // find right smaller element of every element
        // first reverse the array and do the same process
        int[] RRS = new int[n]; // To store right smaller elements in
                                // reverse array
        reverse(arr);
        leftSmaller(arr, n, RRS);

        // find maximum absolute difference b/w LS & RRS
        // In the reversed array right smaller for arr[i] is
        // stored at RRS[n-i-1]
        int result = -1;
        for (int i = 0; i < n; i++)
        {
            result = Math.Max(result, Math.Abs(LS[i] -
                                               RRS[n - 1 - i]));
        }

        // return maximum difference b/w LS & RRS
        return result;
    }

    static void reverse(int[] a)
    {
        int i, k, n = a.Length;
        int t;
        for (i = 0; i < n / 2; i++)
        {
            t = a[i];
            a[i] = a[n - i - 1];
            a[n - i - 1] = t;
        }
    }

    // Driver code
    public static void Main(String []args)
    {
        int []arr = {2, 4, 8, 7, 7, 9, 3};
        int n = arr.Length;
        Console.WriteLine("Maximum diff : " +
                           findMaxDiff(arr, n));
    }
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Function to fill left smaller
// element for every element of
// arr[0..n-1]. These values are
// filled in SE[0..n-1]
function leftSmaller(&$arr, $n, &$SE)
{
    $S = array();

    // Traverse all array elements
    // compute nearest smaller
    // elements of every element
    for ($i = 0; $i < $n; $i++)
    {
        // Keep removing top element
        // from S while the top element
        // is greater than or equal to arr[i]
        while (!empty($S) && max($S) >= $arr[$i])
            array_pop($S);

        // Store the smaller element
        // of current element
        if (!empty($S))
            $SE[$i] = max($S);

        // If all elements in S were
        // greater than arr[i]
        else
            $SE[$i] = 0;

        // Push this element
        array_push($S, $arr[$i]);
    }
}

// Function returns maximum
// difference b/w Left &
// right smaller element
function findMaxDiff(&$arr, $n)
{
    // To store left smaller elements
    $LS = array_fill(0, $n, NULL);

    // find left smaller element
    // of every element
    leftSmaller($arr, $n, $LS);

    // find right smaller element
    // of every element first reverse
    // the array and do the same process

    // To store right smaller
    // elements in reverse array
    $RRS = array_fill(0, $n, NULL);

    $k = 0;
    for($i = $n - 1; $i >= 0; $i--)
        $x[$k++] = $arr[$i];
    leftSmaller($x, $n, $RRS);

    // find maximum absolute difference
    // b/w LS & RRS. In the reversed
    // array right smaller for arr[i]
    // is stored at RRS[n-i-1]
    $result = -1;
    for ($i = 0 ; $i < $n ; $i++)
        $result = max($result, abs($LS[$i] -
                      $RRS[$n - 1 - $i]));

    // return maximum difference
    // b/w LS & RRS
    return $result;
}

// Driver Code
$arr = array(2, 4, 8, 7, 7, 9, 3);
$n = sizeof($arr);
echo "Maximum diff : " .
      findMaxDiff($arr, $n) . "\n";

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
// Javascript program to find the difference b/w left and
// right smaller element of every element in array

    // Function to fill left smaller element for every
    // element of arr[0..n-1]. These values are filled
    // in SE[0..n-1]
    function leftSmaller(arr,n,SE)
    {
        // Create an empty stack
        let S=[]

        // Traverse all array elements
        // compute nearest smaller elements of every element
        for (let i = 0; i < n; i++)
        {
            // Keep removing top element from S while the top
            // element is greater than or equal to arr[i]
            while (S.length!=0 && S[S.length-1] >= arr[i])
            {
                S.pop();
            }

            // Store the smaller element of current element
            if (S.length!=0)
            {
                SE[i] = S[S.length-1];
            }
            // If all elements in S were greater than arr[i]
            else
            {
                SE[i] = 0;
            }

            // Push this element
            S.push(arr[i]);
        }

    }

    // Function returns maximum difference b/w Left &
    // right smaller element
    function findMaxDiff(arr,n)
    {
        // To store left smaller elements
        let LS = new Array(n);
        for(let i=0;i<n;i++)
        {
            LS[i]=0;
        }
        // find left smaller element of every element
        leftSmaller(arr, n, LS);

        // find right smaller element of every element
        // first reverse the array and do the same process
        let RRS = new Array(n); // To store right smaller elements in
        for(let i=0;i<n;i++)
        {
            RRS[i]=0;
        }

        // reverse array
        reverse(arr);
        leftSmaller(arr, n, RRS);

        // find maximum absolute difference b/w LS & RRS
        // In the reversed array right smaller for arr[i] is
        // stored at RRS[n-i-1]
        let result = -1;
        for (let i = 0; i < n; i++)
        {
            result = Math.max(result, Math.abs(LS[i] - RRS[n - 1 - i]));
        }

        // return maximum difference b/w LS & RRS
        return result;
    }

    function reverse(a)
    {
        let i, k, n = a.length;
        let t;
        for (i = 0; i < Math.floor(n / 2); i++)
        {
            t = a[i];
            a[i] = a[n - i - 1];
            a[n - i - 1] = t;
        }
    }

    // Driver code
    let arr=[2, 4, 8, 7, 7, 9, 3];
    let n = arr.length;
    document.write("Maximum diff : "
                + findMaxDiff(arr, n));

    // This code is contributed by rag2127
</script>
```

**输出:**

```
Maximum Diff  : 4
```

**时间复杂度:** O(n)

本文由 **Nishant_singh(pintu)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。