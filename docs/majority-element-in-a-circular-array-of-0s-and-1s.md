# 0 和 1 的圆形数组中的多数元素

> 原文:[https://www . geeksforgeeks . org/0 和 1 的循环数组中的多数元素/](https://www.geeksforgeeks.org/majority-element-in-a-circular-array-of-0s-and-1s/)

给定一个只包含 0 和 1 的圆形数组，大小为 n，其中 n = p*q (p 和 q 都是奇数)。任务是在应用以下操作后，检查是否有方法使 1 占多数:

1.  将圆形阵列分成 p 个子阵列，每个子阵列的大小为 q。
2.  在每个子阵列中，占大多数的数字将被存储到阵列 b 中
3.  现在，如果 1 在数组 b 中占多数，则称其为多数。

**注意:**如果一个数的出现次数超过数组大小的一半，则该数在数组中占多数。
**例:**

> **输入:** p = 3，q = 3，数组[] = {0，0，1，1，0，1，1，0}
> **输出:**是
> 假设数组的索引从 1 到 N，因为数组是圆形的，所以索引 N 和 1 将是相邻的。
> 将这个圆形阵列分成子阵列，方式如下:-
> {2，3，4}，{5，6，7}和{8，9，1}。【这些是元素的索引】
> 在{2，3，4}中，1 占多数，
> 在{5，6，7}中，同样是 1 占多数，
> 在{8，9，1}中，0 占多数。
> 现在将 1，1，0 插入数组 B，因此数组 B = {1，1，0}
> 在数组 B 中，1 是多数元素，因此打印 Yes。
> **输入:** p = 3，q = 3，数组[] = {1，0，0，1，1，0，1，0，0}
> **输出:**否
> 无论如何划分这个圆形子阵，
> 1 都不会占多数。因此，答案是否定的

**进场:**

1.  首先，迭代循环数组，计算每个 p 子数组(大小为 q)中 1 的总数。
2.  将此数字存储到另一个数组(大小为 p)中。
3.  如果在这种情况下，1 是大多数，那么，打印是。
4.  否则，通过移动前一个集合的索引 1 单位(增加或减少)来获取另一个集合，只跟踪给定集合中新的索引，并更新数组中的 1 的数量。
5.  重复第二步和第三步。

如果没有找到多数 1，我们将重复 q 次，直到找到为止，答案将是否定的，否则(像前面的例子一样)答案将是 1。
因为在最大值时，我们可以重复这个过程 q 次，并且每次我们只跟踪每个 p 子阵列中的两个元素。
**解释:**
在给定的示例-1 中，我们将圆形子阵列划分为[indexes]=>{ 1，2，3}，{4，5，6}，{7，8，9}，并将 1 的数目存储在另一个阵列中，该阵列分别为子阵列中的[1，2，1]。
通过增加 1 个单位来获取示例 1 中的另一个集合，因此集合将是{2，3，4}、{5，6，7}、{8，9，1}现在在集合 1 中，唯一的变化是包含元素 4 并移除元素 1，我们将只跟踪这些，因此更新后的 1 的数量将是 2，2，0。
以下是上述方法的实施:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if 1 is the majority
// element or not
void majority(bool a[], int p, int q, int size)
{
    // assuming starting and ending index of 1st subarray
    int start = 0, ends = q;

    // to store majority of p
    int arr[p];

    // subarrays each of size q ;
    int k = 0;

    // Loop to calculate total number
    // of 1's in subarray which will get
    // stored in array arr[]
    while (k < p) {
        int one = 0;
        for (int j = start; j < ends; j++) {
            if (a[j] == 1) {
                one++;
            }
        }

        // starting index of next subarray
        start = ends;

        // ending index of next subarray
        ends = ends + q;

        // storing 1's
        arr[k] = one;
        k++;
    }

    start = 0;
    ends = q;

    // variable to keep a check
    // if 1 is in majority or not
    bool found = 0;

    // In this case, we are repeating
    // the task of calculating
    // total number of 1's backward
    while (ends > 0) {

        // to store the total number of 1's
        int dist_one = 0;

        // Check if 1 is in majority in
        // this subarray
        for (int i = 0; i < p; i++)
            if (arr[i] > q / 2)
                dist_one++;

        // If 1 is in majority return
        if (dist_one > p / 2) {
            found = 1;
            cout << "Yes" << endl;

            return;
        }

        // shifting starting index of
        // subarray by 1 unit leftwards
        start--;

        // shifting ending index of
        // subarray by 1 unit leftwards
        ends--;

        // to ensure it is a valid index
        // ( array is circular) -1 index means
        // last index of a circular array
        if (start < 0)
            start = size + start;

        int st = start, en = ends, l = 0;

        // now to track changes occur
        // due to shifting of the subarray
        while (en < size) {

            if (a[st % size] != a[en % size]) {

                // st refers to starting index of
                // new subarray and en refers to
                // last element of same subarray
                // but in previous iteration
                if (a[st % size] == 1)
                    arr[l]++;

                else
                    arr[l]--;
            }
            l++;

            // now repeating the same
            // for other subarrays too
            st = (st + q);
            en = en + q;
        }
    }

    if (found == 0) {
        cout << "No" << endl;
    }
}

// Driver code
int main()
{
    int p = 3, q = 3;
    int n = p * q;

    bool a[] = { 0, 0, 1, 1, 0, 1, 1, 0, 0 };

    // circular array of given size
    majority(a, p, q, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{
// Function to check if 1 is the majority
// element or not
static void majority(int a[], int p, int q, int size)
{
    // assuming starting and ending index of 1st subarray
    int start = 0, ends = q;

    // to store majority of p
    int []arr = new int[p];

    // subarrays each of size q ;
    int k = 0;

    // Loop to calculate total number
    // of 1's in subarray which will get
    // stored in array arr[]
    while (k < p) {
        int one = 0;
        for (int j = start; j < ends; j++) {
            if (a[j] == 1) {
                one++;
            }
        }

        // starting index of next subarray
        start = ends;

        // ending index of next subarray
        ends = ends + q;

        // storing 1's
        arr[k] = one;
        k++;
    }

    start = 0;
    ends = q;

    // variable to keep a check
    // if 1 is in majority or not
    boolean  found = false;

    // In this case, we are repeating
    // the task of calculating
    // total number of 1's backward
    while (ends > 0) {

        // to store the total number of 1's
        int dist_one = 0;

        // Check if 1 is in majority in
        // this subarray
        for (int i = 0; i < p; i++)
            if (arr[i] > q / 2)
                dist_one++;

        // If 1 is in majority return
        if (dist_one > p / 2) {
            found = true;
            System.out.println( "Yes" );

            return;
        }

        // shifting starting index of
        // subarray by 1 unit leftwards
        start--;

        // shifting ending index of
        // subarray by 1 unit leftwards
        ends--;

        // to ensure it is a valid index
        // ( array is circular) -1 index means
        // last index of a circular array
        if (start < 0)
            start = size + start;

        int st = start, en = ends,l = 0;

        // now to track changes occur
        // due to shifting of the subarray
        while (en < size) {

            if (a[st % size] != a[en % size]) {

                // st refers to starting index of
                // new subarray and en refers to
                // last element of same subarray
                // but in previous iteration
                if (a[st % size] == 1)
                    arr[l]++;

                else
                    arr[l]--;
            }
            l++;

            // now repeating the same
            // for other subarrays too
            st = (st + q);
            en = en + q;
        }
    }

    if (found == false ) {
        System.out.println( "No" );
    }
}

// Driver code
public static void main(String args[])
{
    int p = 3, q = 3;
    int n = p * q;

    int a[] = { 0, 0, 1, 1, 0, 1, 1, 0, 0 };

    // circular array of given size
    majority(a, p, q, n);

}
}
```

## 蟒蛇 3

```
# Python3 implementation of
# above approach

# Function to check if 1 is
# the majority element or not
def majority(a, p, q, size) :

    # assuming starting and
    # ending index of 1st subarray
    start = 0
    ends = q

    # to store arr = []
    arr = [None] * p

    # subarrays each of size q
    k = 0

    # Loop to calculate total number
    # of 1's in subarray which
    # will get stored in array arr
    while (k < p):
        one = 0
        for j in range(start, ends):
            if (a[j] == 1):
                one = one + 1

        # starting index of
        # next subarray
        start = ends

        # ending index of next
        # subarray
        ends = ends + q

        # storing 1's
        arr[k] = one
        k = k + 1

    start = 0
    ends = q

    # variable to keep a check
    # if 1 is in majority or not
    found = 0

    # In this case, we are
    # repeating the task of
    # calculating total number
    # of 1's backward
    while (ends > 0) :

        # to store the total
        # number of 1's
        dist_one = 0

        # Check if 1 is in majority
        # in this subarray
        for i in range(0, p):
            if (arr[i] > q / 2):
                dist_one = dist_one + 1

        # If 1 is in majority return
        if (dist_one > p / 2) :
            found = 1
            print("Yes")
            return

        # shifting starting index of
        # subarray by 1 unit leftwards
        start = start - 1

        # shifting ending index
        # of subarray by 1 unit
        # leftwards
        ends = ends - 1

        # to ensure it is a valid
        # index( array is circular) -1
        # index means last index of
        # a circular array
        if (start < 0):
            start = size + start

        st = start
        en = ends
        l = 0

        # now to track changes occur
        # due to shifting of the
        # subarray
        while (en < size) :

            if (a[st % size] != a[en % size]) :

                # st refers to starting index of
                # new subarray and en refers to
                # last element of same subarray
                # but in previous iteration
                if (a[st % size] == 1):
                    arr[l] = arr[l] + 1

                else:
                    arr[l] = arr[l] - 1

            l = l + 1

            # now repeating the same
            # for other subarrays too
            st = (st + q)
            en = en + q

    if (found == 0) :
        print("No")

# Driver code
p = 3
q = 3
n = p * q

a = [ 0, 0, 1, 1, 0, 1, 1, 0, 0 ]

# circular array of given size
majority(a, p, q, n)

# This code is contributed
# by Yatin Gupta
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{
// Function to check if 1 is the
// majority element or not
public static void majority(int[] a, int p,
                            int q, int size)
{
    // assuming starting and ending
    // index of 1st subarray
    int start = 0, ends = q;

    // to store majority of p
    int[] arr = new int[p];

    // subarrays each of size q ;
    int k = 0;

    // Loop to calculate total number
    // of 1's in subarray which will
    // get stored in array arr[]
    while (k < p)
    {
        int one = 0;
        for (int j = start; j < ends; j++)
        {
            if (a[j] == 1)
            {
                one++;
            }
        }

        // starting index of next subarray
        start = ends;

        // ending index of next subarray
        ends = ends + q;

        // storing 1's
        arr[k] = one;
        k++;
    }

    start = 0;
    ends = q;

    // variable to keep a check
    // if 1 is in majority or not
    bool found = false;

    // In this case, we are repeating
    // the task of calculating
    // total number of 1's backward
    while (ends > 0)
    {

        // to store the total number of 1's
        int dist_one = 0;

        // Check if 1 is in majority in
        // this subarray
        for (int i = 0; i < p; i++)
        {
            if (arr[i] > q / 2)
            {
                dist_one++;
            }
        }

        // If 1 is in majority return
        if (dist_one > p / 2)
        {
            found = true;
            Console.WriteLine("Yes");

            return;
        }

        // shifting starting index of
        // subarray by 1 unit leftwards
        start--;

        // shifting ending index of
        // subarray by 1 unit leftwards
        ends--;

        // to ensure it is a valid index
        // ( array is circular) -1 index means
        // last index of a circular array
        if (start < 0)
        {
            start = size + start;
        }

        int st = start, en = ends, l = 0;

        // now to track changes occur
        // due to shifting of the subarray
        while (en < size)
        {

            if (a[st % size] != a[en % size])
            {

                // st refers to starting index of
                // new subarray and en refers to
                // last element of same subarray
                // but in previous iteration
                if (a[st % size] == 1)
                {
                    arr[l]++;
                }

                else
                {
                    arr[l]--;
                }
            }
            l++;

            // now repeating the same
            // for other subarrays too
            st = (st + q);
            en = en + q;
        }
    }

    if (found == false)
    {
        Console.WriteLine("No");
    }
}

// Driver code
public static void Main(string[] args)
{
    int p = 3, q = 3;
    int n = p * q;

    int[] a = new int[] {0, 0, 1, 1,
                         0, 1, 1, 0, 0};

    // circular array of given size
    majority(a, p, q, n);
}
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP  implementation of above approach

// Function to check if 1 is the majority
// element or not

function  majority($a, $p, $q, $size)
{
    // assuming starting and ending index of 1st subarray
     $start = 0; $ends = $q;

    // to store majority of p
    $arr=array(0);

    // subarrays each of size q ;
    $k = 0;

    // Loop to calculate total number
    // of 1's in subarray which will get
    // stored in array arr[]
    while ($k < $p) {
        $one = 0;
        for ($j = $start; $j < $ends; $j++) {
            if ($a[$j] == 1) {
                $one++;
            }
        }

        // starting index of next subarray
        $start = $ends;

        // ending index of next subarray
        $ends = $ends + $q;

        // storing 1's
        $arr[$k] = $one;
        $k++;
    }

    $start = 0;
    $ends = $q;

    // variable to keep a check
    // if 1 is in majority or not
     $found = 0;

    // In this case, we are repeating
    // the task of calculating
    // total number of 1's backward
    while ($ends > 0) {

        // to store the total number of 1's
        $dist_one = 0;

        // Check if 1 is in majority in
        // this subarray
        for ($i = 0; $i < $p; $i++)
            if ($arr[$i] > $q / 2)
                $dist_one++;

        // If 1 is in majority return
        if ($dist_one > $p / 2) {
            $found = 1;
            echo  "Yes" ,"\n";

            return;
        }

        // shifting starting index of
        // subarray by 1 unit leftwards
        $start--;

        // shifting ending index of
        // subarray by 1 unit leftwards
        $ends--;

        // to ensure it is a valid index
        // ( array is circular) -1 index means
        // last index of a circular array
        if ($start < 0)
            $start = $size + $start;

         $st = $start; $en = $ends; $l = 0;

        // now to track changes occur
        // due to shifting of the subarray
        while ($en < $size) {

            if ($a[$st % $size] != $a[$en % $size]) {

                // st refers to starting index of
                // new subarray and en refers to
                // last element of same subarray
                // but in previous iteration
                if ($a[$st % $size] == 1)
                    $arr[$l]++;

                else
                    $arr[$l]--;
            }
            $l++;

            // now repeating the same
            // for other subarrays too
            $st = ($st + $q);
            $en = $en + $q;
        }
    }

    if ($found == 0) {
        echo  "No" ,"\n";
    }
}

// Driver code
    $p = 3; $q = 3;
    $n = $p * $q;

     $a = array( 0, 0, 1, 1, 0, 1, 1, 0, 0 );

    // circular array of given size
    majority($a, $p, $q, $n);

#This Code is Contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript implementation
    // of above approach

    // Function to check if 1 is the
    // majority element or not
    function majority(a, p, q, size)
    {
        // assuming starting and ending
        // index of 1st subarray
        let start = 0, ends = q;

        // to store majority of p
        let arr = new Array(p);
        arr.fill(0);

        // subarrays each of size q ;
        let k = 0;

        // Loop to calculate total number
        // of 1's in subarray which will
        // get stored in array arr[]
        while (k < p)
        {
            let one = 0;
            for (let j = start; j < ends; j++)
            {
                if (a[j] == 1)
                {
                    one++;
                }
            }

            // starting index of next subarray
            start = ends;

            // ending index of next subarray
            ends = ends + q;

            // storing 1's
            arr[k] = one;
            k++;
        }

        start = 0;
        ends = q;

        // variable to keep a check
        // if 1 is in majority or not
        let found = false;

        // In this case, we are repeating
        // the task of calculating
        // total number of 1's backward
        while (ends > 0)
        {

            // to store the total number of 1's
            let dist_one = 0;

            // Check if 1 is in majority in
            // this subarray
            for (let i = 0; i < p; i++)
            {
                if (arr[i] > parseInt(q / 2, 10))
                {
                    dist_one++;
                }
            }

            // If 1 is in majority return
            if (dist_one > parseInt(p / 2, 10))
            {
                found = true;
                document.write("Yes");

                return;
            }

            // shifting starting index of
            // subarray by 1 unit leftwards
            start--;

            // shifting ending index of
            // subarray by 1 unit leftwards
            ends--;

            // to ensure it is a valid index
            // ( array is circular) -1 index means
            // last index of a circular array
            if (start < 0)
            {
                start = size + start;
            }

            let st = start, en = ends, l = 0;

            // now to track changes occur
            // due to shifting of the subarray
            while (en < size)
            {

                if (a[st % size] != a[en % size])
                {

                    // st refers to starting index of
                    // new subarray and en refers to
                    // last element of same subarray
                    // but in previous iteration
                    if (a[st % size] == 1)
                    {
                        arr[l]++;
                    }

                    else
                    {
                        arr[l]--;
                    }
                }
                l++;

                // now repeating the same
                // for other subarrays too
                st = (st + q);
                en = en + q;
            }
        }

        if (found == false)
        {
            document.write("No");
        }
    }

    let p = 3, q = 3;
    let n = p * q;

    let a = [0, 0, 1, 1, 0, 1, 1, 0, 0];

    // circular array of given size
    majority(a, p, q, n);

</script>
```

**Output:** 

```
Yes
```