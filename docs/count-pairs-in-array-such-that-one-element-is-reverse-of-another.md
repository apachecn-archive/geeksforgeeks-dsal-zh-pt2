# 对数组中的对进行计数，使一个元素与另一个元素相反

> 原文:[https://www . geesforgeks . org/count-pairs-in-array-so-one-element-is-reverse-of-other/](https://www.geeksforgeeks.org/count-pairs-in-array-such-that-one-element-is-reverse-of-another/)

给定一个数组 **arr[]** ，任务是对数组中的对进行计数，使得元素彼此相反。

**示例:**

> **输入:** arr[] = { 16，61，12，21，25 }
> **输出:** 2
> **解释:**
> 两个数字对中，一个数字与另一个数字相反的是{ 16，61}和{12，21}。
> 
> **输入:** arr[] = {10，11，12 }
> T3】输出: 0

### **方法 1:**

**方法:**想法是使用嵌套循环来获取数组中所有可能的数字对。然后，对于每一对，检查一个元素是否是另一个元素的反义词。如果是，则将所需计数增加 1。当所有对都被检查后，它们返回或打印这些对的计数。

下面是上述方法的实现:

## C++

```
// C++ program to count the pairs in array
// such that one element is reverse of another
#include <bits/stdc++.h>
using namespace std;

// Function to reverse the digits
// of the number
int reverse(int num)
{
    int rev_num = 0;

    // Loop to iterate till the number is
    // greater than 0
    while (num > 0) {

        // Extract the last digit and keep
        // multiplying it by 10 to get the
        // reverse of the number
        rev_num = rev_num * 10 + num % 10;
        num = num / 10;
    }
    return rev_num;
}

// Function to find the pairs from the array
// such that one number is reverse of
// the other
int countReverse(int arr[], int n)
{
    int res = 0;

    // Iterate through all pairs
    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)

            // Increment count if one is
            // the reverse of other
            if (reverse(arr[i]) == arr[j]) {
                res++;
            }

    return res;
}

// Driver code
int main()
{
    int a[] = { 16, 61, 12, 21, 25 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << countReverse(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the pairs in array
// such that one element is reverse of another

class Geeks {
    // Function to reverse the digits
    // of the number
    static int reverse(int num) {
        int rev_num = 0;

        // Loop to iterate till the number is
        // greater than 0
        while (num > 0) {

            // Extract the last digit and keep
            // multiplying it by 10 to get the
            // reverse of the number
            rev_num = rev_num * 10 + num % 10;
            num = num / 10;
        }
        return rev_num;
    }

    // Function to find the pairs from the
    // such that one number is reverse of
    // the other
    static int countReverse(int arr[], int n) {
        int res = 0;

        // Iterate through all pairs
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j < n; j++)

                // Increment count if one is
                // the reverse of other
                if (reverse(arr[i]) == arr[j]) {
                    res++;
                }

        return res;
    }

    // Driver code
    public static void main(String[] args) {
        int a[] = { 16, 61, 12, 21, 25 };
        int n = a.length;
        System.out.print(countReverse(a, n));
    }
}

// This code is contributed by Rajnis09
```

## 蟒蛇 3

```
# Python3 program to count the pairs in array
# such that one element is reverse of another

# Function to reverse the digits
# of the number
def reverse(num):
    rev_num = 0

    # Loop to iterate till the number is
    # greater than 0
    while (num > 0):

        # Extract the last digit and keep
        # multiplying it by 10 to get the
        # reverse of the number
        rev_num = rev_num * 10 + num % 10
        num = num // 10

    return rev_num

# Function to find the pairs from the
# such that one number is reverse of
# the other
def countReverse(arr,n):
    res = 0

    # Iterate through all pairs
    for i in range(n):
        for j in range(i + 1, n):

            # Increment count if one is
            # the reverse of other
            if (reverse(arr[i]) == arr[j]):
                res += 1

    return res

# Driver code
if __name__ == '__main__':
    a =  [16, 61, 12, 21, 25]
    n =  len(a)
    print(countReverse(a, n))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program to count the pairs in array
// such that one element is reverse of another
using System;

class GFG
{

// Function to reverse the digits
// of the number
static int reverse(int num)
{
    int rev_num = 0;

    // Loop to iterate till the number is
    // greater than 0
    while (num > 0) {

        // Extract the last digit and keep
        // multiplying it by 10 to get the
        // reverse of the number
        rev_num = rev_num * 10 + num % 10;
        num = num / 10;
    }
    return rev_num;
}

// Function to find the pairs from the
// such that one number is reverse of
// the other
static int countReverse(int []arr, int n)
{
    int res = 0;

    // Iterate through all pairs
    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)

            // Increment count if one is
            // the reverse of other
            if (reverse(arr[i]) == arr[j]) {
                res++;
            }

    return res;
}

// Driver code
public static void Main(String []arr)
{
    int []a = { 16, 61, 12, 21, 25 };
    int n = a.Length;
    Console.Write(countReverse(a, n));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// Javascript program to count the pairs in array
// such that one element is reverse of another

// Function to reverse the digits
// of the number
function reverse(num)
{
    var rev_num = 0;

    // Loop to iterate till the number is
    // greater than 0
    while (num > 0) {

        // Extract the last digit and keep
        // multiplying it by 10 to get the
        // reverse of the number
        rev_num = rev_num * 10 + num % 10;
        num = parseInt(num / 10);
    }
    return rev_num;
}

// Function to find the pairs from the array
// such that one number is reverse of
// the other
function countReverse(arr, n)
{
    var res = 0;

    // Iterate through all pairs
    for (var i = 0; i < n; i++)
        for (var j = i + 1; j < n; j++)

            // Increment count if one is
            // the reverse of other
            if (reverse(arr[i]) == arr[j]) {
                res++;
            }

    return res;
}

// Driver code
var a = [ 16, 61, 12, 21, 25 ];
var n = a.length;
document.write( countReverse(a, n));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
2
```

时间复杂度:O(N <sup>2</sup> )

辅助空间:0(1)

### 方法 2:(使用哈希映射)

我们可以观察到，这里最昂贵的操作是搜索数组中的反转元素(取 O(N))。通过使用哈希映射，这可以减少到 0(1)。

**方法**:想法是将数组的所有元素存储在哈希映射中(通过增加当前元素的频率来解决重复的问题)，并检查反转的元素重复了多少次，并将计数增加该频率。为了避免在数字是回文或我们访问它的反面时重新计数，我们需要从哈希映射中删除当前的数字(这是通过降低该数字的频率来实现的)。

## C++

```
// C++ program to count the pairs in array
// such that one element is reverse of another
#include <bits/stdc++.h>
using namespace std;

// Function to reverse the digits
// of the number
int reverse(int num)
{
    int rev_num = 0;

    // Loop to iterate till the number is
    // greater than 0
    while (num > 0) {

        // Extract the last digit and keep
        // multiplying it by 10 to get the
        // reverse of the number
        rev_num = rev_num * 10 + num % 10;
        num = num / 10;
    }
    return rev_num;
}

// Function to find the pairs from the array
// such that one number is reverse of
// the other
int countReverse(int arr[], int n)
{
    unordered_map<int, int> freq;

    // Iterate over every element in the array
    // and increase the frequency of the element
    // in hash map
    for(int i = 0; i < n; ++i)
        ++freq[arr[i]];

    int res = 0;
    // Iterate over every element in the array
    for (int i = 0; i < n; i++){

        // remove the current element from
        // the hash map by decreasing the
        // frequency to avoid counting
        // when the number is a palindrome
        // or when we visit its reverse
        --freq[arr[i]];

        // Increment the count
        // by the frequency of
        // reverse of the number
        res += freq[reverse(arr[i])];
    }
    return res;
}

// Driver code
int main() {
    int a[] = { 16, 61, 12, 21, 25 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << countReverse(a, n) << '\n';
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the
// pairs in array such that
// one element is reverse of
// another
import java.util.*;
class GFG{

// Function to reverse the digits
// of the number
public static int reverse(int num)
{
  int rev_num = 0;

  // Loop to iterate till
  // the number is greater
  // than 0
  while (num > 0)
  {
    // Extract the last digit
    // and keep multiplying it
    // by 10 to get the reverse
    // of the number
    rev_num = rev_num * 10 +
              num % 10;
    num = num / 10;
  }
  return rev_num;
}

// Function to find the pairs
// from the array such that
// one number is reverse of the
// other
public static int countReverse(int arr[],
                               int n)
{
  HashMap<Integer,
          Integer> freq =
          new HashMap<>();

  // Iterate over every element
  // in the array and increase
  // the frequency of the element
  // in hash map
  for(int i = 0; i < n; ++i)
  {
    if(freq.containsKey(arr[i]))
    {
      freq.replace(arr[i],
      freq.get(arr[i]) + 1);
    }
    else
    {
      freq.put(arr[i], 1);
    }
  }

  int res = 0;

  // Iterate over every element
  // in the array
  for (int i = 0; i < n; i++)
  {
    // remove the current element from
    // the hash map by decreasing the
    // frequency to avoid counting
    // when the number is a palindrome
    // or when we visit its reverse
    if(freq.containsKey(arr[i]))
    {
      freq.replace(arr[i],
      freq.get(arr[i]) - 1);
    }
    else
    {
      freq.put(arr[i], -1);
    }

    // Increment the count
    // by the frequency of
    // reverse of the number
    if(freq.containsKey(reverse(arr[i])))
    {
      res += freq.get(reverse(arr[i]));
    }
  }
  return res;
}

// Driver code   
public static void main(String[] args)
{
  int a[] = {16, 61, 12, 21, 25};
  int n = a.length;
  System.out.println(countReverse(a, n));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to count
# the pairs in array such
# that one element is reverse
# of another
from collections import defaultdict

# Function to reverse
# the digits of the number
def reverse(num):

    rev_num = 0

    # Loop to iterate till
    # the number is greater than 0
    while (num > 0):

        # Extract the last digit and keep
        # multiplying it by 10 to get the
        # reverse of the number
        rev_num = rev_num * 10 + num % 10
        num = num // 10

    return rev_num

# Function to find the pairs
# from the array such that
# one number is reverse of
# the other
def countReverse(arr, n):

    freq = defaultdict (int)

    # Iterate over every element
    # in the array and increase
    # the frequency of the element
    # in hash map
    for i in range (n):
        freq[arr[i]] += 1

    res = 0

    # Iterate over every
    # element in the array
    for i in range (n):

        # remove the current element from
        # the hash map by decreasing the
        # frequency to avoid counting
        # when the number is a palindrome
        # or when we visit its reverse
        freq[arr[i]] -= 1

        # Increment the count
        # by the frequency of
        # reverse of the number
        res += freq[reverse(arr[i])]

    return res

# Driver code
if __name__ == "__main__":

    a = [16, 61, 12, 21, 25]
    n = len(a)
    print (countReverse(a, n))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to count the
// pairs in array such that
// one element is reverse of
// another
using System;
using System.Collections.Generic;  

class GFG{

// Function to reverse the digits
// of the number
static int reverse(int num)
{
    int rev_num = 0;

    // Loop to iterate till
    // the number is greater
    // than 0
    while (num > 0)
    {

        // Extract the last digit
        // and keep multiplying it
        // by 10 to get the reverse
        // of the number
        rev_num = rev_num * 10 +
                      num % 10;
        num = num / 10;
    }
    return rev_num;
}

// Function to find the pairs
// from the array such that
// one number is reverse of the
// other
static int countReverse(int[] arr, int n)
{
    Dictionary<int,
               int> freq = new Dictionary<int,
                                          int>(); 

    // Iterate over every element
    // in the array and increase
    // the frequency of the element
    // in hash map
    for(int i = 0; i < n; ++i)
    {
        if (freq.ContainsKey(arr[i]))
        {
            freq[arr[i]]++;
        }
        else
        {
            freq.Add(arr[i], 1);
        }
    }

    int res = 0;

    // Iterate over every element
    // in the array
    for(int i = 0; i < n; i++)
    {

        // Remove the current element from
        // the hash map by decreasing the
        // frequency to avoid counting
        // when the number is a palindrome
        // or when we visit its reverse
        if (freq.ContainsKey(arr[i]))
        {
            freq[arr[i]]--;
        }
        else
        {
            freq.Add(arr[i], -1);
        }

        // Increment the count
        // by the frequency of
        // reverse of the number
        if (freq.ContainsKey(reverse(arr[i])))
        {
            res += freq[reverse(arr[i])];
        }
    }
    return res;
}

// Driver code   
static void Main()
{
    int[] a = { 16, 61, 12, 21, 25 };
    int n = a.Length;

    Console.WriteLine(countReverse(a, n));
}
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>
// Javascript program to count the
// pairs in array such that
// one element is reverse of
// another

// Function to reverse the digits
// of the number
function reverse(num)
{
    let rev_num = 0;

      // Loop to iterate till
      // the number is greater
      // than 0
      while (num > 0)
      {
        // Extract the last digit
        // and keep multiplying it
        // by 10 to get the reverse
        // of the number
        rev_num = rev_num * 10 +
              num % 10;
        num = Math.floor(num / 10);
      }
      return rev_num;
}

// Function to find the pairs
// from the array such that
// one number is reverse of the
// other
function countReverse(arr,n)
{
     let freq = new Map();

      // Iterate over every element
      // in the array and increase
      // the frequency of the element
      // in hash map
      for(let i = 0; i < n; ++i)
      {
        if(freq.has(arr[i]))
        {
          freq.set(arr[i],
          freq.get(arr[i]) + 1);
        }
        else
        {
          freq.set(arr[i], 1);
        }
      }

     let res = 0;

     // Iterate over every element
      // in the array
      for (let i = 0; i < n; i++)
      {
        // remove the current element from
        // the hash map by decreasing the
        // frequency to avoid counting
        // when the number is a palindrome
        // or when we visit its reverse
        if(freq.has(arr[i]))
        {
              freq.set(arr[i],
              freq.get(arr[i]) - 1);
        }
        else
        {
              freq.set(arr[i], -1);
        }

        // Increment the count
        // by the frequency of
        // reverse of the number
        if(freq.has(reverse(arr[i])))
        {
              res += freq.get(reverse(arr[i]));
        }
      }
      return res;
}

// Driver code  
let a=[16, 61, 12, 21, 25];
let n = a.length;
document.write(countReverse(a, n));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output**

```
2
```

时间复杂度:0(N)

辅助空间:O(N)