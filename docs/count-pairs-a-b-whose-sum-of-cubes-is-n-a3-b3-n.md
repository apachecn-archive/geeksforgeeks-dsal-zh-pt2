# 计数立方之和为 N (a^3 + b^3 = N)的对(a，b)

> 原文:[https://www . geesforgeks . org/count-pairs-a-b-what-sum-cubes-is-n-a3-B3-n/](https://www.geeksforgeeks.org/count-pairs-a-b-whose-sum-of-cubes-is-n-a3-b3-n/)

给定 n，计算满足条件 a^3 + b^3 = N 的所有‘a’和‘b’。
**示例:**

```
Input : N = 9
Output : 2
1^3 + 2^3 = 9
2^3 + 1^3 = 9

Input : N = 28
Output : 2
 1^3 + 3^3 = 28
 3^3 + 1^3 = 28
```

注:- (a，b)和(b，a)被认为是两个不同的对。
问于:土坯

```
Implementation:
Traverse numbers from 1 to cube root of N. 
  a) Subtract cube of current number from 
    N and check if their difference is a 
    perfect cube or not.
      i) If perfect cube then increment count.

2- Return count.
```

以下是上述方法的实现:

## C++

```
// C++ program to count pairs whose sum
// cubes is N
#include<bits/stdc++.h>
using namespace std;

// Function to count the pairs satisfying
// a ^ 3 + b ^ 3 = N
int countPairs(int N)
{
    int count = 0;

    // Check for each number 1 to cbrt(N)
    for (int i = 1; i <= cbrt(N); i++)
    {
        // Store cube of a number
        int cb = i*i*i;

        // Subtract the cube from given N
        int diff = N - cb;

        // Check if the difference is also
        // a perfect cube
        int cbrtDiff = cbrt(diff);

        // If yes, then increment count
        if (cbrtDiff*cbrtDiff*cbrtDiff == diff)
            count++;
    }

    // Return count
    return count;
}

// Driver program
int main()
{
    // Loop to Count no. of pairs satisfying
    // a ^ 3 + b ^ 3 = i for N = 1 to 10
    for (int i = 1; i<= 10; i++)
        cout << "For n = " << i << ", "
             << countPairs(i) <<" pair exists\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count pairs whose sum
// cubes is N

class Test
{
    // method to count the pairs satisfying
    // a ^ 3 + b ^ 3 = N
    static int countPairs(int N)
    {
        int count = 0;

        // Check for each number 1 to cbrt(N)
        for (int i = 1; i <= Math.cbrt(N); i++)
        {
            // Store cube of a number
            int cb = i*i*i;

            // Subtract the cube from given N
            int diff = N - cb;

            // Check if the difference is also
            // a perfect cube
            int cbrtDiff = (int) Math.cbrt(diff);

            // If yes, then increment count
            if (cbrtDiff*cbrtDiff*cbrtDiff == diff)
                count++;
        }

        // Return count
        return count;
    }

    // Driver method
    public static void main(String args[])
    {
        // Loop to Count no. of pairs satisfying
        // a ^ 3 + b ^ 3 = i for N = 1 to 10
        for (int i = 1; i<= 10; i++)
            System.out.println("For n = " + i + ", " +
                     + countPairs(i) + " pair exists");
    }
}
```

## 蟒蛇 3

```
# Python 3 program to count pairs
# whose sum cubes is N
import math

# Function to count the pairs
# satisfying a ^ 3 + b ^ 3 = N
def countPairs(N):

    count = 0

    # Check for each number 1
    # to cbrt(N)
    for i in range(1, int(math.pow(N, 1/3) + 1)):

        # Store cube of a number
        cb = i * i * i

        # Subtract the cube from given N
        diff = N - cb

        # Check if the difference is also
        # a perfect cube
        cbrtDiff = int(math.pow(diff, 1/3))

        # If yes, then increment count
        if (cbrtDiff * cbrtDiff * cbrtDiff == diff):
            count += 1

    # Return count
    return count

# Driver program

# Loop to Count no. of pairs satisfying
# a ^ 3 + b ^ 3 = i for N = 1 to 10
for i in range(1, 11):
    print('For n = ', i, ', ', countPairs(i),
                                ' pair exists')

# This code is contributed by Smitha.
```

## C#

```
// C# program to count pairs whose sum
// cubes is N

using System;
class Test
{
    // method to count the pairs satisfying
    // a ^ 3 + b ^ 3 = N
    static int countPairs(int N)
    {
        int count = 0;

        // Check for each number 1 to cbrt(N)
        for (int i = 1; i <= Math.Pow(N,(1.0/3.0)); i++)
        {
            // Store cube of a number
            int cb = i*i*i;

            // Subtract the cube from given N
            int diff = N - cb;

            // Check if the difference is also
            // a perfect cube
            int cbrtDiff = (int) Math.Pow(diff,(1.0/3.0));

            // If yes, then increment count
            if (cbrtDiff*cbrtDiff*cbrtDiff == diff)
                count++;
        }

        // Return count
        return count;
    }

    // Driver method
    public static void Main()
    {
        // Loop to Count no. of pairs satisfying
        // a ^ 3 + b ^ 3 = i for N = 1 to 10
        for (int i = 1; i<= 10; i++)
            Console.Write("For n = " + i + ", " +
                     + countPairs(i) + " pair exists"+"\n");
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count pairs
// whose sum cubes is N

// Function to count the pairs
// satisfying a ^ 3 + b ^ 3 = N
function countPairs($N)
{
    $count = 0;

    // Check for each number
    // 1 to cbrt(N)
    for ($i = 1;
         $i <= (int)pow($N, 1 / 3); $i++)
    {
        // Store cube of a number
        $cb = $i * $i * $i;

        // Subtract the cube from
        // given N
        $diff = ($N - $cb);

        // Check if the difference is
        // also a perfect cube
        $cbrtDiff = (int)pow($diff, 1 / 3);

        // If yes, then increment count
        if ($cbrtDiff * $cbrtDiff *
                        $cbrtDiff == $diff)
            $count++;
    }

    // Return count
    return $count;
}

// Driver Code

// Loop to Count no. of pairs
// satisfying a ^ 3 + b ^ 3 = i
// for N = 1 to 10
for ($i = 1; $i<= 10; $i++)
    echo "For n = " , $i , ", ",
          countPairs($i) ," pair exists\n";

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>
    // Javascript program to count pairs whose sum cubes is N

    // method to count the pairs satisfying
    // a ^ 3 + b ^ 3 = N
    function countPairs(N)
    {
        let count = 0;

        // Check for each number 1 to cbrt(N)
        for (let i = 1; i <= parseInt(Math.pow(N,(1.0/3.0)), 10); i++)
        {
            // Store cube of a number
            let cb = i*i*i;

            // Subtract the cube from given N
            let diff = N - cb;

            // Check if the difference is also
            // a perfect cube
            let cbrtDiff = parseInt(Math.pow(diff,(1.0/3.0)), 10);

            // If yes, then increment count
            if (cbrtDiff*cbrtDiff*cbrtDiff == diff)
                count++;
        }

        // Return count
        return count;
    }

    // Loop to Count no. of pairs satisfying
    // a ^ 3 + b ^ 3 = i for N = 1 to 10
    for (let i = 1; i<= 10; i++)
      document.write("For n = " + i + ", " + countPairs(i) + " pair exists"+"</br>");

</script>
```

**输出:**

```
For n= 1, 1 pair exists
For n= 2, 1 pair exists
For n= 3, 0 pair exists
For n= 4, 0 pair exists
For n= 5, 0 pair exists
For n= 6, 0 pair exists
For n= 7, 0 pair exists
For n= 8, 1 pair exists
For n= 9, 2 pair exists
For n= 10, 0 pair exists
```

参考:[https://www.careercup.com/question?id=5954491572551680](https://www.careercup.com/question?id=5954491572551680)
本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。