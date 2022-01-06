# 一个人只能吃 N/2 颗的糖果的最大种类

> 原文:[https://www . geeksforgeeks . org/一个人最多能吃多少种糖果-如果只有 n-2 种可以吃的话/](https://www.geeksforgeeks.org/maximum-types-of-candies-a-person-can-eat-if-only-n-2-of-them-can-be-eaten/)

给定一个由 **N** 糖果组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，其中 **N** 为偶数， **arr[i]** 代表糖果的类型。任务是找到一个人只能吃 **N/2** 种不同类型糖果的最大数量。

**示例:**

> **输入:** arr[] = {4，4，5，5，6，6，7，7}
> **输出:** 4
> **说明:**人只能吃 8/2 = 4 颗糖果，数组中有 4 种糖果。因此，每个人可以吃一种类型的糖果。
> 
> **输入:** arr[] = {2，2，3，1}
> **输出:** 2
> **说明:**人只能吃 4/2 = 2，阵中有 3 种糖果。因此，答案是 2，因为最多允许 2 颗糖果。

**天真方法:**想法是找出给定数组中糖果类型的数量。如果允许吃的糖果的最大数量大于给定的糖果类型数量，那么答案就是给定的糖果类型数量。否则，答案就是允许吃的糖果的最大数量。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**想法是使用[散列](https://www.geeksforgeeks.org/hashing-data-structure/)。按照以下步骤解决问题:

*   初始化一个[hashset](https://www.geeksforgeeks.org/unordered_set-in-cpp-stl/)T2 来存储独特的糖果类型。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)， **arr[]** ，插入集合中的所有元素， **s** 。
*   将哈斯塞特 T2 的[大小存储在变量 **M** 中。](https://www.geeksforgeeks.org/hashset-size-method-in-java/)
*   如果 **(M < N/2)** 的值，则打印 **M** ，否则打印 **N/2** 作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find number of candy types
int num_candyTypes(vector<int>& candies)
{
    // Declare a hashset to store candies
    unordered_set<int> s;

    // Traverse the given array and
    // inserts element into set
    for (int i = 0; i < candies.size(); i++) {
        s.insert(candies[i]);
    }

    // Return the result
    return s.size();
}

// Function to find maximum number of
// types of candies a person can eat
void distribute_candies(vector<int>& candies)
{
    // Store the number of candies
    // allowed to eat
    int allowed = candies.size() / 2;

    // Store the number of candy types
    int types = num_candyTypes(candies);

    // Return the result
    if (types < allowed)
        cout << types;
    else
        cout << allowed;
}

// Driver Code
int main()
{
    // Given Input
    vector<int> candies = { 4, 4, 5, 5, 3, 3 };

    // Function Call
    distribute_candies(candies);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find number of candy types
public static int num_candyTypes(int []candies)
{

    // Declare a hashset to store candies
    Dictionary<Integer,
               Integer> s = new Hashtable<Integer,
                                          Integer>();

    // Traverse the given array and
    // inserts element into set
    for(int i = 0; i < candies.length; i++)
    {
        s.put(candies[i], 1);
    }

    // Return the result
    return s.size();
}

// Function to find maximum number of
// types of candies a person can eat
public static void distribute_candies(int []candies)
{

    // Store the number of candies
    // allowed to eat
    int allowed = candies.length / 2;

    // Store the number of candy types
    int types = num_candyTypes(candies);

    // Return the result
    if (types < allowed)
        System.out.println(types);
    else
        System.out.println(allowed);
}

// Driver code
public static void main(String[] args)
{

    // Given Input
    int candies[] =  { 4, 4, 5, 5, 3, 3 };

    // Function Call
    distribute_candies(candies);
}
}

// This code is contributed by mohit kumar 29
```

## 蟒蛇 3

```
# python 3 program for the above approach

# Function to find number of candy types
def num_candyTypes(candies):
    # Declare a hashset to store candies
    s =  set()

    # Traverse the given array and
    # inserts element into set
    for i in range(len(candies)):
        s.add(candies[i])

    # Return the result
    return len(s)

# Function to find maximum number of
# types of candies a person can eat
def distribute_candies(candies):
    # Store the number of candies
    # allowed to eat
    allowed = len(candies)/2

    # Store the number of candy types
    types = num_candyTypes(candies)

    # Return the result
    if (types < allowed):
        print(int(types))
    else:
        print(int(allowed))

# Driver Code
if __name__ == '__main__':

    # Given Input
    candies = [4, 4, 5, 5, 3, 3]

    # Function Call
    distribute_candies(candies)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach

using System;
using System.Collections.Generic;

public class GFG{

    // Function to find number of candy types
public static int num_candyTypes(int []candies)
{

    // Declare a hashset to store candies
    Dictionary<int,int> s = new Dictionary<int,int>();

    // Traverse the given array and
    // inserts element into set
    for(int i = 0; i < candies.Length; i++)
    {
        if(!s.ContainsKey(candies[i]))
            s.Add(candies[i], 1);
    }

    // Return the result
    return s.Count;
}

// Function to find maximum number of
// types of candies a person can eat
public static void distribute_candies(int []candies)
{

    // Store the number of candies
    // allowed to eat
    int allowed = candies.Length / 2;

    // Store the number of candy types
    int types = num_candyTypes(candies);

    // Return the result
    if (types < allowed)
        Console.WriteLine(types);
    else
        Console.WriteLine(allowed);
}

// Driver code

    static public void Main (){

        // Given Input
    int[] candies =  { 4, 4, 5, 5, 3, 3 };

    // Function Call
    distribute_candies(candies);

    }
}

// This code is contributed by unknown2108.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find number of candy types
function num_candyTypes(candies) {
    // Declare a hashset to store candies
    let s = new Set();

    // Traverse the given array and
    // inserts element into set
    for (let i = 0; i < candies.length; i++) {
        s.add(candies[i]);
    }

    // Return the result
    return s.size;
}

// Function to find maximum number of
// types of candies a person can eat
function distribute_candies(candies)
{

    // Store the number of candies
    // allowed to eat
    let allowed = candies.length / 2;

    // Store the number of candy types
    let types = num_candyTypes(candies);

    // Return the result
    if (types < allowed)
        document.write(types);
    else
        document.write(allowed);
}

// Driver Code

// Given Input
let candies = [4, 4, 5, 5, 3, 3];

// Function Call
distribute_candies(candies);

// This code is contribute by gfgking.
</script>
```

**Output**

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)