# 通过递减相邻对

进行零排列

> 原文:[https://www . geeksforgeeks . org/making-zero-array-by-reduced-pairs-of-neighbor/](https://www.geeksforgeeks.org/making-zero-array-by-decrementing-pairs-of-adjacent/)

给定一个非负整数序列，比如 a <sub>1</sub> ，a <sub>2</sub> ，a……，a <sub>n</sub> 。只能对给定序列执行以下操作:

*   从 a[i]和 a[i+1]中减去 1。

查找是否可以使用任何所需数量的上述操作将数列修改为全零。

**示例:**

```
Input  : 1 2
Output : NO
Explanation: Only two elements, if we subtract
1 then it will convert into [0, 1].
so answer is NO. 

Input  : 0 1 1 0
Output : YES
Explanation: Here we can choose both 1 and 
subtract 1 from them then array becomes [0, 0, 0, 
0].
So answer is YES.

Input  :  1 2 3 4
Output : NO
Explanation: if we try to subtract 1 any
number of times then array will be [0, 0, 0, 1].
[1, 2, 3, 4]->[0, 1, 3, 4]->[0, 0, 2, 3]->
[0, 0, 1, 2]->[0, 0, 0, 1]. 
```

**方法 1 :** 如果数组中所有相邻的元素(I，i+1)相等，并且数组中的元素总数为偶数，那么它的所有元素都可以被转换为零。例如，如果数组元素像{1，1，2，2，3，3}，那么它的所有元素都可以转换为零。
那么在这种情况下，每个奇数位置值的和总是等于偶数位置值的和。

## C++

```
// CPP program to find if it is possible
// to make all array elements 0 by decrement
// operations.
#include <bits/stdc++.h>
using namespace std;

bool isPossibleToZero(int a[], int n)
{
    // used for storing the sum of even
    // and odd position element in array.
    int even = 0, odd = 0;

    for (int i = 0; i < n; i++)
    {
        // if position is odd, store sum
        // value of odd position in odd
        if (i & 1)
            odd += a[i];

        // if position is even, store sum
        // value of even position in even
        else
            even += a[i];
    }

    return (odd == even);
}

// Driver program
int main()
{
    int arr[] = { 0, 1, 1, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);
    if (isPossibleToZero(arr, n))
        cout << "YES";
    else
        cout << "NO";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if
// it is possible to make
// all array elements 0 by
// decrement operations.
import java.io.*;

class GFG
{
    static boolean isPossibleToZero(int a[],   
                                    int n)
{
    // used for storing the
    // sum of even and odd
    // position element in array.
    int even = 0, odd = 0;

    for (int i = 0; i < n; i++)
    {
        // if position is odd,
        // store sum value of
        // odd position in odd
        if ((i & 1) == 0)
            odd += a[i];

        // if position is even,
        // store sum value of
        // even position in even
        else
            even += a[i];
    }

    return (odd == even);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 0, 1, 1, 0 };
    int n = arr.length;
    if (isPossibleToZero(arr, n))
        System.out.println("YES");
    else
        System.out.println("NO");
}
}

// This code is contributed by m_kit
```

## 蟒蛇 3

```
# Python3 program to find if it is
# possible to make all array elements
# 0 by decrement operations.
def isPossibleToZero(a, n):

    # used for storing the
    # sum of even and odd
    # position element in array.
    even = 0;
    odd = 0;

    for i in range(n):

        # if position is odd, store sum
        # value of odd position in odd
        if (i & 1):
            odd += a[i];

        # if position is even, store sum
        # value of even position in even
        else:
            even += a[i];

    return (odd == even);

# Driver Code
arr = [0, 1, 1, 0];
n = len(arr);
if (isPossibleToZero(arr, n)):
    print("YES");
else:
    print("NO");

# This code is contributed by mits
```

## C#

```
// C# program to find if
// it is possible to make
// all array elements 0 by
// decrement operations.
using System;

class GFG
{
static bool isPossibleToZero(int []a,
                             int n)
{
    // used for storing the
    // sum of even and odd
    // position element in array.
    int even = 0, odd = 0;

    for (int i = 0; i < n; i++)
    {
        // if position is odd,
        // store sum value of
        // odd position in odd
        if ((i & 1) == 0)
            odd += a[i];

        // if position is even,
        // store sum value of
        // even position in even
        else
            even += a[i];
    }

    return (odd == even);
}

// Driver Code
static public void Main ()
{
    int []arr = {0, 1, 1, 0};
    int n = arr.Length;
    if (isPossibleToZero(arr, n))
        Console.WriteLine("YES");
    else
        Console.WriteLine("NO");
}
}

// This code is contributed
// by m_kit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if it
// is possible to make all
// array elements 0 by
// decrement operations.
function isPossibleToZero($a, $n)
{
    // used for storing the
    // sum of even and odd
    // position element in array.
    $even = 0; $odd = 0;

    for ($i = 0; $i < $n; $i++)
    {
        // if position is odd,
        // store sum value of
        // odd position in odd
        if ($i & 1)
            $odd += $a[$i];

        // if position is even,
        // store sum value of
        // even position in even
        else
            $even += $a[$i];
    }

    return ($odd == $even);
}

// Driver Code
$arr = array (0, 1, 1, 0);
$n = sizeof($arr);
if (isPossibleToZero($arr, $n))
    echo "YES";
else
    echo "NO";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to find if
// it is possible to make
// all array elements 0 by
// decrement operations.
function isPossibleToZero(a, n)
{

    // Used for storing the
    // sum of even and odd
    // position element in array.
    let even = 0, odd = 0;

    for(let i = 0; i < n; i++)
    {

        // If position is odd,
        // store sum value of
        // odd position in odd
        if ((i & 1) == 0)
            odd += a[i];

        // If position is even,
        // store sum value of
        // even position in even
        else
            even += a[i];
    }
    return (odd == even);
}

// Driver code
let arr = [ 0, 1, 1, 0 ];
let n = arr.length;

if (isPossibleToZero(arr, n))
    document.write("YES");
else
    document.write("NO");

// This code is contributed by mukesh07

</script>
```

**Output:** 

```
YES
```

**方法 2:** 如果给定数组元素构成的数可以被 11 整除，那么数组的所有元素也可以转换为零。
**例如:**给定数组{0，1，1，0}，这个数组形成的数是 110，那么它可以被 11 整除。所以所有的元素都可以转换成零。

## C++

```
// CPP implementation of the
// above approach
#include <bits/stdc++.h>
using namespace std;

bool isPossibleToZero(int a[], int n)
{ 
    // converting array element into number
    int num = 0;
    for (int i = 0; i < n; i++)
        num = num * 10 + a[i];

    // Check if divisible by 11
    return (num % 11 == 0);
}

// Driver program
int main()
{
    int arr[] = { 0, 1, 1, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);
    if (isPossibleToZero(arr, n))
        cout << "YES";
    else
        cout << "NO";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;

class GFG {

    static boolean isPossibleToZero(int a[], int n)
    {
        // converting array element into number
        int num = 0;
        for (int i = 0; i < n; i++)
            num = num * 10 + a[i];

        // Check if divisible by 11
        return (num % 11 == 0);
    }

    // Driver program
    public static void main (String[] args)
    {

        int arr[] = {0, 1, 1, 0};
        int n = arr.length;
        if (isPossibleToZero(arr, n))
                System.out.println( "YES");
        else
                System.out.println ("NO");
    }
}

// This code is contributed by @ajit
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

def isPossibleToZero(a, n):

    # converting array element
    # into number
    num = 0;
    for i in range(n):
        num = num * 10 + a[i];

    # Check if divisible by 11
    return (num % 11 == 0);

# Driver Code
arr = [ 0, 1, 1, 0 ];
n = len(arr);
if (isPossibleToZero(arr, n)):
    print("YES");
else:
    print("NO");

# This code is contributed mits
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

static bool isPossibleToZero(int[] a, int n)
{
    // converting array element into number
    int num = 0;
    for (int i = 0; i < n; i++)
        num = num * 10 + a[i];

    // Check if divisible by 11
    return (num % 11 == 0);
}

// Driver Code
public static void Main()
{
    int[] arr = {0, 1, 1, 0};
    int n = arr.Length;
    if (isPossibleToZero(arr, n))
        Console.WriteLine("YES");
    else
        Console.WriteLine("NO");
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of
// the above approach

function isPossibleToZero($a, $n)
{
    // converting array
    // element into number
    $num = 0;
    for ($i = 0; $i < $n; $i++)
        $num = $num * 10 + $a[$i];

    // Check if divisible by 11
    return ($num % 11 == 0);
}

// Driver Code
$arr = array( 0, 1, 1, 0 );
$n = sizeof($arr);
if (isPossibleToZero($arr, $n))
    echo "YES";
else
    echo "NO";

// This code is contributed ajit
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach
function isPossibleToZero(a, n)
{

    // Converting array element into number
    let num = 0;
    for(let i = 0; i < n; i++)
        num = num * 10 + a[i];

    // Check if divisible by 11
    return (num % 11 == 0);
}

// Driver code
let arr = [ 0, 1, 1, 0 ];
let n = arr.length;

if (isPossibleToZero(arr, n))
    document.write("YES");
else
    document.write("NO");

// This code is contributed by divyeshrabadiya07

</script>
```

**Output:** 

```
YES
```

上面的实现导致稍微大一点的数组溢出。我们可以用下面的方法来避免溢出。[检查一个大数是否能被 11 整除](https://www.geeksforgeeks.org/check-large-number-divisible-11-not/)T2】