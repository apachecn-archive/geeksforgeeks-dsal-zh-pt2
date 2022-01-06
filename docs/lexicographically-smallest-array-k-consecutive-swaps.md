# 最多连续 K 次交换后的字典最小数组

> 原文:[https://www . geeksforgeeks . org/词典-最小-数组-k-连续-互换/](https://www.geeksforgeeks.org/lexicographically-smallest-array-k-consecutive-swaps/)

给定一个数组 arr[]，找到在执行最大 k 次连续交换后可以获得的字典上最小的数组。
**例:**

```
Input: arr[] = {7, 6, 9, 2, 1}
        k = 3
Output: arr[] = {2, 7, 6, 9, 1}
Explanation: Array is: 7, 6, 9, 2, 1
Swap 1:   7, 6, 2, 9, 1
Swap 2:   7, 2, 6, 9, 1
Swap 3:   2, 7, 6, 9, 1
So Our final array after k = 3 swaps : 
2, 7, 6, 9, 1

Input: arr[] = {7, 6, 9, 2, 1}
        k = 1
Output: arr[] = {6, 7, 9, 2, 1}
```

We strongly recommend that you click here and practice it, before moving on to the solution.

**天真的方法**是生成数组的所有置换，选出满足最多 k 个置换条件的最小置换。这种方法的时间复杂度为ω(n！)，这肯定会让大价值的 n.
超时一个**高效的**方法是贪婪地思考。我们首先从数组 a <sub>1</sub> 、a <sub>2</sub> 、a<sub>3</sub>……(a<sub>k</sub>或 a <sub>n</sub> )【当 k 较小时，我们考虑 a <sub>k</sub> ，否则 n。将所有这些元素向右移动 1 个位置后，我们将最小的元素放置到 a <sub>0</sub> 位置。我们从 k 中减去交换次数(交换次数是班次数减 1)。如果仍然剩下 k > 0，那么我们从下一个起始位置，即 a <sub>2</sub> 、a <sub>3</sub> 、……(a<sub>k</sub>或 a <sub>n</sub> 开始应用相同的程序，然后将其放置到 a <sub>1</sub> 位置。所以我们继续应用同样的过程，直到 k 变成 0。

## C++

```
// C++ program to find lexicographically minimum
// value after k swaps.
#include<bits/stdc++.h>
using namespace std ;

// Modifies arr[0..n-1] to lexicographically smallest
// with k swaps.
void minimizeWithKSwaps(int arr[], int n, int k)
{
    for (int i = 0; i<n-1 && k>0; ++i)
    {
        // Set the position where we want
        // to put the smallest integer
        int pos = i;
        for (int j = i+1; j<n ; ++j)
        {
            // If we exceed the Max swaps
            // then terminate the loop
            if (j-i > k)
                break;

            // Find the minimum value from i+1 to
            // max k or n
            if (arr[j] < arr[pos])
                pos = j;
        }

        // Swap the elements from Minimum position
        // we found till now to the i index
        for (int j = pos; j>i; --j)
            swap(arr[j], arr[j-1]);

        // Set the final value after swapping pos-i
        // elements
        k -=  pos-i;
    }
}

// Driver code
int main()
{
    int arr[] = {7, 6, 9, 2, 1};
    int n = sizeof(arr)/sizeof(arr[0]);
    int k = 3;

    minimizeWithKSwaps(arr, n, k);

    //Print the final Array
    for (int i=0; i<n; ++i)
        cout << arr[i] <<" ";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find lexicographically minimum
// value after k swaps.
class GFG {

    // Modifies arr[0..n-1] to lexicographically
    // smallest with k swaps.
    static void minimizeWithKSwaps(int arr[], int n, int k)
    {
        for (int i = 0; i < n-1 && k > 0; ++i)
        {

            // Set the position where we want
            // to put the smallest integer
            int pos = i;
            for (int j = i+1; j < n ; ++j)
            {

                // If we exceed the Max swaps
                // then terminate the loop
                if (j - i > k)
                    break;

                // Find the minimum value from i+1 to
                // max k or n
                if (arr[j] < arr[pos])
                    pos = j;
            }

            // Swap the elements from Minimum position
            // we found till now to the i index
            int temp;

            for (int j = pos; j>i; --j)
            {
                temp=arr[j];
                arr[j]=arr[j-1];
                arr[j-1]=temp;
            }

            // Set the final value after swapping pos-i
            // elements
            k -= pos-i;
        }
    }

    // Driver method
    public static void main(String[] args)
    {

        int arr[] = {7, 6, 9, 2, 1};
        int n = arr.length;
        int k = 3;

        minimizeWithKSwaps(arr, n, k);

        //Print the final Array
        for (int i=0; i<n; ++i)
            System.out.print(arr[i] +" ");
    }
}

// This code is contributed by Anant Agarwal.
```

## 计算机编程语言

```
# Python program to find lexicographically minimum
# value after k swaps.
def minimizeWithKSwaps(arr, n, k):

    for i in range(n-1):

        # Set the position where we we want
    # to put the smallest integer
        pos = i
        for j in range(i+1, n):

            # If we exceed the Max swaps
        # then terminate the loop
            if (j-i > k):
                break

            # Find the minimum value from i+1 to
            # max (k or n)
            if (arr[j] < arr[pos]):
                pos = j

        # Swap the elements from Minimum position
        # we found till now to the i index
        for j in range(pos, i, -1):
            arr[j],arr[j-1] = arr[j-1], arr[j]

        # Set the final value after swapping pos-i
        # elements
        k -= pos - i

# Driver Code
n, k = 5, 3
arr = [7, 6, 9, 2, 1]
minimizeWithKSwaps(arr, n, k)

# Print the final Array
for i in range(n):
    print(arr[i], end = " ")
```

## C#

```
// C# program to find lexicographically
// minimum value after k swaps.
using System;

class GFG {

    // Modifies arr[0..n-1] to lexicographically
    // smallest with k swaps.
    static void minimizeWithKSwaps(int []arr, int n,
                                              int k)
    {
        for (int i = 0; i < n-1 && k > 0; ++i)
        {
            // Set the position where we want
            // to put the smallest integer
            int pos = i;
            for (int j = i+1; j < n ; ++j)
            {
                // If we exceed the Max swaps
                // then terminate the loop
                if (j - i > k)
                    break;

                // Find the minimum value from
                // i + 1 to max k or n
                if (arr[j] < arr[pos])
                    pos = j;
            }

            // Swap the elements from Minimum position
            // we found till now to the i index
            int temp;

            for (int j = pos; j>i; --j)
            {
                temp=arr[j];
                arr[j]=arr[j-1];
                arr[j-1]=temp;
            }

            // Set the final value after
            // swapping pos-i elements
            k -= pos-i;
        }
    }

    // Driver method
    public static void Main()
    {
        int []arr = {7, 6, 9, 2, 1};
        int n = arr.Length;
        int k = 3;

        // Function calling
        minimizeWithKSwaps(arr, n, k);

        // Print the final Array
        for (int i=0; i<n; ++i)
          Console.Write(arr[i] +" ");
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php program to find lexicographically minimum
// value after k swaps.

// Modifies arr[0..n-1] to lexicographically
// smallest with k swaps.
function minimizeWithKSwaps($arr, $n, $k)
{
    for ($i = 0; $i < $n-1 && $k > 0; ++$i)
    {
        // Set the position where we want
        // to put the smallest integer
        $pos = $i;
        for ($j = $i+1; $j < $n ; ++$j)
        {
            // If we exceed the Max swaps
            // then terminate the loop
            if ($j-$i > $k)
                break;

            // Find the minimum value from
            // i+1 to max k or n
            if ($arr[$j] < $arr[$pos])
                $pos = $j;
        }

        // Swap the elements from Minimum
        // position we found till now to
        // the i index
        for ($j = $pos; $j > $i; --$j)
        {
            $temp = $arr[$j];
            $arr[$j] = $arr[$j-1];
            $arr[$j-1] = $temp;
        }

        // Set the final value after
        // swapping pos-i elements
        $k -= $pos-$i;
    }

    //Print the final Array
    for ($i = 0; $i < $n; ++$i)
        echo $arr[$i] . " ";
}

// Driver code
$arr = array(7, 6, 9, 2, 1);
$n = count($arr);
$k = 3;

minimizeWithKSwaps($arr, $n, $k);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
    // Javascript program to find lexicographically
    // minimum value after k swaps.

    // Modifies arr[0..n-1] to lexicographically
    // smallest with k swaps.
    function minimizeWithKSwaps(arr, n, k)
    {
        for (let i = 0; i < n - 1 && k > 0; ++i)
        {

            // Set the position where we want
            // to put the smallest integer
            let pos = i;
            for (let j = i+1; j < n ; ++j)
            {
                // If we exceed the Max swaps
                // then terminate the loop
                if (j - i > k)
                    break;

                // Find the minimum value from
                // i + 1 to max k or n
                if (arr[j] < arr[pos])
                    pos = j;
            }

            // Swap the elements from Minimum position
            // we found till now to the i index
            let temp;

            for (let j = pos; j > i; --j)
            {
                temp = arr[j];
                arr[j] = arr[j - 1];
                arr[j - 1] = temp;
            }

            // Set the final value after
            // swapping pos-i elements
            k -= pos - i;
        }
    }

    let arr = [7, 6, 9, 2, 1];
    let n = arr.length;
    let k = 3;

    // Function calling
    minimizeWithKSwaps(arr, n, k);

    // Print the final Array
    document.write("Output: ");
    for (let i = 0; i < n; ++i)
      document.write(arr[i] + " ");

    // This code is contributed by divyesh072019.
</script>
```

```
Output: 2 7 6 9 1
```

**时间复杂度:** O(N <sup>2</sup> )
**辅助空间:** O(1)
**参考文献:**
[http://stack overflow . com/questions/25539423/finding-minimum-辞书-数组](http://stackoverflow.com/questions/25539423/finding-minimal-lexicographical-array)
本文由 [Shubham Bansal](https://www.facebook.com/banalshubham) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。