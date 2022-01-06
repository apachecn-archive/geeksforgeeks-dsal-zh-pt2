# 计数元素小于或等于 X 的子阵列

> 原文:[https://www . geeksforgeeks . org/count-子数组-其中有元素-小于或等于-x/](https://www.geeksforgeeks.org/count-sub-arrays-which-have-elements-less-than-or-equal-to-x/)

给定一个由 n 个元素和一个整数 x 组成的数组。计算该数组中所有元素都小于或等于 x 的子数组的数量。
**示例:**

```
Input : arr[] = {1, 5, 7, 8, 2, 3, 9}  
            X = 6
Output : 6
Explanation : Sub-arrays are {1}, {5}, {2}, {3},
{1, 5}, {2, 3}

Input : arr[] =  {1, 10, 12, 4, 5, 3, 2, 7}   
            X = 9
Output : 16
```

**朴素方法**:简单的方法是使用两个嵌套循环来生成给定数组的所有子数组，一个循环检查子数组的所有元素是否小于或等于 X。
时间复杂度:O(n*n*n)
**高效方法**:一个高效的方法是观察我们只是想要那些所有元素都小于等于 x 的子数组的计数，我们可以创建一个对应于原始数组的 0 和 1 的二进制数组。如果原始数组中的元素小于或等于 X，则二进制数组中对应的元素将为 1，否则为 0。现在，我们的问题简化为计算这个全为 1 的二进制数组中子数组的数量。我们还可以看到，对于全为 1 的阵列，它的所有子阵列都只有 1，子阵列的总数为 len*(len+1)/2。例如，{1，1，1，1}将有 10 个子阵列。
下面是解决上述问题的完整算法:

*   如上所述，创建原始数组的相应二进制数组。
*   将计数器变量初始化为 0，并开始遍历二进制数组，跟踪全为 1 的子数组的长度
*   我们可以很容易地用公式 n*(n+1)/2 计算出全 1 数组的子数组个数，其中 n 是全 1 数组的长度。
*   计算每个全为 1 的子数组的长度，并将计数变量增加长度*(长度+1)/2。我们可以在 O(n)时间复杂度内做到这一点

以下是上述方法的实现:

## C++

```
// C++ program to count all sub-arrays which
// has all elements less than or equal to X
#include <iostream>
using namespace std;

// function to count all sub-arrays which
// has all elements less than or equal to X
int countSubArrays(int arr[], int n, int x)
{
    // variable to keep track of length of
    // subarrays with all 1s
    int len = 0;

    // variable to keep track of all subarrays
    int count = 0;

    // binary array of same size
    int binaryArr[n];

    // creating binary array
    for (int i = 0; i < n; i++) {
        if (arr[i] <= x)
            binaryArr[i] = 1;
        else
            binaryArr[i] = 0;
    }

    // start traversing the binary array
    for (int i = 0; i < n; i++) {

        // once we find the first 1, keep checking
        // for number of consecutive 1s
        if (binaryArr[i] == 1) {
            int j;

            for (j = i + 1; j < n; j++)
                if (binaryArr[j] != 1)
                    break;

            // calculate length of the subarray
            // with all 1s
            len = j - i;

            // increment count
            count += (len) * (len + 1) / 2;

            // initialize i to j
            i = j;
        }
    }

    return count;
}

// Driver code
int main()
{
    int arr[] = { 1, 5, 7, 8, 2, 3, 9 };
    int x = 6;
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countSubArrays(arr, n, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count all sub-arrays which
// has all elements less than or equal to X
import java.io.*;

class GFG {

    // function to count all sub-arrays which
    // has all elements less than or equal to X
    static int countSubArrays(int arr[], int n, int x)
    {

        // variable to keep track of length of
        // subarrays with all 1s
        int len = 0;

        // variable to keep track of all subarrays
        int count = 0;

        // binary array of same size
        int binaryArr[] = new int[n];

        // creating binary array
        for (int i = 0; i < n; i++) {
            if (arr[i] <= x)
                binaryArr[i] = 1;
            else
                binaryArr[i] = 0;
        }

        // start traversing the binary array
        for (int i = 0; i < n; i++) {

            // once we find the first 1, keep checking
            // for number of consecutive 1s
            if (binaryArr[i] == 1) {
                int j;

                for (j = i + 1; j < n; j++)
                    if (binaryArr[j] != 1)
                        break;

                // calculate length of the subarray
                // with all 1s
                len = j - i;

                // increment count
                count += (len) * (len + 1) / 2;

                // initialize i to j
                i = j;
            }
        }

        return count;
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 1, 5, 7, 8, 2, 3, 9 };
        int x = 6;
        int n = arr.length;

        System.out.println(countSubArrays(arr, n, x));
    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# python 3 program to count all sub-arrays which
# has all elements less than or equal to X

# function to count all sub-arrays which
# has all elements less than or equal to X
def countSubArrays(arr, n, x):

    # variable to keep track of length
    # of subarrays with all 1s
    len = 0

    # variable to keep track of
    # all subarrays
    count = 0

    # binary array of same size
    binaryArr = [0 for i in range(n)]

    # creating binary array
    for i in range(0, n, 1):
        if (arr[i] <= x):
            binaryArr[i] = 1
        else:
            binaryArr[i] = 0

    # start traversing the binary array
    for i in range(0, n, 1):

        # once we find the first 1,
        # keep checking for number
        # of consecutive 1s
        if (binaryArr[i] == 1):
            for j in range(i + 1, n, 1):
                if (binaryArr[j] != 1):
                    break

            # calculate length of the
            # subarray with all 1s
            len = j - i

            # increment count
            count += (len) * (int)((len + 1) / 2)

            # initialize i to j
            i = j

    return count

# Driver code
if __name__ == '__main__':
    arr = [1, 5, 7, 8, 2, 3, 9]
    x = 6
    n = len(arr)
    print(int(countSubArrays(arr, n, x)))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to count all sub-arrays which
// has all elements less than or equal to X1
using System;

class GFG {

    // function to count all sub-arrays which
    // has all elements less than or equal
    // to X
    static int countSubArrays(int []arr,
                                int n, int x)
    {

        // variable to keep track of length
        // of subarrays with all 1s
        int len = 0;

        // variable to keep track of all
        // subarrays
        int count = 0;

        // binary array of same size
        int []binaryArr = new int[n];

        // creating binary array
        for (int i = 0; i < n; i++) {
            if (arr[i] <= x)
                binaryArr[i] = 1;
            else
                binaryArr[i] = 0;
        }

        // start traversing the binary array
        for (int i = 0; i < n; i++) {

            // once we find the first 1, keep
            // checking for number of
            // consecutive 1s
            if (binaryArr[i] == 1) {
                int j;

                for (j = i + 1; j< n; j++)
                    if (binaryArr[j] != 1)
                        break;

                // calculate length of the
                // subarray with all 1s
                len = j - i;

                // increment count
                count += (len) * (len + 1) / 2;

                // initialize i to j
                i = j;
            }
        }

        return count;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 1, 5, 7, 8, 2, 3, 9 };
        int x = 6;
        int n = arr.Length;

        Console.WriteLine(
                    countSubArrays(arr, n, x));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count all sub-arrays which
// has all elements less than or equal to X

// function to count all sub-arrays which
// has all elements less than or equal to X
function countSubArrays($arr, $n, $x)
{

    // variable to keep track of length of
    // subarrays with all 1s
    $len = 0;

    // variable to keep track of all subarrays
    $coun = 0;

    // binary array of same size
    $binaryArr = array($n);

    // creating binary array
    for ($i = 0; $i < $n; $i++)
    {
        if ($arr[$i] <= $x)
            $binaryArr[$i] = 1;
        else
            $binaryArr[$i] = 0;
    }

    // start traversing
    // the binary array
    for ($i = 0; $i < $n; $i++)
    {

        // once we find the first 1,
        // keep checking for number
        // of consecutive 1s
        if ($binaryArr[$i] == 1) {

            for ($j = $i + 1; $j < $n; $j++)
                if ($binaryArr[$j] != 1)
                    break;

            // calculate length of
            // the subarray with all 1s
            $len = $j - $i;

            // increment count
            $coun += ($len) * ($len + 1) / 2;

            // initialize i to j
            $i = $j;
        }
    }

    return $coun;
}

    // Driver code
    $arr = array( 1, 5, 7, 8, 2, 3, 9 );
    $x = 6;
    $n = count($arr);
    echo countSubArrays($arr, $n, $x);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
// javascript program to count all sub-arrays which
// has all elements less than or equal to X

    // function to count all sub-arrays which
    // has all elements less than or equal to X
    function countSubArrays(arr , n , x) {

        // variable to keep track of length of
        // subarrays with all 1s
        var len = 0;

        // variable to keep track of all subarrays
        var count = 0;

        // binary array of same size
        var binaryArr = Array(n).fill(0);

        // creating binary array
        for (i = 0; i < n; i++) {
            if (arr[i] <= x)
                binaryArr[i] = 1;
            else
                binaryArr[i] = 0;
        }

        // start traversing the binary array
        for (i = 0; i < n; i++) {

            // once we find the first 1, keep checking
            // for number of consecutive 1s
            if (binaryArr[i] == 1) {
                var j;

                for (j = i + 1; j < n; j++)
                    if (binaryArr[j] != 1)
                        break;

                // calculate length of the subarray
                // with all 1s
                len = j - i;

                // increment count
                count += (len) * (len + 1) / 2;

                // initialize i to j
                i = j;
            }
        }

        return count;
    }

    // Driver code
        var arr = [ 1, 5, 7, 8, 2, 3, 9 ];
        var x = 6;
        var n = arr.length;

        document.write(countSubArrays(arr, n, x));

// This code is contributed by Rajput-Ji
</script>
```

**输出:**

```
6
```

**时间复杂度** : O(n)，其中 n 为数组中的元素个数。
**辅助空间** : O(n)。
**另一种方法:**我们可以在不使用额外空间保持时间复杂度 O(n)的情况下改进上述解决方案。我们可以跟踪每个这样的区域的开始和结束，并在区域结束时更新计数，而不是将元素标记为 0 和 1。

## C++

```
// C++ program to count all sub-arrays which
// has all elements less than or equal to X

#include<bits/stdc++.h>
using namespace std;

int countSubArrays(int arr[], int x, int n )
    {
        int count = 0;
        int start = -1, end = -1;

        for(int i = 0; i < n; i++)
        {
            if(arr[i] < x)
            {
                if(start == -1)
                {

                    //create a new subArray
                    start = i;
                    end = i;
                }
                else
                {

                    // append to existing subarray
                    end=i;
                }
            }
            else
            {
                if(start != -1 && end != -1)
                {

                    // given start and end calculate
                    // all subarrays within this range
                    int length = end - start + 1;
                    count = count + ((length * (length + 1)) / 2);
                }

                start = -1;
                end = -1;
            }

        }

        if(start != -1 && end != -1)
        {

            // given start and end calculate all
            // subarrays within this range
            int length = end - start + 1;
            count = count + ((length * (length + 1)) / 2);
        }

        return count;
    }

    // Driver code
int main()
    {
        int arr[] = { 1, 5, 7, 8, 2, 3, 9 };
        int x = 6;
        int n = sizeof(arr) / sizeof(arr[0]);
        cout<< countSubArrays(arr, x, n);

//This code is contributed by  29AjayKumar

    }
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count all sub-arrays which
// has all elements less than or equal to X

public class GFG {

    public static int countSubArrays(int arr[], int x)
    {
        int count = 0;
        int start = -1, end = -1;

        for(int i = 0; i < arr.length; i++)
        {
            if(arr[i] < x)
            {
                if(start == -1)
                {

                    //create a new subArray
                    start = i;
                    end = i;
                }
                else
                {

                    // append to existing subarray
                    end=i;
                }
            }
            else
            {
                if(start != -1 && end != -1)
                {

                    // given start and end calculate
                    // all subarrays within this range
                    int length = end - start + 1;
                    count = count + ((length * (length + 1)) / 2);
                }

                start = -1;
                end = -1;
            }

        }

        if(start != -1 && end != -1)
        {

            // given start and end calculate all
            // subarrays within this range
            int length = end - start + 1;
            count = count + ((length * (length + 1)) / 2);
        }

        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 5, 7, 8, 2, 3, 9 };
        int x = 6;
        System.out.println(countSubArrays(arr, x));

    }
}
```

## 蟒蛇 3

```
# Python3 program to count all sub-arrays which
# has all elements less than or equal to X

def countSubArrays(arr, x, n ):
    count = 0;
    start = -1; end = -1;

    for i in range(n):
        if(arr[i] < x):
            if(start == -1):

                # create a new subArray
                start = i;
                end = i;
            else:

                # append to existing subarray
                end = i;
        else:
            if(start != -1 and end != -1):

                # given start and end calculate
                # all subarrays within this range
                length = end - start + 1;
                count = count + ((length *
                                 (length + 1)) / 2);
            start = -1;
            end = -1;

    if(start != -1 and end != -1):

        # given start and end calculate all
        # subarrays within this range
        length = end - start + 1;
        count = count + ((length *
                         (length + 1)) / 2);

    return count;

# Driver code
arr = [ 1, 5, 7, 8, 2, 3, 9 ];
x = 6;
n = len(arr);
print(countSubArrays(arr, x, n));

# This code is contributed
# by PrinciRaj1992
```

## C#

```
// C# program to count all sub-arrays which
// has all elements less than or equal to X
using System;

class GFG
{

    public static int countSubArrays(int []arr, int x)
    {
        int count = 0;
        int start = -1, end = -1;

        for(int i = 0; i < arr.Length; i++)
        {
            if(arr[i] < x)
            {
                if(start == -1)
                {

                    //create a new subArray
                    start = i;
                    end = i;
                }
                else
                {

                    // append to existing subarray
                    end=i;
                }
            }
            else
            {
                if(start != -1 && end != -1)
                {

                    // given start and end calculate
                    // all subarrays within this range
                    int length = end - start + 1;
                    count = count + ((length * (length + 1)) / 2);
                }

                start = -1;
                end = -1;
            }

        }

        if(start != -1 && end != -1)
        {

            // given start and end calculate all
            // subarrays within this range
            int length = end - start + 1;
            count = count + ((length * (length + 1)) / 2);
        }

        return count;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = { 1, 5, 7, 8, 2, 3, 9 };
        int x = 6;
        Console.WriteLine(countSubArrays(arr, x));
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript program to count all sub-arrays which
    // has all elements less than or equal to X

    function countSubArrays(arr, x)
    {
        let count = 0;
        let start = -1, end = -1;

        for(let i = 0; i < arr.length; i++)
        {
            if(arr[i] < x)
            {
                if(start == -1)
                {

                    //create a new subArray
                    start = i;
                    end = i;
                }
                else
                {

                    // append to existing subarray
                    end=i;
                }
            }
            else
            {
                if(start != -1 && end != -1)
                {

                    // given start and end calculate
                    // all subarrays within this range
                    let length = end - start + 1;
                    count = count + parseInt((length * (length + 1)) / 2, 10);
                }

                start = -1;
                end = -1;
            }

        }

        if(start != -1 && end != -1)
        {

            // given start and end calculate all
            // subarrays within this range
            let length = end - start + 1;
            count = count + parseInt((length * (length + 1)) / 2, 10);
        }

        return count;
    }

    let arr = [ 1, 5, 7, 8, 2, 3, 9 ];
    let x = 6;
    document.write(countSubArrays(arr, x));

</script>
```

**输出:**

```
6
```

**时间复杂度:** O(n)，其中 n 为数组中的元素个数。
**辅助空间:** O(1)。