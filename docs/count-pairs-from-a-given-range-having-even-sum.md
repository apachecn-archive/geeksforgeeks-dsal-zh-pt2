# 对给定范围内具有偶数和的配对进行计数

> 原文:[https://www . geesforgeks . org/count-pairs-from-a-给定范围-having-sum/](https://www.geeksforgeeks.org/count-pairs-from-a-given-range-having-even-sum/)

给定两个正整数 **L** 和 **R** ，任务是找出范围**【L，R】**内有序对的个数，使得每对元素之和为[甚至](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)。

**示例:**

> **输入:** L = 1，R =3
> **输出:** 5
> **说明:**
> 元素之和为偶数且在[1，3]范围内的对为{ (1，3)，(1，1)，(2，2)，(3，3)，(3，1) }
> 
> **输入:** L = 1，R = 1
> T3】输出: 1

**方法:**利用两个数之和为偶数或者两个数都为奇数的情况下，两个数之和为偶数，可以解决这个问题。按照以下步骤解决此问题:

*   数数所有偶数，说 **cnt_even** ，范围**【L，R】**。按照以下步骤进行计算:
    *   [如果 **L** 为偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，那么**CNT _ even =(R/2)–(L/2)+1**。
    *   [如果 L 为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则**CNT _ even =(R/2)–(L/2)**。
*   元素之和为偶数且两个元素也为偶数的对的计数为 **count_even * count_even** 。
*   同样，在**【L，R】**范围内，计算所有奇数，比如 **count_odd** 。按照以下步骤进行计算:
    *   [如果 **L** 为偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，那么**count _ odd =((R+1)/2)–((L+1)/2)**。
    *   [如果 **L** 为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则**count _ odd =((R+1)/2)–((L+1)/2)+1**。
*   元素之和为偶数且两个元素都为奇数的对的计数为 **count_odd * count_odd**
*   最后打印**(count _ 奇数* count _ 奇数+count _ 偶数* count _ 偶数)**的值

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count of
// ordered pairs having even sum
int countPairs(int L, int R)
{

    // Stores count of even numbers
    // in the range [L, R]
    int count_even;

    // If L is even
    if (L % 2 == 0) {

        // Update count_even
        count_even = (R / 2) - (L / 2) + 1;
    }
    else {

        // Update count_odd
        count_even = (R / 2) - (L / 2);
    }

    // Stores count of odd numbers
    // in the range [L, R]
    int count_odd;
    if (L % 2 == 0) {

        // Update count_odd
        count_odd = ((R + 1) / 2) - ((L + 1) / 2);
    }
    else {

        // Update count_odd
        count_odd = ((R + 1) / 2) - ((L + 1) / 2) + 1;
    }

    // Stores count of pairs whose sum is even and
    // both elements of the pairs are also even
    count_even *= count_even;

    // Stores count of pairs whose sum is even and
    // both elements of the pairs are odd
    count_odd *= count_odd;

    // Print total ordered pairs whose sum is even
    cout << count_even + count_odd;
}

// Driver Code
int main()
{

    // Given L & R
    int L = 1, R = 3;

    // Function Call
    countPairs(L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

  // Function to find the count of
  // ordered pairs having even sum
  static void countPairs(int L, int R)
  {

    // Stores count of even numbers
    // in the range [L, R]
    int count_even;

    // If L is even
    if (L % 2 == 0)
    {

      // Update count_even
      count_even = (R / 2) - (L / 2) + 1;
    }
    else {

      // Update count_odd
      count_even = (R / 2) - (L / 2);
    }

    // Stores count of odd numbers
    // in the range [L, R]
    int count_odd;
    if (L % 2 == 0)
    {

      // Update count_odd
      count_odd = ((R + 1) / 2) - ((L + 1) / 2);
    }
    else
    {

      // Update count_odd
      count_odd = ((R + 1) / 2) - ((L + 1) / 2) + 1;
    }

    // Stores count of pairs whose sum is even and
    // both elements of the pairs are also even
    count_even *= count_even;

    // Stores count of pairs whose sum is even and
    // both elements of the pairs are odd
    count_odd *= count_odd;

    // Print total ordered pairs whose sum is even
    System.out.println(count_even + count_odd);
  }

  // Driver Code
  public static void main (String[] args)
  {

    // Given L & R
    int L = 1, R = 3;

    // Function Call
    countPairs(L, R);
  }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the count of
# ordered pairs having even sum
def countPairs(L, R):

    # Stores count of even numbers
    # in the range [L, R]
    count_even = 0

    # If L is even
    if (L % 2 == 0):

        # Update count_even
        count_even = ((R // 2) -
                      (L // 2) + 1)
    else:

        # Update count_odd
        count_even = ((R // 2) -
                      (L // 2))

    # Stores count of odd numbers
    # in the range [L, R]
    count_odd = 0

    if (L % 2 == 0):

        # Update count_odd
        count_odd = (((R + 1) // 2) -
                     ((L + 1) // 2))
    else:

        # Update count_odd
        count_odd = (((R + 1) // 2) -
                     ((L + 1) // 2) + 1)

    # Stores count of pairs whose sum is
    # even and both elements of the pairs
    # are also even
    count_even *= count_even

    # Stores count of pairs whose sum is
    # even and both elements of the pairs
    # are odd
    count_odd *= count_odd

    # Print total ordered pairs whose
    # sum is even
    print (count_even + count_odd)

# Driver Code
if __name__ == '__main__':

    # Given L & R
    L, R = 1, 3

    # Function Call
    countPairs(L, R)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to find the count of
  // ordered pairs having even sum
  static void countPairs(int L, int R)
  {

    // Stores count of even numbers
    // in the range [L, R]
    int count_even;

    // If L is even
    if (L % 2 == 0)
    {

      // Update count_even
      count_even = (R / 2) - (L / 2) + 1;
    }
    else
    {

      // Update count_odd
      count_even = (R / 2) - (L / 2);
    }

    // Stores count of odd numbers
    // in the range [L, R]
    int count_odd;
    if (L % 2 == 0)
    {

      // Update count_odd
      count_odd = ((R + 1) / 2) - ((L + 1) / 2);
    }
    else
    {

      // Update count_odd
      count_odd = ((R + 1) / 2) - ((L + 1) / 2) + 1;
    }

    // Stores count of pairs whose sum is even and
    // both elements of the pairs are also even
    count_even *= count_even;

    // Stores count of pairs whose sum is even and
    // both elements of the pairs are odd
    count_odd *= count_odd;

    // Print total ordered pairs whose sum is even
    Console.WriteLine(count_even + count_odd);
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // Given L & R
    int L = 1, R = 3;

    // Function Call
    countPairs(L, R);
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program of the above approach

// Function to find the count of
// ordered pairs having even sum
function countPairs(L, R)
{

    // Stores count of even numbers
    // in the range [L, R]
    let count_even;

    // If L is even
    if (L % 2 == 0)
    {

        // Update count_even
        count_even = (R / 2) - (L / 2) + 1;
    }
    else
    {

        // Update count_odd
        count_even = (R / 2) - (L / 2);
    }

    // Stores count of odd numbers
    // in the range [L, R]
    let count_odd;
    if (L % 2 == 0)
    {

        // Update count_odd
        count_odd = ((R + 1) / 2) -
                    ((L + 1) / 2);
    }
    else
    {

        // Update count_odd
        count_odd = ((R + 1) / 2) -
                    ((L + 1) / 2) + 1;
    }

    // Stores count of pairs whose sum is even and
    // both elements of the pairs are also even
    count_even *= count_even;

    // Stores count of pairs whose sum is even and
    // both elements of the pairs are odd
    count_odd *= count_odd;

    // Print total ordered pairs whose sum is even
    document.write(count_even + count_odd);
}

// Driver Code

// Given L & R
let L = 1, R = 3;

// Function Call
countPairs(L, R);

// This code is contributed by avijitmondal1998

</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)