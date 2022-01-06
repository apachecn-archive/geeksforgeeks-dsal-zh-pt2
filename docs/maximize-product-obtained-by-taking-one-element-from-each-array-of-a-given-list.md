# 从给定列表的每个数组中取一个元素得到最大乘积

> 原文:[https://www . geeksforgeeks . org/通过从给定列表的每个数组中取一个元素来最大化产品获得/](https://www.geeksforgeeks.org/maximize-product-obtained-by-taking-one-element-from-each-array-of-a-given-list/)

给定一个由不同长度的数组组成的列表**arr【】**，任务是从列表中的每个数组中取一个元素，找出可以形成的最大乘积。

**示例:**

> **输入:** arr[] = {{-3，-4}，{1，2，-3}}
> **输出:** 12
> **解释:**
> 从第一个数组中拾取-4，从第二个数组中拾取-3。
> 因此，最大可能积为 12。
> 
> **输入:** arr[] = {{1，-1}、{2，3}、{10，-100，20}}
> **输出:** 300
> **解释:**
> 从第一个数组中选取-1，从第二个数组中选取 3，从第三个数组中选取-100。
> 因此，最高产品为 300。

**天真法:**解决这个问题最简单的方法是通过使用[递归](https://www.geeksforgeeks.org/recursion/)从列表的每个数组中取一个元素，找到每个可能的元素组合，并从所有可能的组合中选择最大乘积。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Stores the maximum product
int maximum = -INT_MAX;

// Function to find maximum product
// possible by taking exactly one element
// from each array of the list
void calculateProduct(vector<vector<int> > &List,
                      int index, int product)
{

    // If last index is encountered
    if(index + 1 == List.size())
    {
        for (int i :List[index])
        {

            // Find the maximum product
            maximum = max(maximum, product *i);
        }

    // Otherwise, recursively calculate
    // maximum product for every element
    }
    else
    {
        for(int i: List[index])
            calculateProduct(List, index + 1, product * i);
      }
}

// Driver Code

// Count of given arrays
int main()
{
 int N = 2;

 // Given list of N arrays
 vector<vector<int> > arr = {{-3, -4}, {1, 2, -3}};

  // Calculates the maximum
  // possible product
  calculateProduct(arr, 0, 1);

  // Print the maximum product
  cout << maximum;
  return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the 
// above approach
import java.util.*;

class GFG{

static int maximum = -Integer.MAX_VALUE;

// Function to find maximum product
// possible by taking exactly one element
// from each array of the list
static void calculateProduct(int[][] List,
                             int index,
                             int product)
{

    // If last index is encountered
    if (index + 1 == List.length)
    {
        for(int i:List[index])
        {

            // Find the maximum product
            maximum = Math.max(maximum, product * i);
        }

    // Otherwise, recursively calculate
    // maximum product for every element
    }
    else
    {
        for(int i:List[index])
            calculateProduct(List, index + 1,
                             product * i);
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 2;

    // Given list of N arrays
    int[][] arr = { { -3, -4 }, { 1, 2, -3 } };

    // Calculates the maximum
    // possible product
    calculateProduct(arr, 0, 1);

    // Print the maximum product
    System.out.print(maximum);
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python program for the above approach

# Stores the maximum product
maximum = -float('INF')

# Function to find maximum product
# possible by taking exactly one element
# from each array of the list
def calculateProduct(List, index, product):

    # If last index is encountered
    if(index + 1 == len(List)):

        for i in List[index]:
            global maximum

            # Find the maximum product
            maximum = max(maximum, product * i)

    # Otherwise, recursively calculate
    # maximum product for every element
    else:
        for i in List[index]:
            calculateProduct(List, index + 1, product * i)

# Driver Code

# Count of given arrays
N = 2

# Given list of N arrays
arr = [[-3, -4], [1, 2, -3]]

# Calculates the maximum
# possible product
calculateProduct(arr, 0, 1)

# Print the maximum product
print(maximum)
```

## C#

```
// C# program for the 
// above approach
using System;
public class GFG{

static int maximum = -int.MaxValue;

// Function to find maximum product
// possible by taking exactly one element
// from each array of the list
static void calculateProduct(int[,] list,
                             int index,
                             int product)
{

    // If last index is encountered
    if (index + 1 == list.GetLength(0))
    {
        foreach(int i in GetRow(list,index))
        {

            // Find the maximum product
            maximum = Math.Max(maximum, product * i);
        }

    // Otherwise, recursively calculate
    // maximum product for every element
    }
    else
    {
        foreach(int i in GetRow(list,index))
            calculateProduct(list, index + 1,
                             product * i);
    }
}
public static int[] GetRow(int[,] matrix, int row)
  {
    var rowLength = matrix.GetLength(1);
    var rowVector = new int[rowLength];

    for (var i = 0; i < rowLength; i++)
    {
      rowVector[i] = matrix[row, i];
    }

    return rowVector;
  }

// Driver Code
public static void Main(String[] args)
{

    // Given list of N arrays
    int[,] arr = { { -3, -4,0 }, { 1, 2, -3 } };

    // Calculates the maximum
    // possible product
    calculateProduct(arr, 0, 1);

    // Print the maximum product
    Console.Write(maximum);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Stores the maximum product
var maximum = -1000000000;

// Function to find maximum product
// possible by taking exactly one element
// from each array of the list
function calculateProduct(List, index, product)
{

    // If last index is encountered
    if(index + 1 == List.length)
    {
        for(var i =0; i< List[index].length; i++)
        {

            // Find the maximum product
            maximum = Math.max
            (maximum, product *List[index][i]);
        }

    // Otherwise, recursively calculate
    // maximum product for every element
    }
    else
    {
        for(var i =0; i< List[index].length; i++)
            calculateProduct(List, index + 1,
            product * List[index][i]);
      }
}

// Driver Code

// Count of given arrays
var N = 2;

// Given list of N arrays
var arr = [[-3, -4], [1, 2, -3]];

// Calculates the maximum
 // possible product
calculateProduct(arr, 0, 1);

// Print the maximum product
document.write( maximum);

</script>
```

**Output:** 

```
12
```

**时间复杂度:**O(2<sup>N</sup>)
T5】辅助空间: O(1)

**高效法:**对上述方法进行优化，思路是考虑每个数组的最低负数(如果有的话)和最高正数(如果有的话)，使乘积最大化。按照以下步骤解决问题:

1.  [遍历数组列表](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** 。
2.  对于列表中的每个数组，说出 **arr【索引】**，找到其中存在的[最大和最小元素](https://www.geeksforgeeks.org/maximum-and-minimum-in-an-array/)。
3.  如果已经达到最后一个指数，返回作为[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)获得的**最大值和最小值**。
4.  如果获得的最大值为负值，将其设置为**无**。如果获得的最小值为正，将其设置为**无**
5.  否则:
    1.  递归调用**(索引+ 1)** ，即**计算产品(列表，索引+ 1)** ，并将结果存储在**【正，负】**中。
    2.  查找在**步骤 1** 中获得的**最大值、最小值**的所有组合，以及在**步骤 3.1** 中发现的正值、负值。
    3.  返回所有组合中形成的最大正值和最小负值。
6.  完成上述步骤后，打印形成的最大产品。

下面是上述方法的实现:

## C++14

```
// CPP program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the product of 2 numbers
int findProduct(int number_1, int number_2)
{

  // If any of the two numbers is None
  if(number_1 == INT_MIN or number_2 == INT_MIN)
    return 0;

  // Otherwise, return the product
  else
    return number_1 * number_2;
}

// Function to calculate maximum product
// by taking only one element from each
// array present in the list
pair<int,int> calculateProduct(vector<vector<int>> List,  int index)
{

  // Find the maximum and minimum
  // present in the current array
  int highest = *max_element(List[index].begin(),List[index].end());
  int lowest = *min_element(List[index].begin(),List[index].end());

  // If last index is reached, then
  // return the highest(positive)
  // and lowest(negative) values
  if(index + 1 == List.size()){
    if(lowest < 0 and highest >= 0)
      return {highest, lowest};

    else if(lowest <= 0 and highest <= 0)
      return {INT_MIN, lowest};

    else if(lowest >= 0 and highest >= 0)
      return {highest, INT_MIN};
  }

  // Store the positive and negative products
  // returned by calculating for the
  // remaining arrays
  pair<int,int> temp = calculateProduct(List, index + 1);
  int positive = temp.first;
  int negative = temp.second;

  // Calculate for all combinations of
  // highest, lowest with positive, negative

  // Store highest positive product
  int highPos = findProduct(highest, positive);

  // Store product of highest with negative
  int highNeg = findProduct(highest, negative);

  // Store product of lowest with positive
  int lowPos = findProduct(lowest, positive);

  // Store lowest negative product
  int lowNeg = findProduct(lowest, negative);

  // Return the maximum positive and
  // minimum negative product
  if(lowest < 0 and highest >= 0)
    return {max(highPos, lowNeg), min(highNeg, lowPos)};

  else if(lowest <= 0 and highest <= 0)
    return {lowNeg, lowPos};

  else if(lowest >= 0 and highest >= 0)
    return {max(lowPos, highPos), min(lowNeg, highNeg)};

}

// Driver Code

int main()
{

  // Count of given arrays
  int N = 2;

  // Given list of N arrays
  vector<vector<int>>arr{{-3, -4}, {1, 2, -3}};

  // Store the maximum positive and
  // minimum negative product possible
  pair<int,int> ans = calculateProduct(arr, 0);

  // Print the maximum product
  cout<<ans.first<<endl;
}

// This code is contributed by SURENDRA_GANGWAR.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG
{

    // Function to return the product of 2 numbers
    static int findProduct(int number_1, int number_2)
    {

        // If any of the two numbers is None
        if(number_1 == Integer.MIN_VALUE || number_2 == Integer.MIN_VALUE)
        {
            return 0;
        }

        // Otherwise, return the product
        else
            return number_1 * number_2;
    }

    // Function to calculate maximum product
    // by taking only one element from each
    // array present in the list
    static ArrayList<Integer> calculateProduct(ArrayList<ArrayList<Integer>> List,  int index)
    {

        // Find the maximum and minimum
        // present in the current array
        int highest = Collections.max(List.get(index));
        int lowest = Collections.min(List.get(index));

        // If last index is reached, then
        // return the highest(positive)
        // and lowest(negative) values
        if(index + 1 == List.size())
        {
            if(lowest < 0 && highest >= 0)
            {
                return (new ArrayList<Integer>(Arrays.asList(highest, lowest)));
            }
            else if(lowest <= 0 && highest <= 0)
            {
                return (new ArrayList<Integer>(Arrays.asList(Integer.MIN_VALUE, lowest)));
            }
            else if(lowest >= 0 && highest >= 0)
            {
                return (new ArrayList<Integer>(Arrays.asList(highest,Integer.MIN_VALUE)));
            }
        }

        // Store the positive and negative products
        // returned by calculating for the
        // remaining arrays
        ArrayList<Integer> temp = calculateProduct(List, index + 1);
        int positive = temp.get(0);
        int negative = temp.get(1);

        // Calculate for all combinations of
        // highest, lowest with positive, negative

        // Store highest positive product
        int highPos = findProduct(highest, positive);

        // Store product of highest with negative
        int highNeg = findProduct(highest, negative);

        // Store product of lowest with positive
        int lowPos = findProduct(lowest, positive);

        // Store lowest negative product
        int lowNeg = findProduct(lowest, negative);

        // Return the maximum positive and
        // minimum negative product
        if(lowest < 0 && highest >= 0)
        {
            return (new ArrayList<Integer>(Arrays.asList(Math.max(highPos, lowNeg), Math.min(highNeg, lowPos))));
        }
        else if(lowest <= 0 && highest <= 0)
        {
           return (new ArrayList<Integer>(Arrays.asList(lowNeg, lowPos)));
        }
        else if(lowest >= 0 && highest >= 0)
        {
            return (new ArrayList<Integer>(Arrays.asList(Math.max(lowPos, highPos), Math.min(lowNeg, highNeg))));
        }

        return (new ArrayList<Integer>(Arrays.asList(0,0)));
    }

    // Driver Code
    public static void main (String[] args) {

        // Count of given arrays
        int N = 2;

        // Given list of N arrays
        ArrayList<ArrayList<Integer>> arr = new ArrayList<ArrayList<Integer>>();
        arr.add(new ArrayList<Integer>(Arrays.asList(-3, -4)));
        arr.add(new ArrayList<Integer>(Arrays.asList(1, 2, -3)));

        // Store the maximum positive and
        // minimum negative product possible
        ArrayList<Integer> ans = calculateProduct(arr, 0);

        // Print the maximum product
        System.out.println(ans.get(0));
    }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to return the product of 2 numbers
def findProduct(number_1, number_2):

    # If any of the two numbers is None
    if(number_1 == None or number_2 == None):
        return 0

    # Otherwise, return the product
    else:
        return number_1 * number_2

# Function to calculate maximum product
# by taking only one element from each
# array present in the list
def calculateProduct(List, index):

    # Find the maximum and minimum
    # present in the current array
    highest = max(List[index])
    lowest = min(List[index])

    # If last index is reached, then
    # return the highest(positive)
    # and lowest(negative) values
    if(index + 1 == len(List)):
        if(lowest < 0 and highest >= 0):
            return [highest, lowest]

        elif(lowest <= 0 and highest <= 0):
            return [None, lowest]

        elif(lowest >= 0 and highest >= 0):
            return [highest, None]

    # Store the positive and negative products
    # returned by calculating for the
    # remaining arrays
    [positive, negative] = calculateProduct(List, index + 1)

    # Calculate for all combinations of
    # highest, lowest with positive, negative

    # Store highest positive product
    highPos = findProduct(highest, positive)

    # Store product of highest with negative
    highNeg = findProduct(highest, negative)

    # Store product of lowest with positive
    lowPos = findProduct(lowest, positive)

    # Store lowest negative product
    lowNeg = findProduct(lowest, negative)

    # Return the maximum positive and
    # minimum negative product
    if(lowest < 0 and highest >= 0):
        return [max(highPos, lowNeg), min(highNeg, lowPos)]

    elif(lowest <= 0 and highest <= 0):
        return [lowNeg, lowPos]

    elif(lowest >= 0 and highest >= 0):
        return [max(lowPos, highPos), min(lowNeg, highNeg)]

# Driver Code

# Count of given arrays
N = 2

# Given list of N arrays
arr = [[-3, -4], [1, 2, -3]]

# Store the maximum positive and
# minimum negative product possible
positive, negative = calculateProduct(arr, 0)

# Print the maximum product
print(positive)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
using System.Linq;

public class GFG
{

  // Function to return the product of 2 numbers
  static int findProduct(int number_1, int number_2)
  {

    // If any of the two numbers is None
    if(number_1 == Int32.MinValue || number_2 == Int32.MinValue)
    {
      return 0;
    }

    // Otherwise, return the product
    else
      return number_1 * number_2;
  }

  // Function to calculate maximum product
  // by taking only one element from each
  // array present in the list
  static List<int> calculateProduct(List<List<int>> List,  int index)
  {

    // Find the maximum and minimum
    // present in the current array
    int highest = List[index].Max();
    int lowest = List[index].Min();

    // If last index is reached, then
    // return the highest(positive)
    // and lowest(negative) values
    if(index + 1 == List.Count)
    {
      if(lowest < 0 && highest >= 0)
      {
        return (new List<int>(){highest,lowest});
      }
      else if(lowest <= 0 && highest <= 0)
      {
        return (new List<int>(){Int32.MinValue, lowest});
      }
      else if(lowest >= 0 && highest >= 0)
      {
        return (new List<int>(){highest, Int32.MinValue});
      }
    }

    // Store the positive and negative products
    // returned by calculating for the
    // remaining arrays
    List<int> temp = calculateProduct(List, index + 1);
    int positive = temp[0];
    int negative = temp[1];

    // Calculate for all combinations of
    // highest, lowest with positive, negative

    // Store highest positive product
    int highPos = findProduct(highest, positive);

    // Store product of highest with negative
    int highNeg = findProduct(highest, negative);

    // Store product of lowest with positive
    int lowPos = findProduct(lowest, positive);

    // Store lowest negative product
    int lowNeg = findProduct(lowest, negative);

    // Return the maximum positive and
    // minimum negative product
    if(lowest < 0 && highest >= 0)
    {
      return (new List<int>(){Math.Max(highPos, lowNeg), Math.Min(highNeg, lowPos)});
    }
    else if(lowest <= 0 && highest <= 0)
    {
      return (new List<int>(){lowNeg, lowPos});
    }
    else if(lowest >= 0 && highest >= 0)
    {
      return (new List<int>(){Math.Max(lowPos, highPos), Math.Min(lowNeg, highNeg)});
    }

    return (new List<int>(){0,0});
  }

  // Driver Code
  static public void Main ()
  {

    // Given list of N arrays
    List<List<int>> arr = new List<List<int>>();
    arr.Add(new List<int>(){-3, -4});
    arr.Add(new List<int>(){1, 2, -3});

    // Store the maximum positive and
    // minimum negative product possible
    List<int> ans = calculateProduct(arr, 0);

    // Print the maximum product
    Console.WriteLine(ans[0]);
  }
}

// This code is contributed by rag2127.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to return the product of 2 numbers
function findProduct(number_1,number_2)
{
    // If any of the two numbers is None
        if(number_1 == Number.MIN_VALUE ||
           number_2 == Number.MIN_VALUE)
        {
            return 0;
        }

        // Otherwise, return the product
        else
            return number_1 * number_2;
}

 // Function to calculate maximum product
// by taking only one element from each
// array present in the list
function calculateProduct(List,index)
{
    // Find the maximum and minimum
   // present in the current array
        let highest = Math.max(...List[index]);
        let lowest = Math.min(...List[index]);

        // If last index is reached, then
        // return the highest(positive)
        // and lowest(negative) values
        if(index + 1 == List.length)
        {
            if(lowest < 0 && highest >= 0)
            {
                return ([highest, lowest]);
            }
            else if(lowest <= 0 && highest <= 0)
            {
                return ([Number.MIN_VALUE, lowest]);
            }
            else if(lowest >= 0 && highest >= 0)
            {
                return ([highest,Number.MIN_VALUE]);
            }
        }

        // Store the positive and negative products
        // returned by calculating for the
        // remaining arrays
        let temp = calculateProduct(List, index + 1);
        let positive = temp[0];
        let negative = temp[1];

        // Calculate for all combinations of
        // highest, lowest with positive, negative

        // Store highest positive product
        let highPos = findProduct(highest, positive);

        // Store product of highest with negative
        let highNeg = findProduct(highest, negative);

        // Store product of lowest with positive
        let lowPos = findProduct(lowest, positive);

        // Store lowest negative product
        let lowNeg = findProduct(lowest, negative);

        // Return the maximum positive and
        // minimum negative product
        if(lowest < 0 && highest >= 0)
        {
            return ([Math.max(highPos, lowNeg), Math.min(highNeg,
            lowPos)]);
        }
        else if(lowest <= 0 && highest <= 0)
        {
           return ([lowNeg, lowPos]);
        }
        else if(lowest >= 0 && highest >= 0)
        {
            return ([Math.max(lowPos, highPos), Math.min(lowNeg,
            highNeg)]);
        }

        return ([0,0]);
}

// Driver Code
// Count of given arrays
let N = 2;
// Given list of N arrays
let arr = [[-3, -4],[1, 2, -3]];

// Store the maximum positive and
        // minimum negative product possible
let ans = calculateProduct(arr, 0);
// Print the maximum product
document.write(ans[0]);

// This code is contributed by patel2127

</script>
```

**Output:** 

```
12
```

**时间复杂度:**O(N *长度(数组))
T3】辅助空间: O(1)