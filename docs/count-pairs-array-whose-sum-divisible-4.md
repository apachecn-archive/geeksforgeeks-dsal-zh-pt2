# 计数数组中总和可被 4 整除的对

> 原文:[https://www . geesforgeks . org/count-pairs-array-what-sum-除尽-4/](https://www.geeksforgeeks.org/count-pairs-array-whose-sum-divisible-4/)

如果 n 是正整数，则给定一个数组。计算数组中和可被 4 整除的整数对的数目。
**例:**

```
Input: {2, 2, 1, 7, 5}
Output: 3

Explanation
Only three pairs are possible whose sum
is divisible by '4' i.e., (2, 2), 
(1, 7) and (7, 5)

Input: {2, 2, 3, 5, 6}
Output: 4

```

**天真的方法**是使用两个嵌套的 for 循环迭代数组 bu 的每一对，并计算那些和可被“4”整除的对。这种方法的时间复杂度为 0(n<sup>2</sup>)。

**有效的方法**是使用哈希技术。只有三个条件可以出现，它们的和可以被“4”整除，即，

1.  如果两者都可以被 4 整除。
2.  如果其中一个等于 **1 模 4** ，另一个等于 **3 模 4** 。例如，(1，3)，(5，7)，(5，11)。
3.  如果两者都等于 **2 模 4** ，即(2，2)，(2，6)，(6，10)

**i modulo 4**

```
Thus answer =>

```

## C++

```
// C++ Program to count pairs 
// whose sum divisible by '4'
#include <bits/stdc++.h>
using namespace std;

// Program to count pairs whose sum divisible
// by '4'
int count4Divisibiles(int arr[], int n)
{
    // Create a frequency array to count 
    // occurrences of all remainders when 
    // divided by 4
    int freq[4] = {0, 0, 0, 0};

    // Count occurrences of all remainders
    for (int i = 0; i < n; i++)
        ++freq[arr[i] % 4];

    // If both pairs are divisible by '4'
    int ans = freq[0] * (freq[0] - 1) / 2;

    // If both pairs are 2 modulo 4
    ans += freq[2] * (freq[2] - 1) / 2;

    // If one of them is equal
    // to 1 modulo 4 and the
    // other is equal to 3 
    // modulo 4
    ans += freq[1] * freq[3];

    return ans;
}

// Driver code
int main()
{

    int arr[] = { 2, 2, 1, 7, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << count4Divisibiles(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count pairs 
// whose sum divisible by '4'
import java.util.*;

class Count{
    public static int count4Divisibiles(int arr[] , 
                                             int n )
    {
        // Create a frequency array to count 
        // occurrences of all remainders when 
        // divided by 4
        int freq[] = {0, 0, 0, 0};
        int i = 0;
        int ans;

        // Count occurrences of all remainders
        for (i = 0; i < n; i++)
                ++freq[arr[i] % 4];

        //If both pairs are divisible by '4'
        ans = freq[0] * (freq[0] - 1) / 2;

        // If both pairs are 2 modulo 4
        ans += freq[2] * (freq[2] - 1) / 2;

        // If one of them is equal
        // to 1 modulo 4 and the
        // other is equal to 3 
        // modulo 4
        ans += freq[1] * freq[3];

        return (ans);
    }
    public static void main(String[] args)
    {
        int arr[] = {2, 2, 1, 7, 5};
        int n = 5;
        System.out.print(count4Divisibiles(arr, n));
    }
}

// This code is contributed by rishabh_jain
```

## 蟒蛇 3

```
# Python3 code to count pairs whose 
# sum is divisible by '4'

# Function to count pairs whose 
# sum is divisible by '4'
def count4Divisibiles( arr , n ):

    # Create a frequency array to count 
    # occurrences of all remainders when 
    # divided by 4
    freq = [0, 0, 0, 0]

    # Count occurrences of all remainders
    for i in range(n):
        freq[arr[i] % 4]+=1

    #If both pairs are divisible by '4'
    ans = freq[0] * (freq[0] - 1) / 2

    # If both pairs are 2 modulo 4
    ans += freq[2] * (freq[2] - 1) / 2

    # If one of them is equal
    # to 1 modulo 4 and the
    # other is equal to 3 
    # modulo 4
    ans += freq[1] * freq[3]

    return int(ans)

# Driver code
arr = [2, 2, 1, 7, 5]
n = len(arr)
print(count4Divisibiles(arr, n))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to count pairs 
// whose sum divisible by '4'
using System;

class Count{
    public static int count4Divisibiles(int []arr , 
                                            int n )
    {
        // Create a frequency array to count 
        // occurrences of all remainders when 
        // divided by 4
        int []freq = {0, 0, 0, 0};
        int i = 0;
        int ans;

        // Count occurrences of all remainders
        for (i = 0; i < n; i++)
            ++freq[arr[i] % 4];

        //If both pairs are divisible by '4'
        ans = freq[0] * (freq[0] - 1) / 2;

        // If both pairs are 2 modulo 4
        ans += freq[2] * (freq[2] - 1) / 2;

        // If one of them is equal
        // to 1 modulo 4 and the
        // other is equal to 3 
        // modulo 4
        ans += freq[1] * freq[3];

        return (ans);
    }

    // Driver code
    public static void Main()
    {
        int []arr = {2, 2, 1, 7, 5};
        int n = 5;
        Console.WriteLine(count4Divisibiles(arr, n));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to count pairs 
// whose sum divisible by '4'

// Program to count pairs whose 
// sum divisible by '4'
function count4Divisibiles($arr, $n)
{
    // Create a frequency array to 
    // count occurrences of all 
    // remainders when divided by 4
    $freq = array(0, 0, 0, 0);

    // Count occurrences 
    // of all remainders
    for ( $i = 0; $i < $n; $i++)
        ++$freq[$arr[$i] % 4];

    // If both pairs are
    // divisible by '4'
    $ans = $freq[0] *
          ($freq[0] - 1) / 2;

    // If both pairs are
    // 2 modulo 4
    $ans += $freq[2] * 
           ($freq[2] - 1) / 2;

    // If one of them is equal
    // to 1 modulo 4 and the
    // other is equal to 3 
    // modulo 4
    $ans += $freq[1] * $freq[3];

    return $ans;
}

// Driver code
$arr = array(2, 2, 1, 7, 5);
$n = sizeof($arr) ;

echo count4Divisibiles($arr, $n);

// This code is contributed by ajit
?>
```

**Output :**

```
 3

```

**时间复杂度:**O(n)
T3】辅助空间: O(1)