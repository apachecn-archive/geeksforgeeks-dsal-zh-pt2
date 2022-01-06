# 用奇数异或计数对

> 原文:[https://www.geeksforgeeks.org/count-pairs-odd-xor/](https://www.geeksforgeeks.org/count-pairs-odd-xor/)

给定 n 个整数的数组。找出数组中异或为奇数的对的个数。
**例:**

```
Input : arr[] = { 1, 2, 3 }
Output : 2
All pairs of array
1 ^ 2 = 3
1 ^ 3 = 2
2 ^ 3 = 1

Input : arr[] = { 1, 2, 3, 4 }
Output : 4
```

**天真方法:**我们可以通过运行两个循环来找到异或为奇数的对。如果两个数的异或为奇数，则增加对的计数。

## C++

```
// C++ program to count pairs in array
// whose XOR is odd
#include <iostream>
using namespace std;

// A function will return number of pair
// whose XOR is odd
int countXorPair(int arr[], int n)
{
    // To store count of XOR pair
    int count = 0;

    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++)

            // If XOR is odd increase count
            if ((arr[i] ^ arr[j]) % 2 == 1)
                count++;
    }

    // Return count
    return count;
}

// Driver program to test countXorPair()
int main()
{
    int arr[] = { 1, 2, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countXorPair(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count pairs in array whose
// XOR is odd
public class CountXor {
    // A function will return number of pair
    // whose XOR is odd
    static int countXorPair(int arr[], int n)
    {
        // To store count of XOR pair
        int count = 0;

        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++)

                // If XOR is odd increase count
                if ((arr[i] ^ arr[j]) % 2 == 1)
                    count++;
        }

        // Return count
        return count;
    }

    // Driver program to test countXorPair()
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3 };
        System.out.println(countXorPair(arr, arr.length));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to count
# pairs in array whose XOR is odd

# A function will
# return number of pair
# whose XOR is odd
def countXorPair(arr, n):

    # To store count of XOR pair
    count = 0

    for i in range(n):
        for j in range(i + 1, n):

            # If XOR is odd increase count
            if ((arr[i] ^ arr[j]) % 2 == 1):
                count += 1

    # Return count
    return count

# Driver Code
if __name__ == "__main__":
    arr= [ 1, 2, 3 ]
    n = len(arr)
    print(countXorPair(arr, n))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to count pairs in
// array whose XOR is odd
using System;

public class CountXor {

    // A function will return number of pair
    // whose XOR is odd
    static int countXorPair(int[] arr, int n)
    {
        // To store count of XOR pair
        int count = 0;

        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++)

                // If XOR is odd increase count
                if ((arr[i] ^ arr[j]) % 2 == 1)
                    count++;
        }

        // Return count
        return count;
    }

    // Driver program to test countXorPair()
    public static void Main()
    {
        int[] arr = {1, 2, 3};
        Console.WriteLine(countXorPair(arr, arr.Length));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count
// pairs in array
// whose XOR is odd

// A function will
// return number of pair
// whose XOR is odd
function countXorPair($arr,$n)
{

    // To store count
    // of XOR pair
    $count = 0;

    for ($i = 0; $i < $n; $i++)
    {
        for ($j = $i + 1; $j < $n; $j++)

            // If XOR is odd
            // increase count
            if (($arr[$i] ^ $arr[$j]) % 2 == 1)
                $count++;
    }

    // Return count
    return $count;
}

    // Driver Code
    $arr = array(1, 2, 3);
    $n = count($arr);
    echo countXorPair($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to count pairs in
    // array whose XOR is odd

    // A function will return number of pair
    // whose XOR is odd
    function countXorPair(arr, n)
    {
        // To store count of XOR pair
        let count = 0;

        for (let i = 0; i < n; i++) {
            for (let j = i + 1; j < n; j++)

                // If XOR is odd increase count
                if ((arr[i] ^ arr[j]) % 2 == 1)
                    count++;
        }

        // Return count
        return count;
    }

    let arr = [1, 2, 3];
      document.write(countXorPair(arr, arr.length));

</script>
```

输出:

```
2
```

时间复杂度:O(n*n)
**高效方法:**我们可以观察到:

```
odd ^ odd = even
odd ^ even = odd
even ^ odd = odd
even ^ even = even
```

因此，数组中异或为奇数的总对将等于奇数计数乘以偶数计数。

## C++

```
// C++ program to count pairs in array
// whose XOR is odd
#include <iostream>
using namespace std;

// A function will return number of pair
// whose XOR is odd
int countXorPair(int arr[], int n)
{
    // To store count of odd and even
    // numbers
    int odd = 0, even = 0;

    for (int i = 0; i < n; i++) {
        // Increase even if number is
        // even otherwise increase odd
        if (arr[i] % 2 == 0)
            even++;
        else
            odd++;
    }

    // Return number of pairs
    return odd * even;
}

// Driver program to test countXorPair()
int main()
{
    int arr[] = { 1, 2, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countXorPair(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count pairs in array whose
// XOR is odd

public class CountXor {
    // A function will return number of pair
    // whose XOR is odd
    static int countXorPair(int arr[], int n)
    {
        // To store count of odd and even numbers
        int odd = 0, even = 0;

        for (int i = 0; i < n; i++) {
            // Increase even if number is
            // even otherwise increase odd
            if (arr[i] % 2 == 0)
                even++;
            else
                odd++;
        }

        // Return number of pairs
        return odd * even;
    }

    // Driver program to test countXorPair()
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3 };
        System.out.println(countXorPair(arr, arr.length));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to count
# pairs in array whose XOR is odd

# A function will
# return number of pair
# whose XOR is odd
def countXorPair(arr, n):

    # To store count of
    # odd and even numbers
    odd = 0
    even = 0

    for i in range(n):

        # Increase even if number is
        # even otherwise increase odd
        if arr[i] % 2 == 0:
            even += 1
        else:
            odd += 1

    # Return number of pairs
    return odd * even

# Driver Code
if __name__ == "__main__":
    arr = [ 1, 2, 3 ]
    n = len(arr)
    print(countXorPair(arr, n))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to count pairs in
// array whose XOR is odd
using System;

public class CountXor {

    // A function will return number of pair
    // whose XOR is odd
    static int countXorPair(int[] arr, int n)
    {
        // To store count of odd and even numbers
        int odd = 0, even = 0;

        for (int i = 0; i < n; i++) {

            // Increase even if number is
            // even otherwise increase odd
            if (arr[i] % 2 == 0)
                even++;
            else
                odd++;
        }

        // Return number of pairs
        return odd * even;
    }

    // Driver program to test countXorPair()
    public static void Main()
    {
        int[] arr = {1, 2, 3};
        Console.WriteLine(countXorPair(arr, arr.Length));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count pairs in array
// whose XOR is odd

// A function will return number of pair
// whose XOR is odd

function countXorPair($arr, $n)
{
    // To store count of odd
    // and even numbers
    $odd = 0;
    $even = 0;

    for ($i = 0; $i < $n; $i++)
    {
        // Increase even if number is
        // even otherwise increase odd
        if ($arr[$i] % 2 == 0)
            $even++;
        else
            $odd++;
    }

    // Return number of pairs
    return $odd * $even;
}

// Driver Code
$arr = array( 1, 2, 3 );
$n = sizeof($arr);
echo countXorPair($arr, $n);

// This code is contributed by Ajit_m
?>
```

## java 描述语言

```
<script>
// Javascript program to count pairs in array whose
// XOR is odd

    // A function will return number of pair
    // whose XOR is odd
    function countXorPair(arr, n)
    {

        // To store count of odd and even numbers
        let odd = 0, even = 0;

        for (let i = 0; i < n; i++)
        {

            // Increase even if number is
            // even otherwise increase odd
            if (arr[i] % 2 == 0)
                even++;
            else
                odd++;
        }

        // Return number of pairs
        return odd * even;
    }

    // Driver program to test countXorPair()
    let arr=[ 1, 2, 3 ];
    document.write(countXorPair(arr, arr.length));

    // This code is contributed by rag2127
</script>
```

**输出:**

```
2
```

**时间复杂度:** O(n)
本文由 [**核**](http://www.facebook.com/nuclode) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。