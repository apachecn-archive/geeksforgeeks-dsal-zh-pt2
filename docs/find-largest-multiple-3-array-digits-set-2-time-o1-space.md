# 从数字数组中找到 3 的最大倍数|集合 2(在 O(n)时间和 O(1)空间中)

> 原文:[https://www . geesforgeks . org/find-最大-倍数-3-数组-数字-集合-2-time-o1-space/](https://www.geeksforgeeks.org/find-largest-multiple-3-array-digits-set-2-time-o1-space/)

给定一个数字数组(包含从 0 到 9 的元素)。从数组的**部分或全部数字**中找出能被 3 整除的最大数。同一元素可能在数组中出现多次，但数组中的每个元素只能使用一次。
**例:**

```
Input : arr[] = {5, 4, 3, 1, 1} 
Output : 4311

Input : Arr[] = {5, 5, 5, 7} 
Output : 555 
```

问于:**谷歌采访**

我们已经讨论了基于[队列的解决方案](https://www.geeksforgeeks.org/find-the-largest-number-multiple-of-3/)。这两种解决方案(在之前和这篇文章中讨论过)都是基于这样一个事实，即[当且仅当一个数的位数之和可被 3 整除时，该数可被 3 整除。](https://www.geeksforgeeks.org/check-large-number-divisible-3-not/)
举个例子，我们考虑 555，它能被 3 整除，因为数字的和是 5 + 5 + 5 = 15，它能被 3 整除。如果数字的总和不能被 3 整除，那么余数应该是 1 或 2。
如果我们得到余数‘1’或‘2’，我们必须去掉最大两位数，才能得到可被 3 整除的数:

1.  如果余数为“1”:我们必须删除余数为“1”的单个数字，或者我们必须删除余数为“2”的两个数字(2+2 = > 4% 3 = >“1”)
2.  如果余数为“2”:我们必须删除余数为“2”的单个数字，或者我们必须删除余数为“1”的两个数字(1 + 1 => 2 % 3 => 2)。

示例:

```
Input : arr[] = 5, 5, 5, 7 
Sum of digits = 5 + 5 + 5 + 7 = 22
Remainder = 22 % 3 = 1 
We remove smallest single digit that 
has remainder '1'. We remove 7 % 3 = 1 
So largest number divisible by 3 is : 555

Let's take an another example :
Input : arr[]  = 4 , 4 , 1 , 1 , 1 , 3
Sum of digits  = 4 + 4 + 1 + 1 + 1 + 3 = 14
Reminder = 14 % 3 = 2 
We have to remove the smallest digit that 
has remainder ' 2 ' or two digits that have
remainder '1'. Here there is no digit with 
reminder '2', so we have to remove two smallest 
digits that have remainder '1'. The digits are : 
1, 1\. So largest number divisible by 3 is 4 4 3 1 
```

以下是上述想法的实现。

## C++

```
// C++ program to find the largest number
// that can be mode from elements of the
// array and is divisible by 3
#include<bits/stdc++.h>
using namespace std;

// Number of digits
#define MAX_SIZE 10

// function to sort array of digits using
// counts
void sortArrayUsingCounts(int arr[], int n)
{
    // Store count of all elements
    int count[MAX_SIZE] = {0};
    for (int i = 0; i < n; i++)
        count[arr[i]]++;

    // Store
    int index = 0;
    for (int i = 0; i < MAX_SIZE; i++)
        while (count[i] > 0)
            arr[index++] = i, count[i]--;
}

// Remove elements from arr[] at indexes ind1 and ind2
bool removeAndPrintResult(int arr[], int n, int ind1,
                                        int ind2 = -1)
{
    for (int i = n-1; i >=0; i--)
        if (i != ind1 && i != ind2)
            cout << arr[i] ;
}

// Returns largest multiple of 3 that can be formed
// using arr[] elements.
bool largest3Multiple(int arr[], int n)
{
    // Sum of all array element
    int sum = accumulate(arr, arr+n, 0);

    // Sort array element in increasing order
    sortArrayUsingCounts(arr, n);

    // Sum is divisible by 3 , no need to
    // delete an element
    if (sum%3 == 0)
    {  
          removeAndPrintResult(arr,n,-1,-1);
          return true ;
    }

    // Find reminder
    int remainder = sum % 3;

    // If remainder is '1', we have to delete either
    // one element of remainder '1' or two elements
    // of remainder '2'
    if (remainder == 1)
    {
        int rem_2[2];
        rem_2[0] = -1, rem_2[1] = -1;

        // Traverse array elements
        for (int i = 0 ; i < n ; i++)
        {
            // Store first element of remainder '1'
            if (arr[i]%3 == 1)
            {
                removeAndPrintResult(arr, n, i);
                return true;
            }

            if (arr[i]%3 == 2)
            {
                // If this is first occurrence of remainder 2
                if (rem_2[0] == -1)
                    rem_2[0] = i;

                // If second occurrence
                else if (rem_2[1] == -1)
                    rem_2[1] = i;
            }
        }

        if (rem_2[0] != -1 && rem_2[1] != -1)
        {
            removeAndPrintResult(arr, n, rem_2[0], rem_2[1]);
            return true;
        }
    }

    // If remainder is '2', we have to delete either
    // one element of remainder '2' or two elements
    // of remainder '1'
    else if (remainder == 2)
    {
        int rem_1[2];
        rem_1[0] = -1, rem_1[1] = -1;

        // traverse array elements
        for (int i = 0; i < n; i++)
        {
            // store first element of remainder '2'
            if (arr[i]%3 == 2)
            {
                removeAndPrintResult(arr, n, i);
                return true;
            }

            if (arr[i]%3 == 1)
            {
                // If this is first occurrence of remainder 1
                if (rem_1[0] == -1)
                    rem_1[0] = i;

                // If second occurrence
                else if (rem_1[1] == -1)
                    rem_1[1] = i;
            }
        }

        if (rem_1[0] != -1 && rem_1[1] != -1)
        {
            removeAndPrintResult(arr, n, rem_1[0], rem_1[1]);
            return true;
        }
    }

    cout << "Not possible";
    return false;
}

// Driver code
int main()
{
    int arr[] = {4, 4, 1, 1, 1, 3 } ;
    int n = sizeof(arr)/sizeof(arr[0]);
    largest3Multiple(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the largest number
// that can be mode from elements of the
// array and is divisible by 3
import java.util.*;

class GFG 
{

    // Number of digits
    static int MAX_SIZE = 10;

    // function to sort array of digits using
    // counts
    static void sortArrayUsingCounts(int arr[], 
                                     int n)
    {
        // Store count of all elements
        int[] count = new int[MAX_SIZE];
        for (int i = 0; i < n; i++) 
        {
            count[arr[i]]++;
        }

        // Store
        int index = 0;
        for (int i = 0; i < MAX_SIZE; i++) 
        {
            while (count[i] > 0) 
            {
                arr[index++] = i;
                count[i]--;
            }
        }
    }

    // Remove elements from arr[]
    // at indexes ind1 and ind2
    static void removeAndPrintResult(int arr[], int n, 
                                     int ind1, int ind2)
    {
        for (int i = n - 1; i >= 0; i--)
        {
            if (i != ind1 && i != ind2) 
            {
                System.out.print(arr[i]);
            }
        }
    }

    // Returns largest multiple of 3 
    // that can be formed using
    // arr[] elements.
    static boolean largest3Multiple(int arr[], 
                                    int n)
    {
        // Sum of all array element
        int sum = accumulate(arr, 0, n);

        // Sort array element in increasing order
        sortArrayUsingCounts(arr, n);

        // If sum is divisible by 3, 
        // no need to delete an element
        if (sum % 3 == 0) 
        {
            removeAndPrintResult(arr, n, -1, -1);
            return true;
        }

        // Find reminder
        int remainder = sum % 3;

        // If remainder is '1', we have to 
        // delete either one element of 
        // remainder '1' or two elements of 
        // remainder '2'
        if (remainder == 1)
        {
            int[] rem_2 = new int[2];
            rem_2[0] = -1;
            rem_2[1] = -1;

            // Traverse array elements
            for (int i = 0; i < n; i++) 
            {

                // Store first element of remainder '1'
                if (arr[i] % 3 == 1)
                {
                    removeAndPrintResult(arr, n, i, -1);
                    return true;
                }

                if (arr[i] % 3 == 2)
                {

                    // If this is first occurrence
                    // of remainder 2
                    if (rem_2[0] == -1)
                    {
                        rem_2[0] = i;
                    }

                    // If second occurrence
                    else if (rem_2[1] == -1) 
                    {
                        rem_2[1] = i;
                    }
                }
            }

            if (rem_2[0] != -1 && 
                rem_2[1] != -1) 
            {
                removeAndPrintResult(arr, n, rem_2[0], 
                                             rem_2[1]);
                return true;
            }
        } 

        // If remainder is '2', we have to 
        // delete either one element of 
        // remainder '2' or two elements of
        // remainder '1'
        else if (remainder == 2) 
        {
            int[] rem_1 = new int[2];
            rem_1[0] = -1;
            rem_1[1] = -1;

            // traverse array elements
            for (int i = 0; i < n; i++) 
            {

                // store first element of remainder '2'
                if (arr[i] % 3 == 2) 
                {
                    removeAndPrintResult(arr, n, i, -1);
                    return true;
                }

                if (arr[i] % 3 == 1) 
                {

                    // If this is first occurrence
                    // of remainder 1
                    if (rem_1[0] == -1) 
                    {
                        rem_1[0] = i;
                    } 

                    // If second occurrence
                    else if (rem_1[1] == -1) 
                    {
                        rem_1[1] = i;
                    }
                }
            }

            if (rem_1[0] != -1 && 
                rem_1[1] != -1)
            {
                removeAndPrintResult(arr, n, rem_1[0], 
                                             rem_1[1]);
                return true;
            }
        }
        System.out.print("Not possible");
        return false;
    }

    static int accumulate(int[] arr,
                          int start, 
                          int end) 
    {
        int sum = 0;
        for (int i = 0; i < arr.length; i++) 
        {
            sum += arr[i];
        }
        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {4, 4, 1, 1, 1, 3};
        int n = arr.length;
        largest3Multiple(arr, n);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the largest number
# that can be mode from elements of the
# array and is divisible by 3

# Number of digits
MAX_SIZE = 10

# function to sort array of digits using
# counts
def sortArrayUsingCounts(arr, n):

    # Store count of all elements
    count = [0]*MAX_SIZE
    for i in range(n):
        count[arr[i]] += 1

    # Store
    index = 0
    for i in range(MAX_SIZE):
        while count[i] > 0:
            arr[index] = i
            index += 1
            count[i] -= 1

# Remove elements from arr[] at indexes ind1 and ind2
def removeAndPrintResult(arr, n, ind1, ind2=-1):
    for i in range(n-1, -1, -1):
        if i != ind1 and i != ind2:
            print(arr[i], end="")

# Returns largest multiple of 3 that can be formed
# using arr[] elements.
def largest3Multiple(arr, n):

    # Sum of all array element
    s = sum(arr)

    # Sort array element in increasing order
    sortArrayUsingCounts(arr, n)

    # Sum is divisible by 3, no need to
    # delete an element
    if s % 3 == 0:
        removeAndPrintResult(arr, n, -1)
        return True

    # Find reminder
    remainder = s % 3

    # If remainder is '1', we have to delete either
    # one element of remainder '1' or two elements
    # of remainder '2'
    if remainder == 1:
        rem_2 = [0]*2
        rem_2[0] = -1; rem_2[1] = -1

        # Traverse array elements
        for i in range(n):

            # Store first element of remainder '1'
            if arr[i] % 3 == 1:
                removeAndPrintResult(arr, n, i)
                return True

            if arr[i] % 3 == 2:

                # If this is first occurrence of remainder 2
                if rem_2[0] == -1:
                    rem_2[0] = i

                # If second occurrence
                elif rem_2[1] == -1:
                    rem_2[1] = i

        if rem_2[0] != -1 and rem_2[1] != -1:
            removeAndPrintResult(arr, n, rem_2[0], rem_2[1])
            return True

    # If remainder is '2', we have to delete either
    # one element of remainder '2' or two elements
    # of remainder '1'
    elif remainder == 2:
        rem_1 = [0]*2
        rem_1[0] = -1; rem_1[1] = -1

        # traverse array elements
        for i in range(n):

            # store first element of remainder '2'
            if arr[i] % 3 == 2:
                removeAndPrintResult(arr, n, i)
                return True

            if arr[i] % 3 == 1:

                # If this is first occurrence of remainder 1
                if rem_1[0] == -1:
                    rem_1[0] = i

                # If second occurrence
                elif rem_1[1] == -1:
                    rem_1[1] = i

        if rem_1[0] != -1 and rem_1[1] != -1:
            removeAndPrintResult(arr, n, rem_1[0], rem_1[1])
            return True

    print("Not possible")
    return False

# Driver code
if __name__ == "__main__":

    arr = [4, 4, 1, 1, 1, 3]
    n = len(arr)
    largest3Multiple(arr, n)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to find the largest number
// that can be mode from elements of the
// array and is divisible by 3
using System;

class GFG 
{

    // Number of digits
    static int MAX_SIZE = 10;

    // function to sort array of digits using
    // counts
    static void sortArrayUsingCounts(int []arr, 
                                     int n)
    {
        // Store count of all elements
        int[] count = new int[MAX_SIZE];
        for (int i = 0; i < n; i++) 
        {
            count[arr[i]]++;
        }

        // Store
        int index = 0;
        for (int i = 0; i < MAX_SIZE; i++) 
        {
            while (count[i] > 0) 
            {
                arr[index++] = i;
                count[i]--;
            }
        }
    }

    // Remove elements from arr[]
    // at indexes ind1 and ind2
    static void removeAndPrintResult(int []arr, int n, 
                                     int ind1, int ind2)
    {
        for (int i = n - 1; i >= 0; i--)
        {
            if (i != ind1 && i != ind2) 
            {
                Console.Write(arr[i]);
            }
        }
    }

    // Returns largest multiple of 3 
    // that can be formed using
    // arr[] elements.
    static Boolean largest3Multiple(int []arr, 
                                    int n)
    {
        // Sum of all array element
        int sum = accumulate(arr, 0, n);

        // Sort array element in increasing order
        sortArrayUsingCounts(arr, n);

        // If sum is divisible by 3, 
        // no need to delete an element
        if (sum % 3 == 0) 
        {
            removeAndPrintResult(arr, n, -1, -1);
            return true;
        }

        // Find reminder
        int remainder = sum % 3;

        // If remainder is '1', we have to 
        // delete either one element of 
        // remainder '1' or two elements of 
        // remainder '2'
        if (remainder == 1)
        {
            int[] rem_2 = new int[2];
            rem_2[0] = -1;
            rem_2[1] = -1;

            // Traverse array elements
            for (int i = 0; i < n; i++) 
            {

                // Store first element of remainder '1'
                if (arr[i] % 3 == 1)
                {
                    removeAndPrintResult(arr, n, i, -1);
                    return true;
                }

                if (arr[i] % 3 == 2)
                {

                    // If this is first occurrence
                    // of remainder 2
                    if (rem_2[0] == -1)
                    {
                        rem_2[0] = i;
                    }

                    // If second occurrence
                    else if (rem_2[1] == -1) 
                    {
                        rem_2[1] = i;
                    }
                }
            }

            if (rem_2[0] != -1 && 
                rem_2[1] != -1) 
            {
                removeAndPrintResult(arr, n, rem_2[0], 
                                              rem_2[1]);
                return true;
            }
        } 

        // If remainder is '2', we have to 
        // delete either one element of 
        // remainder '2' or two elements of
        // remainder '1'
        else if (remainder == 2) 
        {
            int[] rem_1 = new int[2];
            rem_1[0] = -1;
            rem_1[1] = -1;

            // traverse array elements
            for (int i = 0; i < n; i++) 
            {

                // store first element of remainder '2'
                if (arr[i] % 3 == 2) 
                {
                    removeAndPrintResult(arr, n, i, -1);
                    return true;
                }

                if (arr[i] % 3 == 1) 
                {

                    // If this is first occurrence
                    // of remainder 1
                    if (rem_1[0] == -1) 
                    {
                        rem_1[0] = i;
                    } 

                    // If second occurrence
                    else if (rem_1[1] == -1) 
                    {
                        rem_1[1] = i;
                    }
                }
            }

            if (rem_1[0] != -1 && 
                rem_1[1] != -1)
            {
                removeAndPrintResult(arr, n, rem_1[0], 
                                             rem_1[1]);
                return true;
            }
        }
        Console.Write("Not possible");
        return false;
    }

    static int accumulate(int[] arr,
                          int start, 
                          int end) 
    {
        int sum = 0;
        for (int i = 0; i < arr.Length; i++) 
        {
            sum += arr[i];
        }
        return sum;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {4, 4, 1, 1, 1, 3};
        int n = arr.Length;
        largest3Multiple(arr, n);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// JavaScript program to find the largest number
// that can be mode from elements of the
// array and is divisible by 3

// Number of digits
const MAX_SIZE = 10;

// function to sort array of digits using
// counts
function sortArrayUsingCounts(arr, n)
{
    // Store count of all elements
    let count = new Uint8Array(MAX_SIZE);
    for (let i = 0; i < n; i++)
        count[arr[i]]++;

    // Store
    let index = 0;
    for (let i = 0; i < MAX_SIZE; i++)
        while (count[i] > 0)
            arr[index++] = i, count[i]--;
}

// Remove elements from arr[] at indexes ind1 and ind2
function removeAndPrintResult(arr, n, ind1, ind2 = -1)
{
    for (let i = n-1; i >=0; i--)
        if (i != ind1 && i != ind2)
            document.write(arr[i]) ;
}

// Returns largest multiple of 3 that can be formed
// using arr[] elements.
function largest3Multiple(arr, n)
{
    // Sum of all array element
    let sum = arr.reduce((a, b) => a + b, 0);

    // Sort array element in increasing order
    sortArrayUsingCounts(arr, n);

    // Sum is divisible by 3 , no need to
    // delete an element
    if (sum%3 == 0)
    {   
        removeAndPrintResult(arr, n, -1);
        return true ;
    }

    // Find reminder
    let remainder = sum % 3;

    // If remainder is '1', we have to delete either
    // one element of remainder '1' or two elements
    // of remainder '2'
    if (remainder == 1)
    {
        let rem_2 = new Array(2);
        rem_2[0] = -1, rem_2[1] = -1;

        // Traverse array elements
        for (let i = 0 ; i < n ; i++)
        {
            // Store first element of remainder '1'
            if (arr[i]%3 == 1)
            {
                removeAndPrintResult(arr, n, i);
                return true;
            }

            if (arr[i]%3 == 2)
            {
                // If this is first occurrence of remainder 2
                if (rem_2[0] == -1)
                    rem_2[0] = i;

                // If second occurrence
                else if (rem_2[1] == -1)
                    rem_2[1] = i;
            }
        }

        if (rem_2[0] != -1 && rem_2[1] != -1)
        {
            removeAndPrintResult(arr, n, rem_2[0], rem_2[1]);
            return true;
        }
    }

    // If remainder is '2', we have to delete either
    // one element of remainder '2' or two elements
    // of remainder '1'
    else if (remainder == 2)
    {
        let rem_1 = new Array(2);
        rem_1[0] = -1, rem_1[1] = -1;

        // traverse array elements
        for (let i = 0; i < n; i++)
        {
            // store first element of remainder '2'
            if (arr[i]%3 == 2)
            {
                removeAndPrintResult(arr, n, i);
                return true;
            }

            if (arr[i]%3 == 1)
            {
                // If this is first occurrence of remainder 1
                if (rem_1[0] == -1)
                    rem_1[0] = i;

                // If second occurrence
                else if (rem_1[1] == -1)
                    rem_1[1] = i;
            }
        }

        if (rem_1[0] != -1 && rem_1[1] != -1)
        {
            removeAndPrintResult(arr, n, rem_1[0], rem_1[1]);
            return true;
        }
    }

    document.write("Not possible");
    return false;
}

// Driver code
    let arr = [4 , 4 , 1 , 1 , 1 , 3];
    let n = arr.length;
    largest3Multiple(arr, n);

// This code is contributed by Surbhi Tyagi.
</script>
```

**输出:**

```
4431
```

**时间复杂度:** O(n)
本文由 [**尼尚辛格**](https://practice.geeksforgeeks.org/user-profile.php?user=_code) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。