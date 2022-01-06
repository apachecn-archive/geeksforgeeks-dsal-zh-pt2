# 计算大小为 2 或 3 的所有可能的组，其和为 3 的倍数

> 原文:[https://www . geesforgeks . org/count-可能组-size-2-3-sum-multiple-3/](https://www.geeksforgeeks.org/count-possible-groups-size-2-3-sum-multiple-3/)

给定一个大小为“n”的未排序整数(仅正值)数组，我们可以形成一个由两个或三个元素组成的组，该组中所有元素的和应该是 3 的倍数。计算以这种方式生成的所有可能的组数。
**例:**

```
Input: arr[] = {3, 6, 7, 2, 9}
Output: 8
// Groups are {3,6}, {3,9}, {9,6}, {7,2}, {3,6,9},
//            {3,7,2}, {7,2,6}, {7,2,9}

Input: arr[] = {2, 1, 3, 4}
Output: 4
// Groups are {2,1}, {2,4}, {2,1,3}, {2,4,3}
```

这个想法是看到每个元素除以 3 后的余数。一组元素只有在余数的太阳是 3 的倍数时才能组成一个群。
**例如:** 8、4、12。现在，余数分别是 2，1 和 0。这意味着 8 距离 3s 倍数(6)为 2，4 距离 3s 倍数(3)为 1，12 距离为 0。所以，我们可以把和写成 8(可以写成 6+2)，4(可以写成 3+1)，12(可以写成 12+0)。现在 8，4 和 12 的和可以写成 6+2+3+1+12+0。现在，6+3+12 总是能被 3 整除，因为所有的项都是 3 的倍数。现在，我们只需要检查 2+1+0(余数)是否能被 3 整除，这就使得整个和能被 3 整除。
由于任务是枚举组，所以我们统计所有余数不同的元素。

```
1\. Hash all elements in a count array based on remainder, i.e, 
   for all elements a[i], do c[a[i]%3]++;
2\. Now c[0] contains the number of elements which when divided
   by 3 leave remainder 0 and similarly c[1] for remainder 1 
   and c[2] for 2.
3\. Now for group of 2, we have 2 possibilities
   a. 2 elements of remainder 0 group. Such possibilities are 
      c[0]*(c[0]-1)/2
   b. 1 element of remainder 1 and 1 from remainder 2 group
      Such groups are c[1]*c[2].
4\. Now for group of 3,we have 4 possibilities
   a. 3 elements from remainder group 0.
      No. of such groups are c[0]C3
   b. 3 elements from remainder group 1.
      No. of such groups are c[1]C3
   c. 3 elements from remainder group 2.
      No. of such groups are c[2]C3
   d. 1 element from each of 3 groups. 
      No. of such groups are c[0]*c[1]*c[2].
5\. Add all the groups in steps 3 and 4 to obtain the result.
```

## C++

```
// C++ Program to count all possible
// groups of size 2 or 3 that have
// sum as multiple of 3

#include<bits/stdc++.h>
using namespace std;

// Returns count of all possible groups
// that can be formed from elements of a[].
int findgroups(int arr[], int n)
{
    // Create an array C[3] to store counts
    // of elements with remainder 0, 1 and 2.
    // c[i] would store count of elements
    // with remainder i
    int c[3] = {0}, i;

    int res = 0; // To store the result

    // Count elements with remainder 0, 1 and 2
    for (i=0; i<n; i++)
        c[arr[i]%3]++;

    // Case 3.a: Count groups of size 2
    // from 0 remainder elements
    res += ((c[0]*(c[0]-1))>>1);

    // Case 3.b: Count groups of size 2 with
    // one element with 1 remainder and other
    // with 2 remainder
    res += c[1] * c[2];

    // Case 4.a: Count groups of size 3
    // with all 0 remainder elements
    res += (c[0] * (c[0]-1) * (c[0]-2))/6;

    // Case 4.b: Count groups of size 3
    // with all 1 remainder elements
    res += (c[1] * (c[1]-1) * (c[1]-2))/6;

    // Case 4.c: Count groups of size 3
    // with all 2 remainder elements
    res += ((c[2]*(c[2]-1)*(c[2]-2))/6);

    // Case 4.c: Count groups of size 3
    // with different remainders
    res += c[0]*c[1]*c[2];

    // Return total count stored in res
    return res;
}

// Driver Code
int main()
{
    int arr[] = {3, 6, 7, 2, 9};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << "Required number of groups are "
         << findgroups(arr,n) << endl;
    return 0;
}

// This code is contributed
// by Akanksha Rai
```

## C

```
// C Program to count all possible
// groups of size 2 or 3 that have
// sum as multiple of 3

#include<stdio.h>

// Returns count of all possible groups that can be formed from elements
// of a[].
int findgroups(int arr[], int n)
{
    // Create an array C[3] to store counts of elements with remainder
    // 0, 1 and 2.  c[i] would store count of elements with remainder i
    int c[3] = {0}, i;

    int res = 0; // To store the result

    // Count elements with remainder 0, 1 and 2
    for (i=0; i<n; i++)
        c[arr[i]%3]++;

    // Case 3.a: Count groups of size 2 from 0 remainder elements
    res += ((c[0]*(c[0]-1))>>1);

    // Case 3.b: Count groups of size 2 with one element with 1
    // remainder and other with 2 remainder
    res += c[1] * c[2];

    // Case 4.a: Count groups of size 3 with all 0 remainder elements
    res += (c[0] * (c[0]-1) * (c[0]-2))/6;

    // Case 4.b: Count groups of size 3 with all 1 remainder elements
    res += (c[1] * (c[1]-1) * (c[1]-2))/6;

    // Case 4.c: Count groups of size 3 with all 2 remainder elements
    res += ((c[2]*(c[2]-1)*(c[2]-2))/6);

    // Case 4.c: Count groups of size 3 with different remainders
    res += c[0]*c[1]*c[2];

    // Return total count stored in res
    return res;
}

// Driver program to test above functions
int main()
{
    int arr[] = {3, 6, 7, 2, 9};
    int n = sizeof(arr)/sizeof(arr[0]);
    printf("Required number of groups are %d\n", findgroups(arr,n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to count all possible
// groups of size 2 or 3 that have
// sum as multiple of 3
class FindGroups
{
    // Returns count of all possible groups that can be formed from elements
    // of a[].

    int findgroups(int arr[], int n)
    {
        // Create an array C[3] to store counts of elements with remainder
        // 0, 1 and 2.  c[i] would store count of elements with remainder i
        int c[] = new int[]{0, 0, 0};
        int i;

        int res = 0; // To store the result

        // Count elements with remainder 0, 1 and 2
        for (i = 0; i < n; i++)
            c[arr[i] % 3]++;

        // Case 3.a: Count groups of size 2 from 0 remainder elements
        res += ((c[0] * (c[0] - 1)) >> 1);

        // Case 3.b: Count groups of size 2 with one element with 1
        // remainder and other with 2 remainder
        res += c[1] * c[2];

        // Case 4.a: Count groups of size 3 with all 0 remainder elements
        res += (c[0] * (c[0] - 1) * (c[0] - 2)) / 6;

        // Case 4.b: Count groups of size 3 with all 1 remainder elements
        res += (c[1] * (c[1] - 1) * (c[1] - 2)) / 6;

        // Case 4.c: Count groups of size 3 with all 2 remainder elements
        res += ((c[2] * (c[2] - 1) * (c[2] - 2)) / 6);

        // Case 4.c: Count groups of size 3 with different remainders
        res += c[0] * c[1] * c[2];

        // Return total count stored in res
        return res;
    }

    public static void main(String[] args)
    {
        FindGroups groups = new FindGroups();
        int arr[] = {3, 6, 7, 2, 9};
        int n = arr.length;
        System.out.println("Required number of groups are "
                + groups.findgroups(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python3 Program to Count groups
# of size 2 or 3 that have sum
# as multiple of 3

# Returns count of all possible
# groups that can be formed
# from elements of a[].
def findgroups(arr, n):

    # Create an array C[3] to store
    # counts of elements with
    # remainder 0, 1 and 2\. c[i]
    # would store count of elements
    # with remainder i
    c = [0, 0, 0]

    # To store the result
    res = 0

    # Count elements with remainder
    # 0, 1 and 2
    for i in range(0, n):
        c[arr[i] % 3] += 1

    # Case 3.a: Count groups of size
    # 2 from 0 remainder elements
    res += ((c[0] * (c[0] - 1)) >> 1)

    # Case 3.b: Count groups of size
    # 2 with one element with 1
    # remainder and other with 2 remainder
    res += c[1] * c[2]

    # Case 4.a: Count groups of size
    # 3 with all 0 remainder elements
    res += (c[0] * (c[0] - 1) * (c[0] - 2)) / 6

    # Case 4.b: Count groups of size 3
    # with all 1 remainder elements
    res += (c[1] * (c[1] - 1) * (c[1] - 2)) / 6

    # Case 4.c: Count groups of size 3
    # with all 2 remainder elements
    res += ((c[2] * (c[2] - 1) * (c[2] - 2)) / 6)

    # Case 4.c: Count groups of size 3
    # with different remainders
    res += c[0] * c[1] * c[2]

    # Return total count stored in res
    return res

# Driver program
arr = [3, 6, 7, 2, 9]
n = len(arr)

print ("Required number of groups are",
               int(findgroups(arr, n)))

# This article is contributed by shreyanshi_arun
```

## C#

```
// C# Program to count all possible
// groups of size 2 or 3 that have
// sum as multiple of 3
using System;

class FindGroups
{

    // Returns count of all possible
    // groups that can be formed
    // from elements of a[].

    int findgroups(int []arr, int n)
    {

        // Create an array C[3] to store
        // counts of elements with remainder
        // 0, 1 and 2\. c[i] would store
        // count of elements with remainder i
        int [] c= new int[]{0, 0, 0};
        int i;

        // To store the result
        int res = 0;

        // Count elements with
        // remainder 0, 1 and 2
        for (i = 0; i < n; i++)
            c[arr[i] % 3]++;

        // Case 3.a: Count groups of size
        // 2 from 0 remainder elements
        res += ((c[0] * (c[0] - 1)) >> 1);

        // Case 3.b: Count groups of size 2
        // with one element with 1 remainder
        // and other with 2 remainder
        res += c[1] * c[2];

        // Case 4.a: Count groups of size 3
        // with all 0 remainder elements
        res += (c[0] * (c[0] - 1) *
               (c[0] - 2)) / 6;

        // Case 4.b: Count groups of size 3
        // with all 1 remainder elements
        res += (c[1] * (c[1] - 1) *
               (c[1] - 2)) / 6;

        // Case 4.c: Count groups of size 3
        // with all 2 remainder elements
        res += ((c[2] * (c[2] - 1) *
                (c[2] - 2)) / 6);

        // Case 4.c: Count groups of size 3
        // with different remainders
        res += c[0] * c[1] * c[2];

        // Return total count stored in res
        return res;
    }

    // Driver Code
    public static void Main()
    {
        FindGroups groups = new FindGroups();
        int []arr = {3, 6, 7, 2, 9};
        int n = arr.Length;
        Console.Write("Required number of groups are "
                       + groups.findgroups(arr, n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to Count groups of size
// 2 or 3 that have sum as multiple of 3

// Returns count of all possible groups
// that can be formed from elements of a[].
function findgroups($arr, $n)
{
    // Create an array C[3] to store counts
    // of elements with remainder 0, 1 and 2.
    // c[i] would store count of elements
    // with remainder i
    $c = array(0, 0, 0);

    // To store the result
    $res = 0;

    // Count elements with remainder
    // 0, 1 and 2
    for($i = 0; $i < $n; $i++)
        $c[$arr[$i] % 3] += 1;

    // Case 3.a: Count groups of size
    // 2 from 0 remainder elements
    $res += (($c[0] * ($c[0] - 1)) >> 1);

    // Case 3.b: Count groups of size
    // 2 with one element with 1
    // remainder and other with 2 remainder
    $res += $c[1] * $c[2];

    // Case 4.a: Count groups of size
    // 3 with all 0 remainder elements
    $res += ($c[0] * ($c[0] - 1) *
            ($c[0] - 2)) / 6;

    // Case 4.b: Count groups of size 3
    // with all 1 remainder elements
    $res += ($c[1] * ($c[1] - 1) *
            ($c[1] - 2)) / 6;

    // Case 4.c: Count groups of size 3
    // with all 2 remainder elements
    $res += (($c[2] * ($c[2] - 1) *
             ($c[2] - 2)) / 6);

    // Case 4.c: Count groups of size 3
    // with different remainders
    $res += $c[0] * $c[1] * $c[2];

    // Return total count stored in res
    return $res;
}

// Driver Code
$arr = array(3, 6, 7, 2, 9);
$n = count($arr);

echo "Required number of groups are " .
           (int)(findgroups($arr, $n));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript Program to count all possible
// groups of size 2 or 3 that have
// sum as multiple of 3

// Returns count of all possible groups
// that can be formed from elements of a[].
function findgroups(arr, n){
    // Create an array C[3] to store counts
    // of elements with remainder 0, 1 and 2.
    // c[i] would store count of elements
    // with remainder i
    let c = [0,0,0];
    let i;
// To store the result
    let res = 0;

    // Count elements with remainder 0, 1 and 2
    for (i=0; i<n; i++)
        c[arr[i]%3]++;

    // Case 3.a: Count groups of size 2
    // from 0 remainder elements
    res += ((c[0]*(c[0]-1))>>1);

    // Case 3.b: Count groups of size 2 with
    // one element with 1 remainder and other
    // with 2 remainder
    res += c[1] * c[2];

    // Case 4.a: Count groups of size 3
    // with all 0 remainder elements
    res += (c[0] * (c[0]-1) * Math.floor((c[0]-2))/6);

    // Case 4.b: Count groups of size 3
    // with all 1 remainder elements
    res += (c[1] * (c[1]-1) * Math.floor((c[1]-2))/6);

    // Case 4.c: Count groups of size 3
    // with all 2 remainder elements
    res += (Math.floor(c[2]*(c[2]-1)*(c[2]-2))/6);

    // Case 4.c: Count groups of size 3
    // with different remainders
    res += c[0]*c[1]*c[2];

    // Return total count stored in res
    return res;
}

// Driver Code

let arr = [3, 6, 7, 2, 9];
let n = arr.length;
document.write("Required number of groups are " + findgroups(arr,n));

</script>
```

**输出:**

```
Required number of groups are 8
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)
本文由 [Amit Jain](http://in.linkedin.com/in/amitjainju) 供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息