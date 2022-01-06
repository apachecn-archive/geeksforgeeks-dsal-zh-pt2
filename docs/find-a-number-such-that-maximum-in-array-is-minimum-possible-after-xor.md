# 求一个数，使异或后数组中的最大值最小

> 原文:[https://www . geesforgeks . org/find-a-number-so-max-in-array-is-minimum-after-xor/](https://www.geeksforgeeks.org/find-a-number-such-that-maximum-in-array-is-minimum-possible-after-xor/)

给定一个非负整数数组。选择一个整数 **P** ，将 **P** 与数组的所有元素进行异或运算。任务是选择 **P** ，使得在用 P 对数组的所有元素进行异或运算后，数组的最大值尽可能最小

**示例:**

> **输入:** arr = {3，2，1}
> **输出:** 2
> **解释:**
> 我们可以选择 P = 3，这样取异或后最大元素是最小可能的。
> 取异或后，arr = {0，1，2}
> 2 是最小可能值。
> **输入:** arr = {5，1}
> **输出:** 4

**进场:**

*   我们可以从最高有效位开始递归地解决这个问题。
*   将元素分成两组，一组元素的当前位为开(1)，另一组元素的当前位为关(0)。
*   如果任何一组都是空的，我们可以相应地分配 P 的当前位，这样我们的答案中的当前位就关闭了。
*   否则，如果两个组都不是空的，那么无论我们给 P 的当前位分配什么值，在我们的答案中，这个位都是 on(1)。
*   现在，为了决定给 P 的当前位分配哪个值，我们将递归调用下一位的每个组，并返回两者的最小值。

下面是上述方法的实现:

## C++

```
// C++ program that find the minimum
// possible maximum
#include <bits/stdc++.h>
using namespace std;

// Recursive function that find the
//  minimum value after exclusive-OR
int RecursiveFunction(vector<int> ref,
                      int bit)
{
    // Condition if ref size is zero or
    // bit is negative then return 0
    if (ref.size() == 0 || bit < 0)
        return 0;

    vector<int> curr_on, curr_off;

    for (int i = 0; i < ref.size(); i++)
    {
        // Condition if current bit is
        // off then push current value
        // in curr_off vector
        if (((ref[i] >> bit) & 1) == 0)
            curr_off.push_back(ref[i]);

        // Condition if current bit is on
        // then push current value in
        // curr_on vector
        else
            curr_on.push_back(ref[i]);
    }

    // Condition if curr_off is empty
    // then call recursive function
    // on curr_on vector
    if (curr_off.size() == 0)
        return RecursiveFunction(curr_on,
                                 bit - 1);

    // Condition if curr_on is empty
    // then call recursive function
    // on curr_off vector
    if (curr_on.size() == 0)
        return RecursiveFunction(curr_off,
                                 bit - 1);

    // Return the minimum of curr_off and 
    // curr_on and add power of 2 of
    // current bit
    return min(RecursiveFunction(curr_off,
                                 bit - 1),
               RecursiveFunction(curr_on,
                                 bit - 1))
           + (1 << bit);
}

// Function that print the minimum
// value after exclusive-OR
void PrintMinimum(int a[], int n)
{
    vector<int> v;

    // Pushing values in vector
    for (int i = 0; i < n; i++)
        v.push_back(a[i]);

    // Printing answer
    cout << RecursiveFunction(v, 30)
         << "\n";
}

// Driver Code
int main()
{
    int arr[] = { 3, 2, 1 };

    int size = sizeof(arr) / sizeof(arr[0]);

    PrintMinimum(arr, size);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program that find the minimum
// possible maximum
import java.util.*;

class GFG{

// Recursive function that find the
// minimum value after exclusive-OR
static int RecursiveFunction(ArrayList<Integer> ref,
                             int bit)
{

    // Condition if ref size is zero or
    // bit is negative then return 0
    if (ref.size() == 0 || bit < 0)
        return 0;

    ArrayList<Integer> curr_on = new ArrayList<>();
    ArrayList<Integer> curr_off = new ArrayList<>();

    for(int i = 0; i < ref.size(); i++)
    {

        // Condition if current bit is
        // off then push current value
        // in curr_off vector
        if (((ref.get(i) >> bit) & 1) == 0)
            curr_off.add(ref.get(i));

        // Condition if current bit is on
        // then push current value in
        // curr_on vector
        else
            curr_on.add(ref.get(i));
    }

    // Condition if curr_off is empty
    // then call recursive function
    // on curr_on vector
    if (curr_off.size() == 0)
        return RecursiveFunction(curr_on, bit - 1);

    // Condition if curr_on is empty
    // then call recursive function
    // on curr_off vector
    if (curr_on.size() == 0)
        return RecursiveFunction(curr_off, bit - 1);

    // Return the minimum of curr_off and
    // curr_on and add power of 2 of
    // current bit
    return Math.min(RecursiveFunction(curr_off,
                                      bit - 1),
                    RecursiveFunction(curr_on,
                                      bit - 1)) +
                                     (1 << bit);
}

// Function that print the minimum
// value after exclusive-OR
static void PrintMinimum(int a[], int n)
{
    ArrayList<Integer> v = new ArrayList<>();

    // Pushing values in vector
    for(int i = 0; i < n; i++)
        v.add(a[i]);

    // Printing answer
    System.out.println(RecursiveFunction(v, 30));
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 3, 2, 1 };
    int size = arr.length;

    PrintMinimum(arr, size);
}
}

// This code is contributed by jrishabh99
```

## 蟒蛇 3

```
# Python3 program that find
# the minimum  possible maximum

# Recursive function that find the
#  minimum value after exclusive-OR
def RecursiveFunction(ref, bit):

    # Condition if ref size is zero or
    # bit is negative then return 0
    if(len(ref) == 0 or bit < 0):
        return 0;
    curr_on = []
    curr_off = []

    for i in range(len(ref)):

        # Condition if current bit is 
        # off then push current value 
        # in curr_off vector
        if(((ref[i] >> bit) & 1) == 0):
            curr_off.append(ref[i])

        # Condition if current bit is on 
        # then push current value in 
        # curr_on vector
        else:
            curr_on.append(ref[i])

    # Condition if curr_off is empty
    # then call recursive function
    # on curr_on vector
    if(len(curr_off) == 0):
        return RecursiveFunction(curr_on,
                                 bit - 1)

    # Condition if curr_on is empty
    # then call recursive function
    # on curr_off vector
    if(len(curr_on) == 0):
        return RecursiveFunction(curr_off,
                                 bit - 1)

    # Return the minimum of curr_off and  
    # curr_on and add power of 2 of
    # current bit
    return(min(RecursiveFunction(curr_off,
                                 bit - 1),
               RecursiveFunction(curr_on,
                                 bit - 1)) + (1 << bit))

# Function that print the minimum
# value after exclusive-OR
def PrintMinimum(a, n):
    v = []

    # Pushing values in vector
    for i in range(n):
        v.append(a[i])

    # Printing answer
    print(RecursiveFunction(v, 30))

# Driver Code
arr = [3, 2, 1]
size = len(arr)
PrintMinimum(arr, size)

#This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program that find the minimum
// possible maximum
using System;
using System.Collections.Generic;

class GFG{

// Recursive function that find the
// minimum value after exclusive-OR
static int RecursiveFunction(List<int> re,
                             int bit)
{

    // Condition if ref size is zero or
    // bit is negative then return 0
    if (re.Count == 0 || bit < 0)
        return 0;

    List<int> curr_on = new List<int>();
    List<int> curr_off = new List<int>();

    for(int i = 0; i < re.Count; i++)
    {

        // Condition if current bit is
        // off then push current value
        // in curr_off vector
        if (((re[i] >> bit) & 1) == 0)
            curr_off.Add(re[i]);

        // Condition if current bit is on
        // then push current value in
        // curr_on vector
        else
            curr_on.Add(re[i]);
    }

    // Condition if curr_off is empty
    // then call recursive function
    // on curr_on vector
    if (curr_off.Count == 0)
        return RecursiveFunction(curr_on,
                                 bit - 1);

    // Condition if curr_on is empty
    // then call recursive function
    // on curr_off vector
    if (curr_on.Count == 0)
        return RecursiveFunction(curr_off,
                                 bit - 1);

    // Return the minimum of curr_off and
    // curr_on and add power of 2 of
    // current bit
    return Math.Min(RecursiveFunction(curr_off,
                                      bit - 1),
                    RecursiveFunction(curr_on,
                                      bit - 1)) +
                                     (1 << bit);
}

// Function that print the minimum
// value after exclusive-OR
static void PrintMinimum(int []a, int n)
{
    List<int> v = new List<int>();

    // Pushing values in vector
    for(int i = 0; i < n; i++)
        v.Add(a[i]);

    // Printing answer
    Console.WriteLine(RecursiveFunction(v, 30));
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 3, 2, 1 };
    int size = arr.Length;

    PrintMinimum(arr, size);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program that find the minimum
// possible maximum

// Recursive function that find the
//  minimum value after exclusive-OR
function RecursiveFunction(ref, bit)
{
    // Condition if ref size is zero or
    // bit is negative then return 0
    if (ref.length == 0 || bit < 0)
        return 0;

    let curr_on = [], curr_off = [];

    for (let i = 0; i < ref.length; i++)
    {
        // Condition if current bit is
        // off then push current value
        // in curr_off vector
        if (((ref[i] >> bit) & 1) == 0)
            curr_off.push(ref[i]);

        // Condition if current bit is on
        // then push current value in
        // curr_on vector
        else
            curr_on.push(ref[i]);
    }

    // Condition if curr_off is empty
    // then call recursive function
    // on curr_on vector
    if (curr_off.length == 0)
        return RecursiveFunction(curr_on,
                                 bit - 1);

    // Condition if curr_on is empty
    // then call recursive function
    // on curr_off vector
    if (curr_on.length == 0)
        return RecursiveFunction(curr_off,
                                 bit - 1);

    // Return the minimum of curr_off and 
    // curr_on and add power of 2 of
    // current bit
    return Math.min(RecursiveFunction(curr_off,
                                 bit - 1),
               RecursiveFunction(curr_on,
                                 bit - 1))
           + (1 << bit);
}

// Function that print the minimum
// value after exclusive-OR
function PrintMinimum(a, n)
{
    let v = [];

    // Pushing values in vector
    for (let i = 0; i < n; i++)
        v.push(a[i]);

    // Printing answer
    document.write(RecursiveFunction(v, 30)
         + "<br>");
}

// Driver Code
    let arr = [ 3, 2, 1 ];

    let size = arr.length;

    PrintMinimum(arr, size);

</script>
```

**Output:** 

```
2
```