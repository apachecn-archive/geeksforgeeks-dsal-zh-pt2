# 检查除数是偶数还是奇数的程序

> 原文:[https://www . geesforgeks . org/c-程序检查除数是偶数还是奇数/](https://www.geeksforgeeks.org/c-program-for-check-if-count-of-divisors-is-even-or-odd/)

给定一个数“n”，求它的除数总数是偶数还是奇数。

示例:

```
Input  : n = 10      
Output : Even

Input:  n = 100
Output: Odd

Input:  n = 125
Output: Even
```

一种天真的方法是[找到所有的除数](https://www.geeksforgeeks.org/find-all-divisors-of-a-natural-number-set-2/)，然后看看除数的总数是偶数还是奇数。

这种解决方案的时间复杂度为 0(平方英尺(n))

```
// Naive Solution to
// find if count of
// divisors is even
// or odd
#include <math.h>
#include <stdio.h>

// Function to count
// the divisors
void countDivisors(int n)
{
    // Initialize count
    // of divisors
    int count = 0;

    // Note that this
    // loop runs till
    // square root
    for (int i = 1; i <= sqrt(n) + 1; i++) {
        if (n % i == 0)

            // If divisors are
            // equal increment
            // count by one
            // Otherwise increment
            // count by 2
            count += (n / i == i) ? 1 : 2;
    }

    if (count % 2 == 0)
        printf("Even\n");

    else
        printf("Odd\n");
}

/* Driver program to test above function */
int main()
{
    printf("The count of divisor: ");
    countDivisors(10);
    return 0;
}
```

**Output:**

```
The count of divisor: Even

```

**有效解:**
我们可以观察到除数只有在完美平方的情况下才是奇数。因此，最好的解决办法是检查给定的数字是否是完美的正方形。如果它是一个完美的正方形，那么除数将是奇数，否则它将是偶数。

```
// C++ program for
// Efficient Solution to find
// if count of divisors is
// even or odd
#include <bits/stdc++.h>
using namespace std;

// Function to find if count
// of divisors is even or
// odd
void countDivisors(int n)
{
    int root_n = sqrt(n);

    // If n is a perfect square,
    // then it has odd divisors
    if (root_n * root_n == n)
        printf("Odd\n");
    else
        printf("Even\n");
}

/* Driver program to test above function */
int main()
{
    cout << "The count of divisors of 10 is: \n";

    countDivisors(10);
    return 0;
}
```

**Output:**

```
The count of divisors of 10 is: 
Even

```

详情请参考[查看除数是偶数还是奇数](https://www.geeksforgeeks.org/check-if-total-number-of-divisors-are-even-or-odd/)整篇文章！