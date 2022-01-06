# 计算产生肯定结果的排列

> 原文:[https://www . geesforgeks . org/count-排列-产生-肯定-结果/](https://www.geeksforgeeks.org/count-permutations-produce-positive-result/)

给定长度 n > 1 的数字数组，数字在 0 到 9 的范围内。我们执行以下三个操作的顺序，直到完成所有数字

1.  选择起始两位数并添加(+)
2.  然后从上述步骤的结果中减去下一个数字(–)。

3.  上述步骤的结果乘以下一个数字。

我们用剩余的数字线性地执行上述操作序列。
任务是找出给定数组经过上述运算后产生正结果的排列数。
例如，考虑输入数字[] = {1，2，3，4，5}。让我们考虑排列 21345 来演示操作序列。

1.  添加前两位数字，结果= 2+1 = 3
2.  减去下一个数字，结果=结果-3= 3-3 = 0
3.  乘以下一个数字，结果=结果*4= 0*4 = 0
4.  添加下一个数字，结果=结果+5 = 0+5 = 5
5.  结果= 5，为正，因此将计数增加 1

示例:

```
Input : number[]="123"
Output: 4
// here we have all permutations
// 123 --> 1+2 -> 3-3 -> 0
// 132 --> 1+3 -> 4-2 -> 2 ( positive )
// 213 --> 2+1 -> 3-3 -> 0
// 231 --> 2+3 -> 5-1 -> 4 ( positive )
// 312 --> 3+1 -> 4-2 -> 2 ( positive )
// 321 --> 3+2 -> 5-1 -> 4 ( positive )
// total 4 permutations are giving positive result

Input : number[]="112"
Output: 2
// here we have all permutations possible
// 112 --> 1+1 -> 2-2 -> 0
// 121 --> 1+2 -> 3-1 -> 2 ( positive )
// 211 --> 2+1 -> 3-1 -> 2 ( positive )
```

**<u>问于:</u>** **摩根士丹利**

我们首先生成给定数字阵列的所有可能排列，并对每个排列顺序执行给定的操作序列，并检查哪个排列结果是正的。下面的代码很容易描述问题的解决方案。
**<u>注:</u>** 我们可以通过迭代的方法生成所有可能的排列，参见[这篇](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)文章，也可以使用 STL 函数[next _ arrangement()](https://www.geeksforgeeks.org/find-the-next-lexicographically-greater-word-than-a-given-word/)函数生成。

## C++

```
// C++ program to find count of permutations that produce
// positive result.
#include<bits/stdc++.h>
using namespace std;

// function to find all permutation after executing given
// sequence of operations and whose result value is positive
// result > 0 ) number[] is array of digits of length of n
int countPositivePermutations(int number[], int n)
{
    // First sort the array so that we get all permutations
    // one by one using next_permutation.
    sort(number, number+n);

    // Initialize result (count of permutations with positive
    // result)
    int count = 0;

    // Iterate for all permutation possible and do operation
    // sequentially in each permutation
    do
    {
        // Stores result for current permutation. First we
        // have to select first two digits and add them
        int curr_result = number[0] + number[1];

        // flag that tells what operation we are going to
        // perform
        // operation = 0 ---> addition operation ( + )
        // operation = 1 ---> subtraction operation ( - )
        // operation = 0 ---> multiplication operation ( X )
        // first sort the array of digits to generate all
        // permutation in sorted manner
        int operation = 1;

        // traverse all digits
        for (int i=2; i<n; i++)
        {
            // sequentially perform + , - , X operation
            switch (operation)
            {
            case 0:
                curr_result += number[i];
                break;
            case 1:
                curr_result -= number[i];
                break;
            case 2:
                curr_result *= number[i];
                break;
            }

            // next operation (decides case of switch)
            operation = (operation + 1) % 3;
        }

        // result is positive then increment count by one
        if (curr_result > 0)
            count++;

    // generate next greater permutation until it is
    // possible
    } while(next_permutation(number, number+n));

    return count;
}

// Driver program to test the case
int main()
{
    int number[] = {1, 2, 3};
    int n = sizeof(number)/sizeof(number[0]);
    cout << countPositivePermutations(number, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find count of permutations
// that produce positive result.
import java.util.*;

class GFG
{

// function to find all permutation after
// executing given sequence of operations
// and whose result value is positive result > 0 )
// number[] is array of digits of length of n
static int countPositivePermutations(int number[],
                                     int n)
{
    // First sort the array so that we get
    // all permutations one by one using
    // next_permutation.
    Arrays.sort(number);

    // Initialize result (count of permutations
    // with positive result)
    int count = 0;

    // Iterate for all permutation possible and
    // do operation sequentially in each permutation
    do
    {
        // Stores result for current permutation.
        // First we have to select first two digits
        // and add them
        int curr_result = number[0] + number[1];

        // flag that tells what operation we are going to
        // perform
        // operation = 0 ---> addition operation ( + )
        // operation = 1 ---> subtraction operation ( - )
        // operation = 0 ---> multiplication operation ( X )
        // first sort the array of digits to generate all
        // permutation in sorted manner
        int operation = 1;

        // traverse all digits
        for (int i = 2; i < n; i++)
        {
            // sequentially perform + , - , X operation
            switch (operation)
            {
            case 0:
                curr_result += number[i];
                break;
            case 1:
                curr_result -= number[i];
                break;
            case 2:
                curr_result *= number[i];
                break;
            }

            // next operation (decides case of switch)
            operation = (operation + 1) % 3;
        }

        // result is positive then increment count by one
        if (curr_result > 0)
            count++;

    // generate next greater permutation until
    // it is possible
    } while(next_permutation(number));

    return count;
}

static boolean next_permutation(int[] p)
{
    for (int a = p.length - 2; a >= 0; --a)
        if (p[a] < p[a + 1])
        for (int b = p.length - 1;; --b)
            if (p[b] > p[a])
            {
                int t = p[a];
                p[a] = p[b];
                p[b] = t;
                for (++a, b = p.length - 1; a < b; ++a, --b)
                {
                    t = p[a];
                    p[a] = p[b];
                    p[b] = t;
                }
                return true;
            }
    return false;
}

// Driver Code
public static void main(String[] args)
{
    int number[] = {1, 2, 3};
    int n = number.length;
    System.out.println(countPositivePermutations(number, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find count of permutations
# that produce positive result.

# function to find all permutation after
# executing given sequence of operations
# and whose result value is positive result > 0 )
# number[] is array of digits of length of n
def countPositivePermutations(number, n):

    # First sort the array so that we get
    # all permutations one by one using
    # next_permutation.
    number.sort()

    # Initialize result (count of permutations
    # with positive result)
    count = 0;

    # Iterate for all permutation possible and
    # do operation sequentially in each permutation
    while True:

        # Stores result for current permutation.
        # First we have to select first two digits
        # and add them
        curr_result = number[0] + number[1];

        # flag that tells what operation we are going to
        # perform
        # operation = 0 ---> addition operation ( + )
        # operation = 1 ---> subtraction operation ( - )
        # operation = 0 ---> multiplication operation ( X )
        # first sort the array of digits to generate all
        # permutation in sorted manner
        operation = 1;

        # traverse all digits
        for i in range(2, n):

            # sequentially perform + , - , X operation
            if operation == 0:
                curr_result += number[i];

            elif operation == 1:
                curr_result -= number[i];

            elif operation == 2:
                curr_result *= number[i];

            # next operation (decides case of switch)
            operation = (operation + 1) % 3;

        # result is positive then increment count by one
        if (curr_result > 0):
            count += 1

        # generate next greater permutation until
        # it is possible
        if(not next_permutation(number)):
            break
    return count;

def next_permutation(p):
    for a in range(len(p)-2, -1, -1):
        if (p[a] < p[a + 1]):
            for b in range(len(p)-1, -1000000000, -1):
                if (p[b] > p[a]):
                    t = p[a];
                    p[a] = p[b];
                    p[b] = t;
                    a += 1
                    b = len(p) - 1
                    while(a < b):          
                        t = p[a];
                        p[a] = p[b];
                        p[b] = t;
                        a += 1
                        b -= 1

                    return True;
    return False;

# Driver Code
if __name__ =='__main__':

    number = [1, 2, 3]
    n = len(number)
    print(countPositivePermutations(number, n));

# This code is contributed by rutvik_56.
```

## C#

```
// C# program to find count of permutations
// that produce positive result.
using System;

class GFG
{

// function to find all permutation after
// executing given sequence of operations
// and whose result value is positive result > 0 )
// number[] is array of digits of length of n
static int countPositivePermutations(int []number,
                                     int n)
{
    // First sort the array so that we get
    // all permutations one by one using
    // next_permutation.
    Array.Sort(number);

    // Initialize result (count of permutations
    // with positive result)
    int count = 0;

    // Iterate for all permutation possible and
    // do operation sequentially in each permutation
    do
    {
        // Stores result for current permutation.
        // First we have to select first two digits
        // and add them
        int curr_result = number[0] + number[1];

        // flag that tells what operation we are going to
        // perform
        // operation = 0 ---> addition operation ( + )
        // operation = 1 ---> subtraction operation ( - )
        // operation = 0 ---> multiplication operation ( X )
        // first sort the array of digits to generate all
        // permutation in sorted manner
        int operation = 1;

        // traverse all digits
        for (int i = 2; i < n; i++)
        {
            // sequentially perform + , - , X operation
            switch (operation)
            {
                case 0:
                    curr_result += number[i];
                    break;
                case 1:
                    curr_result -= number[i];
                    break;
                case 2:
                    curr_result *= number[i];
                    break;
            }

            // next operation (decides case of switch)
            operation = (operation + 1) % 3;
        }

        // result is positive then increment count by one
        if (curr_result > 0)
            count++;

    // generate next greater permutation until
    // it is possible
    } while(next_permutation(number));

    return count;
}

static bool next_permutation(int[] p)
{
    for (int a = p.Length - 2; a >= 0; --a)
        if (p[a] < p[a + 1])
        for (int b = p.Length - 1;; --b)
            if (p[b] > p[a])
            {
                int t = p[a];
                p[a] = p[b];
                p[b] = t;
                for (++a, b = p.Length - 1;
                           a < b; ++a, --b)
                {
                    t = p[a];
                    p[a] = p[b];
                    p[b] = t;
                }
                return true;
            }
    return false;
}

// Driver Code
static public void Main ()
{
    int []number = {1, 2, 3};
    int n = number.Length;
    Console.Write(countPositivePermutations(number, n));
}
}

// This code is contributed by ajit..
```

## java 描述语言

```
<script>

    // Javascript program to find count of permutations
    // that produce positive result.

    // function to find all permutation after
    // executing given sequence of operations
    // and whose result value is positive result > 0 )
    // number[] is array of digits of length of n
    function countPositivePermutations(number, n)
    {
        // First sort the array so that we get
        // all permutations one by one using
        // next_permutation.
        number.sort(function(a, b){return a - b});

        // Initialize result (count of permutations
        // with positive result)
        let count = 0;

        // Iterate for all permutation possible and
        // do operation sequentially in each permutation
        do
        {
            // Stores result for current permutation.
            // First we have to select first two digits
            // and add them
            let curr_result = number[0] + number[1];

            // flag that tells what operation we are going to
            // perform
            // operation = 0 ---> addition operation ( + )
            // operation = 1 ---> subtraction operation ( - )
            // operation = 0 ---> multiplication operation ( X )
            // first sort the array of digits to generate all
            // permutation in sorted manner
            let operation = 1;

            // traverse all digits
            for (let i = 2; i < n; i++)
            {
                // sequentially perform + , - , X operation
                switch (operation)
                {
                    case 0:
                        curr_result += number[i];
                        break;
                    case 1:
                        curr_result -= number[i];
                        break;
                    case 2:
                        curr_result *= number[i];
                        break;
                }

                // next operation (decides case of switch)
                operation = (operation + 1) % 3;
            }

            // result is positive then increment count by one
            if (curr_result > 0)
                count++;

        // generate next greater permutation until
        // it is possible
        } while(next_permutation(number));

        return count;
    }

    function next_permutation(p)
    {
        for (let a = p.length - 2; a >= 0; --a)
            if (p[a] < p[a + 1])
              for (let b = p.length - 1;; --b)
                  if (p[b] > p[a])
                  {
                      let t = p[a];
                      p[a] = p[b];
                      p[b] = t;
                      for (++a, b = p.length - 1;
                                 a < b; ++a, --b)
                      {
                          t = p[a];
                          p[a] = p[b];
                          p[b] = t;
                      }
                      return true;
                  }
        return false;
    }

    let number = [1, 2, 3];
    let n = number.length;
    document.write(countPositivePermutations(number, n));

</script>
```

**输出:**

```
4
```

如果你对这个问题有更好和优化的解决方案，那么请在评论中分享。
本文由 [**沙莎克·米什拉(古卢)**](https://practice.geeksforgeeks.org/user-profile.php?user=Shashank%20Mishra) 供稿，团队 geeksforgeeks 审核。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。