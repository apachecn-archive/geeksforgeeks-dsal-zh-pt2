# 范围[L，R]中最长的一组回文数，其最大值和最小值之间最多有 K 个差值

> 原文:[https://www . geeksforgeeks . org/最长回文集-范围内的数字-最多有 k 个最大值和最小值之差的 l-r/](https://www.geeksforgeeks.org/longest-set-of-palindrome-numbers-from-the-range-l-r-with-at-most-k-difference-between-its-maximum-and-minimum/)

给定三个正整数 **L** 、 **R** 和 **K** ，任务是从范围**【L，R】**中找到最大的一组[回文数，使得组中存在的最大和最小元素之间的差值小于 **K** 。](https://www.geeksforgeeks.org/generate-palindromic-numbers-less-n/)

**示例:**

> **输入:** L = 50，R = 78，K = 12
> **输出:** 2
> **说明:**
> 范围内【50，78】的所有回文数字均为{55，66，77}。
> 回文数{55，66}组的最大和最小元素之差为 11，小于 K( = 12)。
> 因此，组的大小为 2。
> 
> **输入:** L = 98，R = 112，K = 13
> T3】输出: 3

**方法:**给定的问题可以用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)解决。按照以下步骤解决问题:

*   初始化一个辅助[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，说出 **arr[]，**并存储[所有出现在**【L，R】**范围内的回文数字。](https://www.geeksforgeeks.org/program-print-palindromes-given-range/)
*   定义一个函数，比如说**搜索(arr，X)**找到最右边的索引，其值小于 **X** :
    *   初始化三个变量，说**低**为 **0** ，**高**为**(arr . size()–1)**，说 **ans** 为 **-1** 。
    *   重复直到**低≤高**并执行以下操作:
        *   计算**中间**为**低+(高–低)/2** 。
        *   如果索引**中间**的值最多为**X**，则将 **ans** 的值更新为**中间**，**低**的值更新为**(中间+ 1)** 。
        *   否则，将**高值**更新为**(中-1)**。
    *   完成上述步骤后，返回**和**的值作为结果。
*   [遍历阵列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** 并执行以下步骤:
    *   使用函数 **search()** 找到小于或等于**(arr[I]+K–1)**的最右边的索引，并将其存储在一个变量中，比如 **rightIndex** 。
    *   如果 **rightIndex** 的值不等于 **-1** ，则更新**的值，将**计为**计数**和**(right index–I+1)**的最大值。
*   完成上述步骤后，打印**的值，并计算**作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to search the
// rightmost index of given number
static int search(vector<int> list, int num)
{
    int low = 0, high = list.size() - 1;

    // Store the rightmost index
    int ans = -1;

    while (low <= high)
    {

        // Calculate the mid
        int mid = low + (high - low) / 2;

        // If given number <= num
        if (list[mid] <= num)
        {

            // Assign ans = mid
            ans = mid;

            // Update low
            low = mid + 1;
        }
        else

            // Update high
            high = mid - 1;
    }

    // return ans
    return ans;
}

// Function to check if the given
// number is palindrome or not
bool isPalindrome(int n)
{
    int rev = 0;
    int temp = n;

    // Generate reverse
    // of the given number
    while (n > 0)
    {
        rev = rev * 10 + n % 10;
        n /= 10;
    }

    // If n is a palindrome
    return rev == temp;
}

// Function to find the maximum size
// of group of palindrome numbers
// having difference between maximum
// and minimum element at most K
int countNumbers(int L, int R, int K)
{

    // Stores the all the palindromic
    // numbers in the range [L, R]
    vector<int> list;

    // Traverse over the range [L, R]
    for(int i = L; i <= R; i++)
    {

        // If i is a palindrome
        if (isPalindrome(i))
        {

            // Append the number
            // in the list
            list.push_back(i);
        }
    }

    // Stores count of maximum
    // palindromic numbers
    int count = 0;

    // Iterate each element in the list
    for(int i = 0; i < list.size(); i++)
    {

        // Calculate rightmost index in
        // the list < current element + K
        int right_index = search(list,
                                 list[i] + K - 1);

        // Check if there is rightmost
        // index from the current index
        if (right_index != -1)
            count = max(count, right_index - i + 1);
    }

    // Return the count
    return count;
}

// Driver Code
int main()
{
    int L = 98, R = 112;
    int K = 13;

    cout << countNumbers(L, R, K);
}

// This code is contributed by ipg2016107
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

public class Main {

    // Function to find the maximum size
    // of group of palindrome numbers
    // having difference between maximum
    // and minimum element at most K
    static int countNumbers(int L, int R, int K)
    {
        // Stores the all the palindromic
        // numbers in the range [L, R]
        ArrayList<Integer> list
            = new ArrayList<>();

        // Traverse over the range [L, R]
        for (int i = L; i <= R; i++) {

            // If i is a palindrome
            if (isPalindrome(i)) {

                // Append the number
                // in the list
                list.add(i);
            }
        }

        // Stores count of maximum
        // palindromic numbers
        int count = 0;

        // Iterate each element in the list
        for (int i = 0; i < list.size(); i++) {

            // Calculate rightmost index in
            // the list < current element + K
            int right_index
                = search(list, list.get(i) + K - 1);

            // Check if there is rightmost
            // index from the current index
            if (right_index != -1)
                count = Math.max(count,
                                 right_index - i + 1);
        }

        // Return the count
        return count;
    }

    // Function to search the
    // rightmost index of given number
    static int search(
        ArrayList<Integer> list, int num)
    {
        int low = 0, high = list.size() - 1;

        // Store the rightmost index
        int ans = -1;

        while (low <= high) {

            // Calculate the mid
            int mid = low + (high - low) / 2;

            // If given number <= num
            if (list.get(mid) <= num) {

                // Assign ans = mid
                ans = mid;

                // Update low
                low = mid + 1;
            }
            else

                // Update high
                high = mid - 1;
        }

        // return ans
        return ans;
    }

    // Function to check if the given
    // number is palindrome or not
    static boolean isPalindrome(int n)
    {
        int rev = 0;
        int temp = n;

        // Generate reverse
        // of the given number
        while (n > 0) {
            rev = rev * 10 + n % 10;
            n /= 10;
        }

        // If n is a palindrome
        return rev == temp;
    }

    // Driver Code
    public static void main(String args[])
    {
        int L = 98, R = 112;
        int K = 13;

        System.out.print(
            countNumbers(L, R, K));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum size
# of group of palindrome numbers
# having difference between maximum
# and minimum element at most K
def countNumbers(L, R, K):

    # Stores the all the palindromic
    # numbers in the range [L, R]
    list = []

    # Traverse over the range [L, R]
    for i in range(L, R + 1):

        # If i is a palindrome
        if (isPalindrome(i)):

            # Append the number
            # in the list
            list.append(i)

    # Stores count of maximum
    # palindromic numbers
    count = 0

    # Iterate each element in the list
    for i in range(len(list)):

        # Calculate rightmost index in
        # the list < current element + K
        right_index = search(list, list[i] + K - 1)

        # Check if there is rightmost
        # index from the current index
        if (right_index != -1):
            count = max(count, right_index - i + 1)

    # Return the count
    return count

# Function to search the
# rightmost index of given number
def search(list, num):
    low, high = 0, len(list) - 1

    # Store the rightmost index
    ans = -1

    while (low <= high):

        # Calculate the mid
        mid = low + (high - low) // 2

        # If given number <= num
        if (list[mid] <= num):

            # Assign ans = mid
            ans = mid

            # Update low
            low = mid + 1
        else:
            # Update high
            high = mid - 1

    # return ans
    return ans

# Function to check if the given
# number is palindrome or not
def isPalindrome(n):
    rev = 0
    temp = n

    # Generate reverse
    # of the given number
    while (n > 0):
        rev = rev * 10 + n % 10
        n //= 10

    # If n is a palindrome
    return rev == temp

# Driver Code
if __name__ == '__main__':
    L, R = 98, 112
    K = 13

    print(countNumbers(L, R, K))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the maximum size
// of group of palindrome numbers
// having difference between maximum
// and minimum element at most K
static int countNumbers(int L, int R, int K)
{

    // Stores the all the palindromic
    // numbers in the range [L, R]
    List<int> list = new List<int>();

    // Traverse over the range [L, R]
    for(int i = L; i <= R; i++)
    {

        // If i is a palindrome
        if (isPalindrome(i))
        {

            // Append the number
            // in the list
            list.Add(i);
        }
    }

    // Stores count of maximum
    // palindromic numbers
    int count = 0;

    // Iterate each element in the list
    for(int i = 0; i < list.Count; i++)
    {

        // Calculate rightmost index in
        // the list < current element + K
        int right_index = search(list,
                                 list[i] + K - 1);

        // Check if there is rightmost
        // index from the current index
        if (right_index != -1)
            count = Math.Max(count,
                             right_index - i + 1);
    }

    // Return the count
    return count;
}

// Function to search the
// rightmost index of given number
static int search(List<int> list, int num)
{
    int low = 0, high = list.Count - 1;

    // Store the rightmost index
    int ans = -1;

    while (low <= high)
    {

        // Calculate the mid
        int mid = low + (high - low) / 2;

        // If given number <= num
        if (list[mid] <= num)
        {

            // Assign ans = mid
            ans = mid;

            // Update low
            low = mid + 1;
        }
        else

            // Update high
            high = mid - 1;
    }

    // return ans
    return ans;
}

// Function to check if the given
// number is palindrome or not
static bool isPalindrome(int n)
{
    int rev = 0;
    int temp = n;

    // Generate reverse
    // of the given number
    while (n > 0)
    {
        rev = rev * 10 + n % 10;
        n /= 10;
    }

    // If n is a palindrome
    return rev == temp;
}

// Driver Code
public static void Main(string[] args)
{
    int L = 98, R = 112;
    int K = 13;

    Console.WriteLine(countNumbers(L, R, K));
}
}

// This code is contributed by avijitmondal1998
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to search the
// rightmost index of given number
function search(list, num)
{
    var low = 0, high = list.length - 1;

    // Store the rightmost index
    var ans = -1;

    while (low <= high)
    {

        // Calculate the mid
        var mid = low + (high - low) / 2;

        // If given number <= num
        if (list[mid] <= num)
        {

            // Assign ans = mid
            ans = mid;

            // Update low
            low = mid + 1;
        }
        else

            // Update high
            high = mid - 1;
    }

    // return ans
    return ans;
}

// Function to check if the given
// number is palindrome or not
function isPalindrome(n)
{
    var rev = 0;
    var temp = n;

    // Generate reverse
    // of the given number
    while (n > 0)
    {
        rev = rev * 10 + n % 10;
        n = parseInt(n/10);
    }

    // If n is a palindrome
    return rev == temp;
}

// Function to find the maximum size
// of group of palindrome numbers
// having difference between maximum
// and minimum element at most K
function countNumbers(L, R, K)
{

    // Stores the all the palindromic
    // numbers in the range [L, R]
    var list = [];

    // Traverse over the range [L, R]
    for(var i = L; i <= R; i++)
    {

        // If i is a palindrome
        if (isPalindrome(i))
        {

            // Append the number
            // in the list
            list.push(i);
        }
    }

    // Stores count of maximum
    // palindromic numbers
    var count = 0;

    // Iterate each element in the list
    for(var i = 0; i < list.length; i++)
    {

        // Calculate rightmost index in
        // the list < current element + K
        var right_index = search(list,
                                 list[i] + K - 1);

        // Check if there is rightmost
        // index from the current index
        if (right_index != -1)
            count = Math.max(count, right_index - i + 1);
    }

    // Return the count
    return count;
}

// Driver Code
var L = 98, R = 112;
var K = 13;
document.write( countNumbers(L, R, K));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O((R–L)* log(R–L))*
***辅助空间:**O(R–L)*