# 计数数组中持有 i+j= arr[i]+arr[j]

的对

> 原文:[https://www . geesforgeks . org/count-pairs-in-a-arriarj-in-arriarj/](https://www.geeksforgeeks.org/count-pairs-in-an-array-that-hold-ij-arriarrj/)

给定一个整数数组 **arr[]** ，任务是对所有的对 **(arr[i]，arr[j])** 进行计数，使得 **i + j = arr[i] + arr[j]** 对所有的 **0 ≤ i < j < n** 。
**注:**对(x，y)和(y，x)被认为是单对。

**示例:**

> **输入:** arr[] = {8，4，2，1，5，4，2，1，2，3}
> **输出:** 1
> 唯一可能的配对是(arr[4]，arr[5])即(5，4)
> I+j = arr[I]+arr[j]=>4+5 = 5+4
> 
> **输入:** arr[] = {1，0，3，2}
> **输出:** 4

**简单方法:**运行两个嵌套循环，检查每一个可能的循环对是否满足 **i + j = arr[i] + arr[j]** 的条件。如果条件满足，则更新**计数=计数+ 1** 。打印最后的**计数**。
以下是上述方法的实施:

## C++

```
// C++ program to count all the pairs that
// hold the condition i + j = arr[i] + arr[j]
#include <iostream>
using namespace std;

// Function to return the count of pairs that
// satisfy the given condition
int CountPairs(int arr[], int n)
{
    int count = 0;

    // Generate all possible pairs and increment
    // the count if the condition is satisfied
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {
            if ((i + j) == (arr[i] + arr[j]))
                count++;
        }
    }
    return count;
}

// Driver code
int main()
{
    int arr[] = { 1, 0, 3, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << CountPairs(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count all the pairs that
// hold the condition i + j = arr[i] + arr[j]

public class GFG {

    // Function to return the count of pairs that
    // satisfy the given condition
    static int CountPairs(int arr[], int n)
    {
        int count = 0;

        // Generate all possible pairs and increment
        // the count if the condition is satisfied
        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {
                if ((i + j) == (arr[i] + arr[j]))
                    count++;
            }
        }
        return count;
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 1, 0, 3, 2 };
        int n = arr.length ;
        System.out.print(CountPairs(arr, n));
    }

    // This code is contributed by Ryuga.
}
```

## 蟒蛇 3

```
# Python 3 program to count all the pairs that
# hold the condition i + j = arr[i] + arr[j]

# Function to return the count of pairs
# that satisfy the given condition
def CountPairs(arr, n):

    count = 0;

    # Generate all possible pairs and increment
    # the count if the condition is satisfied
    for i in range(n - 1):
        for j in range(i + 1, n):
            if ((i + j) == (arr[i] + arr[j])):
                count += 1;
    return count;

# Driver code
arr = [ 1, 0, 3, 2 ];
n = len(arr);
print(CountPairs(arr, n));

# This code is contributed
# by Akanksha Rai
```

## C#

```
using System;

// C# program to count all the pairs that
// hold the condition i + j = arr[i] + arr[j]

public class GFG {

    // Function to return the count of pairs that
    // satisfy the given condition
    static int CountPairs(int[] arr, int n)
    {
        int count = 0;

        // Generate all possible pairs and increment
        // the count if the condition is satisfied
        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {
                if ((i + j) == (arr[i] + arr[j]))
                    count++;
            }
        }
        return count;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 1, 0, 3, 2 };
        int n = arr.Length ;
        Console.Write(CountPairs(arr, n));
    }

}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count all the pairs that
// hold the condition i + j = arr[i] + arr[j]

// Function to return the count of pairs
// that satisfy the given condition
function CountPairs(&$arr, $n)
{
    $count = 0;

    // Generate all possible pairs and increment
    // the count if the condition is satisfied
    for ($i = 0; $i < $n - 1; $i++)
    {
        for ($j = $i + 1; $j < $n; $j++)
        {
            if (($i + $j) == ($arr[$i] + $arr[$j]))
                $count++;
        }
    }
    return $count;
}

// Driver code
$arr = array(1, 0, 3, 2 );
$n = sizeof($arr);
echo(CountPairs($arr, $n));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
// Javascript program to count all the pairs that
// hold the condition i + j = arr[i] + arr[j]

    // Function to return the count of pairs that
    // satisfy the given condition
    function CountPairs(arr,n)
    {
        let count = 0;

        // Generate all possible pairs and increment
        // the count if the condition is satisfied
        for (let i = 0; i < n - 1; i++) {
            for (let j = i + 1; j < n; j++) {
                if ((i + j) == (arr[i] + arr[j]))
                    count++;
            }
        }
        return count;
    }

    // Driver code
    let arr=[1, 0, 3, 2];
    let n = arr.length ;
    document.write(CountPairs(arr, n));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
4
```

**有效方法:**

1.  将 **i + j = arr[i] + arr[j]** 简化为**(arr[I]–I)=-(arr[j]–j)**。现在，问题简化为找到所有的形式对 **(x，-x)** 。
2.  因此，根据第 1 步的简化，将数组的所有元素更新为**arr[I]= arr[I]–I**。
3.  为了统计形式 **(x，-x)** 的所有对，将所有负元素的频率保存到名为**的[散列表](https://www.geeksforgeeks.org/java-util-hashmap-in-java/)中，将所有正元素(包括 0)的频率保存到**散列表**中。**
4.  现在，对于 **posMap** 中的每个频率说 **x** ，在 **negMap** 中找到 **-x** 的频率。所以 **x** 和 **-x** 之间所有可能的对将是**计数=计数+(频率(x) *频率(-x))** 。
5.  打印最后的**计数**。

下面是上述方法的实现:

## C++

```
#include <iostream>
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of pairs that
// satisfy the given condition
int countValidPairs(int arr[], int n)
{

    int i;

    // Update all the elements as describde
    // in the approach
    for (i = 0; i < n; i++)
        arr[i] -= i;

    // HashMap for storing the frequency of
    // negative elements
    map<int, int> negMap;

    // HashMap for storing the frequency of
    // positive elements (including 0)
    map<int, int> posMap;
    for (i = 0; i < n; i++)
    {

        // For negative elements
        if (arr[i] < 0)
        {

            // If HashMap already contains the integer
            // then increment its frequency by 1
            if (negMap.count(arr[i]))
                negMap.insert({arr[i], negMap.find(arr[i])->second + 1});
            else

                // Else set the frequency to 1
                negMap.insert({arr[i], 1});
        }

        // For positive elements (including 0)
        else
        {

            // If HashMap already contains the integer
            // then increment its frequency by 1
            if (posMap.count(arr[i]))
                posMap.insert({arr[i], posMap.find(arr[i])->second + 1});
            else

                // Else set the frequency to 1
                posMap.insert({arr[i], 1});
        }
    }

    // To store the count of valid pairs
    int count = 0;

    for (auto itr = posMap.begin(); itr != posMap.end(); ++itr)
    {
        int posVal = itr->second;

        // If an equivalent -ve element is found for
        // the current +ve element
        if (negMap.count(-itr->first))
        {
            int negVal = negMap.find(-itr->first)->second;

            // Add all possible pairs to the count
            count += (negVal * posVal);
        }
    }

    // Return the count
    return count;
}

// Driver code
int main()
{
    int arr[] = { 8, 4, 2, 1, 5, 4, 2, 1, 2, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countValidPairs(arr, n);

}

// This code is contributed by ApurvaRaj
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.HashMap;
import java.util.Map;
public class GFG {

    // Function to return the count of pairs that
    // satisfy the given condition
    static int countValidPairs(int arr[], int n)
    {

        int i;

        // Update all the elements as describde
        // in the approach
        for (i = 0; i < n; i++)
            arr[i] -= i;

        // HashMap for storing the frequency of
        // negative elements
        Map<Integer, Integer> negMap = new HashMap<>();

        // HashMap for storing the frequency of
        // positive elements (including 0)
        Map<Integer, Integer> posMap = new HashMap<>();
        for (i = 0; i < n; i++) {

            // For negative elements
            if (arr[i] < 0) {

                // If HashMap already contains the integer
                // then increment its frequency by 1
                if (negMap.containsKey(arr[i]))
                    negMap.put(arr[i], negMap.get(arr[i]) + 1);
                else

                    // Else set the frequency to 1
                    negMap.put(arr[i], 1);
            }

            // For positive elements (including 0)
            else {

                // If HashMap already contains the integer
                // then increment its frequency by 1
                if (posMap.containsKey(arr[i]))
                    posMap.put(arr[i], posMap.get(arr[i]) + 1);
                else

                    // Else set the frequency to 1
                    posMap.put(arr[i], 1);
            }
        }

        // To store the count of valid pairs
        int count = 0;

        for (int posKey : posMap.keySet()) {
            int posVal = posMap.get(posKey);

            // If an equivalent -ve element is found for
            // the current +ve element
            if (negMap.containsKey(-posKey)) {
                int negVal = negMap.get(-posKey);

                // Add all possible pairs to the count
                count += (negVal * posVal);
            }
        }

        // Return the count
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 8, 4, 2, 1, 5, 4, 2, 1, 2, 3 };
        int n = arr.length;
        System.out.println(countValidPairs(arr, n));
    }
}
```

## 蟒蛇 3

```
# Function to return the count of pairs that
# satisfy the given condition
def countValidPairs(arr, n):
    i = 0

    # Update all the elements as described
    # in the approach
    for i in range(n):
        arr[i] -= i

    # HashMap for storing the frequency
    # of negative elements
    negMap = dict()

    # HashMap for storing the frequency of
    # positive elements (including 0)
    posMap = dict()
    for i in range(n):

        # For negative elements
        if (arr[i] < 0):

            # If HashMap already contains the integer
            # then increment its frequency by 1
            negMap[arr[i]] = negMap.get(arr[i], 0) + 1

        # For positive elements (including 0)
        else:

            # If HashMap already contains the integer
            # then increment its frequency by 1
            posMap[arr[i]] = posMap.get(arr[i], 0) + 1

    # To store the count of valid pairs
    count = 0

    for posKey in posMap:
        posVal = posMap[posKey]

        negVal = 0

        if -posKey in negMap:
            negVal = negMap[-posKey]

        # Add all possible pairs to the count
        count += (negVal * posVal)

    # Return the count
    return count

# Driver code
arr = [8, 4, 2, 1, 5, 4, 2, 1, 2, 3]
n = len(arr)
print(countValidPairs(arr, n))

# This code is contributed
# by mohit kumar
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to return the count
// of pairs that satisfy the given
// condition
static int countValidPairs(int []arr,
                           int n)
{
  int i;

  // Update all the elements
  // as described in the approach
  for (i = 0; i < n; i++)
    arr[i] -= i;

  // Dictionary for storing the
  // frequency of negative elements
  Dictionary<int,
             int> negMap =
             new Dictionary<int,
                            int>();

  // Dictionary for storing the
  // frequency of positive elements
  // (including 0)
  Dictionary<int,
             int> posMap =
             new Dictionary<int,
                            int>();
  for (i = 0; i < n; i++)
  {
    // For negative elements
    if (arr[i] < 0)
    {
      // If Dictionary already
      // contains the integer then
      // increment its frequency by 1
      if (negMap.ContainsKey(arr[i]))
        negMap[arr[i]] = negMap[arr[i]] + 1;
      else

        // Else set the frequency to 1
        negMap.Add(arr[i], 1);
    }

    // For positive elements (including 0)
    else
    {
      // If Dictionary already contains
      // the integer then increment its
      // frequency by 1
      if (posMap.ContainsKey(arr[i]))
        posMap.Add(arr[i], posMap[arr[i]] + 1);
      else

        // Else set the frequency to 1
        posMap.Add(arr[i], 1);
    }
  }

  // To store the count of valid pairs
  int count = 0;

  foreach (int posKey in posMap.Keys)
  {
    int posVal = posMap[posKey];

    // If an equivalent -ve element
    // is found for the current +ve element
    if (negMap.ContainsKey(-posKey))
    {
      int negVal = negMap[-posKey];

      // Add all possible pairs to
      // the count
      count += (negVal * posVal);
    }
  }

  // Return the count
  return count;
}

// Driver code
public static void Main(String[] args)
{
  int []arr = {8, 4, 2, 1, 5,
               4, 2, 1, 2, 3};
  int n = arr.Length;
  Console.WriteLine(countValidPairs(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Function to return the count of pairs that
// satisfy the given condition
function countValidPairs(arr,n)
{
        let i;

        // Update all the elements as describde
        // in the approach
        for (i = 0; i < n; i++)
            arr[i] -= i;

        // HashMap for storing the frequency of
        // negative elements
        let negMap = new Map();

        // HashMap for storing the frequency of
        // positive elements (including 0)
        let posMap = new Map();
        for (i = 0; i < n; i++) {

            // For negative elements
            if (arr[i] < 0) {

                // If HashMap already contains the integer
                // then increment its frequency by 1
                if (negMap.has(arr[i]))
                    negMap.set(arr[i], negMap.get(arr[i]) + 1);
                else

                    // Else set the frequency to 1
                    negMap.set(arr[i], 1);
            }

            // For positive elements (including 0)
            else {

                // If HashMap already contains the integer
                // then increment its frequency by 1
                if (posMap.has(arr[i]))
                    posMap.set(arr[i], posMap.get(arr[i]) + 1);
                else

                    // Else set the frequency to 1
                    posMap.set(arr[i], 1);
            }
        }

        // To store the count of valid pairs
        let count = 0;

        for (let posKey of posMap.keys()) {
            let posVal = posMap.get(posKey);

            // If an equivalent -ve element is found for
            // the current +ve element
            if (negMap.has(-posKey)) {
                let negVal = negMap.get(-posKey);

                // Add all possible pairs to the count
                count += (negVal * posVal);
            }
        }

        // Return the count
        return count;
}

// Driver code
let arr=[8, 4, 2, 1, 5, 4, 2, 1, 2, 3];
let n = arr.length;
document.write(countValidPairs(arr, n));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
1
```